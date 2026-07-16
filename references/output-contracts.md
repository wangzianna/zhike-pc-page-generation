# 输出契约

Choose one contract before implementation. Do not mix them.

## A. 可运行页面/组件

Use when the request is for source code or a page in an existing Vue project.

Deliver page and child component files, explicit props/emits, local mock data, scoped token-based styles, a local preview fixture or development-only preview route with mock-state switching, usage notes, and validation evidence. Reusable components must not contain real APIs, permission checks, Vuex/Router orchestration, or host aliases.

## B. Registry-driven page description

Use when a host renderer accepts a constrained page specification.

Deliver only JSON-compatible structured data: a compact module plan if the host compiles plans, or a pageSpec only when the host explicitly accepts pageSpec. Include a registry renderer preview that exposes the raw plan/spec, validator result, and mock data states. Validate every component id, required prop, and fallback. Never substitute HTML, Vue templates, pseudo-code, or unregistered component ids.

## Selection

- “Write/build/refactor a page” → Contract A.
- “Generate pageSpec/registry JSON/render through a playground” → Contract B.
- If ambiguous, inspect the project first; ask one focused question only when both contracts are viable and materially change the deliverable.
