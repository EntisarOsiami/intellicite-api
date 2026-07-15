# IntelliCite API

Backend for **IntelliCite**, an AI-assisted research companion that helps students and researchers search academic literature, judge which papers are actually worth reading, and generate citations — without manually screening dozens of results.

The frontend lives in a companion repo: [intellicite-ui](https://github.com/intisar-alosaimi/intellicite-ui).

## The problem

Academic search engines return a pile of papers with no easy way to judge relevance, credibility, or citation quality without reading each one. IntelliCite lets a user search by topic and get back an AI-generated report explaining *why* each paper matches their query, plus automatic quality badges ("highly cited", "recent", "outdated"). A separate "Cite Check" tool takes a paper's DOI and a research question and tells the user whether that source is actually a good fit — or suggests it isn't.

## Features

- Search academic papers by topic (Semantic Scholar + Unpaywall integration)
- AI-generated relevance reports per paper via an OpenAI Assistant
- Automatic quality badges based on citation metrics (citation count, publication age)
- **Cite Check** — given a DOI and a research question, evaluates whether that source fits and suggests better alternatives if it doesn't
- Save papers, generate citations in multiple formats (APA, MLA, etc.), and track search history
- JWT-based authentication, with a separate admin surface for managing users/content

## Tech stack

| | |
|---|---|
| Runtime | Node.js, TypeScript |
| Framework | Express 5 |
| Database | MongoDB + Mongoose |
| Auth | JWT (`jsonwebtoken`), `bcryptjs` |
| AI | OpenAI (Assistants API) |
| External data | Semantic Scholar API, Unpaywall API |
| Hardening | Helmet, CORS |

## API reference

| Route | Method | Description |
|---|---|---|
| `/api/users` | various | Registration, login, user management |
| `/api/papers/search` | GET | Search academic papers by topic (auth required) |
| `/api/papers/citeCheck` | POST | Evaluate a paper's fit for a research question by DOI (auth required) |
| `/api/bookmarks` | various | Save and manage bookmarked papers |
| `/api/user-history` | various | Track a user's search history |
| `/api/admin` | various | Admin-only user/content management |

## Getting started

```bash
git clone https://github.com/intisar-alosaimi/intellicite-api.git
cd intellicite-api
npm install
cp .env.example .env   # then fill in real values, see below
npm run dev
```

## Environment variables

| Variable | Purpose |
|---|---|
| `PORT` | Port the server listens on |
| `MONGODB_URI` | MongoDB Atlas connection string |
| `DB_NAME` | Database name |
| `JWT_SECRET` | Secret used to sign auth tokens |
| `OPENAI_API_KEY` | OpenAI API key |
| `RESEARCH_ASSISTANT_ID` | ID of an OpenAI Assistant configured for this project (create one in the OpenAI dashboard) |
| `USER_EMAIL` | Contact email sent with Unpaywall API requests (Unpaywall requires this for identification, no account needed) |

## What I'd improve

- Add a test suite — there currently isn't one
- Add input validation (e.g. `zod`) on request bodies instead of trusting client input
- Add rate limiting on public-facing search/cite-check endpoints
- Generate real API docs (Swagger/OpenAPI) instead of a hand-maintained table
- Containerize with Docker so redeploys aren't tied to remembering manual setup steps
- Keep this endpoint table in sync with `app.ts` going forward (e.g. cite-check is nested under `/api/papers`, and the `/api/admin` surface needs documenting too)

## Design

Figma: [Final Tuwaiq Project](https://www.figma.com/design/AOBplsedeefft6SPW3KOt5/Final-Tuwaiq-Project)

## Team

Originally built by:

- **[عبدالرحمن الطامي](https://github.com/Iimvalue)**
- **[عائشة عبدالله](https://github.com/ENG-Aisha-Abdullah)**
- **[انتصار العصيمي](https://github.com/intisar-alosaimi)**
- **[طلال المطيري](https://github.com/TalalAlrashedi)**
