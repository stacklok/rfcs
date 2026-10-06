# ToolHive RFC guidelines

Project-specific rules for RFCs in `toolhive/`. The shared rules in the root [AGENTS.md](../AGENTS.md) also apply.

- **Prefix**: `THV` (`toolhive/THV-NNNN-name.md`)
- **Template**: the shared [`template.md`](../template.md)

## Scope

RFCs here cover the ToolHive ecosystem: changes affecting one or more of the repositories below, cross-cutting concerns, public API or user-facing behavior, security-sensitive changes, and breaking changes or deprecations.

| Repository | Language | Description |
|------------|----------|-------------|
| [toolhive](https://github.com/stacklok/toolhive) | Go | Core platform: CLI (`thv`), operator (`thv-operator`), proxy runner (`thv-proxyrunner`), virtual MCP (`vmcp`) |
| [toolhive-studio](https://github.com/stacklok/toolhive-studio) | TypeScript | Desktop app (Electron) |
| [toolhive-registry](https://github.com/stacklok/toolhive-registry) | Go/JSON | Registry data, server definitions |
| [toolhive-registry-server](https://github.com/stacklok/toolhive-registry-server) | Go | Registry API (`thv-registry-api`), MCP Registry spec compliance |
| [toolhive-cloud-ui](https://github.com/stacklok/toolhive-cloud-ui) | TypeScript/Next.js | Cloud/Enterprise UI, OIDC integration |
| [dockyard](https://github.com/stacklok/dockyard) | Go | Container packaging, security scanning |

Set **Target Repository** in the metadata to one of these, or `multiple` for cross-cutting changes (then identify the impact on each repository).

## Research before writing or reviewing

Read the architecture docs in the `docs/arch/` directory of `stacklok/toolhive` (use `mcp__github__get_file_contents` or fetch from GitHub). Always read `00-overview.md`; read the others when relevant:

| Document | Read when the RFC touches |
|----------|---------------------------|
| `00-overview.md` | Always: platform concepts and key components |
| `01-deployment-modes.md` | Deployment, Kubernetes or local mode |
| `02-core-concepts.md` | New concepts or terminology (Workloads, Transports, Proxy, ...) |
| `03-transport-architecture.md` | MCP transports (stdio, SSE, streamable-http) or the proxy |
| `04-secrets-management.md` | Secrets or credentials |
| `05-runconfig-and-permissions.md` | Configuration format or permission profiles |
| `06-registry-system.md` | Registry architecture, `MCPRegistry` |
| `07-groups.md` | Server grouping |
| `08-workloads-lifecycle.md` | Workload lifecycle management |
| `09-operator-architecture.md` | Kubernetes operator or CRDs |
| `10-virtual-mcp-architecture.md` | Aggregation or virtual MCP |

Then search the target repository (`mcp__github__search_code`) to confirm the proposal fits existing code patterns, doesn't conflict with recent changes, and keeps API changes compatible.

## Architecture summary

ToolHive is a **platform** for MCP server management, not just a container runner:

- A proxy layer with middleware (auth, authz, audit, rate limiting)
- Security by default (network isolation, permission profiles)
- Aggregation via the Virtual MCP Server
- A registry of curated MCP servers
- Local (CLI/UI) and Kubernetes (operator) deployment

| Binary | Repository | Purpose |
|--------|------------|---------|
| `thv` | toolhive | Main CLI |
| `thv-operator` | toolhive | Kubernetes operator |
| `thv-proxyrunner` | toolhive | Kubernetes proxy container |
| `vmcp` | toolhive | Virtual MCP server (aggregation) |
| `thv-registry-api` | toolhive-registry-server | Registry API server |

Transport types: **stdio** (needs protocol translation), **SSE** and **streamable-http** (transparent proxy).

## Design principles to check

1. **Platform, not runner**: enhances the platform abstraction.
2. **Security by default**: maintains or improves the security posture.
3. **Middleware composability**: implemented as middleware where appropriate.
4. **RunConfig portability**: keeps configuration portable (RunConfig is the portable API contract).
5. **Cloud-native**: Kubernetes-friendly where applicable.

## Conventions

- Code examples: **Go** for toolhive and toolhive-registry-server, **TypeScript** for toolhive-studio and toolhive-cloud-ui, **YAML** for configuration.
- Kubernetes RFCs include CRD examples (`apiVersion: toolhive.stacklok.dev/v1alpha1`). CRD types: `MCPServer`, `MCPRegistry`, `MCPToolConfig`, `MCPExternalAuthConfig`, `MCPGroup`, `VirtualMCPServer`. Follow Kubernetes API conventions.
- Use ToolHive terminology correctly (Workloads, Transports, Middleware, RunConfig, ...).
- API and configuration designs stay consistent with existing APIs and RunConfig patterns in the target repository.
