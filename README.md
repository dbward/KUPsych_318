# PSYC 318 – Cognitive Psychology Study Assistant
**University of Kansas | Spring 2026**

A Socratic tutoring chatbot for PSYC 318 (Cognitive Psychology), built to help students think through course concepts, find due dates, and get feedback on drafts — without doing their work for them.

---

## What It Does

- **Socratic tutoring** — guides students to answers through questioning rather than providing direct answers
- **Course logistics** — answers questions about due dates, assignments, policies, and the course schedule
- **Draft feedback** — students can upload a draft and receive guided questions to improve their thinking
- **Practice quizzes** — generates practice questions on course topics on request
- **Grade guardrail** — politely declines all grade-related questions and redirects to the instructor

---

## Tech Stack

| Layer | Tool | Purpose |
|---|---|---|
| Frontend | HTML/CSS/JavaScript | Single-file app (`index.html`) |
| AI | Anthropic Claude API | Powers the chatbot responses |
| API Proxy | Cloudflare Workers | Keeps the API key secret; handles CORS |
| Hosting | GitHub Pages | Serves the static HTML file |
| LMS Embed | Canvas iframe | Embedded in the course as a tool |

---

## How It Works

```
Student's browser
      ↓
GitHub Pages (index.html)
      ↓
Cloudflare Worker (dbward2119.workers.dev)
      ↓
Anthropic API (Claude)
      ↓
Response back to student
```

The Cloudflare Worker acts as a middleman so the Anthropic API key is never exposed in the browser. The Worker injects the key server-side before forwarding the request to Anthropic.

---

## Project Structure

```
/
├── index.html       # The entire app (HTML + CSS + JavaScript)
└── README.md        # This file
```

---

## Course Content

The chatbot's system prompt includes:
- Full 8-module course schedule with all due dates (discussion board posts/replies, assignments, quizzes, and unit exams)
- Course policies (late work, academic integrity, drop/withdraw deadlines, accessibility)
- Detailed content knowledge across all 10 chapters (see below)
- Behavioral guardrails (no grade discussions, no assignment completion, Socratic-only for content questions)

**Textbook:** *Cognitive Foundations v1.1* — Aggregated Open Textbook (Pilegard, 2019), free PDF on Canvas

### Content Coverage (Chapters 1–10)

| Chapter | Topic |
|---|---|
| 1 | History & Research Methods |
| 2 | Perception |
| 3 | Attention |
| 4 | Short-Term & Working Memory |
| 5 | Long-Term Memory |
| 6 | Memory in Context |
| 7 | Knowledge |
| 8 | Language |
| 9 | Problem Solving |
| 10 | Reasoning & Decision Making |

---

## Changelog

### February 2026 — Textbook Content Overhaul

**Textbook source updated** from Juola & Koshino (2022) to *Cognitive Foundations v1.1* (Pilegard, 2019) to match the actual course reading.

**System prompt significantly expanded.** The previous version contained brief bullet-point summaries. The updated prompt incorporates verbatim excerpts and detailed summaries drawn directly from the textbook, including:

- Specific study procedures, statistics, and findings (e.g., Mueller & Oppenheimer (2014) note-taking study; Roediger & Karpicke (2006) testing effect: 61% vs. 40% recall; Wason selection task: 4% vs. 73% accuracy with abstract vs. social content)
- Content that was previously missing, including: Wundt's introspection method; the full Baddeley working memory model including the episodic buffer; all four conditional syllogism forms with accuracy rates; cryptomnesia and the sleeper effect; the Braun et al. (2002) Bugs Bunny false memory study; Kanzi and Washoe animal language research; and the permission schema and evolutionary accounts of the Wason selection task
- Correctly spelled researcher names throughout (Koffka, Shiffrin, Stoffregen, Saffran, Schvaneveldt, Deffenbacher, etc.)

**Textbook text cleanup.** The plain-text source files were converted from RTF using Microsoft Word, which introduced two systematic error types that were corrected programmatically before being used to update the prompt:

1. **Ligature substitutions** — typographic ligatures (ff, fi, fl, ffi, ffl) rendered as `?`, corrupting ~540 words across all three files (e.g., `different` → `di?erent`, `effect` → `e?ect`, `Shiffrin` → `Shi?rin`)
2. **Encoding errors** — ~440 instances of smart quotes, apostrophes, and dashes rendered as UTF-8 replacement characters (`ï¿½`)

Additional corrections included spaced-out headers from PDF rendering (`C H A P T E R 1`), broken compound words (`hareAlike`, `penStax`, `arperCollins`), and missing characters in researcher names.

---

## Development Notes

This app was built using the following workflow:
- **Claude.ai** — used to build, iterate on, and update the app with AI assistance
- **Anthropic Console** (console.anthropic.com) — used to generate the API connector
- **Cloudflare** (cloudflare.com) — Worker acts as a secure API proxy
- **GitHub** (github.com) — hosts the app via GitHub Pages

The chatbot design is intentionally distinct from other course assistants in the same series (e.g., College Algebra). It uses a purple-to-teal color scheme referencing both mind (purple) and neuroscience (teal), with a Socratic badge in the header to signal its pedagogical approach to students.

---

## Related Projects

This is part of a series of course-specific AI study assistants built for KU online courses using the same Cloudflare + GitHub Pages architecture.

---

*Built Spring 2024 | Updated February 2026 | University of Kansas*
