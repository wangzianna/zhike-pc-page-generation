# Agent Execution Protocol

Apply this protocol regardless of the host agent, IDE, or tool provider.

## Before changes

1. Read `SKILL.md` and the references required by the request.
2. Inspect the target project’s manifest, source structure, existing UI conventions, and repository instructions before choosing implementation details.
3. Check for uncommitted or user-authored changes. Preserve unrelated work; do not overwrite, reset, reformat globally, or delete files to simplify the task.
4. Treat user-provided Figma/design documents as the visual authority. If inaccessible, ask for a screenshot, export, or token list; do not invent missing design rules.
5. State material assumptions before acting only when they change the page pattern, output contract, or technology stack.

## During implementation

- Stay inside the requested scope and workspace. Do not publish packages, send network requests, alter remote services, or make unrelated dependency upgrades without authorization.
- Prefer existing project components and utilities when they satisfy the visual and props contract. Create new components only when existing implementations are host-coupled or unsafe to reuse.
- Keep business data, host services, and view rendering separate. Components must render with explicit props and supplied mock data.
- Document gaps and use a compatible simple fallback; never silently remove a requested module.

## Validation and handoff

1. Run the smallest relevant existing validation command. Do not invent a build system or install dependencies without approval.
2. If validation cannot run, explain why and perform appropriate static checks.
3. Summarize files changed, validation evidence, assumptions, and known gaps.
4. Do not claim rendering, integration, or production readiness without evidence.
