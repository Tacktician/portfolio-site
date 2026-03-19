# Component Library Catalog

Extracted from the MCP course HTML files (`components/html/MCP - Module 1–6.html`).

---

## Design System

### Fonts
| Role | Family |
|------|--------|
| Headings, labels, buttons, caps | `'Syne', sans-serif` |
| Body text | `'DM Sans', sans-serif` |
| Code | `'DM Mono', 'Fira Code', 'Courier New', monospace` |

### Color Tokens
| Token | Value | Usage |
|-------|-------|-------|
| `--orange` | `#FF6C37` | Primary accent, CTAs, highlights |
| `--orange-light` | `#FF8C5A` | Hover state for orange |
| `--orange-pale` | `#FFF0EB` | Orange tint backgrounds |
| `--ink` | `#1A1612` | Primary text, dark backgrounds |
| `--ink-mid` | `#4A3F38` | Secondary text |
| `--ink-light` | `#8C7B72` | Muted/placeholder text |
| `--rule` | `#E8DDD6` | Borders, dividers |
| `--white` | `#FFFFFF` | Page background, card backgrounds |
| `--green` | `#2D9E6B` | Success states |
| `--green-pale` | `#EAF7F1` | Success tint backgrounds |
| `--red` | `#E03E2D` | Error states |
| `--red-pale` | `#FEF0EE` | Error tint backgrounds |
| `--blue` | `#2563EB` / `#3B6FE8` | Info accent (Module 3, 5) |
| `--blue-pale` | `#EFF4FF` / `#EEF4FF` | Blue tint backgrounds |
| `--purple` | `#7C3AED` / `#7B5EA7` | Optional/secondary accent |
| `--purple-pale` | `#F5F0FF` / `#F3F0FB` | Purple tint backgrounds |

### Shadows
| Token | Value |
|-------|-------|
| `--card-shadow` | `0 2px 12px rgba(26,22,18,0.08), 0 1px 3px rgba(26,22,18,0.06)` |
| `--card-shadow-lift` | `0 12px 32px rgba(26,22,18,0.14), 0 4px 8px rgba(26,22,18,0.08)` |

### Code Token Colors (dark background)
| Class | Color | Usage |
|-------|-------|-------|
| `.tok-key` / `.tok-k` | `#FF8C5A` | JSON keys |
| `.tok-str` / `.tok-s` | `#7DD3B0` / `#7EC8A0` | String values |
| `.tok-num` / `.tok-v` | `#A8D8EA` | Numbers |
| `.tok-bool` / `.tok-b` | `#C3A8EA` | Booleans |
| `.tok-field` / `.tok-f` | `#FFD4C2` | Field names |
| `.tok-punc` | `#5C5047` | Punctuation |
| `.tok-comment` / `.tok-c` | `#4A3F38` / `#8C7B72` | Comments (italic) |

---

## Interactive Components

### 1. Blurred Reveal Table
**Source:** Module 1
**Description:** A data table where outcome cells are blurred until clicked. Supports "Reveal All" button.

**Key Classes:**
- `.persona-table` — the `<table>` element with orange header
- `.outcome-cell` — clickable `<td>`; add `.revealed` to unblur
- `.outcome-content` — blurred inner content (`filter: blur(6px); opacity: 0.3`)
- `.reveal-hint` — "Reveal" overlay text, disappears when `.revealed`

**JavaScript behavior:**
- Click `.outcome-cell` → adds `.revealed` class → transitions blur to 0
- "Reveal All" button calls the same function on all cells
- Counter tracks `N of 3 revealed`

**Customizable fields:** Table headers, row labels, blurred cell content, number of rows.

---

### 2. Drag-and-Drop Matching Activity
**Source:** Module 2
**Description:** Cards on the left dragged onto labeled drop targets on the right. Checks correctness, shows shake on wrong, flow diagram on perfect score.

**Key Classes:**
- `.drag-arena` — 2-column grid container
- `.cards-pool` — left panel, holds draggable cards
- `.drag-card` — draggable item (`data-id` attribute identifies it)
- `.drop-target` — right panel target (`data-accepts` = correct card id)
- `.drop-target.over` — hover state (orange border/pale bg)
- `.drop-target.correct` — correct placement (green)
- `.drop-target.incorrect` — wrong placement (red + shake animation)
- `.result-panel` — shows after Check (`show`, `success`, `partial` variants)
- `.flow-reveal` — diagram revealed on perfect score

**JavaScript behavior:**
- Full mouse + touch drag implementation with ghost element (fixed position clone)
- `elementFromPoint()` for drop target detection
- `data-accepts` checked against `data-id` to determine correctness
- Cards can be removed from targets and returned to pool

**Customizable fields:** Card labels/emojis, target role descriptions, target analogies, result messages, flow diagram nodes.

---

