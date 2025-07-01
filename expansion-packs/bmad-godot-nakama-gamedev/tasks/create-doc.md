# Create Document Task

## Purpose

Create documents from templates with embedded LLM instructions and dynamic content generation. This task handles the complete document creation workflow including template processing, user interaction, and content validation.

## Template Processing

This task follows the BMAD template format system:

- `{{placeholders}}` - Variables to be replaced with actual content
- `[[LLM: instructions]]` - AI processing directives (never shown to users)
- `^^CONDITION^^` - Conditional content blocks
- `@{examples}` - Guidance examples (processing hints only)
- `REPEAT` sections - Repeatable content blocks

## User Interaction Modes

### Mode 1: Incremental Generation (Default)

- Present template sections one at a time
- Allow user input and refinement for each section
- Build document progressively with user collaboration

### Mode 2: Rapid Generation

- Generate complete document quickly based on brief user input
- Suitable for users who want fast results
- Can be refined afterward using Mode 1 approach

## Instructions

### 1. Template Selection

Ask the user which document they want to create, showing available templates as numbered options:

```
Available document templates:
1. Godot-Nakama Integration Plan
2. Client-Server Architecture
3. Godot Client Architecture
4. Nakama Server Modules
5. Multiplayer Game Requirements
6. Network Sync Strategy

Please select a template (1-6):
```

### 2. Mode Selection

After template selection, ask for generation mode:

```
How would you like to create this document?

1. **Incremental Mode** (Recommended) - Work through each section together for best quality
2. **Rapid Mode** - Quick generation based on brief requirements

Please select mode (1-2):
```

### 3. Document Generation

#### For Incremental Mode:

- Load the selected template
- Process any `[[LLM: instructions]]` sections internally
- Present first section to user for input
- Continue section by section until complete
- Offer refinement opportunities

#### For Rapid Mode:

- Gather basic requirements from user
- Generate complete document using template intelligence
- Present for user review and refinement

### 4. Quality Assurance

- Ensure all placeholder variables are replaced
- Validate document completeness
- Check for consistency and clarity
- Offer final review and editing opportunity

### 5. Document Delivery

Present the final document in a clear, copyable format:

```markdown
# Final Document

[Complete generated document here]

---

**Instructions**: Copy this document and save it to your project's appropriate location.
```

## Template Intelligence Integration

This task leverages embedded template intelligence through `[[LLM: instructions]]` blocks which provide:

- Section-specific guidance and questioning
- Content structure recommendations
- Domain-specific best practices
- Quality validation criteria

## Error Handling

- If template not found, list available options
- If user input insufficient, request clarification
- If generation fails, offer alternative approaches
- Always provide helpful error messages

## Success Criteria

- Document matches template structure and requirements
- All user requirements captured accurately
- Professional quality suitable for project use
- Clear next steps provided to user
