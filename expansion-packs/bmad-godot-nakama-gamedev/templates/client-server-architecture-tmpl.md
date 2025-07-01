# {{project_name}} Client-Server Architecture

[[LLM: This template designs comprehensive client-server architecture for Godot + Nakama multiplayer games. Ask about game type, performance requirements, scalability needs, and security requirements first.]]

## Architecture Overview

**Project**: {{project_name}}
**Architecture Type**: {{architecture_type|default:Client-Server with Authoritative Server}}
**Game Type**: {{game_type}}
**Target Scale**: {{target_scale|default:4-16 concurrent players}}

[[LLM: Understand the game type deeply - real-time action, turn-based, MMO-style, etc. This determines the entire architecture approach.]]

## System Architecture Diagram

```
{{architecture_diagram}}
```

[[LLM: Create a text-based architecture diagram showing the relationship between clients, Nakama server, database, and any external services.]]

## Client Architecture (Godot)

### Client Responsibilities

- **Input Handling**: {{client_input_responsibilities}}
- **Rendering**: {{client_rendering_responsibilities}}
- **Local Prediction**: {{client_prediction_responsibilities}}
- **UI/UX Management**: {{client_ui_responsibilities}}

### Client Components

#### NetworkManager (AutoLoad)

```gdscript
# Primary networking interface
- Connection management
- Authentication handling
- Message routing
- State synchronization
```

#### GameStateManager

```gdscript
# Game state coordination
- Local state management
- Network state integration
- Conflict resolution
- State persistence
```

#### InputManager

```gdscript
# Input processing
- Input capture and validation
- Command generation
- Prediction integration
- Input buffering
```

#### PredictionSystem

```gdscript
# Client prediction
- Movement prediction
- Action prediction
- Rollback handling
- Interpolation/extrapolation
```

[[LLM: Adjust client components based on game type. Action games need prediction, turn-based games may not. Strategy games need different state management than shooters.]]

## Server Architecture (Nakama)

### Server Responsibilities

- **Game Logic Authority**: {{server_logic_responsibilities}}
- **State Management**: {{server_state_responsibilities}}
- **Validation**: {{server_validation_responsibilities}}
- **Data Persistence**: {{server_persistence_responsibilities}}

### Server Modules

#### Match Handler Module

```typescript
// Real-time match management
interface MatchHandler {
  matchInit(): MatchState;
  matchJoinAttempt(): boolean;
  matchJoin(): MatchState;
  matchLeave(): MatchState;
  matchLoop(): MatchState;
  matchTerminate(): MatchState;
}
```

#### Game Logic Module

```typescript
// Core game rules and validation
interface GameLogic {
  validatePlayerAction(): boolean;
  processGameTick(): GameState;
  checkWinConditions(): GameResult;
  handlePlayerInput(): void;
}
```

#### Data Management Module

```typescript
// Player and game data
interface DataManager {
  savePlayerProfile(): void;
  loadPlayerData(): PlayerData;
  recordMatchResult(): void;
  updateLeaderboards(): void;
}
```

#### Anti-Cheat Module

```typescript
// Security and validation
interface AntiCheat {
  validateInput(): boolean;
  detectCheating(): boolean;
  enforceRateLimit(): boolean;
  logSuspiciousActivity(): void;
}
```

[[LLM: Customize server modules based on game requirements. Competitive games need stronger anti-cheat, social games need more communication features.]]

## Data Architecture

### Game State Structure

```typescript
interface GameState {
  // Core game data
  gameId: string
  gamePhase: GamePhase
  startTime: number

  // Player data
  players: Map<string, PlayerState>

  // Game-specific data
  {{game_specific_state}}
}

interface PlayerState {
  userId: string
  position: Vector2
  health: number
  score: number
  // Game-specific player data
  {{player_specific_state}}
}
```

### Data Flow Patterns

#### Client to Server

1. **Input Commands**: {{input_command_flow}}
2. **State Updates**: {{state_update_flow}}
3. **Action Requests**: {{action_request_flow}}

#### Server to Client

1. **State Broadcasts**: {{state_broadcast_flow}}
2. **Event Notifications**: {{event_notification_flow}}
3. **Validation Results**: {{validation_result_flow}}

[[LLM: Design data structures specific to the game type. Racing games need position/velocity, card games need hand/deck state, strategy games need unit positions and resources.]]

## Network Communication

### Synchronization Strategy

**Primary Strategy**: {{sync_strategy|default:State Synchronization}}

^^STATE_SYNC^^
**State Synchronization Approach**

- Server broadcasts authoritative game state
- Clients receive and apply state updates
- Suitable for: Position-based games, MMOs
- Update frequency: {{state_sync_frequency|default:10-20 Hz}}
  ^^/STATE_SYNC^^

^^INPUT_SYNC^^
**Input Synchronization Approach**

- Clients send input commands to server
- Server processes and broadcasts results
- Suitable for: Fighting games, RTS games
- Deterministic simulation required
  ^^/INPUT_SYNC^^

^^HYBRID_SYNC^^
**Hybrid Synchronization Approach**

- Combination of state and input sync
- Different strategies for different data types
- Maximum flexibility and optimization
- Complex but powerful
  ^^/HYBRID_SYNC^^

### Message Types

REPEAT: message_type

- **{{message_name}}**: {{message_description}}
  - **Direction**: {{message_direction}}
  - **Frequency**: {{message_frequency}}
  - **Size**: {{message_size}}
  - **Priority**: {{message_priority}}
    /REPEAT: message_type

