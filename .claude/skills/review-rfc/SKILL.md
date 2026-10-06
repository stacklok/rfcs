---
name: review-rfc
description: Review RFCs for any project in this repository (toolhive, mecatl, ...). Use when the user wants to review, critique, or provide feedback on an RFC, including ones for the toolhive, toolhive-studio, toolhive-registry, toolhive-registry-server, toolhive-cloud-ui, or dockyard repositories.
allowed-tools: Read, Glob, Grep, Bash(git:*), mcp__github__*, mcp__fetch__fetch, WebFetch, Task
---

# Review RFC Skill

This skill helps you thoroughly review RFCs for the projects in this repository, ensuring they meet quality standards, architectural alignment, and security requirements.

## Overview

When reviewing an RFC, you should evaluate it against multiple dimensions: completeness, technical accuracy, architectural alignment, security considerations, and feasibility.

## Review Workflow

### Step 1: Read the RFC

First, read the RFC document completely. If provided a PR number or file path, fetch and read it.

### Step 2: Load Project Context

Read the root `AGENTS.md`, then the `AGENTS.md` in the RFC's project folder. Use its "Research before writing or reviewing" section to fetch the architecture docs relevant to this RFC (for example with `mcp__github__get_file_contents`), and use its architecture summary, design principles and conventions as the standard to review against.

### Step 3: Check Related Existing RFCs

Search the project folder for related RFCs that might:
- Conflict with the proposal
- Be superseded by the proposal
- Provide context or dependencies

### Step 4: Verify Against Target Repository

Search the target repository to verify:
- Proposed changes align with existing code patterns
- No conflicts with recent changes
- API changes are compatible with existing interfaces

## Review Checklist

### A. Structure and Completeness

- [ ] **Metadata present**: Status, Author, Created, Last Updated, Target Repository
- [ ] **Summary**: Clear 2-3 sentence description
- [ ] **Problem Statement**: Clearly articulates the problem, who's affected, why it matters
- [ ] **Goals**: Specific, measurable objectives listed
- [ ] **Non-Goals**: Explicit scope boundaries defined
- [ ] **Proposed Solution**: Detailed design with diagrams where appropriate
- [ ] **Security Considerations**: All required subsections present (see below)
- [ ] **Alternatives Considered**: At least one alternative evaluated
- [ ] **Compatibility**: Backward and forward compatibility addressed
- [ ] **Implementation Plan**: Phased approach with concrete tasks
- [ ] **Testing Strategy**: Multiple test levels covered
- [ ] **Open Questions**: Unresolved items listed (if any)

### B. Security Review (CRITICAL)

The Security Considerations section MUST address all of these:

| Section | Questions to Verify |
|---------|---------------------|
| **Threat Model** | Are potential threats identified? Are attacker capabilities considered? |
| **Authentication** | How does this affect auth? Are new auth requirements clear? |
| **Authorization** | What permission checks are needed? Any new permission models? |
| **Data Security** | Is sensitive data identified? Is encryption addressed? |
| **Input Validation** | What user input is accepted? How is it validated? |
| **Secrets Management** | Are secrets handled properly? Can they be rotated? |
| **Audit and Logging** | Are security events logged? Compliance considered? |
| **Mitigations** | Are concrete mitigations proposed for identified threats? |

**Red flags to watch for:**
- Missing or superficial security section
- "N/A" without justification for security subsections
- No threat model for network-exposed features
- Secrets in configuration examples
- Missing input validation for user-provided data
- No audit logging for security-relevant operations

### C. Technical Accuracy

- [ ] **Correct terminology**: Uses the project's concepts correctly (see the project's `AGENTS.md`)
- [ ] **Architecture alignment**: Follows the design principles in the project's `AGENTS.md`
- [ ] **Code examples**: Syntactically correct, idiomatic for the language
- [ ] **API design**: Consistent with existing APIs in the target repo
- [ ] **Project conventions**: Follows the "Conventions" section of the project's `AGENTS.md` (CRDs, configuration formats, etc.)

### D. Diagrams and Examples

- [ ] **Mermaid diagrams**: Complex flows illustrated clearly
- [ ] **Code examples**: Concrete, not abstract placeholders
- [ ] **Configuration examples**: Realistic YAML/JSON examples
- [ ] **Sequence diagrams**: For multi-component interactions

### E. Feasibility and Impact

- [ ] **Implementation complexity**: Is the phased approach realistic?
- [ ] **Dependencies**: Are external dependencies identified?
- [ ] **Breaking changes**: Are migration paths provided if needed?
- [ ] **Performance impact**: Considered where relevant?
- [ ] **Cross-repo impact**: If `multiple` repos, are all impacts identified?

## Project Context

Target repositories, architecture principles to verify, and domain-specific checks (such as CRD types for Kubernetes RFCs) are defined per project in `<project>/AGENTS.md`. Verify the RFC against each design principle listed there.

## Review Output Format

Structure your review as follows:

```markdown
## RFC Review: [RFC Title]

### Summary
[1-2 sentence summary of your overall assessment]

### Strengths
- [What the RFC does well]

### Areas for Improvement

#### Critical Issues (Must Fix)
- [Issues that must be addressed before acceptance]

#### Suggestions (Should Consider)
- [Improvements that would strengthen the RFC]

#### Minor/Nitpicks (Optional)
- [Small improvements or style suggestions]

### Security Assessment
[Specific feedback on the security section]

### Architectural Alignment
[How well does this align with the project's architecture and design principles?]

### Questions for the Author
- [Clarifying questions that need answers]

### Recommendation
[ ] Ready to accept
[ ] Accept with minor changes
[ ] Needs revision (address critical issues)
[ ] Major rework needed
```

## Common Issues to Watch For

### Problem Statement Issues
- Too vague or abstract
- Doesn't explain who benefits
- Problem already solved elsewhere

### Design Issues
- Over-engineered for the problem
- Missing error handling considerations
- Doesn't consider edge cases
- Breaks existing functionality without migration path

### Security Issues
- Missing threat model
- Hardcoded credentials in examples
- No input validation
- Missing audit logging
- Overly permissive defaults

### Implementation Issues
- Unrealistic phasing
- Missing dependencies
- No rollback plan
- Insufficient testing strategy

## Reference Files

- Shared rules: `AGENTS.md`
- Project rules: `<project>/AGENTS.md`
- Template: `template.md`
- Contributing guide: `CONTRIBUTING.md`
- Existing RFCs: `<project>/<PREFIX>-*.md`
