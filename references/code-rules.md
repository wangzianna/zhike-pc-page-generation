# Code Rules

- Use Vue 2.7 Options API and JavaScript.
- Use Element UI; never mix Ant Design Vue on one page.
- Use scoped SCSS/Less classes and token-like variables; avoid inline visual styles.
- Separate page orchestration from display components. Components receive explicit props and emit simple events.
- Keep mock data at the page boundary. Do not put APIs, Store, Router, permissions, or host aliases in reusable components.
- Split an independent card/panel/detail section into a component with its own props schema.
- Define stable component ids and prop schemas before exposing registry/pageSpec components. Validate ids and required props before rendering.
