---
name: prd-interactive-prototype
description: Create or update interactive HTML prototypes from PRDs, product requirements, feature flows, or user-requested prototype changes. Use when Codex should turn requirements into either a detailed review prototype with a left page tree, center app/desktop simulator, and right requirements annotation panel, or a cleaner demo prototype with only navigation and the simulated product experience. Also use when converting between demo and detailed review versions.
---

# PRD Interactive Prototype

Use this skill to turn a PRD or product idea into a single-file HTML prototype that can be opened in a browser and reviewed by product, design, engineering, stakeholders, or customers.

## Output Modes

Before building a new prototype, determine the requested mode:

- Detailed review mode: for product, design, development, and QA review. Use the full three-pane shell with left navigation, center simulator, and right requirements annotation panel.
- Demo mode: for lightweight presentation and walkthrough. Use a cleaner two-pane shell with left navigation and the simulated product experience only. Do not show the right requirements panel, priority badges, field rules, edge cases, or implementation notes in the visible UI.
- Both modes: produce two HTML files from the same source understanding, one detailed review version and one demo version. Keep page names, flows, states, and copy aligned across both files.

If the user asks for "原型" without specifying a mode, ask whether they want demo mode, detailed review mode, or both. If the user clearly describes the audience, infer the mode:

- "给开发 / 测试 / 评审 / 需求走查" means detailed review mode.
- "给老板 / 客户 / 演示 / demo / 展示" means demo mode.
- "两个版本都要" means both modes.

## Core Output

In detailed review mode, produce a standalone `.html` file with:

- Left page-tree navigation.
- Center simulator preview, usually App at `393 x 852`, optionally desktop at `1080 x 660`.
- Right requirements annotation panel that changes with the selected page.
- Clickable flows, realistic page states, Toasts, bottom sheets, confirmation dialogs, empty states, offline states, and error states when relevant.

In demo mode, produce a standalone `.html` file with:

- Left navigation or compact table of contents.
- Center simulator preview, usually App at `393 x 852`, optionally desktop at `1080 x 660`.
- Clickable flows, realistic page states, Toasts, bottom sheets, confirmation dialogs, empty states, offline states, and error states when they help the demo.
- No visible requirements annotation panel.
- No visible product-rule commentary, priority labels, test notes, field-spec lists, or edge-case explanations unless they are part of the user-facing product UI.

When generating demo mode from a PRD, preserve structured prototype metadata inside the HTML in a non-visible script block so a future detailed review version can be reconstructed more reliably. Include page tree, page purposes, entry paths, important fields, interactions, states, edge cases, data rules, and priority when known.

Use `assets/three-pane-prototype-template.html` as the style and structure reference when building from scratch or when matching the NAS prototype style.

Read `references/style-guide.md` when you need the exact layout, visual, annotation, and interaction conventions.

For UGREEN e-ink frame / 墨水屏相框 App work, read `references/eink-frame-app-baseline.md` and use `assets/eink-frame-app-prototype.html` as the baseline prototype before making changes. This applies to requests about 墨水屏、相框 App、送礼模式、照片墙、相册发送、照片编辑、设备配网、设备日志, or related e-ink frame flows.

## Workflow

1. Read the PRD and identify modules, pages, states, and critical paths.
2. Determine the output mode: detailed review, demo, or both.
3. Build a page tree before building screens.
4. Decide which states deserve separate nav items:
   - Default state.
   - Empty state.
   - Error / offline state.
   - Permission or conflict state.
   - Confirmation / result states.
5. Implement each HTML output as a single file unless the user asks otherwise.
6. Keep the prototype practical and reviewable:
   - Use gray wireframe styling unless the PRD or user asks for visual polish.
   - Show real product copy, not placeholder lorem ipsum.
   - In detailed review mode, put annotations in the right panel, not inside the app screen.
   - In detailed review mode, include P0 / P1 / P2 priority tags in annotations when available.
   - In demo mode, optimize for a clean walkthrough and keep requirements details out of the visible UI.
7. Validate before final response:
   - Run a syntax check for embedded JavaScript.
   - Open through a local static server when feasible.
   - Verify the target page, interaction, and annotation changed as requested.

## Mode Conversion

When converting detailed review mode to demo mode:

- Keep the page tree, simulator screens, interactions, and realistic product copy.
- Remove or hide the right requirements annotation panel from the visible layout.
- Remove visible priority tags, field rules, test notes, and edge-case explanations unless they are part of user-facing product UI.
- Preserve structured requirements metadata in a non-visible script block for future conversion back to detailed review mode.

When converting demo mode to detailed review mode:

- Restore the three-pane shell.
- Reuse the existing navigation, simulator screens, interactions, and states.
- Reconstruct the right requirements annotation panel from preserved metadata when available.
- If no preserved metadata or original PRD is available, infer annotations from the demo and clearly mark uncertain rules as inferred.
- Prefer asking for the original PRD when accuracy matters, especially for permissions, data rules, validation rules, and edge cases.

## Modification Rules

When updating an existing prototype:

- Locate the relevant nav item, annotation key, state object, and render function before editing.
- Preserve the current mode unless the user asks to convert modes.
- For detailed review mode, preserve the three-pane shell.
- For demo mode, preserve the clean navigation plus simulator shell and keep requirements details out of the visible UI.
- Avoid duplicating labels in both metadata and badges unless the UI intentionally needs both.
- Do not nest `<button>` inside `<button>`; use a `<div role="button">` card when the card contains another button.
- In detailed review mode, update both the visible screen and the right-side annotation when behavior changes.
- In demo mode, update the visible flow and the hidden structured metadata when behavior changes.
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
