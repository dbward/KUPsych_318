# PSYC 318 Study Assistant

A course-specific AI study assistant for **PSYC 318 — Cognitive Psychology** at the University of Kansas. Built for Dr. Susan Marshall's Fall 2026 section by Doug Ward at the KU Center for Teaching Excellence.

Live at: `https://dbward.github.io/KUPsych_318/`

> **Status:** Experimental. Not an official KU tool; not reviewed by KU IT. Use is optional for students. Data handling is described under [Privacy](#privacy-and-data-handling) below.

## What it does

The assistant answers student questions about:

- Course logistics — due dates, policies, office hours, contact info
- Cognitive psychology concepts — definitions, explanations, guided reasoning
- Practice quizzes on course topics
- Study notes and study guides students are building for themselves

It **does not** help with graded work — Assignments, Peer Reviews & Reflections, Afterthoughts posts and comments, Contribution activities, or exams. This aligns with the course AI use policy in the syllabus, which permits generative AI for practice questions, note summarization, and study guides, but not for graded submissions.

## Architecture

Two parts, deployed independently:

**Frontend (this repo).** `index.html` is a single self-contained HTML file served by GitHub Pages. It handles the UI, the privacy modal, chat state, and calling the backend. No API keys, no course content, no secrets.

**Backend (Cloudflare Worker).** 
The worker code is maintained directly in the Cloudflare dashboard rather than committed here.

## Files in this repo

| File | Purpose |
|---|---|
| `index.html` | Frontend served by GitHub Pages |
| `README.md` | This file |

## Privacy and data handling

- **Anthropic** processes each message. Per API terms, inputs and outputs are retained for 30 days for abuse monitoring and are not used to train models.
- **Cloudflare** logs a truncated, salted SHA-256 hash of each user's IP along with request counts and timestamps. Raw IPs are never stored. **Message content is not logged.**
- **Browser localStorage** stores only the fact that a student accepted the privacy notice. Nothing else persists client-side.
- **Admin dashboard** at `/admin` is protected by HTTP Basic Auth backed by a Cloudflare secret.

Students see the privacy notice on first use and can re-read it via the "Privacy notice" link in the footer.

## Course policy alignment

The behavioral rules embedded in the worker mirror the syllabus AI policy:

- **Permitted:** practice questions, self-created study notes, concept exploration, factual course questions
- **Not permitted:** draft feedback on graded work, writing any portion of graded work, grade prediction

If the syllabus policy changes in a future term, update the `BEHAVIORAL_RULES` and `SYLLABUS` constants together so the bot's behavior and the reference document remain consistent.

## Known issues

**Textbook mismatch.** PSYC 318 requires Juola & Koshino (2022), *Cognitive Psychology* (4th ed.). The assistant draws on an open-access textbook (*Cognitive Foundations*) that covers the same subject matter but has different chapter numbering and wording. The behavioral rules instruct the bot to focus on concepts and note the mismatch when chapter numbers come up, but literal "what's in Chapter 7?" queries may return content that doesn't match the required text. A permanent fix would require either licensing rights to embed Juola & Koshino or rewriting the schedule and system prompt to reference the open textbook's numbering directly.

## Contact

Doug Ward — dbward@ku.edu — KU Center for Teaching Excellence
---
Site link: https://dbward.github.io/KUPsych_318/

*Built February 2026 | University of Kansas* / Updated August 2026
