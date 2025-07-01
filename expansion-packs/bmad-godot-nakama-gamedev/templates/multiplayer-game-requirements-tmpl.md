# {{game_title}} Multiplayer Requirements

[[LLM: This template creates comprehensive multiplayer game requirements. Start by asking about the game type, target audience, and current project status. Focus on technical requirements, player experience, and integration constraints.]]

## Project Overview

**Game Title**: {{game_title}}
**Current Status**: {{project_status|default:Existing single-player project}}
**Target Platform**: {{target_platform|default:PC/Mobile}}
**Godot Version**: {{godot_version}}

[[LLM: Ask user about their game's current state - is this a new project or existing? What platforms are they targeting? What version of Godot?]]

## Game Type & Genre

**Game Genre**: {{game_genre}}
**Game Type**: {{game_type|default:Real-time multiplayer}}
**Target Audience**: {{target_audience}}

[[LLM: Understand the game genre as this affects networking requirements. Real-time action games need different architecture than turn-based games.]]

## Multiplayer Specifications

### Player Configuration

- **Maximum Players**: {{max_players|default:4}}
- **Minimum Players**: {{min_players|default:2}}
- **Team Structure**: {{team_structure|default:Free-for-all}}
- **Spectator Support**: {{spectator_support|default:No}}

[[LLM: Ask specific questions about player counts and team structures. This directly impacts server architecture and UI design.]]

### Game Modes

REPEAT: game_mode
**{{mode_name}}**

- **Description**: {{mode_description}}
- **Player Count**: {{mode_player_count}}
- **Duration**: {{mode_duration}}
- **Special Requirements**: {{mode_requirements}}
  /REPEAT: game_mode

[[LLM: For each game mode, ask about specific networking requirements, win conditions, and any special features needed.]]

## Technical Requirements

### Performance Targets

- **Target Latency**: {{target_latency|default:<100ms}}
- **Update Frequency**: {{update_frequency|default:10 Hz}}
- **Frame Rate**: {{target_fps|default:60 FPS}}
- **Bandwidth per Player**: {{bandwidth_per_player|default:<50 KB/s}}

[[LLM: Help user understand the relationship between game type and performance requirements. Action games need lower latency than strategy games.]]

### Network Architecture

- **Synchronization Type**: {{sync_type|default:State synchronization}}
- **Server Authority**: {{server_authority|default:Full server authority}}
- **Client Prediction**: {{client_prediction|default:Yes for movement}}
- **Anti-Cheat Level**: {{anticheat_level|default:Server validation}}

[[LLM: Explain different synchronization approaches. State sync for position-based games, input sync for deterministic games, hybrid for complex games.]]

^^EXISTING_PROJECT^^

## Existing Project Integration

### Current Architecture

- **Scene Structure**: {{current_scene_structure}}
- **State Management**: {{current_state_management}}
- **Input System**: {{current_input_system}}
- **Save System**: {{current_save_system}}

### Integration Approach

- **Integration Type**: {{integration_approach|default:Additive integration}}
- **Preservation Strategy**: {{preservation_strategy}}
- **Migration Plan**: {{migration_plan}}

[[LLM: For brownfield projects, understand current architecture deeply. Ask about existing systems that might conflict with or complement multiplayer integration.]]
^^/EXISTING_PROJECT^^

## Gameplay Features

### Core Multiplayer Features

REPEAT: core_feature

- **{{feature_name}}**: {{feature_description}}
  - **Implementation**: {{feature_implementation}}
  - **Networking Impact**: {{feature_network_impact}}
    /REPEAT: core_feature

### Social Features

- **Player Communication**: {{communication_features|default:None}}
- **Friend System**: {{friend_system|default:Not required}}
- **Leaderboards**: {{leaderboard_requirements|default:Basic win/loss tracking}}
- **Player Profiles**: {{profile_requirements|default:Basic stats}}

[[LLM: Ask about social features needed. These often require additional server infrastructure and UI development.]]

## User Experience Requirements

### Matchmaking

- **Matchmaking Type**: {{matchmaking_type|default:Simple lobby system}}
- **Skill-Based Matching**: {{skill_matching|default:No}}
- **Region Preference**: {{region_preference|default:Not required}}
- **Join-in-Progress**: {{join_in_progress|default:No}}

### Connection Handling

- **Reconnection Support**: {{reconnection_support|default:Basic reconnection}}
- **Offline Mode**: {{offline_mode|default:Preserve single-player}}
- **Connection Failure**: {{connection_failure_handling}}

[[LLM: Ask about user experience during network issues. How should the game handle disconnections? Should it fall back to single-player?]]

## Data & Persistence

### Player Data

- **Player Progression**: {{player_progression}}
- **Match History**: {{match_history_requirements}}
- **Statistics Tracking**: {{statistics_requirements}}
- **Cross-Session Data**: {{cross_session_data}}

### Synchronization Requirements

- **Real-time Sync**: {{realtime_sync_objects}}
- **Persistent Sync**: {{persistent_sync_objects}}
- **Conflict Resolution**: {{conflict_resolution_strategy}}

[[LLM: Understand what data needs to persist across sessions and what needs real-time synchronization during gameplay.]]

## Platform & Deployment

### Server Infrastructure

- **Deployment Type**: {{deployment_type|default:Cloud hosting}}
- **Geographic Regions**: {{target_regions|default:Single region}}
- **Scaling Requirements**: {{scaling_requirements|default:Start small, plan to scale}}
- **Monitoring Needs**: {{monitoring_requirements|default:Basic health monitoring}}

### Client Distribution

- **Platform Support**: {{client_platforms}}
- **Update Strategy**: {{update_strategy|default:Automatic updates}}
- **Version Compatibility**: {{version_compatibility_requirements}}

[[LLM: Discuss deployment strategy. Local testing, cloud hosting, geographical distribution needs, and update mechanisms.]]

## Security & Fair Play

### Anti-Cheat Requirements

- **Cheat Prevention**: {{cheat_prevention_level|default:Server-side validation}}
- **Input Validation**: {{input_validation_requirements}}
- **Rate Limiting**: {{rate_limiting_requirements}}
- **Monitoring**: {{security_monitoring_requirements}}

### Player Safety

- **Reporting System**: {{player_reporting|default:Basic reporting}}
- **Moderation Tools**: {{moderation_requirements|default:Basic kick/ban}}
- **Content Filtering**: {{content_filtering|default:Basic profanity filter}}

[[LLM: Assess security needs based on game type and audience. Competitive games need stronger anti-cheat than casual cooperative games.]]

## Development Constraints

### Timeline

- **Development Timeline**: {{development_timeline}}
- **Key Milestones**: {{key_milestones}}
- **MVP Features**: {{mvp_features}}
- **Future Enhancements**: {{future_enhancements}}

### Resources

- **Team Size**: {{team_size}}
- **Technical Expertise**: {{team_expertise}}
- **Budget Constraints**: {{budget_considerations}}
- **Third-party Services**: {{third_party_services}}

[[LLM: Understand project constraints to ensure requirements are realistic and achievable within available resources.]]

## Success Criteria

### Technical Success Metrics

- **Performance**: {{performance_success_criteria}}
- **Reliability**: {{reliability_success_criteria}}
- **Scalability**: {{scalability_success_criteria}}

### User Experience Success Metrics

- **Player Satisfaction**: {{satisfaction_metrics}}
- **Engagement**: {{engagement_metrics}}
- **Retention**: {{retention_metrics}}

### Business Success Metrics

- **User Acquisition**: {{acquisition_metrics}}
- **Revenue Impact**: {{revenue_metrics}}
- **Development ROI**: {{development_roi}}

[[LLM: Help define measurable success criteria. What metrics will determine if the multiplayer integration was successful?]]

## Risk Assessment

### Technical Risks

REPEAT: technical_risk

- **Risk**: {{risk_description}}
- **Impact**: {{risk_impact}}
- **Likelihood**: {{risk_likelihood}}
- **Mitigation**: {{risk_mitigation}}
  /REPEAT: technical_risk

### Project Risks

REPEAT: project_risk

- **Risk**: {{risk_description}}
- **Impact**: {{risk_impact}}
- **Likelihood**: {{risk_likelihood}}
- **Mitigation**: {{risk_mitigation}}
  /REPEAT: project_risk

[[LLM: Identify potential risks specific to this project. Consider technical complexity, team capabilities, timeline constraints, and integration challenges.]]

## Next Steps

### Immediate Actions

1. {{immediate_action_1}}
2. {{immediate_action_2}}
3. {{immediate_action_3}}

### Architecture Phase

1. {{architecture_action_1}}
2. {{architecture_action_2}}
3. {{architecture_action_3}}

### Implementation Planning

1. {{implementation_action_1}}
2. {{implementation_action_2}}
3. {{implementation_action_3}}

[[LLM: Based on requirements gathered, provide specific next steps for moving forward with the multiplayer integration project.]]

---

**Document Prepared By**: {{preparer_name|default:Multiplayer Game Project Director}}
**Date**: {{current_date}}
**Review Required**: {{review_required|default:Technical Architecture Review}}

@{This template should result in comprehensive requirements that drive technical architecture decisions and implementation planning. Ensure all sections are thoroughly completed before proceeding to architecture design.}
