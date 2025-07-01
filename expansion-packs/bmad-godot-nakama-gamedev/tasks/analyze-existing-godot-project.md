# Analyze Existing Godot Project Task

## Purpose

Conduct comprehensive analysis of existing Godot projects to understand current architecture, identify potential compatibility issues, and plan safe integration of Nakama multiplayer functionality.

## When to Use This Task

**Use this task when:**

- Planning to add multiplayer to existing Godot project
- Need to understand project structure before integration
- Assessing compatibility with Nakama integration
- Creating brownfield integration strategy

**Prerequisites:**

- Access to existing Godot project files
- project.godot configuration file
- Understanding of current project functionality

## Instructions

### Phase 1: Project Information Gathering

#### 1.1 Basic Project Information

Ask the user to provide:

**Essential Information:**

```
I need to analyze your existing Godot project. Please provide:

1. **project.godot File Content**:
   - Copy and paste your complete project.godot file

2. **Godot Version**:
   - What version of Godot are you using?

3. **Project Type**:
   - 2D game, 3D game, or mixed?
   - What genre/style of game?

4. **Current Functionality**:
   - Brief description of what your game currently does
   - Any existing networking or multiplayer features?
```

#### 1.2 Plugin and Dependencies Analysis

**Request Plugin Information:**

```
Plugin Information Needed:

1. **Installed Plugins**:
   - List all plugins in your project
   - Which ones are currently enabled?

2. **Custom Scripts/Systems**:
   - Any custom networking code?
   - Existing state management systems?
   - Custom input handling systems?

3. **External Dependencies**:
   - Any external services your game connects to?
   - Third-party SDKs or APIs?
```

#### 1.3 Architecture Information

**Gather Structural Details:**

```
Project Structure Information:

1. **Scene Organization**:
   - Main scene and how scenes are organized
   - Key scenes (menu, gameplay, etc.)

2. **AutoLoad Configuration**:
   - List all AutoLoad scripts and their purposes
   - Any existing singletons or managers?

3. **Script Architecture**:
   - How is your code organized?
   - Any design patterns you're following?
```

### Phase 2: Compatibility Analysis

#### 2.1 Plugin Compatibility Assessment

For each identified plugin, assess:

**Compatibility Categories:**

- ✅ **Compatible**: Known to work well with Nakama
- ⚠️ **Needs Attention**: May require configuration changes
- ❌ **Conflicting**: May interfere with Nakama integration
- ❓ **Unknown**: Requires investigation

**Common Plugin Assessment:**

| Plugin Type        | Compatibility Risk | Notes                 |
| ------------------ | ------------------ | --------------------- |
| UI Frameworks      | Low                | Usually compatible    |
| Audio Systems      | Low                | Independent systems   |
| Input Systems      | Medium             | May need coordination |
| Networking Plugins | High               | Potential conflicts   |
| State Management   | Medium             | May need integration  |
| Performance Tools  | Low                | Usually beneficial    |

#### 2.2 Architecture Pattern Analysis

**Identify Current Patterns:**

- **Scene Management**: How scenes are loaded and managed
- **State Management**: How game state is handled
- **Event Systems**: How components communicate
- **Resource Management**: How assets are loaded and cached

**Assess Nakama Integration Impact:**

- Which patterns support multiplayer integration?
- Which patterns may need modification?
- What new patterns are needed?

### Phase 3: Risk Assessment

#### 3.1 Integration Risk Categories

**High Risk Items:**

- Existing networking code that conflicts with Nakama
- Complex state management that's tightly coupled
- Custom input systems that don't support prediction
- Performance-critical systems that may be affected

**Medium Risk Items:**

- AutoLoad dependencies that may need reordering
- Scene structures that need multiplayer awareness
- UI systems that need multiplayer status display

**Low Risk Items:**

- Independent systems (audio, graphics, etc.)
- Static content and assets
- Single-player gameplay mechanics

#### 3.2 Risk Mitigation Strategies

For each identified risk, provide:

