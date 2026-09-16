# Microsoft Fundamentals Practice — AI-901 · SC-900 · AB-900

A free, no-account practice quiz for three Microsoft Fundamentals exams, each on its own tab:

| Tab | Exam | Questions |
|---|---|---|
| **AI-901** | Azure AI Fundamentals | 112 |
| **SC-900** | Security, Compliance, and Identity Fundamentals (skills measured July 28, 2026) | 129 |
| **AB-900** | Microsoft 365 Copilot and Agent Administration Fundamentals (skills measured July 22, 2026) | 126 |

Every question is original, scenario-based, and comes with a full explanation of why the correct
answer is right *and* why each distractor is wrong. Distractors are deliberately plausible: the
wrong options are real products, real features or real-sounding rules, so you have to know the
difference, not just recognise a name.

## Features

- **Three exams, three tabs** — switch with the tabs at the top or link straight to one with
  `#ai901`, `#sc900` or `#ab900`
- **Pick your topics** — drill any combination of the areas of an exam
- **Progress saved locally** — uses `localStorage` with one save per exam, so there are no
  accounts, no sign-in, no server
- **Retry what you got wrong** — a dedicated mode pools only your previously-incorrect questions;
  a question leaves the list once you answer it correctly
- **"Not yet attempted" mode** — work through questions you haven't seen
- **Per-topic results** — sorted weakest-first, so you know where to revise
- Exam-style formats: multiple choice, multi-select, sentence completion (dropdown), and true/false
  (the real exams' Yes/No statement items)

## Cram sheets

Two night-before revision documents live in `docs/`, one per new exam, written from the same
research as the question banks: every domain of the outline, comparison tables, the numbers, a
"if the question says… pick…" mapping table, a rename table, and a last-30-minutes checklist.

- [`docs/SC-900-cram.md`](docs/SC-900-cram.md)
- [`docs/AB-900-cram.md`](docs/AB-900-cram.md)

## Topics

### SC-900

| Topic | Questions |
|---|---|
| Security & identity concepts | 16 |
| Entra — identities & authentication | 18 |
| Entra — access, protection & governance | 18 |
| Azure security & Defender for Cloud | 14 |
| Sentinel & Security Copilot | 10 |
| Microsoft Defender XDR | 16 |
| Purview — compliance, privacy & Priva | 10 |
| Purview — information protection & lifecycle | 15 |
| Purview — insider risk, eDiscovery & audit | 12 |

Weighted to match the exam: concepts 10–15%, Entra 25–30%, security solutions 35–40%,
compliance solutions 20–25%. Covers the newer outline items too: agent identities (Entra Agent ID),
Global Secure Access, Verified ID, Security Copilot, the unified SecOps platform, Exposure Management,
unified eDiscovery, Audit Standard vs Premium, Priva.

### AB-900

| Topic | Questions |
|---|---|
| M365 core objects & admin centers | 17 |
| Security principles & Defender XDR | 10 |
| Entra ID & core security features | 17 |
| Purview capabilities | 16 |
| Copilot data security & responsible AI | 10 |
| Purview risk & discovery tools | 13 |
| SharePoint oversharing & SAM | 8 |
| Copilot & agents — features & licensing | 15 |
| Copilot & agent admin tasks | 20 |

Weighted to match the exam: core Microsoft 365 services 30–35%, data protection and governance
35–40%, Copilot and agent administration 25–30%. Includes the traps that catch people: restricted
access control vs restricted content discovery, Block vs Remove, pay-as-you-go budgets that only
notify, no 300-seat minimum, E5 vs E7, Data explorer vs Content explorer, Content search inside
eDiscovery, Researcher and Analyst sitting outside agent settings, AI Administrator as the approval
role, the retired compliance portal.

### AI-901

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
index.html            markup and script tags
styles.css            styling (including the exam tabs)
questions.js          AI-901 question bank
sc900-questions.js    SC-900 question bank
ab900-questions.js    AB-900 question bank
app.js                quiz logic, exam tabs, progress, scoring
docs/SC-900-cram.md   SC-900 cram sheet
docs/AB-900-cram.md   AB-900 cram sheet
```

Each bank is a plain array of `{ id, topic, tag, q, options, answer, why, format }` objects, so
adding a question is a copy-and-edit job.

## A note on the questions

These are **original** questions written from the published skills outlines — they are not real
exam questions, which are covered by an NDA. They're deliberately written to be at least as hard as
the real thing, with plausible distractors rather than obvious throwaways, and the explanations call
out the specific trap each item is built around.

Option order is shuffled at run time and option lengths were balanced programmatically, so the
correct answer is neither consistently the longest option nor clustered on one letter.

Microsoft renames and reshuffles products constantly (Purview portal, Data explorer, unified
eDiscovery, Copilot Credits, E7…). The SC-900 and AB-900 banks reflect the July 2026 skills outlines
and product state as of September 2026. If a detail surprises you, verify it against
[Microsoft Learn](https://learn.microsoft.com/) — and do the official free practice assessments
for [SC-900](https://learn.microsoft.com/credentials/certifications/security-compliance-and-identity-fundamentals/)
and [AB-900](https://learn.microsoft.com/credentials/certifications/copilot-and-agent-administration-fundamentals/),
which are the closest match to the real exams.

## Licence

MIT — use it, fork it, add your own questions.
