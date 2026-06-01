# Personal Knowledge Base

> Turn your own information — meetings, notes, documents, tasks — into raw material for reasoning.

A WorkBuddy skill that aggregates your activity across platforms and turns scattered records into structured insight: weekly reports, action plans, and deep-dive topic research. Built for people who think through writing and decide through evidence.

**This is not a note-taking tool.** It is a reasoning layer on top of the information you already produce — meetings you attend, decisions you make, signals you notice but haven't acted on yet.

---

## What It Does

### 1. Weekly Reports

Pulls your actual activity from connected platforms and generates a structured report:

- **What got done** — traced to specific meetings, documents, and tasks
- **Meetings you attended** — with key conclusions, not just a calendar dump
- **Decisions made** — extracted from meeting transcripts and documents
- **What's still open** — tasks mentioned but not closed, follow-ups owed
- **Next week's schedule** — from your calendar

Every claim is sourced. Nothing fabricated. No "looks like you were busy" filler.

### 2. Action Planning

Generates next-week action recommendations backed by evidence from the previous week:

```
Action: [concrete action]
Why: [one-sentence reason]
Evidence: [day X, in Y meeting/document, you said/appeared Z]
```

Categories tracked:
- **Completed** — delivered, shipped, closed
- **Decisions** — conclusions reached, documents finalized, commitments made
- **Unresolved** — mentioned but no follow-up, deferred, awaiting confirmation
- **Overlooked signals** — issues raised but never converted into actions

### 3. Cross-Platform Topic Research

Search across all your connected platforms for everything you've accumulated on a given topic. Returns:

- Documents and notes with summaries
- Relevant meetings with key conclusions
- Your own stated positions and judgments
- Open questions you've raised but never answered

---

## How It Works

```
Your platforms → Raw data → Structured insight → Your Obsidian vault
```

1. **Connect your platforms** — one-time setup per platform
2. **Tell it what you want** — weekly report, action plan, or topic research
3. **Get structured output** — written to your Obsidian vault with evidence links
4. **Build judgment over time** — Maps, backlinks, and the business analysis framework turn one-off insights into reusable knowledge

---

## Supported Platforms

| Platform | What It Pulls |
|----------|---------------|
| **Lark / Feishu** | Documents, Bitable records, meeting minutes & transcripts, calendar |
| **GetNotes** (Biji) | Voice-to-text transcripts, knowledge base entries, semantic search |
| **Tencent Meeting** | Meeting history, duration, participants, AI-generated summaries |
| **IMA** (Knowledge Assistant) | Saved reference materials and knowledge base content |

More platforms can be added. The architecture treats each platform as a modular data source.

---

## Obsidian Integration

Outputs are written directly to your Obsidian vault, organized by **future use** — not by source platform:

```
YourVault/
├── 商业判断/              # Business judgment notes
│   ├── 机会判断/
│   ├── 交易与定价/
│   └── ...
├── Maps/                 # Synthesis pages (projects, topics, people, MOCs)
├── _Evidence/            # Raw transcripts and sources (archival layer)
└── ...
```

Every claim links back to its source transcript with timestamped block references. The goal is traceability — you should always be able to answer "where did I get that from?"

For a full breakdown of the linking strategy, see [`references/obsidian-linking-strategy.md`](references/obsidian-linking-strategy.md).

---

## Business Judgment Framework

For business-related materials, this skill applies a structured analysis framework that goes beyond summarization. The goal is not to archive — it is to **train judgment**.

Each saved business item answers:
- Why was this worth saving?
- What changed in my understanding?
- What mechanism, pattern, opportunity, or risk is hidden inside?
- What evidence supports that judgment?

The framework uses **semi-structured templates** with composable analysis tools — lenses, scene reconstruction, case-based reasoning, deepwater analysis — rather than a rigid one-size-fits-all format.

See [`references/business-judgment-analysis.md`](references/business-judgment-analysis.md) for the full methodology.

---

## Setup

### Prerequisites

- [WorkBuddy](https://www.codebuddy.cn/docs/workbuddy/Overview) installed
- An Obsidian vault (optional but recommended)
- One or more supported platform accounts

### 1. Install the Skill

Copy this skill into your WorkBuddy skills directory:

```bash
cp -r personal-knowledge-base ~/.workbuddy/skills/
```

### 2. Configure Platforms

When you first trigger the skill, it walks you through platform setup one at a time. For each platform you enable:

- **Lark / Feishu** — requires a Lark app with appropriate permissions; uses `lark-cli`
- **GetNotes** — requires an API key from [biji.com/openapi](https://www.biji.com/openapi)
- **Tencent Meeting** — requires the official MCP skill installed
- **IMA** — requires the official IMA skill and API key

All credentials are stored in environment variables or in a local private config file (`~/.codex/pkb.local.json`) — **never in the skill package itself**.

### 3. Set Your Obsidian Vault

Set the environment variable `PKB_OBSIDIAN_VAULT` to your vault path, or add it to your local config:

```json
{
  "obsidianVault": "/path/to/your/vault",
  "platforms": ["lark", "get-notes"]
}
```

---

## Security Design

This skill is designed to be **distributable without exposing credentials**:

- All API keys, tokens, and secrets go into environment variables or a local private config file
- `pkb.local.json` is excluded by `.gitignore` — it never leaves your machine
- The skill package contains only documentation, workflows, and analysis frameworks
- Reference files use placeholder values (`xxxxx`, `<your-api-key>`) — never real credentials

If you're packaging this skill for distribution, run a quick audit first:

```bash
grep -rIn 'sk-\|ghp_\|Bearer\|Authorization' . --include='*.md' | grep -v '#\|placeholder\|xxxxx\|<your'
```

---

## Philosophy

Most knowledge tools ask: **how can I store more?**

This skill asks: **how can I think better with what I already have?**

- **Your information, not the internet's.** Only processes what you produced or participated in.
- **Evidence over inference.** Every claim traced to a specific source.
- **Judgment over accumulation.** The output is not a bigger pile — it's a sharper lens.
- **Structure that earns its keep.** Templates exist to surface what matters, not to fill fields.

---

## License

MIT

---

## Related

- [Obsidian Linking Strategy](references/obsidian-linking-strategy.md)
- [Business Judgment Analysis Guide](references/business-judgment-analysis.md)
