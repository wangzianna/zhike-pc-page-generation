---
name: zhike-pc-page-generation
description: Generate or refactor Zhike-style desktop B-end pages from natural-language requirements or reference screenshots in Vue 2.7. Use when an agent needs a Zhike PC list page, dashboard, enterprise profile, management master-detail page, or reusable visual component that must follow the Zhike Figma design system and run without original-project API, store, router, permission, map, upload, or graph dependencies.
---

# Zhike PC Page Generation

Turn a business requirement into a runnable, props-driven Zhike-style PC page or component package. This skill is tool-neutral: any agent capable of reading Markdown and editing the target workspace can follow it.

## Required reading

- Page layout: [page-patterns.md](references/page-patterns.md)
- Component selection: [component-rules.md](references/component-rules.md)
- Region and industry filter defaults: [filter-rules.md](references/filter-rules.md)
- Reference-image workflow: [image-reference-rules.md](references/image-reference-rules.md)
- High-frequency enterprise search and result-list patterns: [high-frequency-patterns.md](references/high-frequency-patterns.md)
- Tokens and visual rules: [visual-rules.md](references/visual-rules.md)
- Icon selection and IconPark usage: [icon-rules.md](references/icon-rules.md)
- Vue/code constraints: [code-rules.md](references/code-rules.md)
- Prompt/output examples: [examples.md](references/examples.md)
- Test prompt suite: [test-cases.md](examples/test-cases.md)
- Prohibitions: [anti-patterns.md](references/anti-patterns.md)
- Delivery check: [final-skill-check.md](references/final-skill-check.md)
- Agent execution protocol: [agent-protocol.md](references/agent-protocol.md)
- Output contracts: [output-contracts.md](references/output-contracts.md)
- Preview rules: [preview-rules.md](references/preview-rules.md)

## Default interaction

Treat the user’s next natural-language message and any attached reference image as the page requirement; users do not need to paste a prefix or select a contract.

If the skill is invoked without a concrete page requirement, send this concise onboarding message and wait:

```text
我会按智客 Figma 规范，把你的需求生成成可预览的 PC 页面：先识别页面类型和输出方式，再生成可复用组件、mock 数据与正常/加载/空状态预览，最后做校验。

请直接描述你想要的页面，例如“生成科技金融潜客筛选页，支持行业和地区筛选，展示企业卡和分页”。
```

If the user already supplies a concrete requirement or a usable reference image, do not repeat the onboarding or ask them to choose a contract. Briefly state the selected page mode and output contract, then begin the workflow. Ask one focused question only when a missing choice materially changes the deliverable; otherwise make a documented, conservative assumption.

## Workflow

1. Read `agent-protocol.md`, then inspect the target workspace, package manifest, existing conventions, and uncommitted changes before editing.
2. Read `visual-rules.md`, `icon-rules.md`, `page-patterns.md`, and references relevant to the requested page. Requirements containing region or industry filters must also read `filter-rules.md`; attached reference images must also read `image-reference-rules.md`; enterprise candidate search or enterprise result lists must also read `high-frequency-patterns.md`.
3. For an attached image, extract a compact reference map before planning. Identify `list`, `dashboard`, `enterprise-detail`, or `master-detail`; build a compact module plan with task, title, filters, metrics, primary content, secondary content, and states.
4. Select only existing or explicitly created props-driven components. Choose the applicable output contract before producing code or JSON.
5. Implement with Vue 2.7 Options API and Element UI. Keep mock data at the page boundary and pass data through props.
6. Apply Figma tokens before local adjustments. Use `#0080FF`, not legacy `#409EFF`.
7. Build or update the applicable preview described in `preview-rules.md`; include normal, loading, and empty states for every data region.
8. Run the workspace’s smallest relevant safe validation and verify the preview path.
9. Report edited files, preview command/URL, validation evidence, assumptions, and unresolved gaps.

## Non-negotiable rules

- Use one UI library per page: Element UI.
- Use existing Element UI icons first and IconPark as the supplemental icon library; follow `icon-rules.md`. Never draw substitute business icons with CSS, Unicode/emoji, or handcrafted SVG.
- Do not include real APIs, permissions, Vuex, router orchestration, upload/download flows, maps, relationship graphs, or approval workflows in reusable output.
- Do not make cards, gradients, pills, shadows, or color decoration compete with information hierarchy.
- Preserve business modules stated by the user. If no dedicated component exists, use a simple compatible fallback rather than silently omitting the module.
