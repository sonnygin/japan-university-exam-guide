---
name: academic-cold-email
description: Automate academic cold-emailing to Japanese professors for graduate admission. Deep-research professor webpages (including Japanese-language pages), generate a tailored research direction bridging professor's work with applicant background, draft bilingual (English + Chinese) cold emails, and archive all intelligence and drafts to Notion. Triggered when user wants to contact a professor for graduate school admission inquiry or "套瓷".
---

# Academic Cold Email

Automate the end-to-end cold-email workflow for graduate admission inquiries to Japanese university professors. Execute deep web intelligence gathering, dynamic research topic generation, bilingual professional email drafting, and structured Notion archiving.

## Prerequisites

- **Notion MCP** must be available for archiving results.
- **Browser** must be available for deep webpage traversal.

## Applicant Profile

Before starting, confirm the user has provided these three fields (ask if missing):

1. **Name** (姓名)
2. **Current Status** (当前院校/专业/年级)
3. **Strengths/Highlights** (核心技能与经历优势，如项目经验、论文、竞赛等)

Store these as the default applicant profile for all subsequent steps. If the user provides multiple professor URLs in one session, reuse the same profile without re-asking.

## Task Input

The user provides one or more professor homepage URLs per invocation. Process each URL through Steps 1-4 in order before moving to the next URL.

## Workflow

### Step 1: Deep Web Intelligence Extraction

Open the professor's homepage URL in browser. **Actively click into every navigable sub-page**, including but not limited to: Publications, Research, Profile, Members, Contact, News, Prospective Students (受験生へ/入学希望の方へ), Access, etc.

**Language handling:** Many Japanese professor pages are primarily in Japanese. Use page context and common academic Japanese terms to navigate. Key terms to recognize:
- 研究内容 / 研究紹介 = Research
- 業績 / 発表論文 = Publications
- メンバー = Members
- 受験生へ / 入学希望の方へ = For Prospective Students
- 連絡先 = Contact

**Red-line checks (highest priority):**
1. Scan for specific contact requirements: required email subject format, mandatory forms, guides to read first, or explicit "not accepting students" (学生の受け入れは行っておりません) statements.
2. If the professor explicitly states they are NOT accepting students, **stop immediately**, report this to the user, and skip Steps 2-3. Still archive the finding in Step 4 with status "Not Accepting".
3. Extract a valid email address. If no email is found on any page, note this and suggest the user check the university's faculty directory.

**Academic analysis:**
- Read research introduction and recent 3-year publication list.
- Identify core research directions and at least 2 representative recent papers (title, venue, year).
- Note any ongoing funded projects, industry collaborations, or specific research tools/datasets the lab uses.

**Source tracking:** Record the exact sub-page URL where each piece of information was found. Never fabricate sources.

### Step 2: Dynamic Research Topic Generation

Cross-match the professor's recent research focus (from Step 1) with the applicant's profile. Produce **1 concrete, feasible research direction** that:
- Aligns with the professor's current active trajectory (not decade-old work)
- Leverages the applicant's documented strengths
- Is expressed as a specific application scenario or technical entry point (not a broad field like "machine learning" or "NLP")
- Is realistically achievable within a master's program scope

### Step 3: Draft the Cold Emails

Draft **two versions** of the cold email:

**English version:** Under 400 words. See `references/email-template.md` for structure, examples, and red-line checks.

**Chinese version:** Under 500 字. See `references/email-template.md` for the Chinese template section. Use formal academic Chinese; avoid overly casual or flattering language.

Key rules for both versions:
- If Step 1 found special contact requirements, follow them absolutely.
- Reference a specific recent paper from Step 1 (by title).
- Weave in the proposed topic from Step 2 and the applicant's strengths.
- The two versions should convey the same core content but be independently natural in their respective languages, NOT literal translations of each other.

Present both drafts to the user for review before archiving.

### Step 4: Archive to Notion

Create a Notion page with all gathered intelligence and the draft emails. See `references/notion-archiving.md` for the page title format, content template, and MCP tool usage.

Language rules for the archive:
- Summaries and analysis sections: **Chinese**
- Technical terms and paper titles: **original language** (English/Japanese)
- Draft emails: English version in English, Chinese version in Chinese

## Strict Constraints

- **Zero fabrication**: Every paper title, email address, URL, and factual claim must come directly from the browsed pages. Use `[未确认]` for anything that could not be verified.
- **Respect professor preferences**: Any contact requirement found on the professor's page takes absolute priority over default templates.
- **No exaggeration**: Do not inflate the applicant's background. Keep descriptions factual and verifiable.
- **Source traceability**: Every piece of intelligence in the Notion archive must have a source URL.
