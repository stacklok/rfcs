# RFC repository guidelines

This repository holds design documents (RFCs) for Stacklok projects, one folder per project. These rules apply to every project. Each project folder has its own `AGENTS.md` with project-specific rules; **read the root file and the file in the project folder you are working in before writing, reviewing or editing an RFC.**

## Layout

```
template.md          Shared RFC template
<project>/           One folder per project
├── AGENTS.md        Project scope, repositories, architecture context, conventions
└── <PREFIX>-NNNN-descriptive-name.md
```

| Project | Folder | Prefix | Guidelines |
|---------|--------|--------|------------|
| ToolHive ecosystem | `toolhive/` | `THV` | [toolhive/AGENTS.md](toolhive/AGENTS.md) |
| Mecatl | `mecatl/` | `MEC` | [mecatl/AGENTS.md](mecatl/AGENTS.md) |

If the user doesn't say which project an RFC belongs to, ask. Never create RFCs at the repository root.

## File naming

`<project>/<PREFIX>-<NNNN>-<kebab-case-name>.md`, for example `toolhive/THV-0083-stateless-vmcp.md`.

- `NNNN` is the pull request number, zero-padded to four digits. The sequence is shared across projects; only the prefix differs.
- The PR number isn't known until the PR exists. Draft as `<PREFIX>-XXXX-<name>.md` and tell the user to rename the file once the PR is opened.
- CI (`.github/workflows/validate-proposal-naming.yml`) rejects new files whose folder isn't registered in its `PREFIXES` map or whose name doesn't match the rule above.

## Writing an RFC

1. Start from [`template.md`](template.md). Keep its section order. A section that doesn't apply gets a one-line justification, not deletion.
2. Fill in the metadata block: Status (`Draft` for new RFCs), Author(s), Created, Last Updated, Target Repository, Related Issues.
3. **Security Considerations is required for every RFC.** Address all of: Threat Model, Authentication and Authorization, Data Security, Input Validation, Secrets Management, Audit and Logging, Mitigations. "N/A" needs a reason.
4. Use Mermaid for diagrams, concrete examples instead of placeholders, and never put real secrets in examples.
5. Keep each RFC to one cohesive change. Split large proposals.
6. Read the existing RFCs in the project folder first. Check for ones that overlap, conflict with or are superseded by the proposal.
7. Commits need a `Signed-off-by` trailer (Developer Certificate of Origin). PR titles look like `RFC: <short description>`.

## Reviewing an RFC

Check, in order: structure and completeness against the template; security section (all seven areas, no unjustified "N/A", no threat model missing for network-exposed features); technical accuracy against the project's architecture context; diagrams and examples; feasibility, phasing and cross-repo impact. Also apply the project's own review checks from its `AGENTS.md`.

## Lifecycle

Statuses: Draft, Under Review, Accepted, Rejected, Implemented, Superseded. After acceptance, update the RFC with implementation PR links, deviations from the design, and the final status.

## Skills

The `write-rfc`, `review-rfc` and `respond-to-rfc-comments` skills in `.claude/skills/` work for every project. They take project-specific knowledge from the project's `AGENTS.md`, so put it there rather than in a skill.

## Adding a project

1. Create `<project>/AGENTS.md` (copy `mecatl/AGENTS.md` as a starting point).
2. Register the folder and prefix in the `PREFIXES` map in `.github/workflows/validate-proposal-naming.yml`.
3. Add a row to the table above and to the Projects table in `README.md`.
