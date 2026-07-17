# Zhike PC Page Generation

Generate runnable Zhike-style desktop B-end pages from natural-language requirements or reference screenshots. The skill targets Vue 2.7 and Element UI, while keeping generated components independent of the original Zhike project's API, Store, Router, permission, map, upload, and graph dependencies.

Business rules and UI copy remain Chinese; shared technical workflow and contracts are written in English for consistent use across agents.

## What it produces

- Enterprise list/search pages, dashboards, enterprise profiles, and master-detail management pages.
- Props-driven Vue 2.7 components with page-level mock data.
- A local preview with normal, loading, and empty states.
- Or, when requested, a registry/pageSpec-only result with validation and a registry preview.

The default filter behaviour is built in:

- Region: province → city → district/county cascade.
- Industry: national-standard category → division → group → class cascade.
- Enterprise screening: dense facets and reusable result rows, including industry fit and investment/migration signals.

## Installation

Keep one canonical copy and expose it to both agents with symbolic links:

```sh
ln -sfn /absolute/path/zhike-pc-page-generation ~/.agents/skills/zhike-pc-page-generation
ln -sfn /absolute/path/zhike-pc-page-generation ~/.claude/skills/zhike-pc-page-generation
```

Codex discovers the first location; Claude Code discovers the second. Start a new agent session after changing a skill if the current session has already loaded its instructions.

## Usage

Invoke the skill, then describe the page in Chinese or English. A prefix or output-contract selection is unnecessary for a concrete request.

```text
做一个园区招商用的企业筛选页面。
招商人员按照产业、地区、企业规模、融资、知识产权、资质筛选企业；
突出产业匹配度、迁移或投资可能，以及“招商意向：规则待配置”。
```

If the request is not yet concrete, the skill asks for a single natural-language page requirement. It makes conservative assumptions unless an unresolved choice changes the page mode, output contract, or technology stack.

## Output contracts

| Contract | Use when | Delivers |
| --- | --- | --- |
| A — Runnable page/component | Building or refactoring a Vue page | Vue files, explicit props/emits, local mock data, preview fixture/route, validation evidence |
| B — Registry/pageSpec | A host renderer accepts a constrained specification | JSON-compatible module plan/pageSpec, registry validation, and renderer preview |

Contracts are mutually exclusive. Contract B never substitutes raw HTML or unregistered component ids.

## Design and icon policy

- Follow Zhike Figma tokens; primary colour is `#0080FF`, not `#409EFF`.
- Use Element UI as the sole page UI library.
- Use existing Element UI icons first; use `@icon-park/vue` (IconPark) for supplemental domain icons.
- Never draw substitute icons with CSS, emoji/Unicode characters, or handcrafted SVG paths. If IconPark is unavailable, use a text-labelled control and report the dependency gap.

## Preview and validation

Every generated page needs a low-friction local preview. Prefer the target project's existing preview convention; do not add a preview-only dependency. The preview must show normal, loading, and empty data states without a backend.

Validate the skill itself with:

```sh
python3 /path/to/skill-creator/scripts/quick_validate.py /absolute/path/zhike-pc-page-generation
```

For implementation details, read [SKILL.md](SKILL.md). The `references/` directory contains the design, filter, icon, contract, and preview rules; `examples/` contains prompts for forward testing.
