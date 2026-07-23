# AI-901 Practice Questions

A free, no-account practice quiz for the **Microsoft AI-901 (Azure AI Fundamentals)** exam.

**112 original questions** across 7 topics, each with a full explanation of why the correct
answer is right *and* why each distractor is wrong.

## Features

- **Pick your topics** — drill any combination of the seven areas
- **Progress saved locally** — uses `localStorage`, so there are no accounts, no sign-in, no server
- **Retry what you got wrong** — a dedicated mode pools only your previously-incorrect questions;
  a question leaves the list once you answer it correctly
- **"Not yet attempted" mode** — work through questions you haven't seen
- **Per-topic results** — sorted weakest-first, so you know where to revise
- Exam-style formats: multiple choice, multi-select, dropdown, and true/false

## Topics

| Topic | Questions |
|---|---|
| Foundry & Endpoints | 34 |
| Code & endpoints (advanced) | 16 |
| Concepts & Responsible AI (hard) | 16 |
| Python SDK | 14 |
| Concepts & Responsible AI | 12 |
| Foundry Hub architecture | 12 |
| Foundry Tools (services) | 8 |

## Running it

It's a plain static site — no build step, no dependencies, no framework.

**Locally:** open `index.html` in any browser. That's it; it works offline.

**Deploy to Vercel:** go to [vercel.com/new](https://vercel.com/new), import this repository,
and click Deploy. Vercel detects it as a static site and needs no configuration.

## Files

```
index.html      markup and script tags
styles.css      styling
questions.js    the question bank
app.js          quiz logic, progress, scoring
```

## A note on the questions

These are **original** questions written from the published AI-901 skills outline — they are not
real exam questions, which are covered by an NDA. They're deliberately written to be harder than
the real thing, with plausible distractors rather than obvious throwaways.

Answer positions and option lengths were balanced programmatically, so the correct answer is
neither consistently the longest option nor clustered on one letter.

Azure and Foundry change quickly. If a detail surprises you, verify it against
[Microsoft Learn](https://learn.microsoft.com/) — and do the
[official free practice assessment](https://learn.microsoft.com/credentials/certifications/azure-ai-fundamentals/),
which is the closest match to the real exam.

## Licence

MIT — use it, fork it, add your own questions.
