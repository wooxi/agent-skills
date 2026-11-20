# Agent Skills

A collection of Agent Skills for coding agents (OpenCode, Claude Code, Gemini CLI, etc.), following the standard `SKILL.md` format.

## Skills

### Lark / Feishu Suite (28 skills)

Official-grade skills for the Feishu (Lark) open platform, driven by `lark-cli`. Each skill covers one product domain with references and scripts:

| Skill | Domain |
|---|---|
| `lark-shared` | Auth setup: login / status / scopes for `lark-cli` |
| `lark-im` | Instant messaging: messages, chats, cards, reactions |
| `lark-mail` | Feishu Mail: draft, send, triage, listen |
| `lark-doc` | Docs & Wiki pages: read, create, edit, attachments |
| `lark-sheets` | Spreadsheets: structure, cells, formulas, charts |
| `lark-base` | Bitable: tables, fields, records, views, workflows |
| `lark-slides` | Slides: decks, pages, shapes |
| `lark-whiteboard` | Whiteboards in docs: export, update nodes |
| `lark-drive` | Drive: upload, download, share, permission, import |
| `lark-markdown` | Native Markdown files in Drive |
| `lark-wiki` | Knowledge spaces and node management |
| `lark-calendar` | Calendar events and meeting rooms |
| `lark-task` | Tasks, lists, task agents |
| `lark-approval` | Approval instances and definitions |
| `lark-attendance` | Attendance records |
| `lark-contact` | Contacts: name ↔ open_id resolution |
| `lark-meeting` | Video conferencing, notes, live content Q&A |
| `lark-minutes` | Minutes (routes to `lark-meeting`) |
| `lark-note` | Notes (routes to `lark-meeting`) |
| `lark-vc` / `lark-vc-agent` | VC (routes to `lark-meeting`) |
| `lark-event` | Real-time event streaming (NDJSON) |
| `lark-apps` | Miaoda/Spark apps: hosting, full-stack dev, triggers |
| `lark-okr` | OKR cycles, objectives, key results |
| `lark-openapi-explorer` | Raw Lark OpenAPI discovery |
| `lark-skill-maker` | Author custom `lark-cli` skills |
| `lark-workflow-meeting-summary` | Meeting-minutes digest workflow |
| `lark-workflow-standup-report` | Calendar + tasks standup summary |

### UI Suite

- `clean-workbench-ui` — Palette-agnostic skill for modern, crisp, high-density SaaS workbenches:
  - **Semantic tokens**: swap neutral base (Slate / Zinc / Stone / Neutral) and primary accent freely while keeping a crisp surface hierarchy.
  - **12-column asymmetric layout**: sticky control panel + fluid live preview/result stream with clean mobile adaptation.
  - **Tactile restraint**: 3-tier radius ladder, subtle hairline borders, light/dark parity, `150–200ms` transitions.
  - **Precision typography**: clean UI sans-serif paired with monospace strictly for technical/numeric data.
  - **Affordance over explanation**: zero instructional fluff, zero emoji icons, zero gradient buttons.

## Directory Layout

```text
skills/
├── clean-workbench-ui/
│   ├── SKILL.md
│   └── references/
└── lark-*/
    ├── SKILL.md
    ├── references/
    └── scripts/
```

## Usage

### Install via Agent Skills CLI
```bash
npx skills add wooxi/agent-skills
```

### Or Use Directly in Your Workspace
Copy a skill directory into:
- Workspace: `.agents/skills/<skill-name>/`
- Global: `~/.gemini/config/skills/<skill-name>/`
