> **Review status:** Draft

## Why

<!-- Problem or opportunity from the user's perspective. Why is this change required? Why now? -->

## Business Metrics

<!-- Business metrics this change should move, with baseline and target where known. Do not invent; ask the user. -->

## What Changes

<!-- High-level changes. Be specific about new capabilities, modifications, or removals. No detailed spec or technical implementation details. -->

## Capabilities

### New Capabilities
<!-- Capabilities being introduced. Use kebab-case for path segments you introduce
     (e.g., user-auth or identity/user-auth) that follow the project's existing
     spec organization. Each creates specs/<capability-path>/spec.md. -->
- `<capability-path>`: <brief description of what this capability covers>

### Modified Capabilities
<!-- Existing capabilities whose REQUIREMENTS are changing (not just implementation).
     Only list here if spec-level behavior changes. Each needs a delta spec file.
     Use the exact existing path under openspec/specs/. Leave empty if no requirement
     changes. A change with no capabilities at all (pure refactor, tooling, docs)
     must set `skip_specs: true` in its .openspec.yaml - openspec validate rejects
     a zero-delta change without that marker. Do not invent a requirement just to
     satisfy validation. -->
- `<existing-capability-path>`: <what requirement is changing>

## Impact

<!-- Affected specs, systems, teams and other areas. High level only. -->

## Open Questions & Unknowns

<!-- | # | Question / Unknown | Status (open/resolved) | User's answer | Date | -->
