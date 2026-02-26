# PSYC 318 – Cognitive Psychology Study Assistant
**University of Kansas | Spring 2026**

A Socratic tutoring chatbot for PSYC 318 (Cognitive Psychology), built to help students think through course concepts, find due dates, and get feedback on drafts without doing their work for them.

---

## What It Does

- **Socratic tutoring.** Guides students to answers through questioning rather than providing direct answers
- **Course logistics.** Answers questions about due dates, assignments, policies, and the course schedule
- **Draft feedback.** Students can upload a draft and receive guided questions to improve their thinking
- **Practice quizzes.** Generates practice questions on course topics on request
- **Grade guardrail.** Politely declines all grade-related questions and redirects to the instructor

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

## Setup & Deployment

### Prerequisites
- GitHub account with Pages enabled on this repo
- Cloudflare account with a Worker configured
- Anthropic API key (from console.anthropic.com)

### Cloudflare Worker Configuration
The Worker script forwards requests from the app to the Anthropic API. It must:
1. Accept `POST` requests and handle `OPTIONS` (CORS preflight)
2. Read the request body and forward it to `https://api.anthropic.com/v1/messages`
3. Inject the `x-api-key` header using a stored environment variable
4. Return the Anthropic response with `Access-Control-Allow-Origin: *`

The API key is stored as an environment variable in Cloudflare:
- **Variable name:** `ANTHROPIC_API_KEY`
- Set via: Cloudflare Dashboard → Workers & Pages → [worker name] → Settings → Variables

### GitHub Pages
- Pages is enabled on the `main` branch, root directory
- The app is served at: `https://dbward.github.io/KUPsych_318/`

### Canvas Embed
The app can be embedded in a Canvas page using an iframe:
```html
<iframe 
  src="https://dbward.github.io/KUPsych_318/" 
  width="100%" 
  height="700px" 
  frameborder="0">
</iframe>
```

---

## Course Content

The chatbot's system prompt includes:
- Full 8-module course schedule with all due dates (discussion board posts/replies, assignments, quizzes, and unit exams)
- Course policies (late work, academic integrity, drop/withdraw deadlines, accessibility)
- Content knowledge across all modules: attention, memory systems, language, problem solving, decision making, and more
- Behavioral guardrails (no grade discussions, no assignment completion, Socratic-only for content questions)

**Textbook:** Juola & Koshino (2022), *Cognitive Psychology* (4th ed.), BVT Publishing

---

## Development Notes

This app was built using the following workflow:
- **Claude.ai** — used to build and iterate on the app with AI assistance
- **Anthropic Console** (console.anthropic.com) — used to generate the API connector
- **Cloudflare** (cloudflare.com) — Worker acts as a secure API proxy
- **GitHub** (github.com) — hosts the app via GitHub Pages

The chatbot design is intentionally distinct from other course assistants in the same series (e.g., College Algebra). It uses a purple-to-teal color scheme referencing both mind (purple) and neuroscience (teal), with a Socratic badge in the header to signal its pedagogical approach to students.

---

## Related Projects

This is part of a series of course-specific AI study assistants built for KU online courses using the same Cloudflare + GitHub Pages architecture.

---

*Built Spring 2024 | University of Kansas*