### 3. Tabbed Primitives Explorer
**Source:** Module 3
**Description:** Three tabs, each showing a concept with description, analogy, use-case pills, and a code sample.

**Key Classes:**
- `.primitives-explorer` — outer wrapper
- `.prim-tab-strip` — tab row
- `.prim-tab` — individual tab button (`data-prim`); `.active` = selected
- `.tab-icon`, `.tab-name`, `.tab-badge` — parts of each tab button
- `.prim-panel` — content panel; `.active` = visible
- `.prim-explain` — text explanation side
- `.prim-eyebrow` — small "Primitive N" label
- `.prim-desc` — description paragraph
- `.prim-analogy` — analogy block (styled box)
- `.prim-use-cases` / `.uc-pill` — pill-style example tags
- `.prim-code` — code block on dark background

**JavaScript behavior:**
- Click `.prim-tab` → removes `.active` from all panels/tabs, adds to clicked

**Customizable fields:** Tab count, tab labels/icons/badges, content in each panel.

---

### 4. Code Tabs with Copy Button
**Source:** Module 3
**Description:** Tabbed code panels with a copy-to-clipboard button and syntax highlighting.

**Key Classes:**
- `.code-tabs-wrap` — outer container
- `.code-tab-strip` — tab row (alternative: `.code-tabs-nav` with `.ctab-btn`)
- `.code-tab-btn` / `.ctab-btn` — tab button; `.active` = selected (dark bg)
- `.code-panel` — dark code container
- `.code-panel-topbar` — filename + copy button row
- `.code-panel-filename` — label (e.g. "Postman MCP Request Setup")
- `.code-panel-inner` — syntax-highlighted content block; `.active` = visible
- `.copy-btn` — clipboard button; `.copied` = green check state

**Alternative variant** (Module 5, simpler):
- `.code-tabs-nav` / `.ctab-btn` — tabs
- `.ctab-panel` — panels; `.active` = visible
- `.code-block` — code container (no topbar)

**JavaScript behavior:**
- Click tab → swap `.active` class on tabs and panels
- Click copy → `navigator.clipboard.writeText()` → temporary "Copied ✓" state (2s)

**Customizable fields:** Tab labels, filenames, code content.

---

### 5. Annotated Code Explorer ("Decode This")
**Source:** Module 3
**Description:** JSON on a dark background where each line is clickable; clicking activates a corresponding annotation card on the right.

**Key Classes:**
- `.decode-wrap` — outer container
- `.decode-layout` — 2-column grid (JSON left, annotations right)
- `.decode-json` — dark code block
- `.annotate-line` — clickable code line (`data-ann` = annotation number); `.active` = highlighted
- `.annotate-marker` — numbered circle that appears on hover/active
- `.decode-annotations` — right column, holds annotation cards
- `.annotation-card` — individual annotation; `.active` = full opacity, no translateX
- `.ann-num`, `.ann-title`, `.ann-body` — annotation card parts

**JavaScript behavior:**
- Click `.annotate-line` → remove `.active` from all lines and cards, add to clicked line and its matching card (`#ann-{data-ann}`)

**Customizable fields:** JSON content, number of annotated lines, annotation titles and body text.

---

### 6. Mermaid Flowchart Diagram
**Source:** Module 4
**Description:** A Mermaid.js flowchart rendered inside a styled card. Requires external Mermaid CDN.

**Key Classes:**
- `.diagram-wrap` — card container with orange top border
- `.diagram-label` — caption above the diagram
- `#mcpFlowDiagram` — target element; JS sets `.mermaid` class and injects diagram text

**JavaScript behavior:**
- Polls for `mermaid` global with 50ms retry
- Calls `mermaid.initialize()` with custom theme variables matching the design system
- Node colors: orange start (`#FF6C37`), green end (`#2D9E6B`), dark process nodes (`#1A1612`)
- Calls `mermaid.run()` to render

**External dependency:** Mermaid.js CDN (not offline-capable without bundling).

**Customizable fields:** Diagram definition string, node labels, colors.

---

### 7. Accordion
**Source:** Module 5
**Description:** Expandable/collapsible sections. One open at a time (exclusive).

**Key Classes:**
- `.accordion` — container
- `.acc-item` — each section; `.open` = expanded
- `.acc-trigger` / `.acc-trigger-inner` — clickable header area
- `.acc-icon` — emoji icon
- `.acc-label`, `.acc-sublabel` — title text within trigger
- `.acc-body` — collapsible body (`max-height: 0` → expanded)
- `.acc-body-inner` — inner content wrapper
- `.acc-code` — inline code block within body
- `.acc-anno` — annotation note within body

**JavaScript behavior:**
- Click trigger → if not open: close all, open clicked; if open: close it
- Uses `max-height` CSS transition for smooth animation

**Customizable fields:** Number of items, icons, labels, sublabels, body content.

---

