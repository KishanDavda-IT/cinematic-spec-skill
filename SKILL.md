---
name: cinematic-build-prompt
description: >
  Formats and presents UI/frontend build prompts in a precise, cinematic spec style — structured
  by tech stack, design system, component tree, and per-section breakdowns with exact class strings,
  animation values, asset URLs, inline SVG paths, and copy text. Use this skill whenever the user
  asks to "write a build prompt", "spec out a landing page", "document a UI build", "turn this
  design into a prompt", "make a prompt for a dev to build", or wants to produce a hand-off document
  that an AI or developer could use to recreate a UI exactly. Also trigger for requests like
  "format this prompt properly", "make this more detailed/precise", "write a spec for this page",
  "cinematic prompt", or "build spec". Trigger liberally — if the user is describing a UI and
  wants it documented in a way someone else could build it, this skill applies.
---

# Cinematic Build Prompt Style

A skill for writing frontend build prompts that are precise enough for an AI or developer to reproduce a UI exactly — without needing any design files.

## Core Philosophy

The output is a **complete specification document**, not a description. Every value is concrete. No guessing, no "something like", no "approximately". If a color is `rgba(255,255,255,0.45)`, write `rgba(255,255,255,0.45)`. If a delay is `0.4s`, write `0.4s`. Exact Tailwind class strings go in backtick spans or inline as-is.

The spec is **layered** — global first, then section-by-section, then component-by-component, then behavior detail. A reader scans top-down and gets progressively more specific context.

---

## Document Structure (in order)

### 1. Title Line

```
Build Prompt: [Descriptive Name of the Page/Feature]
```

Followed by one sentence: what the build produces at the highest level.

### 2. Tech Stack (pinned, CDN-only)

- List every dependency: library name, exact version, full CDN `<script>` or `<link>` tag
- Include integrity hashes where available
- List framework-level wiring (e.g., `window.Motion = window.FramerMotion`)
- Note body/root defaults (bg color, mount point)
- One-liner: how Babel/JSX is set up

### 3. Fonts

- Google Fonts import line (or CDN URL)
- Tailwind `fontFamily` config additions with exact key names
- Usage note per font (e.g., "always italic in use")

### 4. Design System / Global Utilities

- Tailwind config overrides (border-radius defaults, etc.)
- Custom CSS classes with full verbatim CSS in fenced code blocks
- Pseudo-element variants (`:before`, `:after`) included
- One class = one code block; no abbreviations like "same but..."
- Explain the visual effect of each class in one sentence after the block

### 5. Shared Components (reusable, defined once)

For each shared component:

- **Name** as a subheading
- What triggers/mounts it
- Behavior as a numbered list (event handlers, rAF logic, timing constants)
- Props if any
- Cleanup logic on unmount

### 6. Page Sections (one subheading per section)

Each section follows this sub-structure:

**Background / Media**
- Asset URL (full, exact)
- Positioning classes verbatim: `absolute left-1/2 top-0 -translate-x-1/2 object-cover z-0`
- Inline style overrides if any: `{ width: "120%", height: "120%" }`
- Overlay treatment (or explicit "No overlay")

**Layout Shell**
- Container classes
- Z-index layering map (`z-0` = video, `z-10` = content, `z-50` = nav, etc.)
- Flex/grid structure

**Components** (listed top → bottom in DOM order)

Each component block contains:

- **Position/Layout** — Exact classes: `fixed top-4 px-8 lg:px-16 z-50 flex items-center justify-between`
- **Children** (indented sub-sections, left → right or top → bottom)
  Each child has:
  - Element type and classes
  - Text content in quotes: `"Claim a Spot"`
  - Icon: named + SVG path data verbatim if inline
  - **Framer Motion** (if animated)
    - `initial`, `animate` values (all properties: `filter`, `opacity`, `y`, etc.)
    - `transition` (`duration`, `delay`, `ease`)
    - Keyframe arrays with `times` if multi-step
- **State / Interaction** — Bullet points for hover, click, intersection logic

### 7. Icons Section (if inline SVGs are used)

List each icon:
- Name
- `viewBox`
- Path data (verbatim `d` attribute)
- `strokeWidth`, `fill`, `linecap` if relevant

### 8. Notes

A final section for:
- Implementation gotchas ("rAF-driven, no CSS transitions")
- Browser compatibility caveats
- Things that look wrong but are intentional
- Suppressible warnings

---

## Formatting Rules

### Class Strings

Write Tailwind classes exactly as they appear — no line breaks mid-class-string, no paraphrasing:

```
flex items-center gap-6 mt-6
```

Not: "flex with items centered and 6-unit gap, margin-top 6".

### Colors and Values

Always literal:
- `rgba(255,255,255,0.01)` — not "near-transparent white"
- `text-[5.5rem]` — not "roughly 88px"
- `delay 0.4s` — not "slight delay"
- `tracking-[-4px]` — not "tight tracking"

### Text Copy

Wrap all UI copy in quotes: `"Maiden Crewed Voyage to Mars Arrives 2026"`. Never paraphrase.

