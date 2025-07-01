# Godot + Nakama Gamedev Expansion Pack Plan

## Overview

- **Pack Name**: bmad-godot-nakama-gamedev
- **Display Name**: Godot + Nakama Multiplayer Game Development Pack
- **Description**: Comprehensive AI agent team for developing multiplayer games with Godot engine and Nakama game server, specializing in brownfield integration and client-server architecture
- **Target Domain**: Multiplayer game development with focus on existing Godot projects
- **Author**: BMAD Community

## Problem Statement

Developers working with existing Godot projects face significant challenges when adding multiplayer functionality using Nakama:

1. **Complex Integration**: Safely integrating Nakama without breaking existing single-player functionality
2. **Architecture Decisions**: Choosing between state sync vs input sync, client prediction strategies
3. **Compatibility Issues**: Managing plugin conflicts and version compatibility
4. **Brownfield Constraints**: Respecting existing code patterns and project structure
5. **Client-Server Coordination**: Coordinating frontend (Godot) and backend (Nakama) development cycles

## Target Users

- Godot developers adding multiplayer to existing games
- Indie game developers using Nakama for multiplayer services
- Teams transitioning from single-player to multiplayer games
- Developers seeking brownfield-safe integration strategies

## Components to Create

### Agents

- [ ] `godot-nakama-orchestrator` - **REQUIRED**: Master project coordinator for Godot+Nakama development

  - Key commands: *analyze-project, *plan-integration, *coordinate-development, *validate-compatibility
  - Manages: Project analysis, integration strategy, development coordination
  - Character: Maya Chen - Multiplayer Game Project Director

- [ ] `godot-project-analyzer` - Existing Godot project analysis specialist

  - Tasks used: analyze-existing-godot-project, assess-plugin-compatibility, create-integration-strategy
  - Templates used: project-analysis-report-tmpl, compatibility-assessment-tmpl
  - Data required: godot-plugin-compatibility-db.md
  - Character: Alex Rodriguez - Godot Architecture Analyst

- [ ] `godot-client-dev` - Godot client-side development expert

  - Tasks used: create-godot-scene-structure, implement-client-networking, optimize-client-performance
  - Templates used: godot-client-architecture-tmpl, scene-structure-tmpl
  - Data required: godot-best-practices.md, gdscript-patterns.md
  - Character: Jamie Park - Godot Client Developer

- [ ] `nakama-server-dev` - Nakama server development specialist

  - Tasks used: implement-nakama-modules, design-server-api, setup-nakama-deployment
  - Templates used: nakama-server-modules-tmpl, nakama-api-spec-tmpl
  - Data required: nakama-best-practices.md, server-patterns.md
  - Character: Dr. Sarah Kim - Backend Game Server Architect

- [ ] `multiplayer-architect` - Client-server architecture designer
  - Tasks used: design-network-architecture, plan-sync-strategy, create-anti-cheat-design
  - Templates used: client-server-architecture-tmpl, network-sync-strategy-tmpl
  - Data required: multiplayer-patterns.md, network-optimization.md
  - Character: Chris Taylor - Multiplayer Systems Architect

### Tasks

- [ ] `analyze-existing-godot-project.md` - Comprehensive analysis of existing Godot projects (used by: godot-project-analyzer)
- [ ] `create-godot-nakama-integration-plan.md` - Create brownfield integration strategy (used by: godot-project-analyzer)
- [ ] `implement-nakama-modules.md` - Develop custom Nakama server modules (used by: nakama-server-dev)
- [ ] `create-godot-scene-structure.md` - Design multiplayer-ready scene architecture (used by: godot-client-dev)
- [ ] `design-network-sync-strategy.md` - Plan state synchronization approach (used by: multiplayer-architect)
- [ ] `validate-integration-compatibility.md` - Ensure brownfield safety (used by: godot-nakama-orchestrator)

### Templates

