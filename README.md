# 智客 PC 页面生成 / Zhike PC Page Generation

根据自然语言需求或参考截图，生成可运行的智客风格 PC 端 B 端页面。本 Skill 面向 Vue 2.7 与 Element UI，生成的组件不依赖原智客项目的 API、Store、Router、权限、地图、上传或图谱能力。

Generate runnable Zhike-style desktop B-end pages from natural-language requirements or reference screenshots. This skill targets Vue 2.7 and Element UI; generated components are independent of the original Zhike project's API, Store, Router, permission, map, upload, and graph dependencies.

业务规则与页面文案保留中文；通用技术流程和契约使用英文，以便 Codex、Claude Code 等 Agent 稳定共用。

Business rules and UI copy remain Chinese; shared technical workflow and contracts are written in English for consistent use across Codex, Claude Code, and other agents.

## 能生成什么 / What it produces

- 企业列表与筛选页、驾驶舱、企业画像页、管理主从页。<br>
  Enterprise list/search pages, dashboards, enterprise profiles, and master-detail management pages.
- 基于 props 的 Vue 2.7 组件，以及页面边界的本地 mock 数据。<br>
  Props-driven Vue 2.7 components with page-level local mock data.
- 含正常、加载、空状态的本地预览。<br>
  A local preview with normal, loading, and empty states.
- 当宿主支持时，生成仅包含 Registry/pageSpec 的结果及其校验和预览。<br>
  When supported by the host, a registry/pageSpec-only result with validation and a registry preview.

默认内置以下筛选行为：

- 地区：省 → 市 → 区/县三级联动。
- 行业：国标门类 → 大类 → 中类 → 小类四级联动。
- 企业筛选：高密度条件区与可复用企业结果行，支持产业匹配度、迁移/投资可能性等招商线索。

The following defaults are built in:

- Region: province → city → district/county cascade.
- Industry: national-standard category → division → group → class cascade.
- Enterprise screening: dense facets and reusable result rows, including industry fit and investment/migration signals.

## 安装 / Installation

保留一份 Skill 源目录，再通过符号链接同时暴露给 Codex 和 Claude Code：

Keep one canonical skill directory, then expose it to both Codex and Claude Code through symbolic links:

```sh
ln -sfn /absolute/path/zhike-pc-page-generation ~/.agents/skills/zhike-pc-page-generation
ln -sfn /absolute/path/zhike-pc-page-generation ~/.claude/skills/zhike-pc-page-generation
```

Codex 从第一处发现 Skill，Claude Code 从第二处发现。若当前会话已经加载过 Skill，修改后请新开一个 Agent 会话。

Codex discovers the first location and Claude Code discovers the second. Start a new agent session after changing a skill if the current session has already loaded its instructions.

## 使用方式 / Usage

调用 Skill 后，直接用中文或英文描述页面即可。需求已具体时，不需要再添加前缀或手动选择输出契约。

Invoke the skill, then describe the page in Chinese or English. A concrete request does not need a prefix or manual output-contract selection.

```text
做一个园区招商用的企业筛选页面。
招商人员按照产业、地区、企业规模、融资、知识产权、资质筛选企业；
突出产业匹配度、迁移或投资可能，以及“招商意向：规则待配置”。
```

若需求还不具体，Skill 会要求输入一条自然语言页面需求。除非未决问题会改变页面模式、输出契约或技术栈，否则会采用保守且明确记录的假设继续执行。

If the request is not yet concrete, the skill asks for one natural-language page requirement. It makes documented conservative assumptions unless an unresolved choice changes the page mode, output contract, or technology stack.

## 输出契约 / Output contracts

| 契约 / Contract | 适用场景 / Use when | 交付内容 / Delivers |
| --- | --- | --- |
| A — 可运行页面/组件 / Runnable page/component | 编写或重构 Vue 页面 / Building or refactoring a Vue page | Vue 文件、props/emits、本地 mock、预览 fixture/路由、校验证据 / Vue files, explicit props/emits, local mock data, preview fixture/route, validation evidence |
| B — Registry/pageSpec | 宿主只接受受约束的页面描述 / A host renderer accepts a constrained specification | JSON 兼容的模块计划/pageSpec、Registry 校验和渲染预览 / JSON-compatible module plan/pageSpec, registry validation, and renderer preview |

两种契约不可混用；契约 B 不会以原始 HTML 或未注册组件 ID 代替合法结果。

The contracts are mutually exclusive. Contract B never substitutes raw HTML or unregistered component ids for a valid result.

## 设计与图标规则 / Design and icon policy

- 遵循智客 Figma Token；主色为 `#0080FF`，不是 `#409EFF`。<br>
  Follow Zhike Figma tokens; the primary colour is `#0080FF`, not `#409EFF`.
- 页面 UI 库统一使用 Element UI。<br>
  Use Element UI as the sole page UI library.
- 优先使用 Element UI 现有图标；领域补充图标使用 `@icon-park/vue`（IconPark）。<br>
  Use existing Element UI icons first; use `@icon-park/vue` (IconPark) for supplemental domain icons.
- 不得用 CSS、emoji/Unicode 字符或手写 SVG path 伪造图标；IconPark 不可用时，暂用带文字的控件并报告依赖缺口。<br>
  Never draw substitute icons with CSS, emoji/Unicode characters, or handcrafted SVG paths. If IconPark is unavailable, use a text-labelled control and report the dependency gap.

## 预览与校验 / Preview and validation

每个生成页面都需要低摩擦的本地预览。优先复用目标项目已有的预览机制，不为预览单独增加依赖；预览必须能在无后端情况下检查正常、加载和空状态。

Every generated page needs a low-friction local preview. Prefer the target project's existing preview convention; do not add a preview-only dependency. The preview must show normal, loading, and empty states without a backend.

校验 Skill 本身：

Validate the skill itself:

```sh
python3 /path/to/skill-creator/scripts/quick_validate.py /absolute/path/zhike-pc-page-generation
```

详细实现规则请阅读 [SKILL.md](SKILL.md)。`references/` 包含视觉、筛选、图标、契约和预览规则；`examples/` 包含用于前向测试的需求案例。

For implementation details, read [SKILL.md](SKILL.md). The `references/` directory contains design, filter, icon, contract, and preview rules; `examples/` contains prompts for forward testing.
