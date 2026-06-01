# Obsidian Linking Strategy for Personal Knowledge Base

Use this guide whenever synchronizing or restructuring personal knowledge-base content into Obsidian, especially Get笔记 notes, meeting transcripts, meeting summaries, personal notes, tasks, and project materials.

## Goal

Obsidian sync is not file transfer. The goal is to turn personal records into traceable knowledge:

- Preserve source evidence.
- Keep readable notes lightweight.
- Organize readable notes by future use, not by source channel.
- Build a small number of useful project/topic maps.
- Use backlinks to connect evidence to claims, not to decorate text.
- For business-related personal materials, create judgment-oriented notes using `business-judgment-analysis.md`; do not treat summaries as the final knowledge product.

## Priority for Business Materials

Most content in this user's PKB is business-related. For these materials, the main note should be an insight note, not a copied Get笔记 summary.

Default behavior:
- Use the full transcript as the evidence base when available.
- Use Get笔记 AI summary only as a reference, not as the main output.
- Do not generate a separate Source file when it would only duplicate the Get笔记 summary already visible elsewhere.
- Do not write API metadata into Obsidian unless the user explicitly asks for debugging/export records.
- The main note should answer: why was this saved, what changed in my judgment, what business mechanism is reusable, and what evidence supports it.

## Use-Based Folder Model

The source platform is metadata, not the primary folder. A note from Get笔记 should not automatically live under `Get笔记/Business Insights`.

Use three physical layers:

1. **Main knowledge layer**: readable notes organized by future use, for example:

```text
商业判断/机会判断/
商业判断/交易与定价/
商业判断/客户与关系/
商业判断/产品与交付/
商业判断/组织与产业/
商业判断/融资与资本/
个人判断/生命与关系/
```

2. **Map layer**: synthesis pages that organize many notes by project, topic, person, organization, method, or MOC:

```text
Maps/Projects/
Maps/Topics/
Maps/People/
Maps/Organizations/
Maps/Methods/
Maps/_MOCs/
```

3. **Evidence archive layer**: transcripts and raw sources that are rarely opened manually but must remain inside the vault so exact timestamp/block links work:

```text
_Evidence/Get笔记/Transcripts/<knowledge-base>/
_Evidence/Get笔记/Sources/<knowledge-base>/
```

A long note should choose one primary folder by `主用途`; all other meanings belong in properties, wikilinks, and Maps. Do not duplicate the same note into multiple folders.

## Three-Layer Model

Use three conceptual layers.

## Required Obsidian Properties

Every main Obsidian note created from PKB material must put basic information in Obsidian properties/frontmatter, not as a duplicated Markdown table in the body.

Default properties:

```yaml
---
来源平台: Get笔记
内容类型: 会议 / 录音 / 文档 / 笔记 / 商业洞察
主用途:
适用问题:
  - ...
标题:
创建时间:
更新时间:
发生时间:
知识库:
标签:
  - ...
相关项目:
  - "[[...]]"
相关主题:
  - "[[...]]"
原始材料: "[[...]] / 无 / API未提供"
Get笔记ID:
---
```

Rules:
- Do not add an H1 that repeats the filename/title. Obsidian already renders the file name as the page title.
- The file name should carry the date and title, e.g. `2026-05-26 - 供应链AI转型项目合作与人才培训沟通会议.md`.
- Use readable Chinese property names for user-facing notes; avoid machine-oriented properties such as `source`, `note_id`, `layer`, `created_at`, and `updated_at` unless explicitly needed for debugging.
- Do not duplicate the same basic information as a Markdown table immediately below the properties.
- Prefer `无` or `API未提供` over deleting common fields; consistent shape matters.
- Use links in property values only for high-value stable objects, such as project pages, transcript notes, or source notes.
- Use one `原始材料` property for the source anchor. For insight notes, link it to the transcript or original source file. For transcript/source notes that are themselves the raw material, use `当前文件`. Do not duplicate this as separate `原始文件`, `原文来源`, and `完整转录` fields unless there are genuinely different files.
- Any timestamp used as evidence in a main note must be a clickable Obsidian block link to the exact transcript/source segment, e.g. `[[Transcript File#^t002045|00:20:45]]`. Plain text timestamps are not acceptable evidence links.

### 1. Sources

Sources are faithful records.

Examples:
- Full meeting transcript.
- Raw Get笔记 export.
- Original audio/video metadata.
- Original meeting summary when it is the only available source.

Rules:
- Do not heavily rewrite Sources.
- Keep source metadata: platform, note_id, original title, created_at, participants when available, tags, API fields.
- If full transcript is available, save it separately under a transcript/source path and link it from the main note.
- Add stable block ids to transcript/source segments that may be cited from analysis notes. Use timestamp-derived ids such as `^t002045` for `[00:20:45]` speaker segments so links remain readable and stable.
- Long transcripts should not be embedded directly in project or topic pages.

Recommended paths:

```text
_Evidence/Get笔记/Sources/<knowledge-base>/<date - title>.md
_Evidence/Get笔记/Transcripts/<knowledge-base>/<date - title - transcript>.md
```

