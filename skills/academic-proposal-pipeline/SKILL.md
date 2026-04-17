---
name: academic-proposal-pipeline
description: Generate a tailored graduate research proposal for Japanese university admission. Research professor webpages, infer the professor's active trajectory, propose one feasible topic aligned with the applicant's strengths, collect supporting literature, build an outline, and write a complete proposal in English or Chinese. Triggered when the user wants a research proposal for a specific professor or a Japanese graduate school application.
---

# Academic Proposal Pipeline

Generate a complete research-proposal workflow for Japanese graduate admission. Use this skill when the user wants a **research proposal**, not a cold email.

## Prerequisites

- **Browser** must be available for deep traversal of professor or lab webpages.
- The user should provide at least one professor homepage URL.
- The user may optionally provide PDFs, notes, abstracts, or an existing topic idea.

## Applicant Profile

Before starting, confirm the user has provided the following information. Ask only for missing items.

1. **Applicant Background**: name, school/major/grade, or current status.
2. **Strengths/Highlights**: skills, projects, publications, methods, datasets, internships, or domain experience.
3. **Professor Information**: one or more professor homepage URLs.
4. **Proposal Requirements**:
   - academic domain
   - output language (**English** or **中文**)
   - target word count (default: ~3,000 words)
5. **Optional Materials**: PDFs, paper lists, literature notes, or topic preferences.

If multiple professor URLs are provided in one session, reuse the same applicant profile unless the user updates it.

## Workflow

Execute the following steps in order. Do not skip confirmation steps unless the user explicitly asks you to proceed without them.

### Step 1: Deep Web Intelligence Extraction

Open the professor's homepage URL in browser. **Actively click into relevant sub-pages**, including Research, Publications, Profile, Projects, Members, News, Prospective Students, Contact, and similar pages.

**Language handling:** Many Japanese professor pages are primarily in Japanese. Recognize common labels such as:
- 研究内容 / 研究紹介 = Research
- 業績 / 発表論文 = Publications
- メンバー = Members
- 受験生へ / 入学希望の方へ = For Prospective Students
- 連絡先 = Contact

**Red-line check:**
1. Look for explicit statements that the professor is **not accepting students**.
2. If such a statement is found, stop and inform the user immediately.
3. Do not continue proposal generation unless the user still wants a speculative draft despite the admission warning.

**Extract and record:**
- the professor's current active research directions
- at least 2 representative recent papers with **title, venue, year**
- methods, datasets, application areas, grants, collaborations, or projects if visible
- the exact source URL where each key finding was found

Never fabricate papers, source URLs, or research directions.

### Step 2: Topic Generation

Cross-match the professor's recent research trajectory with the applicant's background. Produce **exactly 1 concrete, feasible research direction** that:
- aligns with the professor's recent active work
- uses the applicant's real strengths
- is narrow enough for a master's or early-stage doctoral application
- contains a plausible research gap and method path

Present the proposed topic to the user and get approval before continuing.

### Step 3: Literature Collection

After the topic is approved, gather literature for four buckets:
- **Background**
- **Current State**
- **Research Gap**
- **Methodology**

Prioritize recent review articles, foundational papers, and high-quality recent studies. Incorporate user-provided PDFs or paper lists when available. Build a usable evidence base before outlining.

### Step 4: Outline Generation

Read `references/STRUCTURE_GUIDE.md`.

Create a structured outline tailored to the approved topic and academic domain. The standard proposal structure usually includes:
- Title
- Abstract
- Introduction
- Literature Review
- Research Questions / Objectives
- Methodology
- Timeline
- Expected Contributions / Significance
- References

Present the outline to the user and wait for confirmation before drafting the full proposal.

### Step 5: Proposal Writing

Read `references/WRITING_STYLE_GUIDE.md`.

Write the full proposal in Markdown.

**Requirements:**
- Use **prose-first academic writing**. Avoid bullet-heavy drafting.
- Integrate literature into the argument instead of making generic claims.
- Explicitly connect the applicant's strengths to feasibility.
- Include **3-5 figure suggestions** at appropriate locations using the format:
  `> **[Figure X Suggestion]** *Title: ...* Content: ...`
- For PhD-level proposals, aim for **at least 40 references** unless the user requests otherwise.

### Step 6: Quality Check

Read `references/QUALITY_CHECKLIST.md`.

Review the proposal before delivery. Check structure, logical coherence, alignment with the professor, literature coverage, citation consistency, and language consistency. Fix issues before delivering the final Markdown file.

## Strict Constraints

- **No fabrication**: Do not invent papers, labs, source URLs, methods, datasets, or citations.
- **Trajectory matching**: Do not build the proposal around outdated work if the professor's recent work points elsewhere.
- **Confirmation gates**: Require user approval after topic generation and after outline generation.
- **Language consistency**: Keep the final proposal fully in the requested language, except original-language paper titles in references.
- **Deliverable discipline**: Deliver a clean Markdown proposal file suitable for later editing or export.
