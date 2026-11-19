---
name: clean-workbench-ui
description: >-
  Design and build modern, high-density SaaS workbench and utility web interfaces
  characterized by crisp card hierarchy, semantic color tokens (palette-agnostic),
  12-column asymmetric split layouts, JetBrains Mono data accents, dark/light parity,
  and self-explanatory zero-fluff UX. Use when creating or redesigning web tools,
  dashboards, consoles, file processors, or productivity apps where clarity, speed,
  and tactile precision matter more than marketing decoration.
---

# Clean Workbench UI

A palette-agnostic design language for modern web utilities, developer tools, and SaaS workbenches. It prioritizes **spatial clarity, tactile restraint, information density, and affordance over explanation**—independent of any fixed brand color.

---

## Core Design Philosophy

1. **Palette-Agnostic Semantic Tokens**: Never hardcode a single fixed brand color into the philosophy. Choose a neutral surface scale (e.g., Slate, Zinc, Neutral, or Stone) and **one** intentional primary accent suited to the product domain, mapped through semantic CSS variables (`--background`, `--card`, `--foreground`, `--muted-foreground`, `--primary`, `--border`, plus semantic soft status tones for success/warning/danger/info).
2. **Affordance Over Explanation (Self-Explanatory UI)**: Let layout, labels, segmented controls, icons, and live previews speak for themselves. Eliminate onboarding banners, instructional paragraphs, marketing taglines, and verbose empty-state lectures.
3. **Asymmetric Workbench Hierarchy**: Pair a sticky control/input column with a fluid preview/result stream so users edit parameters and inspect live output simultaneously without excessive scrolling.
4. **Crisp Surface Separation**: Use a subtle tinted canvas (`--background`) behind clean elevated cards (`--card`) with 1px hairline borders (`--border`) and restrained micro-shadows—never muddy blur-heavy glassmorphism.
5. **Dual-Theme Parity**: Treat Light and Dark modes as first-class equals. Apply the theme before first paint (prevent FOUC) and preserve contrast hierarchy in both themes.

---

## Workflow When Applying This Skill

1. **Lock a Project Token Sheet First**
   - Pick **1 neutral family** (canvas, card, border, text) + **1 primary accent** + **4 semantic status tones** (success, warning, danger, info).
   - Define them once as CSS variables (see [layout-and-tokens.md](./references/layout-and-tokens.md)).
   - Never scatter raw color hex values inside feature components.

2. **Structure the Page Shell**
   - **Sticky Header (`h-16`)**: Translucent surface (`bg-card/85 backdrop-blur-md`) with a hairline bottom border. Left: compact brand mark + lightweight segmented navigation (`rounded-xl` track + elevated active pill) + context pill (e.g., workspace/room/project). Right: compact utility buttons + theme toggle.
   - **Main Container**: Centered `max-w-7xl` with responsive horizontal padding (`px-4 sm:px-6 lg:px-8`).
   - **12-Column Workbench Grid (`lg:grid-cols-12 gap-6`)**:
     - Left (`lg:col-span-5 lg:sticky lg:top-24`): Parameter panel, composer, or input controls inside a structured card (header bar → scrollable body → action footer).
     - Right (`lg:col-span-7 min-w-0`): Live preview canvas, result stream, filterable list, or dropzone.
   - **Mobile Adaptation (`<768px`)**: Collapse side-by-side panels cleanly into stacked cards or a compact 2-option segmented bar; use horizontal scroll (`no-scrollbar`) for filter/preset pill strips.

3. **Enforce Typography, Radius & Elevation Discipline**
   - **Typography**: Clean UI sans-serif (`Inter` + native CJK/system fallbacks) paired with monospace (`JetBrains Mono`) strictly for structured data: file sizes, dimensions, counts, percentages, timestamps, extensions, IDs, code, and keyboard hints.
   - **Scale**: Favor compact precision (`10 / 11 / 12 / 14 / 16px`, using `12px` as the workhorse for controls and metadata).
   - **3-Tier Radius Ladder**:
     - `16px` (`rounded-2xl`): Outer cards, modals, empty dropzones.
     - `12px` (`rounded-xl` / `rounded-lg`): Nested panels, segmented tracks, buttons, inputs.
     - `6px` / Pill (`rounded-md` / `rounded-full`): Badges, status chips, filter pills.
   - **Elevation**: `shadow-xs` on resting cards, `shadow-md` on interactive card hover, `shadow-2xl` on dialogs, subtle accent-tinted `shadow-sm` on primary buttons only.
   - **Icons**: Consistent monochrome stroke icons (`lucide-react`), strictly sized (`14px / 16px / 20px / 24px`).

4. **Interaction & Motion Standards**
   - Transitions stay crisp at `150–200ms ease` (`300ms` max for dropzone/dialog fades).
   - Respect `prefers-reduced-motion` (preserve only functional status indicators such as live connection dots).
   - Dropzones use `border-2 border-dashed` and shift to primary border + 5% primary tint on dragover.
   - Destructive actions require a confirmation dialog with initial focus on the safe **Cancel** button.

---

## Strict Anti-Patterns (Do Not Use)

- **No instructional fluff**: No "How it works" cards, no multi-sentence empty-state guides, no promotional hero sections on utility screens.
- **No emoji as UI icons**: Always use crisp vector icons.
- **No gradient buttons or neon glows**: Solid primary fill with clean hover/active shade steps.
- **No oversized cartoonish rounding or bloated padding**: Keep density purposeful and aligned.
- **No ad-hoc unstyled controls**: Reuse shared primitives (`Button`, `Badge`, `Input`, `Dialog`, `DropdownMenu`, `Progress`).
- **No unsplit heavy tool bundles**: Dynamically lazy-load heavy client-side libraries (e.g., PDF/Wasm engines) so the primary screen loads instantaneously.

---

## Verification Checklist

Before considering any UI implementation complete:
- [ ] Both Light and Dark modes maintain clear surface separation (canvas vs. card vs. nested block) and readable contrast.
- [ ] Brand accent is driven by semantic tokens—swapping `--primary` re-themes the app cleanly.
- [ ] Desktop (`≥1024px`) uses balanced asymmetric columns; mobile (`375px`) has zero horizontal overflow in header or controls.
- [ ] Numbers, metrics, file extensions, and IDs render in monospace.
- [ ] Zero decorative emoji, zero gradient buttons, and zero redundant instructional copy.

For concrete token templates, alternative color palettes, and reusable component recipes, read [references/layout-and-tokens.md](./references/layout-and-tokens.md).
