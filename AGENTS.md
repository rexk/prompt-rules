# Agent Instructions

I am an AI agent working in this repository.
Before starting any task, I MUST:
1. Check `rules/general` for global engineering standards.
2. Check `rules/languages` for language-specific guidelines relevant to the current task.
3. Check `rules/frameworks` for framework-specific guidelines (if applicable).

## Rule Precedence
If rules conflict, I must follow this order of precedence (highest to lowest):
1. **Framework Rules** (e.g., `rules/frameworks/nextjs.mdc`)
2. **Language Rules** (e.g., `rules/languages/typescript.mdc`)
3. **General Rules** (e.g., `rules/general/no-utils.mdc`)