### 8. Generator Step Carousel
**Source:** Module 5
**Description:** Horizontal step-by-step slides with Previous/Next navigation, dot indicators, and progress bar.

**Key Classes:**
- `.carousel-wrap` — outer container
- `.carousel-track` — card wrapper
- `.carousel-header` — step counter + dot row
- `.carousel-step-info` — "Step N of 8" text
- `.carousel-dots` / `.cdot` — dot indicators; `.active` = current
- `.carousel-slide` — current slide content (replaced by JS)
- `.carousel-footer` — nav buttons + progress bar
- `.progress-bar-wrap` / `.progress-bar-fill` — horizontal progress bar
- `#carPrev`, `#carNext` — navigation buttons

**Slide structure (rendered by JS):**
- `.car-slide-title` — step title
- `.car-slide-body` — main text (HTML)
- `.car-slide-why` — "Why this matters" annotation block

**JavaScript behavior:**
- Array of slide objects `{title, body, why}`
- `renderSlide(index)` injects HTML into `.carousel-slide`
- Progress bar = `(index + 1) / total * 100%`
- Prev disabled on first slide; Next changes to "Done ✓" on last

**Customizable fields:** Number of steps, step titles, body text, "why" annotations.

---

### 9. Decision Tree
**Source:** Module 5
**Description:** Branching 3-question quiz that maps answer paths to one of 3 outcome types.

**Key Classes:**
- `.decision-card` — card container
- `.dt-history` — breadcrumb row at top
- `.dt-crumb` — individual breadcrumb chip
- `.dt-progress-strip` / `.dt-progress-fill` — progress bar (0→33→66→100%)
- `.dt-question-area` — question + options
- `.dt-q-num` — "Question N of 3" label
- `.dt-q-text` — question heading
- `.dt-options` / `.dt-opt` — option buttons (full-width, hover orange)
- `.dt-result` — outcome area (animated slide-up)
- `.dt-result-badge` — outcome pill (`.flows`, `.generator`, or `.both`)
- `.dt-result-title`, `.dt-result-body` — outcome text
- `.dt-restart-row` — restart button

**JavaScript behavior:**
- Tree defined as `{question, options: [{label, value, next}]}`
- Navigate by clicking options; `path` array accumulates answer values
- Path mapped to outcome (e.g. `["existing-api"]` → generator outcome)
- Restart clears path, re-renders first question

**Customizable fields:** Questions, option labels, path-to-outcome mapping, outcome titles and descriptions.

---

### 10. Config Generator with Pill Tabs
**Source:** Module 6 (Section 1)
**Description:** Pill-tab selector switches between config variants; shows syntax-highlighted code with copy button, annotations, and a file path note.

**Key Classes:**
- `.cg-wrap` — outer container
- `.cg-card` — card with header / code / annotations / file-note sections
- `.cg-header` — pill row area
- `.cg-pill-label` — "Choose a host" label
- `.cg-pills` / `.cg-pill` — pill buttons (`data-host`); `.active` = selected
- `.cg-code-wrap` — dark code area
- `.cg-copy-btn` — copy button (top-right); `.copied` = green state
- `.cg-code` — syntax-highlighted code block
- `.cg-annotations` / `.cg-anno` — annotation rows below code
- `.cg-anno-dot`, `.cg-anno p` — dot + text per annotation
- `.cg-file-note` — italic file path note at card bottom

**Token classes:** `.tok-key` (orange), `.tok-str` (teal), `.tok-punc` (muted), `.tok-comment` (dark italic)

**JavaScript behavior:**
- `hosts` object: each key has `lines[]`, `tokens{}`, `annotations[]`, `note`
- `renderConfig(hostKey)` — rebuilds code (line-by-line with token spans), annotations, and file note
- Click pill → remove `.active` from all, add to clicked, call `renderConfig`
- Copy → joins `lines` with `\n`, writes to clipboard

**Customizable fields:** Pill labels/keys, config lines, token highlights, annotation text, file note.

---

### 11. Step-Flow Navigator
**Source:** Module 6 (Section 2)
**Description:** Visual node track at top shows progress; body shows current step title and text; Prev/Next navigation.

**Key Classes:**
- `.sf-wrap` — outer container
- `.sf-card` — card with track / body / footer
- `.sf-track` — horizontal node row (flex, scroll on mobile)
- `.sf-node` — individual step node; `.active` = current (orange, scaled up), `.done` = completed (green)
- `.sf-node-icon` — icon box (46×46px rounded)
- `.sf-node-lbl` — step label text
- `.sf-connector` — arrow between nodes; `.done` = green
- `.sf-body` — step content area (animated slide-in on change)
- `.sf-step-eyebrow` — "Step N of 4" label
- `.sf-step-title` — step heading
- `.sf-step-text` — step description
- `.sf-footer` — nav buttons + counter
- `.sf-btn` / `.sf-btn-primary` / `.sf-btn-ghost` — nav buttons
- `.sf-disabled` — disabled state (opacity 0.3, pointer-events none)
- `.sf-counter` — "Step N of 4" counter (right-aligned)

