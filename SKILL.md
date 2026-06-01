---
name: prd-interactive-prototype
description: Create or update three-pane interactive HTML prototypes from PRDs, product requirements, feature flows, or user-requested prototype changes. Use when Codex should turn requirements into an annotated clickable wireframe with a left page tree, center app/desktop simulator, and right requirements annotation panel, or when modifying an existing prototype in that style.
---

# PRD Interactive Prototype

Use this skill to turn a PRD or product idea into a single-file HTML prototype that can be opened in a browser and reviewed by product, design, and engineering.

## Core Output

Produce a standalone `.html` file with:

- Left page-tree navigation.
- Center simulator preview, usually App at `393 x 852`, optionally desktop at `1080 x 660`.
- Right requirements annotation panel that changes with the selected page.
- Clickable flows, realistic page states, Toasts, bottom sheets, confirmation dialogs, empty states, offline states, and error states when relevant.

Use `assets/three-pane-prototype-template.html` as the style and structure reference when building from scratch or when matching the NAS prototype style.

Read `references/style-guide.md` when you need the exact layout, visual, annotation, and interaction conventions.

## Workflow

1. Read the PRD and identify modules, pages, states, and critical paths.
2. Build a page tree before building screens.
3. Decide which states deserve separate nav items:
   - Default state.
   - Empty state.
   - Error / offline state.
   - Permission or conflict state.
   - Confirmation / result states.
4. Implement the HTML as a single file unless the user asks otherwise.
5. Keep the prototype practical and reviewable:
   - Use gray wireframe styling unless the PRD or user asks for visual polish.
   - Show real product copy, not placeholder lorem ipsum.
   - Put annotations in the right panel, not inside the app screen.
   - Include P0 / P1 / P2 priority tags in annotations when available.
6. Validate before final response:
   - Run a syntax check for embedded JavaScript.
   - Open through a local static server when feasible.
   - Verify the target page, interaction, and annotation changed as requested.

## Modification Rules

When updating an existing prototype:

- Locate the relevant nav item, annotation key, state object, and render function before editing.
- Preserve the three-pane shell.
- Avoid duplicating labels in both metadata and badges unless the UI intentionally needs both.
- Do not nest `<button>` inside `<button>`; use a `<div role="button">` card when the card contains another button.
- Update both the visible screen and the right-side annotation when behavior changes.
- Keep backups before overwriting user-owned desktop files when practical.

## Annotation Rules

Right-panel annotations should answer:

- What page or state is this?
- Entry path.
- Display fields.
- Interaction rules.
- Edge cases.
- Data or permission rules.
- Priority.

Prefer compact annotation cards:

```html
<ul class="space-y-3 text-xs">
  <li class="p-3 bg-gray-50 rounded-lg border">
    <strong>页面名称【P0】</strong><br>
    页面用途、入口、默认状态。
  </li>
  <li class="p-3 bg-gray-50 rounded-lg border">
    <strong>模块 / 规则</strong><br>
    字段、点击行为、异常状态、边界条件。
  </li>
</ul>
```

## File Placement

Default output location:

`/Users/ugreen/Documents/New project/`

If the user is working on a project folder, place output under that project, preferably:

`项目名/原型/`

If the source HTML is outside the writable workspace, create or update a working copy in the workspace first. Only write back to the original path after approval, and keep a backup for substantial changes.
