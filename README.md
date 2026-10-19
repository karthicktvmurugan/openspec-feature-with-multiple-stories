# OpenSpec: Feature with Multiple Stories

A gated, multi-developer workflow schema for OpenSpec that breaks complex features into independently deliverable stories with rigorous review gates at every step.

## Overview

This schema enforces a structured workflow for planning and implementing features:

**Planning workflow:** proposal → specs → design → story-map → stories → tasks

**Key principles:**
- ✅ **Gated**: User confirmation required after each artifact
- 🔄 **Resumable**: Resume from the last unconfirmed artifact, with smart restart logic
- 👥 **Multi-developer**: Multiple developers can implement different stories in parallel
- 🛡️ **Immutable implemented stories**: Once a story is fully implemented, changes don't modify it—new stories are created for incremental changes
- ❌ **No gap filling**: Every gap is questioned; all unknowns are documented
- 📊 **INVEST-compliant**: Stories are vertical slices, independently deployable

## What's Included

```
schema/
├── schema.yaml                 # Optimized schema with extracted rules
├── templates/
│   ├── proposal.md            # Business case and scope
│   ├── spec.md                # Functional requirements in Given/When/Then
│   ├── design.md              # Architecture with Mermaid diagrams
│   ├── story-map.md           # Story sequence, dependencies, MVP ordering
│   ├── story.md               # Individual story with acceptance criteria
│   └── tasks.md               # Implementation checklist
```

## Schema Structure

### Rules (shared across all artifacts)
- **Gate**: No artifact proceeds without upstream dependencies confirmed
- **No gap filling**: Ask users; never assume or infer
- **Unknowns**: Record every unknown in "Open Questions & Unknowns" section

### Resume Strategy (handles changes mid-workflow)
- **Level detection**: Distinguish proposal/spec changes from design-only changes
- **Conditional reset**: Only affected stories reset to draft; unaffected ones stay confirmed
- **Immutable stories**: Fully implemented stories cannot be modified—new stories are created instead
- **New story proposal**: If a change logically calls for a new vertical slice, propose it

## Quick Start

### 1. Install OpenSpec

```bash
npm install -g @fission-ai/openspec
```

### 2. Add This Schema to Your Project

```bash
# Copy the schema into your project
mkdir -p openspec/schemas
cp -r schema/feature-with-multiple-stories openspec/schemas/

# Update openspec/config.yaml
echo "schema: feature-with-multiple-stories" > openspec/config.yaml
```

### 3. Create a Change

```bash
openspec new change my-feature --schema feature-with-multiple-stories
```

### 4. Follow the Gated Workflow

```bash
# 1. Draft proposal
openspec instructions proposal --change my-feature

# 2. Confirm proposal
# ... user reviews and confirms ...

# 3. Draft specs
openspec instructions specs --change my-feature

# ... continue through design, story-map, stories, tasks ...

# 4. Implement
openspec apply --change my-feature
```

## Workflow Details

### Proposal
- Business justification, problem statement, impact
- Identifies which specs will be new or modified
- High-level only; no detailed requirements

### Specs
- Functional requirements in Given/When/Then format
- Edge cases and error handling
- Spec-level (external behavior only); no technical details

### Design
- Architecture with Mermaid diagrams
- Components, responsibilities, interactions
- API contracts, data model, non-functional requirements
- Solution overview; no code or low-level implementation

### Story Map
- Stories sequenced by MVP order and dependencies
- Each story is a vertical slice (complete, testable, deployable)
- INVEST principle: Independent, Negotiable, Valuable, Estimable, Small, Testable

### Stories
- One file per story (stories-and-tasks/story-N/story-N.md)
- All scenarios (positive, negative, edge cases)
- Acceptance criteria
- No unknowns; must be complete before review

### Tasks
- One file per story (stories-and-tasks/story-N/task-N.md)
- Implementation checklist with verification steps
- Scoped to the story; no work beyond it

### Apply (Implementation)
- One story at a time
- **Parallelizable**: multiple developers can implement different stories simultaneously
- Only the chosen story must be confirmed; others can be in-review or draft

## Multi-Developer Scenarios

### Two developers, two stories

```
Story 1: ✅ IMPLEMENTED (all tasks done)
Story 2: ✅ CONFIRMED (ready for implementation)
Story 3: 🔄 IN-REVIEW (waiting for user confirmation)

Developer A: /opsx:apply → implements story 2
Developer B: /opsx:apply → implements story 3 in parallel
```

Both work independently. Conflicts handled at merge time in version control.

### Handling Changes Mid-Implementation

Change introduced after some stories are implemented:

1. **Restart logic determines**: Does this affect proposal/specs or only design?
2. **Affected assessment**: AI proposes which stories are affected, which stay confirmed
3. **User confirms**: User reviews and approves the affected/unaffected list
4. **Immutable protection**: Fully implemented stories are never modified
5. **New stories for incremental work**: If a change requires tweaking an implemented story, a new story is created instead

Example:
```
Story 1: ✅ IMPLEMENTED
Story 2: 🔄 IN-REVIEW
Story 3: ✏️ DRAFT

Change: Design updated to use caching

AI proposes:
  - Story 1: EXCLUDE (fully implemented, cannot modify)
  - Story 2: AFFECTED (caching impacts API design)
  - Story 3: UNAFFECTED (independent)
  - If caching tweak needed in story 1: propose new Story 4

User confirms. Only story 2 resets to draft.
```

## Customization

### Modify rules
Edit `schema/schema.yaml` in the `rules:` section. Changes apply everywhere they're referenced.

### Adjust artifact instructions
Edit individual artifact instructions in `schema.yaml`. Each artifact references the shared rules, so focus on unique guidance.

### Update templates
Edit files in `schema/templates/`. These are the starting point for each artifact.

### Add diagrams
Design uses Mermaid for architecture diagrams. Supports:
- Component diagrams (graph TB/LR)
- Sequence diagrams (sequenceDiagram)
- Flowcharts (graph TD)
- State diagrams (stateDiagram)

See [Mermaid documentation](https://mermaid.js.org)

## Examples

See the `examples/` folder for:
- A simple CRUD feature
- A multi-service integration
- A complex workflow with dependencies

## Contributing

Contributions welcome! Ways to help:
- Add more examples
- Improve templates based on feedback
- Document common patterns your team discovers
- Report issues or suggest enhancements

## License

MIT License - See LICENSE file

## Support

- OpenSpec documentation: https://github.com/fission-ai/openspec
- Mermaid diagrams: https://mermaid.js.org
- Questions? Open an issue on this repo

## Credits

Created for teams practicing specification-driven development with OpenSpec.

Version: 1.0  
Schema version: 3  
Last updated: 2026-10-19
