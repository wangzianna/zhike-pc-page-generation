# Preview Rules

Every generated page must have a low-friction local preview. Reuse the project’s existing preview, Storybook, playground, or development server before creating a new mechanism. Do not add a dependency solely for previewing.

## Contract A: Vue page/component preview

1. Build a preview wrapper that imports the generated page/components and supplies local mock data.
2. Expose `normal`, `loading`, and `empty` states through a small local switcher or fixture controls. Keep these controls in the preview wrapper, not the reusable component.
3. Prefer the existing application routing/preview convention. If none exists, add a development-only route or isolated preview entry using the project’s established bootstrapping pattern.
4. Make the preview self-contained: no API, Store, permission, or route-query data may be required for it to render.
5. Report the command and route/URL. Verify the default state loads and the state switcher does not white-screen.

Suggested shape:

```text
src/previews/<feature>/PreviewPage.vue     # mock data + state switcher
src/previews/<feature>/index.vue           # imports the generated page
```

Adapt the location to the repository rather than forcing this structure.

## Contract B: Registry/pageSpec preview

1. Use the host registry renderer/playground; do not make a separate Vue page that bypasses the registry.
2. Render the generated ModulePlan/pageSpec with mock props.
3. Show the raw plan/spec and validator result next to or below the preview.
4. Provide normal, loading, and empty mock scenarios where the renderer supports them.
5. Block and report unknown component ids or invalid props before visual rendering.

## Preview acceptance

- The user can reach the preview with one documented command and route/URL.
- The first visible frame follows the Figma visual rules.
- Normal, loading, and empty states are inspectable without a backend.
- Console/runtime errors and invalid registry references are resolved or explicitly reported.
