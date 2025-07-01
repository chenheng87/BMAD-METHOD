# BMAD Template Format Specification

## Overview

BMAD templates use a sophisticated markup system that combines document structure with embedded AI processing instructions. This specification defines the syntax and processing rules for all BMAD templates.

## Core Markup Elements

### Variable Substitution

```markdown
{{variable_name}}
```

- **Purpose**: Placeholder for dynamic content
- **Processing**: Replaced with actual values during document generation
- **Example**: `{{project_name}}` becomes `"My Game Project"`

### AI Processing Instructions

```markdown
[[LLM: instruction text]]
```

- **Purpose**: Embedded instructions for AI agents
- **Processing**: Used by AI for guidance, never displayed to users
- **Example**: `[[LLM: Ask user about their preferred networking approach]]`

### Conditional Content Blocks

```markdown
^^CONDITION_NAME^^
Content that appears when condition is met
^^/CONDITION_NAME^^
```

- **Purpose**: Include/exclude content based on conditions
- **Processing**: Evaluated during template processing
- **Example**:
  ```markdown
  ^^MULTIPLAYER^^
  This section only appears for multiplayer games
  ^^/MULTIPLAYER^^
  ```

### Guidance Examples

```markdown
@{example_content}
```

- **Purpose**: Provide guidance without including in final output
- **Processing**: Used by AI for context, never shown to users
- **Example**: `@{Common player counts: 2-4 for competitive, 8+ for social}`

### Repeatable Sections

```markdown
REPEAT: section_name
Template content that can be repeated
/REPEAT: section_name
```

- **Purpose**: Define content that may appear multiple times
- **Processing**: AI can repeat section as needed
- **Example**:
  ```markdown
  REPEAT: feature

  - **{{feature_name}}**: {{feature_description}}
    /REPEAT: feature
  ```

## Advanced Markup

### Nested Variables

```markdown
{{section.subsection.variable}}
```

- **Purpose**: Hierarchical variable references
- **Processing**: Access nested data structures
- **Example**: `{{game.settings.max_players}}`

### Variable Modifiers

```markdown
{{variable_name|modifier}}
```

- **Purpose**: Apply formatting or transformation
- **Common Modifiers**:
  - `|upper` - Convert to uppercase
  - `|lower` - Convert to lowercase
  - `|title` - Title case formatting
  - `|default:value` - Use default if variable empty

### Conditional Variables

```markdown
{{variable_name?condition:value_if_true:value_if_false}}
```

- **Purpose**: Conditional variable substitution
- **Processing**: Evaluate condition and use appropriate value
- **Example**: `{{player_count?multiplayer:Many Players:Single Player}}`

## Processing Rules

### Order of Operations

1. **Parse Structure**: Identify all markup elements
2. **Process Conditions**: Evaluate conditional blocks
3. **Execute LLM Instructions**: Apply AI processing directives
4. **Substitute Variables**: Replace all variable placeholders
5. **Clean Output**: Remove processing markup, format final document

### Error Handling

- **Missing Variables**: Log warning, leave placeholder or use default
- **Invalid Syntax**: Report error with line number and suggestion
- **Circular References**: Detect and report with resolution suggestion
- **Malformed Conditions**: Provide clear error message and example

### Validation Rules

- All `[[LLM:]]` blocks must be properly closed
- Variable names must be valid identifiers
- Conditional blocks must have matching open/close tags
- No nested `[[LLM:]]` blocks allowed

## Template Structure Guidelines

### Document Organization

```markdown
# {{document_title}}

[[LLM: Initial processing instructions for entire document]]

## Section 1: {{section_name}}

[[LLM: Section-specific instructions]]

{{section_content}}

## Section 2: {{another_section}}

[[LLM: Different section instructions]]

{{more_content}}

[[LLM: Final processing and validation instructions]]
```

### Best Practices

#### For Template Authors

- Use descriptive variable names
- Keep LLM instructions focused and specific
- Group related variables logically
- Provide clear examples in guidance sections
- Test templates with various input scenarios

#### For AI Agents

- Process LLM instructions in order
- Maintain context between sections
- Validate all variable substitutions
- Ensure output quality meets standards
- Handle errors gracefully with user feedback

#### For Variable Naming

- Use `snake_case` for consistency
- Be descriptive: `player_count` not `pc`
- Group related variables: `game.title`, `game.genre`
- Avoid reserved words and special characters

## Integration with BMAD Tasks

### Template Loading

Templates are loaded by the `create-doc` task, which:

- Parses template markup
- Executes LLM instructions
- Manages user interaction for variable collection
- Processes conditional logic
- Generates final document

### Quality Assurance

- All variables must be resolved
- LLM instructions must be processed
- Output must be clean of markup
- Document structure must be preserved
- Content quality must meet standards

## Examples

### Simple Template

```markdown
# {{project_name}} Requirements

[[LLM: Ask user about their project goals and target audience]]

## Project Overview

**Project Name**: {{project_name}}
**Target Platform**: {{target_platform}}
**Expected Players**: {{player_count}}

[[LLM: Based on player count, provide multiplayer guidance if > 1]]
```

### Complex Template

```markdown
# {{game_title}} Technical Architecture

[[LLM: This template creates technical architecture docs. Ask about existing systems first.]]

^^EXISTING_PROJECT^^

## Current System Analysis

**Existing Technology**: {{current_tech_stack}}
**Migration Strategy**: {{migration_approach}}
^^/EXISTING_PROJECT^^

REPEAT: system_component

### {{component_name}}

**Purpose**: {{component_purpose}}
**Technology**: {{component_tech}}
**Dependencies**: {{component_deps}}
/REPEAT: system_component

[[LLM: Validate architecture completeness and suggest improvements]]
```

This specification ensures consistent, powerful template processing across all BMAD expansion packs while maintaining clarity and usability.
