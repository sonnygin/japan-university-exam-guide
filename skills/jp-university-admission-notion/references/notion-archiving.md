# Notion Archiving Reference

This document provides instructions for archiving extracted Japanese university admission information to Notion using the Notion MCP.

## Archiving Mode

**Default: Standalone Page** — Create a workspace-level private page with no parent. Do NOT ask the user for a database ID unless they explicitly offer one.

**Optional: Database Page** — If the user provides a `database_id` or `data_source_id`, create the page under that database instead, and set database properties accordingly.

## Page Content Structure (Notion-flavored Markdown)

The page content must follow this exact structure. Use Chinese for all summaries and analysis. Preserve original Japanese/English for official terms, dates, and requirements.

```markdown
## 出愿状态

**状态**: 未开始 / 准备中 / 已出愿 / 已考试 / 已合格 / 未合格
**最近截止日期**: [最近的一个关键截止日期及事项]

---

## 🔴 核心门槛与一票否决项 (Critical)

**出愿资格**:
[填写学历、年龄、在留资格要求]

**语言要求**:
- 日语: [EJU/JLPT 要求及有效期]
- 英语: [TOEFL/TOEIC/IELTS 要求、提交方式及有效期]

**事前审查**:
[是否需要，截止日期，所需材料]

---

## 🟡 考试内容与核心材料 (Important)

**选考方式**:
[书类审查、笔试、面试等详细说明]

**核心出愿材料清单**:
- 必须提供原件: [材料列表]
- 需要教授签字: [材料列表]
- 特殊要求: [翻译/公证/内诺等说明]

**研究计划书要求**:
[格式、页数限制、语言要求等，若无则写"无特殊格式要求"]

**报名费 (検定料)**:
[金额、支付方式、支付期限]

---

## 🟢 录取与入学信息 (General)

**募集人数**:
[具体招生名额]

**学费与奖学金**:
[初年度纳付金，学费减免制度]

**校区位置**:
[考试地点及入学后就读校区]

---

## 📅 申请时间线 (Timeline)

- `[YYYY-MM-DD] 至 [YYYY-MM-DD]` - `[事件名称]` - `[详细说明]`
- ⚠️ `[YYYY-MM-DD]` - `[容易遗漏的截止日期]` - `[详细说明]`

---

## 📝 备注

[补充说明、注意事项、文件中未明确但需要确认的事项]
```

## Notion MCP Tool Usage

### Default: Standalone Page (no database)

Omit the `parent` field entirely to create a workspace-level private page.

```bash
manus-mcp-cli tool call notion-create-pages --server notion --input '{
  "pages": [{
    "properties": {
      "title": "🎓 [大学名称] - [研究科/学部名称] [年度] 募集要項"
    },
    "icon": "🎓",
    "content": "[Notion-flavored Markdown 内容]"
  }]
}'
```

### Optional: Database Page (user provides ID)

Only use this when the user explicitly provides a database ID or data source ID.

```bash
manus-mcp-cli tool call notion-create-pages --server notion --input '{
  "parent": {"data_source_id": "[USER_PROVIDED_ID]"},
  "pages": [{
    "properties": {
      "title": "[大学名称] - [研究科/学部名称]"
    },
    "icon": "🎓",
    "content": "[Notion-flavored Markdown 内容]"
  }]
}'
```

## Key Rules for Notion MCP

- The `content` parameter must be the full Notion-flavored Markdown string.
- Do NOT include the page title inside `content`; it goes in `properties.title` only.
- Use `---` for horizontal rules (dividers) between sections.
- Use standard Markdown headings (`##`) for sections.
- Escape special characters if necessary.
- Do NOT use HTML tables with `<thead>`, `<tbody>`, `<th>` tags.
- For tables, use Notion format: `<table header-row="true"><tr><td>...</td></tr></table>` with each tag on its own line.