**JavaScript behavior:**
- `steps[]` array: each has `{icon, label, title, body}`
- `renderTrack()` — rebuilds node row with active/done classes
- `renderBody()` — injects step content, updates prev/next disabled states
- On last step: Next becomes "Done ✓" and is disabled

**Customizable fields:** Number of steps, icons, node labels, step titles, body text.

---

### 12. Interactive Checklist
**Source:** Module 6 (Section 3)
**Description:** Checklist with progress bar. Clicking rows toggles checked state. Win state reveals when all required items are checked.

**Key Classes:**
- `.cl-wrap` — outer container
- `.cl-card` — card with header / rows / footer / win
- `.cl-header` — title + progress bar row
- `.cl-title` — checklist title
- `.cl-prog-wrap` / `.cl-prog-bar` / `.cl-prog-fill` — progress bar (`width: N%`)
- `.cl-prog-label` — "N / 5" counter
- `.cl-row` — each checklist item; `.is-checked` = checked state (green bg, strikethrough title)
- `.cl-box` — custom checkbox div; turns green on checked
- `.cl-check` — SVG checkmark (opacity 0 → 1 with `checkPop` animation)
- `.cl-text` / `.cl-row-title` / `.cl-row-desc` — text content
- `.cl-badge` — pill badge; `.req` (orange) or `.opt` (purple)
- `.cl-footer-note` — italic instruction text
- `.cl-win` — success message; `.show` = visible

**Animations:** `@keyframes checkPop` (scale 0.6 → 1.2 → 1)

**JavaScript behavior:**
- `checklistItems[]` array: each has `{title, desc, badge, required}`
- Click row → toggle `checked[i]`, re-render row classes, update progress
- Win condition: all `required: true` items checked

**Customizable fields:** Item titles, descriptions, badge types (req/opt), required flags, win message text.

---

## Static Components

### S1. Objectives Box
**Source:** Modules 1, 4, 5, 6
**Classes:** `.objectives-box`, `.obj-label`, `.objectives-list`, `.obj-item`, `.obj-bullet`
**Description:** Orange-pale card listing lesson objectives with numbered orange bullet circles.

### S2. Analogy Card Pair
**Source:** Module 1
**Classes:** `.analogy-pair`, `.analogy-card`, `.analogy-card.usbc`, `.analogy-card.telephone`, `.analogy-verdict`
**Description:** 2-column grid of comparison cards. One muted (gray top border, 72% opacity), one highlighted (orange top border). Each has tag, icon, heading, text, verdict chip.

### S3. CTA Aside ("Try This")
**Source:** Modules 1, 4, 6
**Classes:** `.cta-aside`, `.cta-label`
**Description:** Left-border callout card (4px solid orange). White background with subtle shadow.

### S4. What's Next Footer
**Source:** All modules
**Classes:** `.whats-next`, `.next-icon`, `.next-text`, `.next-label`
**Description:** Dark ink card with orange icon box, label, and title. CSS `::after` arrow animates right on hover.

### S5. Callout Box
**Source:** Modules 2, 3, 4
**Classes:** `.callout`, `.callout-icon`, `.callout-text`
**Description:** Orange-pale card with emoji icon and text. Used for goals, tips, or warnings.

### S6. Video Placeholder
**Source:** Modules 1, 3, 4, 5, 6
**Classes:** `.video-placeholder`, `.video-play`, `.video-label`, `.video-sublabel`
**Description:** Dark ink card with diagonal stripe pattern, orange play button circle, and label. Used as a placeholder until real video is embedded.

### S7. Flow Steps List
**Source:** Module 4
**Classes:** `.flow-steps`, `.flow-step`, `.flow-step-num`, `.flow-step-title`, `.flow-step-desc`, `.step-tag`
**Description:** Numbered vertical step list. Each step has a dark numbered circle, bold title (with optional orange pill tag), and description text.

### S8. Analogy Banner
**Source:** Modules 5, 6
**Classes:** `.analogy-banner`, `.ab-icon`, `.ab-eyebrow`, `.ab-text`
**Description:** Dark ink card (wide) with large emoji icon and an eyebrow label above body text. Used to introduce a memorable mental model.

### S9. Section Label + Lesson Title
**Source:** All modules
**Classes:** `.section-label`, `h1.lesson-title` (with `em` for orange accent), `.lesson-intro`
**Description:** Orange uppercase label → large Syne heading → orange left-border intro paragraph.

### S10. Divider
**Source:** All modules
**Classes:** `.divider`
**Description:** 1px horizontal rule using `--rule` color. `max-width: 720px`.
