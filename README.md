# Prompt Rules

**Centralized Engineering Standards for AI Agents.**

## Motivation
We built this repository to solve three core problems in AI-assisted development:

1.  **Eliminate Repetition**: We were spending 10-20 minutes per task just typing out "boilerplate" requirements (e.g., "don't use utils folders"). This repo automates that context.
2.  **Enforce Consistency**: Whether using Cursor, Antigravity, or Windsurf, we want a single source of truth for our engineering standards.
3.  **Prevent "Context Contamination"**: Agents often confuse languages in multi-language frameworks (like Godot). By strictly scoping rules, we ensure C# patterns don't bleed into GDScript, and vice versa.

## The Philosophy: "The Matrix Approach"
We organize rules not just by topic, but by **Scope**. Every rule file defines exactly *when* it applies using file globs.

*   **Specificity Trumps Generality**:
    *   **Framework Rules** (e.g., `godot.mdc`) override...
    *   **Language Rules** (e.g., `typescript.mdc`), which override...
    *   **General Rules** (e.g., `no-utils.mdc`).

## Repository Structure

The `rules/` directory is the heart of this project.

```
rules/
├── general/       # Global standards (e.g., Naming, Folder Structure)
│                  # Applies to: Everyone (Globs: *)
│
├── languages/     # Language-specific best practices
│   ├── typescript.mdc  # (Globs: *.ts, *.tsx)
│   ├── gdscript.mdc    # (Globs: *.gd)
│   └── csharp.mdc      # (Globs: *.cs)
│
└── frameworks/    # Engine/Framework specifics
    └── godot.mdc       # (Globs: project.godot, *.tscn)

templates/         # Copy-paste templates for other projects
└── AGENTS.md      # The "System Instructions" template
```

## Usage

### 1. For Your Projects (The "Target")
To use these rules in another project (e.g., your Game or Web App):
1.  **Copy the Template**: Copy `templates/AGENTS.md` to your project's root.
2.  **Install Rules**: Copy the relevant `.mdc` files from `rules/` to your project's `.cursor/rules/` (or `prompts/`) directory.

### 2. For This Repository (The "Source")
This repository *itself* uses the rules!
- **`AGENTS.md`** (at root): Tells agents how to contribute to *this* repo (e.g., "Check `no-utils` before creating new folders").
