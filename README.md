# Clean Workbench UI Skill

A palette-agnostic Agent Skill for building modern, crisp, high-density SaaS workbenches and web utility interfaces.

## What This Skill Captures

- **Palette-agnostic semantic tokens**: Swap neutral base (Slate / Zinc / Stone / Neutral) and primary accent freely while keeping crisp surface hierarchy.
- **12-column asymmetric workbench layout**: Sticky control panel + fluid live preview/result stream with clean mobile adaptation.
- **Tactile restraint**: 3-tier radius ladder (`rounded-2xl` / `rounded-xl` / `rounded-md`), subtle hairline borders, light/dark parity, and `150–200ms` transitions.
- **Precision typography**: Clean UI sans-serif paired with monospace strictly for technical/numeric data.
- **Affordance over explanation**: Zero instructional fluff, zero emoji icons, zero gradient buttons.

## Directory Layout

```text
skills/
└── clean-workbench-ui/
    ├── SKILL.md
    └── references/
        └── layout-and-tokens.md
```

## Usage

### Install via Agent Skills CLI
```bash
npx skills add wooxi/agent-skills
```

### Or Use Directly in Antigravity / Workspace
Copy `skills/clean-workbench-ui` into:
- Workspace: `.agents/skills/clean-workbench-ui/`
- Global: `~/.gemini/config/skills/clean-workbench-ui/`
