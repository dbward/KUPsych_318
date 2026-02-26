Overview
This is a course chatbot for Psychology 318 at the University of Kansas in Lawrence. 

Course Content
The chatbot's system prompt includes:

Full 8-module course schedule with all due dates (discussion board posts/replies, assignments, quizzes, and unit exams)
Course policies (late work, academic integrity, drop/withdraw deadlines, accessibility)
Content knowledge across all modules: attention, memory systems, language, problem solving, decision making, and more
Behavioral guardrails (no grade discussions, no assignment completion, Socratic-only for content questions)

Textbook: Juola & Koshino (2022), Cognitive Psychology (4th ed.), BVT Publishing

Development Notes
This app was built using the following workflow:

Claude.ai — used to build and iterate on the app with AI assistance
Anthropic Console (console.anthropic.com) — used to generate the API connector
Cloudflare (cloudflare.com) — Worker acts as a secure API proxy
GitHub (github.com) — hosts the app via GitHub Pages

The chatbot design is intentionally distinct from other course assistants in the same series (e.g., College Algebra). It uses a purple-to-teal color scheme referencing both mind (purple) and neuroscience (teal), with a Socratic badge in the header to signal its pedagogical approach to students.

Related Projects
This is part of a series of course-specific AI study assistants built for KU online courses using the same Cloudflare + GitHub Pages architecture.

Built Spring 2026 | University of Kansas