- **Specific Impact**: What problems could occur
- **Likelihood**: How likely is this to be a problem
- **Mitigation**: Specific steps to reduce risk
- **Rollback Plan**: How to undo changes if needed

### Phase 4: Integration Strategy Development

#### 4.1 Integration Approach Selection

**Recommend one of three approaches:**

**Approach A: Additive Integration (Recommended)**

- Add new multiplayer systems alongside existing code
- Preserve all existing functionality
- Create multiplayer-specific scenes
- Minimal risk to existing systems

**Approach B: Hybrid Integration**

- Enhance existing systems with multiplayer awareness
- Gradual transition from single-player to multiplayer
- Moderate integration complexity
- Some risk to existing systems

**Approach C: Comprehensive Refactor**

- Only when existing architecture fundamentally incompatible
- Significant changes to existing code
- High risk but potentially better long-term architecture
- Requires comprehensive testing

#### 4.2 Implementation Roadmap

Create step-by-step integration plan:

```
Integration Roadmap:

Phase 1: Foundation Setup (Low Risk)
- [ ] Install Nakama-Godot plugin
- [ ] Create NetworkManager AutoLoad
- [ ] Set up basic connection testing
- [ ] Validate existing functionality unchanged

Phase 2: Core Integration (Medium Risk)
- [ ] Implement authentication flow
- [ ] Create multiplayer scene variants
- [ ] Add network state synchronization
- [ ] Test single-player compatibility

Phase 3: Feature Development (Variable Risk)
- [ ] Implement specific multiplayer features
- [ ] Add multiplayer UI elements
- [ ] Performance optimization
- [ ] Comprehensive integration testing

Phase 4: Production Preparation (Low Risk)
- [ ] Deployment configuration
- [ ] Monitoring and logging
- [ ] Performance validation
- [ ] Rollback procedures
```

### Phase 5: Documentation and Handoff

#### 5.1 Analysis Report Creation

Generate comprehensive analysis report including:

**Project Summary:**

- Current architecture overview
- Key systems and dependencies
- Existing functionality assessment

**Compatibility Assessment:**

- Plugin compatibility matrix
- Architecture pattern compatibility
- Risk assessment with mitigation plans

**Integration Strategy:**

- Recommended approach with rationale
- Detailed implementation roadmap
- Success criteria and validation checkpoints

**Next Steps:**

- Immediate actions required
- Dependencies that must be resolved
- Recommended specialist handoffs

#### 5.2 Specialist Handoff Preparation

**For Multiplayer Architect:**

- Architecture constraints and requirements
- Performance requirements and current metrics
- Integration approach and technical requirements

**For Client Developer:**

- Current Godot project structure and patterns
- Existing code that must be preserved
- Integration points and modification requirements

**For Server Developer:**

- Game logic requirements and rules
- Data storage and persistence needs
- Performance and scalability requirements

## Quality Validation

### Analysis Completeness Checklist

- [ ] All project configuration analyzed
- [ ] Plugin compatibility assessed
- [ ] Architecture patterns documented
- [ ] Risk assessment completed
- [ ] Integration strategy defined
- [ ] Implementation roadmap created
- [ ] Specialist handoff packages prepared

### Risk Assessment Validation

- [ ] All high-risk items identified and mitigated
- [ ] Medium-risk items have monitoring plans
- [ ] Low-risk items documented for awareness
- [ ] Rollback procedures defined for each phase

## Success Criteria

The analysis is successful when:

1. **Complete Understanding**: Comprehensive knowledge of existing project
2. **Risk Clarity**: All potential issues identified with mitigation plans
3. **Clear Strategy**: Unambiguous integration approach selected
4. **Actionable Roadmap**: Step-by-step implementation plan
5. **Team Readiness**: All specialists have necessary context to proceed

## Handoff Statement

"Analysis complete. Project architecture understood, risks assessed, and integration strategy defined. Ready to proceed with [recommended approach] using the detailed roadmap. All specialist teams have necessary context to begin their work safely."
