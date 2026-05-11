---
name: cold-email-check
description: Full academic cold-email pipeline with MANDATORY comprehensive fact-checking (40+ items). Runs the original academic-cold-email workflow (professor research → research topic → bilingual draft) then AUTOMATICALLY performs exhaustive fact-checking covering ALL claims, paper content accuracy, technical nouns, research direction correctness, URLs, admission schedules, and research feasibility — with source links and corrections embedded into the output file. No user approval needed for fact-checking. Triggered when user wants a verified, professor-safe cold email for graduate admission to Japanese universities.
---

# Cold Email with Mandatory Fact-Check

Two-phase pipeline: (1) draft generation using the academic-cold-email skill, then (2) AUTOMATIC exhaustive fact-checking (40+ items) against primary sources. **Fact-checking runs automatically without asking — do NOT prompt the user for approval.**

---

## Phase 1: Draft Generation (academic-cold-email workflow)

Execute the full `academic-cold-email` skill workflow as defined in `/Users/admin/.claude/skills/academic-cold-email/SKILL.md`. Key checklist:

- [ ] Confirm applicant profile (Name, Current Status, Strengths)
- [ ] **Read the user's personal cold email style file** at `~/Downloads/coldEmail.md` — all drafted emails MUST match this style
- [ ] Deep web intelligence extraction (browse professor pages, click all sub-pages, note Japanese keywords)
- [ ] Red-line checks (contact requirements, not-accepting statements, email extraction)
- [ ] Dynamic research topic generation (cross-match professor work × applicant background)
- [ ] Draft English version (<400 words) and Chinese version (<500字), following the user's style
- [ ] Archive to Notion if available

### User's Personal Cold Email Style (from `~/Downloads/coldEmail.md`)

Before drafting, read `~/Downloads/coldEmail.md` to internalize the user's established style. The following patterns are extracted from the user's previous successful cold emails and MUST be followed:

**Structural pattern (English version):**

1. **Subject line**: `Inquiry regarding Admission: [Specific Topic Keywords] - [Name]`
2. **Paragraph 1 (2-3 sentences)**: Name, university, graduation date, major. State intent to pursue graduate studies under the professor. Keep it factual — do NOT over-explain.
3. **Paragraph 2 (3-5 sentences, the core)**: Reference a SPECIFIC recent paper or project by the professor (by title or topic). State what impressed the applicant. Then propose a concrete, feasible research direction that bridges the professor's work with the applicant's background.
4. **Paragraph 3 (2-3 sentences)**: Describe the applicant's strengths. Use "Rather than building X from scratch, my core strength lies in Y" pattern. Do NOT claim to lead/design/architect — use "participated in" or "contributed to" language. Mention one concrete industry experience (e.g., Shopee) and one learning effort (e.g., CS229).
5. **Paragraph 4 (2-3 sentences)**: Mention exam preparation status. Politely ask whether professor is accepting students. Offer to send CV and research proposal. End with "Thank you very much for your time and consideration."

**Tone rules:**
- Professional but not overly formal. No flattery or exaggeration.
- Avoid "strongly believe", "passionate about", "truly inspired" — stay factual.
- Do NOT claim to "design", "lead", "architect", or "spearhead" at work. Use "participated in", "contributed to", "was involved in".
- Correctly identify the professor's co-workers' work vs. the professor's own work. If a paper is by DBCLS colleagues, say "DBCLS's recent work" not "your recent work" unless the professor is an author.
- English only for the English version. The Chinese version (if requested) follows the `academic-cold-email` Chinese template.

### Output File

Save the complete output to a **new `.md` file** at `~/Downloads/coldEmail-[Professor-LastName].md`. The file must include:

```
# [教授姓名] ([英文名]) — 套瓷信

## 教授信息
[表格：姓名、职称、所属、地址、电话、Email、主页链接、招生状态]

## 研究方向
[3 个研究方向，含代表项目和工具]

## 近期代表性成果
[5 篇/项，含标题、期刊/来源、日期]

## 拟定研究方向
[研究方向描述 + 与教授工作的衔接说明]

## 套瓷信（English）
[完整英文邮件正文]

## 套瓷信（中文）
[完整中文邮件正文]

## 待办
- [ ] 确认邮箱
- [ ] 确认招生
- [ ] ...
```

---

## Phase 2: Mandatory Fact-Checking (AUTOMATIC — DO NOT ASK)

**This phase runs automatically after Phase 1 completes. Do NOT ask the user whether to proceed.** Immediately begin fact-checking all claims against primary sources.

Perform an exhaustive **40+ item** fact-check across four rounds. Append all findings to the same `.md` file under `## 事实核查报告` section.

### Fact-Check Focus: Content Accuracy

The primary focus is on **content truthfulness** — is every claim about the professor, their papers, their research, and technical concepts factually correct?

