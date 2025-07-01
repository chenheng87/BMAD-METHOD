# BMAD Workflow Management System

## Overview

The BMAD workflow management system orchestrates complex multi-agent workflows, manages handoffs between agents, and ensures proper validation at each stage. This system is essential for coordinating the sophisticated agent interactions in BMAD expansion packs.

## Core Concepts

### Workflow Phases

Workflows are organized into distinct phases:

- **Analysis Phase**: Understanding current state and requirements
- **Planning Phase**: Strategic design and architecture planning
- **Implementation Phase**: Parallel development and integration
- **Validation Phase**: Quality assurance and compatibility testing
- **Deployment Phase**: Production readiness and rollout

### Agent Handoffs

Structured transitions between agents with:

- **Context Transfer**: Complete information package for next agent
- **Validation Gates**: Quality checks before handoff
- **Rollback Points**: Safe return to previous phase if needed
- **Decision Trees**: Conditional routing based on assessment results

### Workflow States

Each workflow maintains state tracking:

- **Current Phase**: Where the workflow currently stands
- **Completed Artifacts**: Documents and deliverables created
- **Pending Actions**: Next steps requiring attention
- **Blocking Issues**: Problems preventing progression
- **Quality Gates**: Validation checkpoints and their status

## Workflow Orchestration

### Phase Management

#### Phase Initiation

```yaml
phase:
  name: "Project Analysis"
  entry_criteria:
    - user_requirements_defined
    - project_access_available
  primary_agent: godot-project-analyzer
  support_agents: [godot-nakama-orchestrator]
  expected_duration: "1-2 hours"
```

#### Phase Execution

1. **Agent Activation**: Primary agent takes control
2. **Task Execution**: Agent performs defined tasks
3. **Artifact Creation**: Documents and deliverables produced
4. **Quality Validation**: Self-check and peer review
5. **Handoff Preparation**: Package context for next phase

#### Phase Completion

- All required artifacts created and validated
- Quality gates passed
- Next phase requirements satisfied
- Handoff context prepared and verified

### Agent Coordination

#### Parallel Execution

When multiple agents work simultaneously:

- **Workstream Separation**: Clear boundaries between agent responsibilities
- **Synchronization Points**: Regular coordination meetings
- **Conflict Resolution**: Process for handling overlapping concerns
- **Integration Planning**: Strategy for combining parallel work

#### Sequential Handoffs

For dependent work streams:

- **Context Package**: Complete information transfer
- **Validation Handshake**: Receiving agent confirms understanding
- **Quality Review**: Previous work meets requirements
- **Rollback Protocol**: Return mechanism if issues discovered

### Decision Management

#### Decision Points

Workflows include structured decision points:

```yaml
decision:
  trigger: "Architecture complexity assessment"
  options:
    simple_integration:
      condition: "Low complexity, existing patterns"
      next_phase: "Direct Implementation"
    complex_integration:
      condition: "High complexity, architectural changes"
      next_phase: "Detailed Architecture Design"
    blocked_integration:
      condition: "Incompatible requirements"
      next_phase: "Requirements Refinement"
```

#### Decision Criteria

- **Technical Factors**: Complexity, compatibility, performance
- **Business Factors**: Timeline, resources, risk tolerance
- **Quality Factors**: Standards, maintainability, testability
- **Risk Factors**: Implementation risk, integration risk, rollback complexity

## Quality Assurance Integration

### Validation Gates

Each phase includes validation checkpoints:

#### Entry Validation

- Prerequisites satisfied
- Required information available
- Agent readiness confirmed
- Resource availability verified

#### Progress Validation

- Intermediate deliverables reviewed
- Quality standards maintained
- Timeline adherence checked
- Risk factors monitored

#### Exit Validation

- Phase objectives completed
- Quality gates passed
- Handoff requirements satisfied
- Next phase readiness confirmed

### Continuous Improvement

- **Workflow Metrics**: Track phase duration, quality scores, rework rates
- **Agent Performance**: Monitor task completion, quality ratings, user satisfaction
- **Process Refinement**: Regular workflow optimization based on feedback
- **Knowledge Capture**: Document lessons learned and best practices

## Brownfield Workflow Specialization

### Safety-First Progression

Brownfield workflows prioritize safety:

- **Non-Destructive Analysis**: Examine without modifying
- **Incremental Changes**: Small, reversible modifications
- **Validation Loops**: Confirm compatibility at each step
- **Rollback Ready**: Always maintain path to previous state

### Risk Management

- **Compatibility Assessment**: Early identification of potential conflicts
- **Impact Analysis**: Understand scope of changes required
- **Mitigation Planning**: Strategies for handling identified risks
- **Contingency Preparation**: Backup plans for common failure scenarios

### Integration Patterns

- **Additive Integration**: New functionality alongside existing
- **Replacement Integration**: Careful migration from old to new
- **Hybrid Integration**: Partial adoption with fallback options
- **Parallel Integration**: New system alongside existing with gradual migration

## User Experience Management

### Progress Communication

- **Phase Announcements**: Clear communication of workflow progression
- **Milestone Celebrations**: Recognition of completed phases
- **Blocker Notification**: Transparent communication of obstacles
- **Next Step Guidance**: Clear direction for user actions

### Interaction Patterns

- **Approval Gates**: User confirmation before proceeding
- **Choice Points**: User decisions that affect workflow direction
- **Information Requests**: Structured data gathering from users
- **Feedback Loops**: User input on quality and satisfaction

### Workflow Transparency

Users always understand:

- Where they are in the workflow
- What has been accomplished
- What comes next
- How to get help or make changes
- How to exit or restart if needed

## Implementation Guidelines

### For Orchestrator Agents

- Maintain workflow state throughout process
- Provide clear phase transitions and announcements
- Handle exceptions and rollbacks gracefully
- Ensure user understanding and approval at key points

### For Specialist Agents

- Understand your role in the larger workflow
- Prepare proper handoff packages for next agents
- Validate inputs from previous phases
- Communicate blockers and issues promptly

### For Quality Assurance

- Validate phase completion before allowing progression
- Ensure artifact quality meets standards
- Verify handoff completeness and accuracy
- Monitor overall workflow health and progress

This workflow management system ensures coordinated, high-quality outcomes while maintaining the flexibility and safety required for complex brownfield integrations.