- [ ] `godot-nakama-integration-plan-tmpl.md` - Brownfield integration planning document (used by: godot-project-analyzer)
- [ ] `client-server-architecture-tmpl.md` - Technical architecture specification (used by: multiplayer-architect)
- [ ] `godot-client-architecture-tmpl.md` - Godot-specific client design (used by: godot-client-dev)
- [ ] `nakama-server-modules-tmpl.md` - Server module development guide (used by: nakama-server-dev)
- [ ] `multiplayer-game-requirements-tmpl.md` - Game requirements with multiplayer focus (used by: godot-nakama-orchestrator)
- [ ] `network-sync-strategy-tmpl.md` - Network synchronization design document (used by: multiplayer-architect)

### Checklists

- [ ] `godot-nakama-integration-checklist.md` - Comprehensive integration validation
- [ ] `brownfield-safety-checklist.md` - Ensures existing functionality preservation
- [ ] `multiplayer-performance-checklist.md` - Network performance validation
- [ ] `deployment-readiness-checklist.md` - Production deployment verification

### Data Files Required from User

Users must add these files to their project docs/ folder:

- [ ] `existing-project-structure.md` - Documentation of current Godot project structure

  - Format: Markdown with scene tree diagrams
  - Purpose: Understanding existing architecture for safe integration
  - Example: Scene hierarchy, AutoLoad configs, existing network code

- [ ] `game-requirements.md` - Multiplayer game requirements and constraints
  - Format: Structured markdown document
  - Purpose: Defining multiplayer scope and technical requirements
  - Example: Player count, game mechanics, performance targets

### Knowledge Base Files

- [ ] `godot-plugin-compatibility-db.md` - Database of known plugin compatibility issues
- [ ] `godot-best-practices.md` - Godot development patterns and conventions
- [ ] `nakama-best-practices.md` - Nakama server development guidelines
- [ ] `multiplayer-patterns.md` - Common multiplayer architecture patterns
- [ ] `brownfield-integration-guide.md` - Safe integration strategies for existing projects

## Workflow Overview

1. **Project Analysis Phase** - godot-project-analyzer examines existing project structure, plugins, and architecture
2. **Integration Planning** - multiplayer-architect designs safe integration strategy respecting existing constraints
3. **Parallel Development Setup** - Coordinate separate client and server development tracks
4. **Incremental Integration** - Step-by-step integration with rollback safety at each step
5. **Testing & Validation** - Comprehensive compatibility and performance validation
6. **Production Deployment** - Deployment strategy with monitoring and rollback capabilities

## Integration Points

- Depends on core agents: architect (for technical review), po (for validation)
- Extends teams: Could be added to team-fullstack for projects requiring multiplayer
- Workflow integration: Brownfield workflows for safe existing project enhancement

## Success Criteria

- [ ] All components created and cross-referenced correctly
- [ ] No orphaned task/template references
- [ ] Brownfield safety patterns implemented throughout
- [ ] Character personas provide engaging user experience
- [ ] Integration strategies prioritize existing project preservation
- [ ] Comprehensive validation checklists ensure quality
- [ ] Knowledge base covers common compatibility issues
- [ ] README provides clear setup and usage instructions

## User Approval

- [ ] Plan reviewed by user
- [ ] Approval to proceed with implementation

---

**Next Steps**: Once approved, I will proceed with Phase 2 implementation starting with the orchestrator agent, followed by specialist agents, tasks, templates, and checklists in dependency order.

## Implementation Notes

This expansion pack will be unique in its focus on:

1. **Brownfield Integration First** - Every component designed to work with existing projects
2. **Character-Driven Experience** - Each agent has a distinct professional persona
3. **Safety-First Approach** - Comprehensive validation and rollback strategies
4. **Technology-Specific Expertise** - Deep knowledge of both Godot and Nakama ecosystems
5. **Incremental Development** - Step-by-step integration that minimizes risk