Critical questions to answer for each claim:
- Does the paper actually say what the email claims it says? (check abstract/body)
- Is the professor's research direction accurately described? (check lab page × paper titles)
- Are technical nouns, frameworks, and methodologies real and correctly used? (check official docs)
- Does the proposed research direction align with what the lab actually does? (cross-reference)

---

### Round 1: Professor Identity & Institution (12 items)

| # | Claim to Verify | Verification Method | Source |
|---|----------------|-------------------|--------|
| 1.1 | Professor name (kanji + romaji spelling) | University lab page + ResearchMap API | Dual source |
| 1.2 | Professor title/position (教授/准教授/客員教授/ユニット長 etc.) | Lab page + official recruitment page | Dual source |
| 1.3 | All affiliated institutions (university + research center) | Lab page + ResearchMap affiliations | Dual source |
| 1.4 | Department/program full name (English + Japanese) | University page `<title>` tag | Official page |
| 1.5 | Email address existence and accuracy | Find on professor/lab/contact pages; mark `[未确认]` if hidden | Professor page |
| 1.6 | Lab/research unit full name in both languages | Lab page + institution page | Dual source |
| 1.7 | Physical address (postal code, building, campus) | Official institution page footer | Official page |
| 1.8 | Phone number | Lab/contact page | Official page |
| 1.9 | Lab homepage URL accessibility | Direct browser access, verify 200 | URL verification |
| 1.10 | All additional profile URLs (ResearchMap, ORCID, Google Scholar) | Access each URL, verify it returns professor's profile | URL verification |
| 1.11 | Professor's degree and education history | ResearchMap education section + CV if available | ResearchMap |
| 1.12 | Committee memberships / professional roles | ResearchMap committee section | ResearchMap |

### Round 2: Research Content & Paper Accuracy (14 items)

This is the **core round** — every claim about papers and research must be verified against the actual paper content.

| # | Claim to Verify | Verification Method | Source |
|---|----------------|-------------------|--------|
| 2.1 | Paper 1: exact title (character-by-character) | AAAI/PubMed/DOI page title field | Official paper page |
| 2.2 | Paper 1: ALL author names and order | Official paper page author list | Official paper page |
| 2.3 | Paper 1: journal/conference name, volume, pages, year | Official paper page metadata | DOI / PubMed |
| 2.4 | Paper 1: DOI format and resolvability | Check DOI resolves correctly | doi.org |
| 2.5 | Paper 1: ABSTRACT content — does the email's description match what the paper actually says? | Read abstract, compare with email claims line-by-line | Paper abstract |
| 2.6 | Paper 1: METHOD name accuracy (e.g., "DkGSB", "AGL") — does the paper use this exact term? | Search paper for exact term | Paper full text/abstract |
| 2.7 | Paper 1: KEY CLAIMS — are numerical results, benchmarks, or comparisons stated accurately? | Cross-check email claims with paper results section | Paper full text |
| 2.8 | Paper 2-5: title, authors, journal, date (at least 3 additional papers) | ResearchMap + PubMed + DOI | Multi-source |
| 2.9 | Research direction 1 — verify against lab page description and paper titles | Compare email description with lab page × 3+ paper titles | Lab page + papers |
| 2.10 | Research direction 2 — same verification | Same method | Lab page + papers |
| 2.11 | Research direction 3 — same verification | Same method | Lab page + papers |
| 2.12 | ALL technical nouns in the email — verify each exists and is correctly used | For each noun: check if it appears in the professor's actual papers or official docs | Papers + official docs |
| 2.13 | Professor's RESEARCH TRAJECTORY — is the email's framing of "ongoing work" accurate for recent 3 years? | Check 3-year publication timeline, verify active projects | ResearchMap projects + papers |
| 2.14 | Co-author relationships — who are the professor's frequent collaborators? Does the email attribute work correctly? | Check author lists across papers | ResearchMap papers |

### Round 3: Technical Infrastructure & Tools (8 items)

| # | Claim to Verify | Verification Method | Source |
|---|----------------|-------------------|--------|
| 3.1 | Each software/tool/database mentioned — does it exist? | Access official website/GitHub | Official site |
| 3.2 | Each tool's function — does the email describe it correctly? | Compare email description with tool's README/docs | Official docs |
| 3.3 | Tool version/release date if mentioned | Check GitHub releases or news | GitHub |
| 3.4 | Tool license and availability (open source? public?) | GitHub LICENSE file | GitHub |
| 3.5 | Programming language / tech stack of key tools | GitHub repo language stats | GitHub |
| 3.6 | Architecture/diagram claims — does the official architecture doc match? | Research page architecture diagram | Official research page |
| 3.7 | Benchmark/performance claims — does the project have benchmark data? | Check for benchmark/ directory or paper results | GitHub + paper |
| 3.8 | Code/data availability statements in referenced papers | Check paper for "Code Availability" or "Data Availability" sections | Paper |

### Round 4: Admissions, Feasibility & Risk (8 items)

