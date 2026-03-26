# Notion Archiving Reference

## Page Title Format

```
[中文大学名称] - [中文教授姓名] - [中文核心研究方向] - [YYYY-MM-DD]
```

Example: `东京大学 - 田中太郎 - 自然语言处理 - 2026-03-25`

## Page Content Structure (Notion-flavored Markdown)

Use the following template. All section summaries in Chinese; keep technical terms, paper titles in original language; English email in English, Chinese email in Chinese.

```
## 基本信息

**教授**: [教授姓名（原文）]
**职称**: [职称]
**所属**: [大学] [研究科/学部] [研究室名称]
**Email**: [教授邮箱]
**主页**: [教授主页链接]
**信息来源**: [找到邮箱的页面链接]

---

## 套瓷状态

**状态**: 待发送 / 已发送 / 已回复 / 不招生
**发送日期**: [填写实际发送日期，初始为"—"]
**回复情况**: [填写回复摘要，初始为"—"]

---

## 特殊要求

[用中文总结教授页面上发现的套瓷/联系特殊要求。若无特殊要求则写"无特殊要求，按默认模板发送即可"]
**来源**: [要求页面的链接，若无则写"N/A"]

---

## 研究方向与近期成果

[用中文概括教授核心研究方向，括号内保留英文/日文术语]

**近期代表论文**:
1. [论文原标题] ([会议/期刊], [年份])
2. [论文原标题] ([会议/期刊], [年份])

**进行中的项目**: [如有，用中文简述；如无则写"未公开"]
**来源**: [论文列表所在网页链接]

---

## 拟定研究方向

[用中文阐述为申请者动态构思的研究课题，说明：
1. 如何与教授当前研究衔接
2. 如何发挥申请者的背景优势
3. 具体的切入点或应用场景]

---

## 套瓷信（English）

**Subject**: [邮件标题]

[纯英文套瓷信正文]

---

## 套瓷信（中文）

**标题**: [邮件标题]

[中文套瓷信正文]
```

## Notion MCP Tool Usage

Create standalone page (no parent database):

```bash
manus-mcp-cli tool call notion-create-pages --server notion --input '{
  "pages": [{
    "properties": {"title": "[页面标题]"},
    "icon": "📧",
    "content": "[Notion-flavored Markdown 内容]"
  }]
}'
```

Key rules:
- Do NOT include page title inside `content`; it goes in `properties.title` only.
- Use `---` for horizontal rules (dividers) between sections.
- Use standard Markdown headings (`##`) for sections.
- Escape special characters: `\ * ~ \` $ [ ] < > { } | ^`
- Do NOT use HTML tables with `<thead>`, `<tbody>`, `<th>` tags.
- For tables, use Notion format: `<table header-row="true"><tr><td>...</td></tr></table>` with each tag on its own line.
- The `content` parameter must be the full Notion-flavored Markdown string, NOT a file path.
