# Multiplayer Game Patterns Knowledge Base

## Synchronization Patterns

### State Synchronization Pattern

**Best For**: Position-based games, MMOs, real-time action games

**How It Works**:

- Server maintains authoritative game state
- Server broadcasts state updates to all clients
- Clients apply received state updates
- Client prediction for local player responsiveness

**Implementation**:

```gdscript
# Server broadcasts game state
func broadcast_game_state():
    var state_data = {
        "players": get_all_player_states(),
        "objects": get_dynamic_objects(),
        "timestamp": Time.get_unix_time()
    }
    send_to_all_clients(state_data)

# Client applies received state
func apply_server_state(state_data):
    for player_id in state_data.players:
        update_player_state(player_id, state_data.players[player_id])
```

**Pros**: Simple, works with any game logic, good for variable player counts
**Cons**: Higher bandwidth usage, potential for state conflicts

### Input Synchronization Pattern

**Best For**: Fighting games, RTS games, deterministic simulations

**How It Works**:

- Clients send input commands to server
- Server processes all inputs in deterministic order
- Server broadcasts input results or confirmation
- All clients run identical simulation

**Implementation**:

```gdscript
# Client sends input command
func send_input_command(input_data):
    var command = {
        "player_id": local_player_id,
        "input": input_data,
        "frame": current_frame,
        "timestamp": Time.get_unix_time()
    }
    send_to_server(command)

# Server processes input in order
func process_input_command(command):
    if validate_input(command):
        apply_input_to_simulation(command)
        broadcast_input_result(command)
```

**Pros**: Lower bandwidth, perfect synchronization, replay capability
**Cons**: Requires deterministic simulation, complex rollback systems

### Hybrid Synchronization Pattern

**Best For**: Complex games with different data types

**How It Works**:

- Critical data uses input sync (combat, scoring)
- Non-critical data uses state sync (cosmetics, chat)
- Different update frequencies for different data types

**Implementation**:

```gdscript
# Different sync strategies for different data
func update_network():
    # High-frequency state sync for positions
    if frame % 3 == 0:  # 20Hz for 60fps game
        sync_player_positions()

    # Low-frequency state sync for health/score
    if frame % 30 == 0:  # 2Hz
        sync_player_stats()

    # Input sync for critical actions
    process_pending_action_inputs()
```

## Client Prediction Patterns

### Basic Movement Prediction

**Purpose**: Reduce perceived input lag for local player

```gdscript
func handle_movement_input():
    var input_vector = Input.get_vector("left", "right", "up", "down")

    # Apply movement immediately for local player
    if is_local_player:
        apply_movement(input_vector)

        # Send input to server for validation
        send_movement_input(input_vector)

    # Store input for potential rollback
    input_history.append({
        "frame": current_frame,
        "input": input_vector,
        "position": global_position
    })

func handle_server_correction(server_position, server_frame):
    # Check if correction needed
    var predicted_position = get_predicted_position(server_frame)
    var error = predicted_position.distance_to(server_position)

    if error > correction_threshold:
        # Rollback and replay
        rollback_to_frame(server_frame)
        global_position = server_position
        replay_inputs_from_frame(server_frame)
```

### Action Prediction Pattern

**Purpose**: Immediate feedback for player actions

```gdscript
func handle_action_input(action_type):
    # Show immediate feedback
    play_action_animation(action_type)
    show_action_effects(action_type)

    # Send to server for validation
    var action_id = generate_action_id()
    send_action_to_server(action_type, action_id)

    # Store for potential rollback
    predicted_actions[action_id] = {
        "type": action_type,
        "timestamp": Time.get_unix_time(),
        "effects": current_effects
    }

func handle_action_validation(action_id, success):
    if not success and action_id in predicted_actions:
        # Rollback action effects
        var action = predicted_actions[action_id]
        reverse_action_effects(action.effects)
        show_action_failed_feedback()
```

## Network Architecture Patterns

### Authoritative Server Pattern

**Security**: High - Server validates all actions
**Performance**: Good - Centralized processing
**Scalability**: Limited by single server capacity

```gdscript
# Server-side game logic
func process_player_action(player_id, action):
    # Validate action is possible
    if not can_player_perform_action(player_id, action):
        send_action_denied(player_id, "Action not allowed")
        return

    # Validate action timing
    if not is_action_timing_valid(player_id, action):
        send_action_denied(player_id, "Invalid timing")
        return

    # Apply action to game state
    apply_action(player_id, action)

    # Broadcast result to all players
    broadcast_action_result(player_id, action)
```

### Peer-to-Peer Pattern

**Security**: Lower - Trust between peers required
**Performance**: Good - Distributed processing
**Scalability**: Good for small groups

```gdscript
# P2P message handling
func handle_peer_message(peer_id, message):
    # Verify message authenticity
    if not verify_peer_signature(peer_id, message):
        report_potential_cheat(peer_id)
        return

    # Apply peer's action
    apply_peer_action(peer_id, message.action)

    # Forward to other peers if needed
    if message.should_forward:
        forward_to_other_peers(message, exclude_peer = peer_id)
```

## Anti-Cheat Patterns

### Server Validation Pattern

**Purpose**: Prevent common cheating attempts

