---
name: jp-university-admission-notion
description: Automate the rigorous extraction of critical admission information from Japanese university application guidelines (募集要项) and archive the structured data to Notion. Triggered when a user provides a PDF, text, or URL of Japanese university admission guidelines and requests information extraction, summary, or Notion archiving. Also triggered by keywords like "募集要项", "出愿", "招生简章".
---

# Japanese University Admission Guidelines Extractor & Notion Archiver

This skill performs rigorous, zero-hallucination extraction of admission requirements from Japanese university application guidelines (募集要项) and automatically archives the structured data into Notion as a standalone page (or optionally into a database if the user provides one).

## Prerequisites

- **Notion MCP** must be available for archiving results.
- **Browser** or **File Reading** tools must be available to process the provided guidelines.

## Initialization

When triggered, immediately reply to the user with exactly this message:
"我已经准备好为您解读募集要项并写入Notion。请发送您的PDF文件、文本或网页链接，我将立即开始严谨的审查工作。"

Wait for the user to provide the document/URL before proceeding.

## Input Handling

The user may provide guidelines in various formats:

- **PDF file**: Read the full text. Japanese PDFs may contain vertical text or scanned images; if text extraction fails or is garbled, inform the user and suggest providing a URL or text version instead.
- **URL**: Navigate to the page and extract content. Some universities host guidelines as embedded PDFs on their website; download and read the PDF if so.
- **Pasted text**: Process directly.

**Multi-program documents**: Some universities publish a single guideline covering multiple departments (研究科) or programs. If the document covers multiple programs, ask the user which specific program they are targeting before extraction. Extract only the relevant program's information to avoid confusion.

## Workflow

Execute Steps 1-3 strictly in order for each provided guideline document.

### Step 1: Information Extraction (Strict Classification)

Read the provided document thoroughly. Extract information strictly according to the following priorities.

**Critical Rules (Zero Hallucination & Sourcing):**
1. All extracted information MUST come 100% from the provided text. NEVER guess or fill in blanks using general knowledge.
2. If a key piece of information is missing, explicitly mark it: `⚠️ 文件中未明确提及，需查阅官网或联系教务处`.
3. Extract exact dates and clearly distinguish between: Application Period (出愿期间), Exam Date (考学日), Result Announcement (合格发表日), and Enrollment Procedure Deadline (入学手续日).
4. Strictly differentiate and highlight whether document submission requires a postmark by the deadline (`消印有効`) or must arrive by the deadline (`必着`). This distinction is critical and frequently causes applicants to miss deadlines.
5. For language scores, clearly note whether the requirement is a minimum threshold or a recommendation, and whether the score must be submitted before application or can be supplemented later.

**Extraction Categories:**

*   **Priority 1: Critical Requirements (Core Thresholds)**
    *   **Eligibility (出愿资格):** Specific requirements for education level, age, and residence status. Note if 16-year education is required or if a pre-screening (事前资格审查) can waive this.
    *   **Language Requirements:**
        *   Japanese: EJU subjects/scores or JLPT level. Note score validity periods.
        *   English: TOEFL/TOEIC/IELTS acceptance, minimum scores, submission method (Official Score Report vs. copy), and validity period (usually within 2 years).
    *   **Preliminary Screening (事前审查):** Is an eligibility pre-screening required? If yes, extract the deadline and required materials.
*   **Priority 2: Exam Content & Core Materials (Important)**
    *   **Selection Method (选考方式):** Document screening, written exam (e.g., specialized subjects, short essay), interview. Note if the interview is online or in-person.
    *   **Core Material Checklist:**
        *   Originals required (e.g., graduation certificate, transcript).
        *   Professor signature required (e.g., recommendation letter, statement of purpose).
        *   Special requirements (e.g., translation/notarization, prior contact with supervisor for "内诺", research plan format/page limit).
    *   **Application Fee (検定料):** Amount, payment method (credit card/convenience store/overseas transfer), and payment deadline.
*   **Priority 3: Admission & Enrollment Info (General)**
    *   **Quota (募集人数):** Specific admission capacity for the department/school.
    *   **Tuition & Scholarships:** First-year fees (admission fee + tuition), availability of tuition reduction for international students.
    *   **Campus Location:** Exam location and enrollment campus.

### Step 2: Timeline Generation

Create a clear chronological timeline of all date-related events.

**Format:**
`[YYYY-MM-DD] 至 [YYYY-MM-DD]` - `[事件名称]` - `[详细说明：如网页登录截止、材料必着截止等]`

Mark deadlines that are particularly easy to miss (e.g., early pre-screening deadlines, score report mailing lead time) with a `⚠️` prefix.

### Step 3: Action (Notion Archiving)

First, present the extracted information (Step 1) and timeline (Step 2) to the user for confirmation.
Once the user confirms, use the Notion MCP to archive the data.

**Default behavior:** Create a standalone workspace-level Notion page (no database required). Only use a database if the user explicitly provides a `database_id` or `data_source_id`.

See `references/notion-archiving.md` for the exact page content structure and Notion MCP usage instructions.

## Strict Constraints

- **Zero hallucination**: Every date, score requirement, fee amount, and procedural detail must come directly from the provided document. Never infer or assume.
- **Source marking**: If information cannot be found in the document, mark it explicitly rather than omitting it silently.
- **Deadline precision**: Always specify whether a deadline is `消印有効` (postmark) or `必着` (arrival). Getting this wrong can cause an applicant to miss their application window.
- **No paraphrasing of requirements**: For eligibility conditions and material requirements, preserve the original wording as closely as possible to avoid misinterpretation.
