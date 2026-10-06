---
name: write-rfc
description: Write RFCs for any project in this repository (toolhive, mecatl, ...). Use when the user wants to create a new RFC, proposal, or design document for a project covered here, including the toolhive, toolhive-studio, toolhive-registry, toolhive-registry-server, toolhive-cloud-ui, or dockyard repositories.
allowed-tools: Read, Glob, Grep, Bash(git:*), mcp__github__*, mcp__fetch__fetch, WebFetch, Task, Edit, Write, AskUserQuestion
---

# Write RFC Skill

This skill helps you write high-quality RFCs for the projects in this repository following established patterns and conventions.

## Overview

RFCs live in one folder per project and are named `<project>/<PREFIX>-{NUMBER}-{descriptive-name}.md`. The NUMBER must match the PR number and be zero-padded to 4 digits. Project-specific knowledge (scope, repositories, architecture docs, conventions) lives in `<project>/AGENTS.md`, not in this skill.

## Workflow

### Step 1: Identify the Project and Gather Requirements

1. Read the root `AGENTS.md`.
2. Determine the project (folder). If the user hasn't said, ask. Then read `<project>/AGENTS.md`; it defines the prefix, target repositories, architecture docs and conventions.

Then ask the user about:

1. **Problem Statement**: What problem are they trying to solve?
2. **Target Repository**: Which repository does this affect? Offer the list from the project's `AGENTS.md`, plus `multiple` for cross-cutting changes.
3. **Scope**: What are the goals and explicit non-goals?

### Step 2: Research

Before drafting:

1. Read the architecture docs and code locations listed under "Research before writing or reviewing" in the project's `AGENTS.md` (use `mcp__github__get_file_contents` or `mcp__github__search_code`).
2. Read the existing RFCs in `<project>/` to understand patterns and find related proposals.

### Step 3: Draft the RFC

Create the RFC following the template structure from `template.md`.

#### Required Metadata

```markdown
# RFC-XXXX: Title

- **Status**: Draft
- **Author(s)**: Name (@github-handle)
- **Created**: YYYY-MM-DD
- **Last Updated**: YYYY-MM-DD
- **Target Repository**: [from step 1]
- **Related Issues**: [links if applicable]
```

#### Core Sections

1. **Summary** - 2-3 sentences capturing the essence
2. **Problem Statement** - Current limitation, who's affected, why it matters
3. **Goals** - Specific objectives (bulleted)
4. **Non-Goals** - Explicit scope boundaries
5. **Proposed Solution**
   - High-Level Design (with Mermaid diagrams)
   - Detailed Design: Component changes, API changes, configuration changes, data model changes
6. **Security Considerations** (REQUIRED) - See security checklist below
7. **Alternatives Considered** - Other approaches evaluated
8. **Compatibility** - Backward and forward compatibility
9. **Implementation Plan** - Phased approach with tasks
10. **Testing Strategy** - Unit, integration, E2E, performance, security tests
11. **Documentation** - What needs documenting
12. **Open Questions** - Unresolved items
13. **References** - Related links

#### Security Considerations Checklist (REQUIRED)

Every RFC MUST address:

- [ ] **Threat Model** - Potential threats, attacker capabilities
- [ ] **Authentication and Authorization** - Auth changes, permission models
- [ ] **Data Security** - Sensitive data handling, encryption
- [ ] **Input Validation** - User input, injection vectors
- [ ] **Secrets Management** - Credentials storage, rotation
- [ ] **Audit and Logging** - Security events, compliance
- [ ] **Mitigations** - Security controls implemented

### Step 4: Use Proper Conventions

Follow the "Conventions" section of the project's `AGENTS.md` (code example languages, API and CRD conventions, terminology). Generally:

- Use **YAML** for configuration examples
- Use **Mermaid** for diagrams (flowcharts, sequence diagrams)

### Step 5: File Naming

Name the file `<project>/<PREFIX>-XXXX-{descriptive-name}.md`, where `<PREFIX>` comes from the project's `AGENTS.md` and XXXX is the PR number. Since you don't know the PR number yet, use the `XXXX` placeholder and remind the user to rename the file to match the PR number after creating the PR.

### Step 6: Review Checklist

Before finalizing, verify:

- [ ] Problem is clearly stated
- [ ] Goals and non-goals are explicit
- [ ] Security section is complete (all 7 areas addressed)
- [ ] Alternatives are discussed
- [ ] Diagrams illustrate complex flows
- [ ] Code examples are concrete and in the correct language
- [ ] Implementation phases are defined
- [ ] Testing strategy covers all levels
- [ ] File is in the project folder and follows the naming convention
- [ ] Project-specific conventions from `<project>/AGENTS.md` are followed

## Reference Files

- Shared rules: `AGENTS.md`
- Project rules: `<project>/AGENTS.md`
- Template: `template.md`
- Contributing guide: `CONTRIBUTING.md`
- Existing RFCs: `<project>/*.md`
