# Delivery Acceptance Checklist

- [ ] The selected page mode matches the task and uses Figma tokens (`#0080FF`, type scale, 4px radius, correct borders/background).
- [ ] Element UI is the only page UI library; hierarchy and long-text behaviour are clear.
- [ ] Every data region has normal, loading, and empty states.
- [ ] A local preview shows normal, loading, and empty states without host APIs.
- [ ] The preview command, route/URL, and manual verification steps are reported.
- [ ] Components render from explicit props and mock data; reusable code contains no API, Store, Router, permission, map/graph, upload/download, or host alias.
- [ ] If used, region filters cascade province/city/district and industry filters cascade through the four national-standard levels; verify parent resets, clear actions, and full-path display.
- [ ] When a reference image is supplied, map its layout and component intent; report conflicts with Zhike rules, unsupported details, and conservative assumptions.
- [ ] Enterprise screening/list pages use the shared dense-filter and result-row pattern; filters, selected chips, sorting, pagination, follow/selection, loading, and empty states remain synchronized.
- [ ] Registry/pageSpec includes only known ids and valid props.
- [ ] No legacy primary color, mixed libraries, excessive inline styles, or decorative noise remains.
