# Tooling Architecture Proposal (Phase 2)

## Overview
To provide a `cheat.sh`-style experience for both Humans (CLI) and Agents (MCP), we propose building a tooling layer in this repository.

## Recommended Stack
- **Language**: **TypeScript**
- **Runtime**: **Node.js** (LTS)
- **Package Manager**: **npm** (for simplicity and ubiquity)
- **Execution**: **tsx** (for instant "save-and-run" iteration without compilation)
- **Why**:
    - Native language of MCP (Model Context Protocol).
    - Native language of VS Code / Cursor extensions.
    - Easy to share logic between the CLI and the MCP server.
    - Zero-install distribution via `npx`.

## Directory Structure
We will adopt a "Monorepo" structure where Content and Code live together:
```
.
├── rules/              # [CONTENT] The Markdown/MDC files
│   ├── general/
│   └── ...
├── src/                # [CODE] The Tooling
│   ├── cli.ts          # Entry point for CLI (e.g., `npx prompt-rules install`)
│   ├── server.ts       # Entry point for MCP (e.g., `npx prompt-rules serve`)
│   └── resolver.ts     # Shared logic (finding files, resolving conflicts)
├── package.json
└── README.md
```

## Capabilities

### 1. CLI (`npx prompt-rules`)
- **Install**: `npx prompt-rules install --tags nextjs,typescript`
    - **Filtering**: Selects rules based on frontmatter tags (e.g., `tags: ["frontend", "react"]`).
    - **Conflict Resolution**: If multiple files match (e.g., `typescript-strict.mdc` vs `typescript-loose.mdc`), the CLI prompts the user or uses a priority weight.

- **List**: `npx prompt-rules list`
    - Shows available rule sets and their tags.

### 2. MCP Server (`npx prompt-rules serve`)
- **Resources**: Exposes rules as read-only resources (`rules://languages/typescript`).
- **Prompts**: Exposes "System Prompts" for bootstrapping.
- **Tools**:
    - `recommend_rules(context: string, files: string[])`: Analyzes a project description or file list and returns a list of recommended rules to install.
    - `scan_project(path: string)`: Scans a local project to auto-detect frameworks and suggest the matching stack.

## Future Considerations
- **Rust/Go**: If performance or binary size becomes an issue, the `src/` folder can be rewritten in Rust or Go using their respective official MCP SDKs. For now, TypeScript offers the fastest iteration speed.
