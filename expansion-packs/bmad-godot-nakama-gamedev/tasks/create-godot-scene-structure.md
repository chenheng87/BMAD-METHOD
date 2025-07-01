# Create Godot Scene Structure Task

## Purpose

Design multiplayer-ready Godot scene structures that integrate networking functionality while preserving existing single-player functionality.

## When to Use

- Setting up scenes for multiplayer integration
- Organizing network-aware scene hierarchies
- Implementing multiplayer spawning systems
- Creating UI for multiplayer features

## Implementation Phases

### Phase 1: Scene Architecture Planning

**Analyze Current Structure:**

- Existing scene organization and hierarchy
- AutoLoad scripts and their responsibilities
- Current state management patterns
- UI and menu systems

**Design Multiplayer Additions:**

- NetworkManager singleton for centralized networking
- Multiplayer-specific scene variants
- Player spawning and synchronization systems
- Network-aware UI components

### Phase 2: Core Network Architecture

**Create NetworkManager AutoLoad:**

```gdscript
# NetworkManager.gd - AutoLoad singleton
extends Node

signal connected_to_server
signal disconnected_from_server
signal player_joined(player_data)
signal player_left(player_id)

var nakama_client: NakamaClient
var nakama_session: NakamaSession
var nakama_socket: NakamaSocket
var current_match: NakamaRtApi.Match

func _ready():
    initialize_nakama()

func initialize_nakama():
    nakama_client = Nakama.create_client("defaultkey", "localhost", 7350, "http")

func connect_to_server():
    var session = await nakama_client.authenticate_device_async(OS.get_unique_id())
    if session.is_exception():
        print("Authentication failed: ", session.get_exception())
        return false

    nakama_session = session
    nakama_socket = Nakama.create_socket_from(nakama_client)
    await nakama_socket.connect_async(nakama_session)

    connected_to_server.emit()
    return true
```

### Phase 3: Multiplayer Scene Structure

**Main Scene Hierarchy:**

```
Main
├── UI (CanvasLayer)
│   ├── MainMenu
│   ├── MultiplayerLobby
│   ├── GameHUD
│   └── NetworkStatus
├── GameWorld
│   ├── Level (Existing single-player content)
│   ├── Players (MultiplayerSpawner)
│   │   └── PlayerScene (Networked player)
│   ├── NetworkObjects (MultiplayerSpawner)
│   │   └── NetworkedItems
│   └── LocalEffects (Non-networked visual effects)
└── NetworkManager (Reference to AutoLoad)
```

**Multiplayer Scene Template:**

```gdscript
# MultiplayerGame.gd
extends Node

@onready var players_spawner = $GameWorld/Players
@onready var objects_spawner = $GameWorld/NetworkObjects

func _ready():
    # Configure multiplayer spawners
    players_spawner.spawn_function = spawn_player
    objects_spawner.spawn_function = spawn_object

    # Connect network events
    NetworkManager.player_joined.connect(_on_player_joined)
    NetworkManager.player_left.connect(_on_player_left)

func spawn_player(data: Dictionary):
    var player_scene = preload("res://scenes/NetworkPlayer.tscn")
    var player = player_scene.instantiate()
    player.setup_player(data)
    return player

func _on_player_joined(player_data):
    print("Player joined: ", player_data.username)

func _on_player_left(player_id):
    print("Player left: ", player_id)
```

### Phase 4: Network Player Implementation

**Networked Player Scene:**

```gdscript
# NetworkPlayer.gd
extends CharacterBody2D
class_name NetworkPlayer

@export var player_id: String
@export var username: String
@export var is_local_player: bool = false

# Network synchronization
var network_position: Vector2
var network_velocity: Vector2
var network_animation: String

func _ready():
    # Configure multiplayer synchronizer
    if has_node("MultiplayerSynchronizer"):
        var sync = $MultiplayerSynchronizer
        sync.set_multiplayer_authority(player_id.hash())

func _physics_process(delta):
    if is_local_player:
        handle_local_input()
        send_network_update()
    else:
        interpolate_network_state(delta)

func handle_local_input():
    var input_vector = Input.get_vector("ui_left", "ui_right", "ui_up", "ui_down")
    velocity = input_vector * 300
    move_and_slide()

func send_network_update():
    if NetworkManager.nakama_socket:
        var data = {
            "position": global_position,
            "velocity": velocity,
            "animation": current_animation
        }
        NetworkManager.send_match_data(data)

func interpolate_network_state(delta):
    # Smooth interpolation for remote players
    global_position = global_position.lerp(network_position, delta * 10)
```

### Phase 5: UI Integration

**Multiplayer Lobby UI:**

```gdscript
# MultiplayerLobby.gd
extends Control

@onready var player_list = $VBoxContainer/PlayerList
@onready var start_button = $VBoxContainer/StartButton
@onready var leave_button = $VBoxContainer/LeaveButton

func _ready():
    NetworkManager.player_joined.connect(_on_player_joined)
    NetworkManager.player_left.connect(_on_player_left)
    NetworkManager.match_found.connect(_on_match_found)

func _on_join_match_pressed():
    NetworkManager.find_or_create_match()

func _on_player_joined(player_data):
    var player_label = Label.new()
    player_label.text = player_data.username
    player_label.name = "player_" + str(player_data.user_id)
    player_list.add_child(player_label)

    # Enable start button if enough players
    start_button.disabled = player_list.get_child_count() < 2

func _on_start_game_pressed():
    NetworkManager.start_match()
    get_tree().change_scene_to_file("res://scenes/MultiplayerGame.tscn")
```

### Phase 6: Brownfield Integration

**Preserve Existing Functionality:**

```gdscript
# GameManager.gd - Enhanced existing manager
extends Node

enum GameMode { SINGLE_PLAYER, MULTIPLAYER }
var current_mode: GameMode = GameMode.SINGLE_PLAYER

func start_single_player():
    current_mode = GameMode.SINGLE_PLAYER
    get_tree().change_scene_to_file("res://scenes/SinglePlayerGame.tscn")

func start_multiplayer():
    current_mode = GameMode.MULTIPLAYER
    if not NetworkManager.is_connected():
        await NetworkManager.connect_to_server()
    get_tree().change_scene_to_file("res://scenes/MultiplayerLobby.tscn")

func is_multiplayer_mode() -> bool:
    return current_mode == GameMode.MULTIPLAYER
```

## Quality Validation

### Scene Structure Checklist

- [ ] NetworkManager AutoLoad configured
- [ ] Multiplayer spawners set up correctly
- [ ] Player synchronization working
- [ ] UI properly integrated
- [ ] Single-player functionality preserved

### Performance Validation

- [ ] Network updates efficient (10-20 Hz)
- [ ] Interpolation smooth (60+ FPS)
- [ ] Scene transitions fast
- [ ] Memory usage optimized

## Success Criteria

1. **Functional**: Multiplayer scenes work correctly
2. **Compatible**: Existing functionality preserved
3. **Performance**: Smooth networking at target framerate
4. **Usable**: Clear UI for multiplayer features
5. **Maintainable**: Clean, organized scene structure
