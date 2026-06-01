# Three-Pane Prototype Style Guide

## Layout

Use a full-window three-pane layout:

- Left navigation: about `232px`, white background, page tree.
- Center preview shell: gray background, toolbar, simulator centered and scaled to fit.
- Right annotation panel: about `450px`, white background, scrollable annotation content.

The simulator should support:

- App mode: `393 x 852`, rounded phone shell.
- Desktop mode when useful: `1080 x 660`, browser-like chrome.

## Visual Style

- Wireframe-first, grayscale-friendly.
- Body background: light gray.
- App screen background: white or `#f9fafb`.
- Cards: white, subtle border, 8-16px radius.
- Primary action: `#111827`.
- Secondary text: gray.
- Status color use:
  - Green for online / active / success.
  - Amber for waiting / controlled elsewhere / pending.
  - Red for destructive actions.
  - Blue for selection.

Use Font Awesome icons when the template already uses them.

## Shell Structure

Keep these conceptual areas:

```html
<div class="ltt-layout">
  <aside class="page-tree-nav">...</aside>
  <div class="preview-shell">
    <div class="preview-toolbar">...</div>
    <div class="preview-stage">
      <div class="preview-monitor">
        <div class="preview-screen">...</div>
      </div>
    </div>
  </div>
  <aside class="annotation-panel">...</aside>
</div>
```

## State Model

Use a single JS `state` object for current page and interactive state:

- `currentPage`
- `currentNavId`
- module tabs
- selected items
- modal / sheet state
- current device / active object id
- offline / empty / conflict flags

Use data arrays for devices, albums, photos, plans, records, or other product objects.

## Page Tree

Represent the left nav as `menuTree`.

Each leaf should include:

- `id`
- `name`
- `page`
- optional `stateOverride`

Use `stateOverride` to show important variants without hard-coding separate pages.

## Annotation Mapping

Use an `annotations` object keyed by nav id.

Update annotation whenever:

- A new page is added.
- A state branch is added.
- A behavior or edge case changes.
- A UI label changes in a way that affects requirements.

## Interaction Patterns

Common interactions to implement:

- Tap card to open detail.
- Back navigation.
- Bottom sheet for secondary choices and confirmations.
- Toast for lightweight results.
- Long press / right click menu when relevant.
- Multi-select with bottom action bar.
- Empty state with primary action.
- Conflict state with clear label and recovery action.
- Destructive action with second confirmation.

Important HTML rule:

Do not nest `<button>` inside another `<button>`. If a clickable card needs a button inside it, use:

```html
<div role="button" tabindex="0" onclick="...">
  ...
  <button type="button" onclick="event.stopPropagation();...">Action</button>
</div>
```

## Review Checklist

Before finishing:

- The requested page is reachable from the left nav.
- The center simulator shows the requested state.
- The right annotation documents the behavior.
- Buttons and nested click targets are valid HTML.
- JS syntax check passes.
- No obvious text overflow or duplicate status labels.