### 2. Notes

Notes are readable working summaries.

Examples:
- Meeting summary.
- Key decisions.
- Action items.
- Important excerpts.
- AI-generated summary after light cleanup.

Rules:
- A Note may link to its Source and Transcript.
- A Note should include source evidence links, but should not become a dense wiki page.
- Avoid linking every noun.
- Prefer a short "Links" or "Related" section over inline link spam when the link is useful but not central.

Recommended paths:

```text
商业判断/<主用途>/<date - title>.md
个人判断/<主用途>/<date - title>.md
Projects/<project>/<date - meeting title>.md
```

### 3. Maps

Maps are where knowledge is organized.

Examples:
- Project page.
- Topic page.
- Person page.
- Organization page.
- MOC/Hub page.

Rules:
- Maps synthesize across multiple Notes and Sources.
- Claims on Maps should link back to evidence Notes.
- Maps should be few and useful; do not create empty pages for one-off terms.
- Maps are the right place for "what we know", "open questions", "decisions", "next actions", and "timeline".

Recommended paths:

```text
Maps/Projects/<project>.md
Maps/Topics/<topic>.md
Maps/Organizations/<organization>.md
Maps/People/<person>.md
Maps/_MOCs/<domain>.md
```

## Backlink Rules

### Link These

Create or use backlinks for stable objects:

- Long-running projects.
- Organizations or clients.
- People with repeated involvement.
- Products or named initiatives.
- Durable themes that recur across notes.
- Decisions, standards, frameworks, or operating principles that will be reused.

Examples:

```markdown
[[供应链AI知识库项目]]
[[供应链AI转型项目]]
[[AI人才培养]]
[[OPC认证]]
[[企业AI转型]]
```

### Do Not Link These by Default

Avoid links for one-off or generic terms:

- Common nouns.
- Meeting filler.
- Single-use tasks.
- Broad words that create noisy graph nodes.
- Phrases that are only meaningful inside one note.

Examples to avoid unless they become recurring concepts:

```markdown
[[合同草案]]
[[成本测算]]
[[本地部署]]
[[沟通安排]]
[[资料共享]]
```

## Evidence Links

Use links where they preserve traceability.

Good:

```markdown
2026-05-26 会议确认：首期先做边界清晰的付款流程工作流智能体。
来源：[[2026-05-26 - 供应链AI转型项目合作与人才培训沟通会议]]
```

Bad:

```markdown
本次[[会议]]确认[[首期]][[项目]]先做[[付款]][[流程]][[工作流]][[智能体]]。
```

## Original Transcript Policy

When using APIs such as Get笔记:

1. First inspect whether the API returns full transcript fields, speaker segments, raw media text, attachments, or only AI summary content.
2. If only summary content is available, clearly mark the note as "AI summary / structured content, not full transcript".
3. If full transcript is available:
   - Save the transcript separately.
   - Link it from the readable main note.
   - Do not mix long transcript text into Map pages.
4. Speaker-segmented transcripts should preserve timestamps and speaker labels when available.

Suggested main note properties:

```yaml
---
来源平台: Get笔记
内容类型: AI summary
标题: ...
创建时间: ...
更新时间: ...
知识库: ...
原始材料: "[[... - transcript]] / API未提供"
Get笔记ID: ...
---
```

## Project and Topic Pages

For repeated topics, create or update Maps instead of overlinking every source note.

A useful project page usually contains:

```markdown
# Project Name

## Current State

## Timeline

## Decisions

## Open Questions

## Next Actions

## Evidence
```

Rules:
- Add links to source Notes under Evidence.
- Keep each decision tied to a source.
- Merge synonymous topic names instead of creating multiple near-duplicate pages.

## Sync Behavior

When importing a batch:

1. For business materials, create or update the main insight note first.
2. Preserve Transcript files when available; use them as evidence, not as graph-heavy knowledge nodes.
3. Create Source files only when they contain unique original material not already represented by the main note or Transcript.
4. Identify recurring stable objects from titles, tags, topics, and the actual judgment in the note.
5. Propose or create a small set of Map pages.
6. Add backlinks only where they improve retrieval, traceability, or synthesis.
7. Prefer updating existing Map pages over creating duplicate pages.
8. Report what was imported, what was linked, and what was intentionally not linked.

## Anti-Patterns

Avoid:

- Bulk wikilinking every extracted keyword.
- Creating empty topic pages for every tag.
- Putting all transcripts into one giant note.
- Treating AI summaries as original transcript without marking the difference.
- Letting Source notes become the only knowledge structure.
- Building a graph that looks dense but has no useful retrieval value.

## Default Recommendation

For Get笔记 knowledge-base sync:

- Create one readable main note per Get笔记 item, but place it by future use rather than under a Get笔记 folder.
- Create one Source or Transcript note per item only when raw/full content is available, and place it under `_Evidence/Get笔记/...`.
- Create one MOC/index page for the imported knowledge base under `Maps/_MOCs/`.
- Create or update a few Maps for recurring projects/topics.
- Use evidence links from Maps to Notes.
- Keep inline links sparse and intentional.