### Animation Specs

Full object form:

```js
initial: { filter: 'blur(10px)', opacity: 0, y: 20 }
animate: { filter: 'blur(0px)', opacity: 1, y: 0 }
transition: { duration: 0.7, delay: 0.4, ease: 'easeOut' }
```

For keyframes:

```js
animate: {
  filter: ['blur(10px)', 'blur(5px)', 'blur(0px)'],
  opacity: [0, 0.5, 1],
  y: [50, -5, 0]
}
transition: { duration: 0.7, times: [0, 0.5, 1], ease: 'easeOut' }
```

### Behavior Specs (for JS-heavy components)

Use numbered steps. Name constants upfront. Use code-style for variable names:

1. `FADE_MS = 500`, `FADE_OUT_LEAD = 0.55` seconds.
2. `fadeTo(target, duration)`: uses `requestAnimationFrame`; reads current opacity from `video.style.opacity` so each fade resumes from current state.
3. On `loadeddata`: set opacity 0, call `play()`, call `fadeTo(1)`.
4. On `timeupdate`: if not already fading out and `duration − currentTime ≤ 0.55`, set `fadingOutRef` and call `fadeTo(0)`.
5. On `ended`: set opacity 0; after 100ms `setTimeout` reset `currentTime = 0`, call `play()`, clear `fadingOutRef`, call `fadeTo(1)`.
6. Cleanup on unmount: `cancelAnimationFrame`, remove all event listeners.

### SVG Path Data

Inline verbatim — never describe the icon in prose when path data is available:

```jsx
// ArrowUpRight
<svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor"
  strokeWidth="2" strokeLinecap="round">
  <path d="M7 17L17 7"/>
  <path d="M7 7h10v10"/>
</svg>
```

---

## Tone and Voice

- Imperative, technical, zero fluff. No "you might want to", no "consider using".
- Present tense: "wraps a `<video>`", "triggers on 10% visibility".
- Sections are dense — a competent builder reads, not skims.
- No motivational copy. No "this creates a beautiful effect". Just spec.

---

## Quality Checklist

Before finalizing a build prompt, verify:

- [ ] Every dependency has a pinned version
- [ ] Every color/opacity/size is a literal value, not a description
- [ ] Every component has exact class strings
- [ ] All text copy is quoted verbatim
- [ ] All Framer Motion animations have `initial` + `animate` + `transition` (with `delay`)
- [ ] Shared components defined once, not re-described per use
- [ ] SVG paths are literal `d` attribute strings
- [ ] Background media URLs are full absolute URLs
- [ ] A Notes section exists for implementation caveats
- [ ] DOM order matches visual order (top → bottom, left → right)

---

## Anti-Patterns to Avoid

| Don't write | Write instead |
|---|---|
| "Use a glassmorphism style" | Full `.liquid-glass` CSS block verbatim |
| "Add a slight delay" | `delay: 0.4` |
| "Something like Framer Motion" | Exact `motion.div` props |
| "A nice italic serif font" | `font-heading italic text-[5.5rem]` |
| "An arrow icon" | SVG path `d="M7 17L17 7 M7 7h10v10"` |
| "Fade the video in and out" | Full `fadeTo()` rAF spec with timing constants |
| "Use Tailwind for layout" | `flex items-center justify-between gap-4 px-8 lg:px-16` |
| "Approximate the spacing" | `mt-6 gap-6 p-5 w-[220px] rounded-[1.25rem]` |

---

## Example Output Shape

A finished build prompt produced with this skill looks like:

```
Build Prompt: [Name]
[One-sentence description]

Tech stack (pinned, CDN-only)
[script tags with integrity hashes]
[window aliases]

Fonts
[Google Fonts import]
[Tailwind config additions]

Liquid-glass utilities (exact CSS, in a <style> block)
[CSS code blocks, one per class]

[ComponentName] component
[Numbered behavior spec]

Section 1 — [Name] ([layout descriptor])
  Background video (...)
    src: [full URL]
    class: [verbatim classes]
    style: [inline style object]

  Navbar ([descriptor])
    Left: [...]
    Center: [...]
    Right: [...]

  [ComponentName] (descriptor)
    [Sub-element]: [classes] — "[copy text]"
    [Sub-element]: [classes] — "[copy text]"
    [Framer Motion spec]

Section 2 — [Name]
[...]

Icons (inline SVGs)
[name]: [viewBox], path d="..."

Notes
[Bulleted gotchas]
```

---

## How to Use

When the user provides a design description, reference image, or rough prompt:

1. Extract all concrete values (colors, sizes, spacing, timing, copy text, asset URLs)
2. Identify the tech stack (or ask if not specified)
3. Structure the output following the document structure above
4. Fill in every section — if information is missing, use reasonable defaults and note them in the Notes section
5. Run through the Quality Checklist before delivering

If the user provides a rough/draft prompt to "make more precise", parse it and fill in gaps with exact values, class strings, and animation specs. Preserve the user's design intent — just make it buildable.