```gdscript
# Movement validation
func validate_movement(player_id, old_pos, new_pos, delta_time):
    var distance = old_pos.distance_to(new_pos)
    var max_distance = get_player_max_speed(player_id) * delta_time

    if distance > max_distance * 1.1:  # 10% tolerance
        log_suspicious_activity(player_id, "Speed hack detected")
        return false

    # Check for wall/obstacle collision
    if has_collision_between(old_pos, new_pos):
        log_suspicious_activity(player_id, "Wall hack detected")
        return false

    return true

# Action validation
func validate_action(player_id, action):
    var player_state = get_player_state(player_id)

    # Check cooldowns
    if not is_action_ready(player_id, action.type):
        return false

    # Check resources (mana, ammo, etc.)
    if not has_required_resources(player_id, action):
        return false

    # Check range/line of sight
    if not is_target_valid(player_id, action.target):
        return false

    return true
```

### Rate Limiting Pattern

**Purpose**: Prevent spam and DoS attacks

```gdscript
# Rate limiting implementation
class RateLimiter:
    var actions_per_second: int = 10
    var burst_limit: int = 20
    var player_buckets: Dictionary = {}

    func can_perform_action(player_id: String) -> bool:
        if not player_id in player_buckets:
            player_buckets[player_id] = TokenBucket.new(actions_per_second, burst_limit)

        return player_buckets[player_id].try_consume()

    func _ready():
        # Refill buckets every second
        var timer = Timer.new()
        timer.wait_time = 1.0
        timer.timeout.connect(_refill_buckets)
        timer.autostart = true
        add_child(timer)

    func _refill_buckets():
        for bucket in player_buckets.values():
            bucket.refill()
```

## Latency Compensation Patterns

### Lag Compensation Pattern

**Purpose**: Fair hit detection despite network latency

```gdscript
# Server-side lag compensation
func process_hit_scan(player_id, target_pos, timestamp):
    var player_latency = get_player_latency(player_id)
    var compensation_time = timestamp - player_latency

    # Rewind game state to when player fired
    var historical_state = get_world_state_at_time(compensation_time)

    # Check hit in historical context
    var hit_result = check_hit_in_state(historical_state, target_pos)

    if hit_result.hit:
        # Apply damage using current game state
        apply_damage(hit_result.target, hit_result.damage)

        # Notify all clients of hit
        broadcast_hit_confirmation(player_id, hit_result)
```

### Interpolation Pattern

**Purpose**: Smooth visual updates for remote players

```gdscript
# Client-side interpolation
func update_remote_player(delta):
    if network_updates.size() < 2:
        return

    var current_time = Time.get_unix_time()
    var interpolation_delay = 0.1  # 100ms buffer
    var target_time = current_time - interpolation_delay

    # Find two updates to interpolate between
    var from_update = find_update_before(target_time)
    var to_update = find_update_after(target_time)

    if from_update and to_update:
        var alpha = (target_time - from_update.timestamp) / (to_update.timestamp - from_update.timestamp)

        # Interpolate position
        global_position = from_update.position.lerp(to_update.position, alpha)

        # Interpolate rotation
        rotation = lerp_angle(from_update.rotation, to_update.rotation, alpha)
```

## Scalability Patterns

### Load Balancing Pattern

**Purpose**: Distribute players across multiple servers

```gdscript
# Simple round-robin load balancer
class LoadBalancer:
    var servers: Array = []
    var current_index: int = 0

    func add_server(server_info):
        servers.append(server_info)

    func get_best_server() -> Dictionary:
        # Round-robin selection
        var server = servers[current_index]
        current_index = (current_index + 1) % servers.size()
        return server

    func get_server_by_load() -> Dictionary:
        # Find server with lowest player count
        var best_server = servers[0]
        for server in servers:
            if server.player_count < best_server.player_count:
                best_server = server
        return best_server
```

### Instance Management Pattern

**Purpose**: Manage multiple game instances efficiently

```gdscript
# Game instance manager
class InstanceManager:
    var instances: Dictionary = {}
    var max_players_per_instance: int = 100

    func find_or_create_instance(player_preferences) -> String:
        # Try to find existing instance with space
        for instance_id in instances:
            var instance = instances[instance_id]
            if instance.player_count < max_players_per_instance:
                if matches_preferences(instance, player_preferences):
                    return instance_id

        # Create new instance
        var new_instance_id = generate_instance_id()
        create_instance(new_instance_id, player_preferences)
        return new_instance_id

    func create_instance(instance_id: String, preferences):
        var instance = GameInstance.new()
        instance.initialize(preferences)
        instances[instance_id] = instance
```

## Common Implementation Gotchas

### Float Precision Issues

```gdscript
# Bad: Direct float comparison
if player.position.x == target.x:
    do_something()

# Good: Use epsilon comparison
if abs(player.position.x - target.x) < 0.001:
    do_something()
```

### Frame Rate Dependencies

```gdscript
# Bad: Frame rate dependent
velocity += acceleration

# Good: Delta time independent
velocity += acceleration * delta
```

### State Desynchronization

```gdscript
# Always validate state consistency
func apply_network_update(update):
    # Validate update makes sense
    if not is_update_valid(update):
        request_state_resync()
        return

    apply_update(update)

    # Periodic state validation
    if should_validate_state():
        if not validate_state_consistency():
            request_state_resync()
```

This knowledge base provides proven patterns for common multiplayer game development challenges in Godot + Nakama projects.
