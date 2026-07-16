---
name: zhike-pc-page-generation
description: Generate or refactor Zhike-style desktop B-end pages from natural-language requirements in Vue 2.7. Use when an agent needs a Zhike PC list page, dashboard, enterprise profile, management master-detail page, or reusable visual component that must follow the Zhike Figma design system and run without original-project API, store, router, permission, map, upload, or graph dependencies.
---

# 智客 PC 页面生成

Turn a business requirement into a runnable, props-driven Zhike-style PC page or component package. This skill is tool-neutral: any agent capable of reading Markdown and editing the target workspace can follow it.

## Required reading

- Page layout: [page-patterns.md](references/page-patterns.md)
- Component selection: [component-rules.md](references/component-rules.md)
- Tokens and visual rules: [visual-rules.md](references/visual-rules.md)
- Vue/code constraints: [code-rules.md](references/code-rules.md)
- Prompt/output examples: [examples.md](references/examples.md)
- Prohibitions: [anti-patterns.md](references/anti-patterns.md)
- Delivery check: [final-skill-check.md](references/final-skill-check.md)
- Agent execution protocol: [agent-protocol.md](references/agent-protocol.md)
- Output contracts: [output-contracts.md](references/output-contracts.md)
- Preview rules: [preview-rules.md](references/preview-rules.md)

## Workflow

1. Read `agent-protocol.md`, then inspect the target workspace, package manifest, existing conventions, and uncommitted changes before editing.
2. Read `visual-rules.md`, `page-patterns.md`, and references relevant to the requested page.
3. Identify `list`, `dashboard`, `enterprise-detail`, or `master-detail`; build a compact module plan with task, title, filters, metrics, primary content, secondary content, and states.
4. Select only existing or explicitly created props-driven components. Choose the applicable output contract before producing code or JSON.
5. Implement with Vue 2.7 Options API and Element UI. Keep mock data at the page boundary and pass data through props.
6. Apply Figma tokens before local adjustments. Use `#0080FF`, not legacy `#409EFF`.
7. Build or update the applicable preview described in `preview-rules.md`; include normal, loading, and empty states for every data region.
8. Run the workspace’s smallest relevant safe validation and verify the preview path.
9. Report edited files, preview command/URL, validation evidence, assumptions, and unresolved gaps.

## Non-negotiable rules

- Use one UI library per page: Element UI.
- Do not include real APIs, permissions, Vuex, router orchestration, upload/download flows, maps, relationship graphs, or approval workflows in reusable output.
- Do not make cards, gradients, pills, shadows, or color decoration compete with information hierarchy.
- Preserve business modules stated by the user. If no dedicated component exists, use a simple compatible fallback rather than silently omitting the module.
