# RFCs

This repository contains Requests for Comments (RFCs) for Stacklok projects, organized by project. RFCs are design documents that describe significant changes, new features, or architectural decisions.

## What is an RFC?

An RFC (Request for Comments) is a design document that proposes a significant change to a project. RFCs provide a consistent and controlled path for new features and changes to enter the project, ensuring that all stakeholders have an opportunity to provide feedback.

## When to Write an RFC

You should write an RFC for:

- New features that affect multiple components or repositories
- Significant architectural changes
- Changes that affect the public API or user-facing behavior
- Security-sensitive changes
- Cross-cutting concerns that span multiple projects or repositories
- Breaking changes or deprecations

You probably **don't** need an RFC for:

- Bug fixes
- Documentation improvements
- Minor refactoring
- Performance improvements that don't change behavior
- Changes isolated to a single component with no external impact

## Projects

Each project has its own folder, filename prefix and `AGENTS.md` describing its scope, repositories and conventions. Because most RFCs are drafted with AI assistance, that file is where project guidelines live: AI tools read it automatically, and it is just as readable by people.

| Project | Folder | Prefix |
|---------|--------|--------|
| ToolHive ecosystem | [`toolhive/`](toolhive/AGENTS.md) | `THV` |
| Mecatl | [`mecatl/`](mecatl/AGENTS.md) | `MEC` |

To onboard a new project, see [Adding a project](AGENTS.md#adding-a-project) in the root `AGENTS.md`.

## RFC Process

### 1. Pre-RFC Discussion (Optional)

Before writing a full RFC, consider opening a thread on [Discord](https://discord.gg/stacklok) to gather initial feedback on your idea. This can help refine the proposal before investing time in a full RFC.

### 2. Create the RFC

1. Fork this repository
2. Copy `template.md` to `<project>/<PREFIX>-XXXX-descriptive-name.md` (e.g. `toolhive/THV-XXXX-descriptive-name.md`)
   - Keep `XXXX` as a placeholder while drafting, then rename the file to the number of your Pull Request once it is open
   - Use a short, descriptive name with hyphens
3. Fill in the RFC template
4. Submit a Pull Request

### 3. RFC Review

- The RFC will be reviewed by maintainers and community members
- Feedback will be provided via PR comments
- The author should address feedback and update the RFC as needed
- Discussion should focus on technical merit and alignment with project goals

### 4. RFC Decision

RFCs can be:
- **Accepted**: The RFC is approved and can be implemented
- **Rejected**: The RFC is not approved (with explanation)
- **Superseded**: A newer RFC replaces it
- **Implemented**: The accepted RFC has been implemented

### 5. Implementation

Once accepted, the RFC can be implemented. The RFC should be updated with:
- Links to implementation PRs
- Any deviations from the original design
- Final status (implemented, partially implemented, superseded)

## RFC Numbering

RFCs are numbered based on the PR numbers, so they are incremental, but not necessarily sequential (0001, 0002, 0004, etc.). The number sequence is shared across all projects; only the prefix differs. Draft with `XXXX` and rename the file to your PR number once the PR is open. A CI task will ensure you're using the right number.

For RFCs that originate from issues in specific repositories, you may reference the issue number in the RFC (e.g., "This RFC addresses toolhive#1234").

## Directory Structure

```
rfcs/
├── README.md                    # This file
├── CONTRIBUTING.md              # Contribution guidelines
├── AGENTS.md                    # Shared rules for AI assistants and authors
├── template.md                  # RFC template shared by all projects
├── toolhive/                    # One folder per project
│   ├── AGENTS.md                # Project scope, repositories and conventions
│   └── THV-XXXX-*.md            # RFCs, prefixed per project
└── mecatl/
    ├── AGENTS.md
    └── MEC-XXXX-*.md
```

## License

This repository is licensed under the Apache License 2.0. See [LICENSE](LICENSE) for details.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines on writing and submitting RFCs.
