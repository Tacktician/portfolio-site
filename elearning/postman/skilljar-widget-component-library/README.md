# Skilljar Widget Component Library

A collection of interactive and static HTML widgets for use in courses and lessons on [academy.postman.com](https://academy.postman.com). Each component is a self-contained `.html` file that can be copied into a Skilljar lesson's rich-text/HTML editor.

---

## Browsing the Library

Open `index.html` in a browser (or serve it with any local HTTP server) to access the full component browser. It provides:

- A searchable sidebar listing all 22 components
- A live **Preview** tab to see each widget rendered
- A **Source** tab to view and copy the raw HTML

> **Tip:** Press `/` anywhere in the browser to jump focus to the search bar.

---

## How to Use a Snippet in Skilljar

1. Open the component file you want (e.g. `components/07-accordion.html`) in the component browser or your text editor.
2. Click **Source** → **⎘ Copy** (or copy the file contents directly).
3. In the Skilljar lesson editor, switch to **HTML / Source** mode.
4. Paste the snippet.

### What to keep vs. what to strip

Skilljar strips the outer document shell when it processes pasted HTML. **You do not need to include**, and Skilljar will ignore, any of the following:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" ...>
  <title>...</title>
  ...
</head>
<body>
  ...
</body>
</html>
```

You only need the content that lives **inside `<body>`**, along with the `<style>` block and `<script>` block that accompany it. A minimal paste looks like this:

```html
<style>
  /* component styles */
</style>

<!-- component markup -->
<div class="my-widget">...</div>

<script>
  // component JavaScript
</script>
```

Skilljar will render the `<style>` and `<script>` tags inline alongside the lesson content.

---

## Combining Multiple Widgets in One Lesson

Each snippet is **standalone by design** — it ships with its own `<style>` block containing a full `:root {}` token set and all necessary class definitions. This makes individual snippets safe to drop in, but creates risks when combining several in the same lesson.

### CSS conflicts

Every component redefines the same CSS custom properties (e.g. `--orange`, `--ink`, `--card-shadow`) inside a `:root {}` block. When multiple `<style>` blocks are present in the same lesson, the **last one wins** for any conflicting property. In practice the values are identical across all components, so this is usually harmless — but if you ever customise a token in one component, that change will bleed into all others on the same page.

More dangerous are **shared class names**. Many components use generic names like `.accordion`, `.callout`, `.card`, `.progress-bar-fill`, `.copy-btn`, etc. If two widgets use the same class name with different style rules, whichever `<style>` block appears last in the DOM will take precedence, and one or both widgets will look broken.

**How to fix it:** Scope conflicting styles by wrapping each widget in a unique container and prefixing its classes, or add a unique `id` to the outermost element and qualify every rule with it:

```css
/* Before (global, may clash) */
.copy-btn { background: white; }

/* After (scoped) */
#widget-code-tabs .copy-btn { background: white; }
```

### JavaScript conflicts

Each component's `<script>` block declares top-level variables and functions (e.g. `renderSlide`, `renderConfig`, `checklistItems`, `steps`). If two components use the same function or variable name in the same lesson, the second declaration will silently overwrite the first, breaking whichever widget loaded first.

**How to fix it:** Wrap each component's JavaScript in an immediately-invoked function expression (IIFE) to create an isolated scope:

```html
<script>
(function () {
  // all of the component's original JS goes here
})();
</script>
```

This prevents any name from leaking into the global scope and colliding with another widget.

### Google Fonts

Every component includes the same `<link>` to Google Fonts for `Syne`, `DM Sans`, and `DM Mono`. If Skilljar allows `<link>` tags, having duplicates is harmless but redundant. If it strips them, add a single shared font import at the top of the lesson instead.

---

## Component Reference

### Interactive Components

These widgets contain JavaScript-driven behavior. They require both a `<style>` block and a `<script>` block to function.

| # | Name | Source Module | Description |
|---|------|---------------|-------------|
| 01 | **Blurred Reveal Table** | M1 | Data table where outcome cells are blurred until clicked. Includes "Reveal All" and a reveals counter. |
| 02 | **Drag-and-Drop Matching** | M2 | Cards dragged onto labeled drop targets. Shows correctness feedback, shake animation on wrong answer, success diagram on perfect score. Supports mouse and touch. |
| 03 | **Tabbed Primitives Explorer** | M3 | Three tabs each showing a concept with description, analogy, use-case pills, and a code sample. |
| 04 | **Code Tabs with Copy** | M3 | Tabbed code panels with a copy-to-clipboard button and syntax highlighting. |
| 05 | **Annotated Code Explorer** | M3 | Clickable JSON lines that activate matching annotation cards on the right. |
| 06 | **Mermaid Flowchart** | M4 | A Mermaid.js flowchart rendered inside a styled card. Requires the Mermaid CDN to be reachable. |
| 07 | **Accordion** | M5 | Expandable/collapsible sections. One section open at a time with a smooth `max-height` transition. |
| 08 | **Step Carousel** | M5 | Horizontal step-by-step slides with Prev/Next navigation, dot indicators, and a progress bar. |
| 09 | **Decision Tree** | M5 | A branching 3-question quiz that maps answer paths to one of 3 outcome types. |
| 10 | **Config Generator** | M6 | Pill-tab selector switches between config variants, showing syntax-highlighted code with a copy button and annotations. |
| 11 | **Step-Flow Navigator** | M6 | A visual node track at the top shows progress; the body shows the current step title and content; Prev/Next navigation. |
| 12 | **Interactive Checklist** | M6 | A checklist with a progress bar. Rows toggle checked state. A win state reveals when all required items are checked. |

### Static Components

These widgets are pure HTML/CSS with no JavaScript. They can be dropped in as-is with minimal collision risk, though CSS class name conflicts can still occur (see above).

| # | Name | Source Module | Description |
|---|------|---------------|-------------|
| S1 | **Objectives Box** | M1, M4–M6 | Orange-pale card listing lesson objectives with numbered orange bullet circles. |
| S2 | **Analogy Card Pair** | M1 | Two-column comparison cards — one muted (gray), one highlighted (orange). Each has a tag, icon, heading, body text, and verdict chip. |
| S3 | **CTA Aside** | M1, M4, M6 | Left-border callout card with a 4px solid orange border. Used for "Try This" prompts. |
| S4 | **What's Next Footer** | All | Dark ink card with orange icon box, label, and title. Arrow animates right on hover. |
| S5 | **Callout Box** | M2–M4 | Orange-pale card with an emoji icon and text. Used for goals, tips, or warnings. |
| S6 | **Video Placeholder** | M1, M3–M6 | Dark card with diagonal stripe pattern, orange play button circle, and label. Placeholder until a real video is embedded. |
| S7 | **Flow Steps List** | M4 | Numbered vertical step list. Each step has a dark numbered circle, bold title with an optional orange pill tag, and description text. |
| S8 | **Analogy Banner** | M5–M6 | Dark wide card with a large emoji, an eyebrow label, and body text. Used to introduce a memorable mental model. |
| S9 | **Section Label + Title** | All | Orange uppercase label → large Syne heading → orange left-border intro paragraph. |
| S10 | **Divider** | All | 1px horizontal rule. |

---

## Design System

All components share the same design tokens. If you customise one, update all of them for consistency.

### Fonts (loaded via Google Fonts)

| Role | Family |
|------|--------|
| Headings, labels, buttons | `'Syne', sans-serif` |
| Body text | `'DM Sans', sans-serif` |
| Code | `'DM Mono', monospace` |

### Color Tokens

| Token | Value | Usage |
|-------|-------|-------|
| `--orange` | `#FF6C37` | Primary accent, CTAs, highlights |
| `--orange-light` | `#FF8C5A` | Hover state for orange |
| `--orange-pale` | `#FFF0EB` | Orange tint backgrounds |
| `--ink` | `#1A1612` | Primary text, dark backgrounds |
| `--ink-mid` | `#4A3F38` | Secondary text |
| `--ink-light` | `#8C7B72` | Muted / placeholder text |
| `--rule` | `#E8DDD6` | Borders, dividers |
| `--white` | `#FFFFFF` | Page / card backgrounds |
| `--green` | `#2D9E6B` | Success states |
| `--red` | `#E03E2D` | Error states |
| `--blue` | `#2563EB` | Info accent |
| `--purple` | `#7C3AED` | Optional / secondary accent |

---

## Special Notes

### Mermaid Flowchart (06)
This component loads Mermaid.js from a CDN at runtime. It will not render in environments that block external scripts. If Skilljar's content security policy prevents external CDN scripts from running, this widget will silently fail to render the diagram.

### Drag-and-Drop Matching (02)
Touch support is implemented via `touchstart`/`touchmove`/`touchend` events with a ghost clone element. This works on most mobile browsers, but the learner experience is better on desktop.

### Copy-to-Clipboard buttons (04, 10)
These use the `navigator.clipboard` API, which requires a **secure context (HTTPS)**. Since academy.postman.com is served over HTTPS this is not an issue, but copy buttons will silently fail if the snippet is previewed over `http://` or `file://`.

---

## Repository Structure

```
skilljar-widget-component-library/
├── index.html               # Component browser (open this locally)
├── catalog.md               # Design system reference and component class documentation
├── README.md                # This file
└── components/
    ├── 01-blurred-reveal-table.html
    ├── 02-drag-drop-matching.html
    ├── 03-tabbed-primitives-explorer.html
    ├── 04-code-tabs.html
    ├── 05-annotated-code-explorer.html
    ├── 06-mermaid-flowchart.html
    ├── 07-accordion.html
    ├── 08-generator-step-carousel.html
    ├── 09-decision-tree.html
    ├── 10-config-generator.html
    ├── 11-step-flow-navigator.html
    ├── 12-interactive-checklist.html
    ├── s1-objectives-box.html
    ├── s2-analogy-card-pair.html
    ├── s3-cta-aside.html
    ├── s4-whats-next-footer.html
    ├── s5-callout-box.html
    ├── s6-video-placeholder.html
    ├── s7-flow-steps-list.html
    ├── s8-analogy-banner.html
    ├── s9-section-label.html
    └── s10-divider.html
```