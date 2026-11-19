# Layout & Semantic Token Reference

This reference provides concrete CSS variable structures, swappable color palettes, and component layout patterns for the **Clean Workbench UI** skill.

---

## 1. Semantic Token Architecture (Palette-Agnostic)

Define all surfaces and accents through semantic variables so any project can swap its neutral base or accent hue without rewriting components.

```css
:root {
  --radius: 0.75rem;
  --background: /* subtle tinted page canvas (e.g. neutral-100 / slate-100 / stone-100) */;
  --card: /* elevated crisp surface (#ffffff) */;
  --foreground: /* high-contrast ink (900-level neutral) */;
  --muted-foreground: /* secondary labels (500-level neutral) */;
  --border: /* hairline border (200-level neutral) */;
  --primary: /* single brand accent (600-level) */;
  --primary-foreground: #ffffff;
  --ring: /* focus ring (500-level brand accent) */;
  --destructive: #e11d48;
}

.dark {
  --background: /* deep neutral canvas (950-level) */;
  --card: /* elevated dark card (900-level) */;
  --foreground: /* light ink (100-level) */;
  --muted-foreground: /* secondary labels (400-level) */;
  --border: /* hairline dark border (800-level) */;
  --primary: /* brand accent (500/600-level with WCAG AA contrast) */;
  --primary-foreground: #ffffff;
  --ring: /* focus ring */;
}
```

### Example Swappable Theme Presets

Use the aesthetic with **any** color personality that fits the product:

| Preset | Neutral Base | Primary Accent | Best Fit |
| :--- | :--- | :--- | :--- |
| **Cool Studio** | Slate (`#f1f5f9` / `#020617`) | Indigo (`#4f46e5`) | Dev tools, file utilities, productivity workbenches |
| **Botanical Ops** | Zinc (`#f4f4f5` / `#09090b`) | Emerald (`#059669`) | Monitoring, finance, infrastructure, clean data tools |
| **Warm Editorial** | Stone (`#f5f5f4` / `#0c0a09`) | Amber/Orange (`#d97706`) | Writing tools, publishing, creative studios |
| **Crisp Cobalt** | Neutral (`#f5f5f5` / `#0a0a0a`) | Blue (`#2563eb`) | Enterprise consoles, analytics, API workbenches |
| **Monochrome Pro** | Zinc (`#f4f4f5` / `#09090b`) | Zinc-900 / White | Minimalist notes, terminal-adjacent tools |

### Semantic Soft Badges (Consistent Across Themes)

Use tinted 50-level light / 950-level dark backgrounds with matching 200/800 hairline borders (`border-*-200/60 dark:border-*-800/60`):
- **Success**: Emerald (saved, connected, size reduced)
- **Warning**: Amber (expiring soon, medium latency, caution)
- **Danger**: Rose (delete, error, high latency)
- **Info**: Sky/Blue (links, external references)
- **Neutral**: Base neutral 100/800 (metadata, default tags)

---

## 2. Standard Card Anatomy

Every primary control card follows a predictable 3-zone vertical rhythm:

```text
┌───────────────────────────────────────────────────┐
│ Header Strip: [accent dot] TITLE    [meta badge]  │  ← border-b, muted tint bg, px-4 py-3
├───────────────────────────────────────────────────┤
│ Body:                                             │
│  - Segmented mode switch (rounded-xl track)       │  ← p-4, space-y-4
│  - Parameter rows (label + font-mono value pill)  │
│  - Section dividers (border-t border-border/60)   │
├───────────────────────────────────────────────────┤
│ Action Footer: [Primary Action]   [Secondary/Send]│  ← border-t, subtle tint bg, p-3 sm:px-4
└───────────────────────────────────────────────────┘
```

---

## 3. Navigation & Sub-Navigation Patterns

- **Top-Level Switcher (in Sticky Header)**:
  - Compact segmented track (`rounded-xl bg-muted p-1`) with 2–4 concise items (`px-2.5 py-1 text-xs`).
  - Active item uses elevated card surface (`bg-card font-semibold text-foreground shadow-xs`).
- **Secondary Filter / Tool Bar (Top of Main Content)**:
  - Single `rounded-2xl` card bar containing horizontal scrollable tabs (`no-scrollbar overflow-x-auto`) on the left and search / clear / status indicator on the right.
  - Active tab uses high-contrast fill (`bg-foreground text-background` in light or `bg-primary text-primary-foreground` in dark).

---

## 4. Empty States & Dropzones

- Keep empty states **quiet and actionable**:
  - `min-h-[340px] rounded-2xl border-2 border-dashed`
  - Centered icon container (`size-16 rounded-2xl bg-muted`) that scales gently (`group-hover:scale-105`) and shifts to primary soft tint on hover.
  - At most 1 short action title + 1 concise capability/format hint line (`text-xs text-muted-foreground`).

---

## 5. Typography & Data Formatting Rules

- **UI Sans**: `Inter, -apple-system, BlinkMacSystemFont, "PingFang SC", "Microsoft YaHei", sans-serif`
- **Data Mono**: `"JetBrains Mono", ui-monospace, SFMono-Regular, Menlo, Consolas, monospace`
- Always apply `font-mono` to:
  - Byte sizes (`12.4 KB`, `1.8 MB`)
  - Dimensions & counts (`1920×1080`, `3 / 12 页`, `-68%`)
  - Latency & timers (`42ms`, `04:59`)
  - File extension blocks (`PDF`, `PNG`, `WEBP`)
  - Shortcuts, routes, and identifiers (`#public`, `P1`)
