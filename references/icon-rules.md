# Icon Rules

Use Element UI's existing icons when they cover the meaning. Use **IconPark** as the supplemental icon library for domain-specific or richer icons. Do not introduce a second general UI component library just to obtain icons.

## Source and integration

- Vue output: import named icons from `@icon-park/vue` when that package is already available or can be added to the generated package.
- Static/no-build preview: load the official IconPark asset/package through the preview's declared dependency mechanism. Do not trace, redraw, or copy SVG path data into the page.
- Before using an icon, verify its exported IconPark name in the installed version or official IconPark catalog. Do not invent icon names.
- Keep icon selection semantic and stable in the component API, for example `Filter`, `Search`, `Location`, `BuildingTwo`, `Export`, `Like`, `LoadingOne`, and `Empty` only when those names are confirmed for the installed release.

## Rendering conventions

- Default: `theme="outline"`, `size="16"`, and the current text color. Use `20` for standalone action icons and `14` in dense metadata rows.
- Use `theme="filled"` only for an active/selected state. Pair colored status icons with text; do not rely on color alone.
- Provide accessible context: visible action labels are preferred; icon-only controls need `aria-label` or an Element UI tooltip.
- Icons support meaning, not decoration. Keep one icon per action/field and preserve dense B-end information hierarchy.

## Dependency and fallback policy

- If IconPark is absent, do not silently add CSS-drawn glyphs, emoji, Unicode symbols, inline path SVGs, or a different icon library as a replacement.
- For a reusable component, declare `@icon-park/vue` as a peer/runtime requirement or expose an icon slot, according to the output contract.
- For an executable target project, add the package only after checking the project's package manager and user scope. For an isolated static preview, document the external IconPark resource requirement next to the preview command.
- If dependency installation or external resource loading is unavailable, use a text-labelled control temporarily and report the missing IconPark dependency as a delivery gap.