| # | Claim to Verify | Verification Method | Source |
|---|----------------|-------------------|--------|
| 4.1 | Exam schedule — application dates, exam dates, result dates | Admission schedule page | Official page |
| 4.2 | Exam schedule year correctness (e.g., "Summer 2026" → verify it's 令和9年度) | Check Japanese academic year on schedule page | Official page |
| 4.3 | Enrollment term matching — can the applicant actually enroll in the claimed term? | Foreign applicant flowchart PDF | University PDF |
| 4.4 | Visa/COE timeline feasibility for the claimed enrollment term | FAQ document for foreign applicants | University PDF |
| 4.5 | RECRUITMENT STATUS — does professor have ○ on CBMS page? Does their own page say they recruit? | CBMS recruitment page HTML + professor's own page | Dual source |
| 4.6 | If no ○ on Schedule A, what alternative pathways exist? | Professor's page recruitment section | Professor page |
| 4.7 | Research proposal FEASIBILITY — architecture alignment, demand, scope | Cross-reference proposal with lab's actual tech stack + papers | Multi-source |
| 4.8 | Research proposal RISKS — what assumptions does the proposal make that might not hold? | Critical analysis of proposal assumptions | — |

### Round 4b: Email Style & Tone Verification (optional, does not count toward 40)

| # | Check |
|---|-------|
| 4b.1 | Word count (English: <400 words) |
| 4b.2 | No prohibited tone words ("passionate", "truly inspired", "strongly believe") |
| 4b.3 | No exaggerated authority claims ("designed", "led", "spearheaded") |
| 4b.4 | Correct attribution of group work vs. professor's own work |

---

### Fact-Check Report Format

Each verified claim must follow this format:

```markdown
### 声明 N：[简短描述]

> "[引用邮件原文中被核查的具体句子]"

| 项目 | 结果 |
|------|------|
| **判定** | ✅ 准确 / ⚠️ 有偏差 / 🔴 高风险 / 🔵 用户自述 |
| **证据** | [论文原文引用、页面原文引用、API 返回内容等具体证据] |
| **来源** | [一手来源超链接] |
| **修正建议** | [如有偏差，说明如何修正；无偏差则写 N/A] |
```

### Correction Protocol

- **✅ 准确**: No action needed
- **⚠️ 有偏差**: **Immediately edit the email text** in the md file to correct the factual error. Record the change in the report.
- **🔴 高风险**: Flag prominently with `⚠️` in the summary table. Strongly advise user to verify before sending. If the risk is about the wrong application pathway, rewrite the relevant email paragraph.
- **🔵 用户自述**: Note as unverifiable via web. Suggest user prepare supporting evidence if challenged.

---

### Post-Check Summary (REQUIRED)

After all four rounds, produce:

```markdown
## 核查总结论

| 轮次 | 核查声明数 | ✅ 准确 | ⚠️ 有偏差 | 🔴 高风险 | 🔵 用户自述 |
|------|-----------|---------|-----------|----------|-----------|
| 第一轮: 教授身份 | N | N | N | N | N |
| 第二轮: 论文内容 | N | N | N | N | N |
| 第三轮: 技术工具 | N | N | N | N | N |
| 第四轮: 入学可行性 | N | N | N | N | N |
| **合计** | **≥40** | N | N | N | N |

### 已修正的偏差

| # | 修正前 | 修正后 | 原因 |
|---|--------|--------|------|

### 仍需用户确认的风险

[列出所有 🔴 高风险项]

### 套瓷信总体可信度：[高/中/低]

[一句话说明判断依据]
```

---

## Strict Constraints

- **MANDATORY fact-checking**: Fact-checking runs AUTOMATICALLY after Phase 1. NEVER ask the user whether to proceed — just do it.
- **40+ items minimum**: Every fact-check must have at least 40 verified claims. If the email is short, go deeper into content verification (paper abstract analysis, cross-referencing, risk analysis) until 40 is reached.
- **Content-first verification**: The primary focus is on whether paper descriptions, research directions, and technical claims in the email match what the actual sources say. Surface-level URL/name checks are not enough.
- **Source-first**: Every verification must reference a specific, clickable URL. No "from the website" without a URL.
- **Dual-source for critical claims (1.1–1.6, 2.1–2.7, 4.5–4.6)**: Professor title, paper dates/titles/authors, email, and recruitment status require confirmation from 2+ independent sources.
- **Date precision**: Paper dates must be epub/publication date from PubMed or DOI metadata, NOT the news announcement date. Flag any discrepancy immediately.
- **Coverage**: No factual claim, technical noun, or proper name in the email may be skipped. Read the email word by word — every project name, method name, number, date, and institutional name must be checked.
- **Correct inline**: When a deviation is found, fix it in the email text AND record it in the report.
- **Never fabricate sources**: If a source cannot be found, mark as `[未确认]` and state exactly what was attempted and why it failed.
- **Respect user's style**: Corrections should match the user's existing email tone and structure. Don't rewrite the entire email — only fix factual errors.