[[LLM: Define specific message types based on game requirements. Include technical details like frequency and size estimates.]]

## Performance Optimization

### Client Optimization

- **Prediction Strategy**: {{client_prediction_strategy}}
- **Interpolation**: {{client_interpolation_strategy}}
- **LOD System**: {{client_lod_strategy}}
- **Culling**: {{client_culling_strategy}}

### Server Optimization

- **Tick Rate**: {{server_tick_rate|default:10-20 Hz}}
- **State Compression**: {{state_compression_strategy}}
- **Update Filtering**: {{update_filtering_strategy}}
- **Load Balancing**: {{load_balancing_strategy}}

### Network Optimization

- **Bandwidth Target**: {{bandwidth_target|default:<50KB/s per player}}
- **Latency Target**: {{latency_target|default:<100ms}}
- **Compression**: {{compression_strategy}}
- **Batching**: {{message_batching_strategy}}

[[LLM: Provide specific optimization strategies based on game type and scale. Include realistic performance targets.]]

## Security Architecture

### Authentication

- **Player Identity**: {{authentication_method|default:Device-based with optional accounts}}
- **Session Management**: {{session_management_strategy}}
- **Token Validation**: {{token_validation_strategy}}

### Authorization

- **Action Validation**: {{action_authorization_strategy}}
- **Resource Access**: {{resource_authorization_strategy}}
- **Admin Privileges**: {{admin_authorization_strategy}}

### Anti-Cheat Measures

- **Input Validation**: {{input_validation_strategy}}
- **Movement Validation**: {{movement_validation_strategy}}
- **Action Validation**: {{action_validation_strategy}}
- **Rate Limiting**: {{rate_limiting_strategy}}

### Data Protection

- **Data Encryption**: {{data_encryption_strategy}}
- **Privacy Compliance**: {{privacy_compliance_requirements}}
- **Data Retention**: {{data_retention_policy}}

[[LLM: Assess security requirements based on game type and audience. Competitive games need stronger security than casual cooperative games.]]

## Scalability Design

### Horizontal Scaling

- **Match Distribution**: {{match_distribution_strategy}}
- **Load Balancing**: {{load_balancing_strategy}}
- **Server Instances**: {{server_instance_strategy}}

### Database Scaling

- **Data Partitioning**: {{data_partitioning_strategy}}
- **Caching Strategy**: {{caching_strategy}}
- **Read Replicas**: {{read_replica_strategy}}

### Performance Monitoring

- **Metrics Collection**: {{metrics_collection_strategy}}
- **Alert Thresholds**: {{alert_threshold_strategy}}
- **Auto-Scaling**: {{auto_scaling_strategy}}

[[LLM: Design for the expected scale but also plan for growth. Include specific scaling triggers and procedures.]]

## Error Handling & Recovery

### Client Error Handling

- **Connection Loss**: {{client_connection_loss_handling}}
- **Timeout Recovery**: {{client_timeout_recovery}}
- **State Desync**: {{client_state_desync_handling}}
- **Invalid Data**: {{client_invalid_data_handling}}

### Server Error Handling

- **Player Disconnection**: {{server_disconnection_handling}}
- **Invalid Input**: {{server_invalid_input_handling}}
- **System Overload**: {{server_overload_handling}}
- **Data Corruption**: {{server_data_corruption_handling}}

### Graceful Degradation

- **Offline Mode**: {{offline_mode_strategy}}
- **Reduced Functionality**: {{reduced_functionality_strategy}}
- **Fallback Systems**: {{fallback_system_strategy}}

[[LLM: Ensure robust error handling that maintains good user experience even when things go wrong.]]

## Development & Deployment

### Development Environment

- **Local Testing**: {{local_testing_setup}}
- **Development Server**: {{dev_server_setup}}
- **Testing Tools**: {{testing_tools_requirements}}

### Production Deployment

- **Server Infrastructure**: {{production_infrastructure}}
- **Database Setup**: {{database_setup_requirements}}
- **Monitoring**: {{monitoring_setup_requirements}}
- **Backup Strategy**: {{backup_strategy}}

### CI/CD Pipeline

- **Build Process**: {{build_process_requirements}}
- **Testing Automation**: {{testing_automation_requirements}}
- **Deployment Automation**: {{deployment_automation_requirements}}
- **Rollback Procedures**: {{rollback_procedures}}

[[LLM: Provide practical deployment guidance based on team size and technical expertise.]]

## Implementation Roadmap

### Phase 1: Core Architecture

1. {{architecture_implementation_step1}}
2. {{architecture_implementation_step2}}
3. {{architecture_implementation_step3}}

### Phase 2: Feature Development

1. {{feature_development_step1}}
2. {{feature_development_step2}}
3. {{feature_development_step3}}

### Phase 3: Optimization & Polish

1. {{optimization_step1}}
2. {{optimization_step2}}
3. {{optimization_step3}}

### Phase 4: Production Readiness

1. {{production_step1}}
2. {{production_step2}}
3. {{production_step3}}

[[LLM: Create realistic implementation timeline with specific deliverables and milestones.]]

---

**Architecture Designed By**: {{architect_name|default:Multiplayer Systems Architect}}
**Date**: {{design_date}}
**Review Status**: {{review_status|default:Pending Implementation Review}}
**Implementation Team**: {{implementation_team}}

@{This architecture document should provide complete technical guidance for implementing a robust, scalable multiplayer system that meets the specific needs of this game project.}
