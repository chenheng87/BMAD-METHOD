# Execute Checklist Task

## Purpose

Execute comprehensive validation checklists with star ratings, detailed assessment, and actionable recommendations. This task ensures quality standards are met while providing clear guidance for improvements.

## Checklist Processing

### Star Rating System

- ⭐ = Basic functionality
- ⭐⭐ = Standard quality
- ⭐⭐⭐ = Production ready
- ⭐⭐⭐⭐ = High quality
- ⭐⭐⭐⭐⭐ = Critical/Essential

### Assessment Levels

- **Pass**: Item meets or exceeds requirements
- **Needs Work**: Item requires improvement before proceeding
- **N/A**: Item not applicable to current context
- **Blocked**: Item cannot be assessed due to missing dependencies

## Instructions

### 1. Checklist Selection

Present available checklists as numbered options:

```
Available validation checklists:
1. Godot-Nakama Integration Checklist
2. Brownfield Safety Checklist
3. Multiplayer Performance Checklist
4. Deployment Readiness Checklist

Please select checklist to execute (1-4):
```

### 2. Context Gathering

Before executing checklist, gather necessary context:

- Project information (if not provided)
- Specific areas of concern
- Assessment scope and depth required
- Available documentation/artifacts to review

### 3. Checklist Execution

For each checklist item:

#### Assessment Process

1. **Review Item**: Understand what needs validation
2. **Gather Evidence**: Request necessary information from user
3. **Evaluate**: Apply professional judgment against criteria
4. **Rate**: Assign star rating based on assessment
5. **Document**: Record findings and recommendations

#### Presentation Format

```
## [Category Name]

### [Item Name] ⭐⭐⭐⭐
- **Status**: Pass/Needs Work/N/A/Blocked
- **Assessment**: [Detailed evaluation]
- **Evidence**: [What was reviewed]
- **Recommendations**: [Specific improvement suggestions]
- **Next Steps**: [Actionable items if needed]
```

### 4. Summary Report

After completing all items, provide comprehensive summary:

#### Overall Assessment

- Total items assessed
- Pass/Fail breakdown by star rating
- Critical issues identified
- Overall readiness level

#### Priority Actions

List highest priority items requiring attention:

1. **Critical Issues** (⭐⭐⭐⭐⭐ items that failed)
2. **High Priority** (⭐⭐⭐⭐ items needing work)
3. **Standard Priority** (⭐⭐⭐ items for improvement)

#### Success Metrics

Define what "ready" looks like:

- All ⭐⭐⭐⭐⭐ items must pass
- All ⭐⭐⭐⭐ items should pass
- Majority of ⭐⭐⭐ items should pass

### 5. Action Planning

Provide specific guidance for addressing failures:

```
## Action Plan

### Immediate Actions (Do First)
- [ ] [Critical issue 1 - specific steps]
- [ ] [Critical issue 2 - specific steps]

### Short Term Actions (Do Next)
- [ ] [High priority item 1 - specific steps]
- [ ] [High priority item 2 - specific steps]

### Ongoing Improvements
- [ ] [Standard improvement 1]
- [ ] [Standard improvement 2]
```

## User Interaction Guidelines

### For Information Requests

- Be specific about what information is needed
- Explain why the information is important for assessment
- Provide examples of good responses
- Offer alternatives if direct information unavailable

### For Failed Items

- Explain clearly why item failed
- Provide specific, actionable recommendations
- Suggest resources or references when helpful
- Estimate effort required for fixes

### For Complex Assessments

- Break down complex items into sub-components
- Use progressive disclosure for detailed findings
- Prioritize most important aspects first
- Provide both technical and business context

## Quality Standards

### Assessment Accuracy

- Base ratings on objective criteria when possible
- Clearly distinguish between facts and professional judgment
- Acknowledge limitations in assessment scope
- Request additional information when needed for accuracy

### Recommendation Quality

- Provide specific, actionable recommendations
- Prioritize recommendations by impact and effort
- Include relevant context and reasoning
- Reference industry standards and best practices

## Success Criteria

- All checklist items thoroughly assessed
- Clear pass/fail determinations with supporting evidence
- Actionable recommendations for all failed items
- Overall readiness assessment with confidence level
- Clear next steps for achieving quality goals
