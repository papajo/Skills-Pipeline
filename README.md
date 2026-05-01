# 🗂️ Universal Portfolio + Blog — Project Skill Pipeline

> A set of 13 AI agent skills that guide you from raw idea to production-ready release.  
> Each skill is a JSON instruction file you load into your AI coding assistant (Claude Code, Cursor, Windsurf, etc.) to run a specific phase of your project lifecycle.

---

## What Is a Skill?

A **skill** is a structured JSON file that acts as a precision prompt for your AI assistant. Instead of typing freeform instructions and hoping the AI stays on track, you load a skill and it:

- Knows **exactly what phase** of the project it's responsible for
- Knows what its **prerequisites** are (so it won't skip steps)
- Has **guardrails** that prevent common mistakes
- Produces **specific outputs** that feed the next skill in the pipeline

Think of it as a pre-written playbook that turns your AI into a disciplined senior engineer for that one phase of work.

---

## The 13-Skill Pipeline

```
 PHASE 1  ┌─────────────────────────────┐
          │  01 · Clarify Requirements  │  ← Start here. Every time.
          └──────────────┬──────────────┘
                         │
 PHASE 2  ┌──────────────▼──────────────┐
          │  02 · Domain Decomposition  │  ← Break it into bounded domains
          └──────────────┬──────────────┘
                         │
 PHASE 3  ┌──────────────▼──────────────┐
          │  03 · Architecture Proposal │  ← Stack, structure, key decisions
          └──────────────┬──────────────┘
                         │
 PHASE 4  ┌──────────────▼──────────────┐
          │  04 · Threat Modeling       │  ← Security before a line of code
          └──────────────┬──────────────┘
                         │
 PHASE 5  ┌──────────────▼──────────────┐
          │  05 · ADR Generation        │  ← Capture every major decision
          └──────────────┬──────────────┘
                         │
 PHASE 6  ┌──────────────▼──────────────┐
          │  06 · API Design            │  ← Routes, schemas, data contracts
          └──────────────┬──────────────┘
                         │
 PHASE 7  ┌──────────────▼──────────────┐
          │  07 · Code Scaffolding      │  ← Generate the file/folder skeleton
          └──────────────┬──────────────┘
                         │
 PHASE 8  ┌──────────────▼──────────────┐
          │  08 · Refactoring           │  ← Improve without breaking
          └──────────────┬──────────────┘
                         │
 PHASE 9  ┌──────────────▼──────────────┐
          │  09 · Test Generation       │  ← Unit, integration, E2E
          └──────────────┬──────────────┘
                         │
 PHASE 10 ┌──────────────▼──────────────┐
          │  10 · PR Review             │  ← Pre-merge checklist + critique
          └──────────────┬──────────────┘
                         │
 PHASE 11 ┌──────────────▼──────────────┐
          │  11 · Documentation         │  ← Inline docs + guides + README
          └──────────────┬──────────────┘
                         │
 PHASE 12 ┌──────────────▼──────────────┐
          │  12 · Project Snapshot      │  ← State-of-the-world summary
          └──────────────┬──────────────┘
                         │
 PHASE 13 ┌──────────────▼──────────────┐
          │  13 · Release Notes         │  ← Human-readable changelog
          └─────────────────────────────┘
```

---

## Quick Start

### Step 1 — Pick your AI tool

These skills work with any AI assistant that accepts file-based context:

| Tool | How to load a skill |
|---|---|
| **Claude Code** | `claude --file 01-clarify-requirements.json` or paste into the chat |
| **Cursor** | Add to `.cursor/rules/` or reference via `@file` |
| **Windsurf** | Drop into `.windsurf/skills/` and reference with `@skill` |
| **ChatGPT / any chat AI** | Open the JSON, copy the contents, paste as your first message |
| **Custom agent** | Read the JSON, use `instructions` array as your system prompt |

### Step 2 — Always start with Skill 01

```
Load: 01-clarify-requirements.json
Say:  "Run /clarify-requirements"
```

The skill will interview you section by section. **Do not skip this.** Every downstream skill uses the outputs from this phase.

### Step 3 — Follow the chain

Each skill tells you what its prerequisite is. Don't run Skill 04 (Threat Modeling) before Skill 03 (Architecture Proposal) is confirmed. The pipeline is sequential by design.

### Step 4 — Confirm before proceeding

Every skill ends with an `instructions` block that says: *"Confirm with the user before proceeding."* Take that seriously. The skill is asking you to review, push back, and make decisions — not just rubber-stamp AI output.

---

## Skill-by-Skill Reference

---

### `01-clarify-requirements.json`
**Trigger:** `/clarify-requirements`  
**Time:** 20–40 min  
**What it does:** Runs a structured 7-section interview covering persona scope, portfolio domain, blog domain, identity/customisation, navigation, integrations, and deployment constraints.  
**You get:** `docs/requirements/requirements-summary.md` — the spec document all other skills refer back to.  
**Guardrail:** The AI will not make architecture decisions during this phase. If it starts talking about Next.js configs, redirect it.

---

### `02-domain-decomposition.json`
**Trigger:** `/domain-decomposition`  
**Prerequisite:** Skill 01 complete  
**Time:** 15–25 min  
**What it does:** Breaks the project into 7 bounded domains: Identity, Portfolio, Blog, Theme & Customisation, Navigation, SEO & Meta, Integrations. Each domain gets its own data model and interface contract.  
**You get:** `docs/architecture/domain-map.md` — the map that prevents spaghetti architecture.  
**Guardrail:** No domain imports from another domain's internal modules — only through public interfaces. The AI enforces this.

---

### `03-architecture-proposal.json`
**Trigger:** `/architecture-proposal`  
**Prerequisite:** Skill 02 complete  
**Time:** 20–30 min  
**What it does:** Proposes the full technical stack (Next.js 15 App Router, TypeScript, MDX, CSS Custom Properties, Vercel Edge), directory structure, and 6 key architectural decisions with rationale.  
**You get:** `docs/architecture/architecture-proposal.md` + confirmed stack decisions.  
**Guardrail:** No database, no paid CMS, no required build steps beyond `next build`. Override any decision by telling the AI — it will create a new ADR in phase 5.

---

### `04-threat-modeling.json`
**Trigger:** `/threat-modeling`  
**Prerequisite:** Skill 03 complete  
**Time:** 20–30 min  
**What it does:** Identifies 7 threat vectors (contact form spam, XSS via MDX, secrets in config files, client bundle exposure, supply chain attacks, open redirect, CSP gaps) with severity ratings and specific mitigations.  
**You get:** `docs/security/threat-model.md`  
**⚠️ Non-negotiable threats:** T01 (contact form abuse) and T03 (secrets in config) must be mitigated before any API code is written.  
**Guardrail:** "It's just a portfolio" is not a valid reason to skip security. Templates are cloned by thousands of people.

---

### `05-adr-generation.json`
**Trigger:** `/adr-generation`  
**Prerequisite:** Skills 03 + 04 complete  
**Time:** 15–20 min  
**What it does:** Generates 7 Architecture Decision Records documenting: framework choice, MDX vs CMS, CSS Custom Properties vs Tailwind, config-file customisation, feature flags, Zod validation, and opt-in integrations.  
**You get:** `docs/adr/ADR-001.md` through `ADR-007.md` + an index.  
**Guardrail:** ADRs are never deleted — only superseded. If you change your mind on a decision, the AI creates a new ADR and marks the old one as Superseded.

---

### `06-api-design.json`
**Trigger:** `/api-design`  
**Prerequisite:** Skill 05 complete  
**Time:** 20–30 min  
**What it does:** Designs all API routes (`POST /api/contact`, `GET /rss.xml`, `GET /sitemap.xml`, `GET /robots.txt`, `GET /og`), the content-fetching library (`lib/content.ts`), and the SEO library (`lib/seo.ts`) — with full request/response schemas.  
**You get:** `docs/api/api-design.md` + confirmed function signatures.  
**Guardrail:** No route exposes internal error details in the response. Content-fetching functions are server-only.

---

### Skills 07–13 *(Coming Soon)*

| # | Skill | Trigger | What it produces |
|---|---|---|---|
| 07 | Code Scaffolding | `/scaffold` | Full file/folder skeleton with placeholder implementations |
| 08 | Refactoring | `/refactor` | Improvement plan with atomic commits, no behaviour changes |
| 09 | Test Generation | `/generate-tests` | Unit tests (Vitest), integration tests, E2E tests (Playwright) |
| 10 | PR Review | `/review-pr` | Pre-merge checklist, security scan, accessibility audit |
| 11 | Documentation | `/generate-docs` | JSDoc, inline comments, content-guide.md, updated README |
| 12 | Project Snapshot | `/snapshot` | State-of-the-world summary: what's built, what's pending |
| 13 | Release Notes | `/release-notes` | Human-readable changelog entry for any version |

---

## Anatomy of a Skill File

Every skill JSON shares this structure:

```jsonc
{
  "skill": "kebab-case-name",       // Machine-readable ID
  "version": "1.0.0",              // Semver — increment when skill changes
  "project": "...",                // Which project this skill is tuned for
  "phase": 1,                      // Position in the pipeline
  "title": "Human Readable Title",
  "description": "...",            // What this skill does in plain English
  "trigger": "/slash-command",     // What you type to invoke it

  "prerequisite": "...",           // What must be done first (optional)

  // The meat — what the AI should actually do, step by step
  "instructions": [ "Step 1...", "Step 2...", "..." ],

  // What files/documents this skill produces
  "outputs": [ "docs/...", "..." ],

  // Hard rules the AI must not violate
  "guardrails": [ "Never do X", "Always do Y" ]
}
```

The `guardrails` array is the most important field. It prevents the AI from doing what AI agents do by default: skip steps, over-engineer, make assumptions, and move too fast.

---

## Adapting These Skills to Your Own Project

These skills were generated for a **Universal Portfolio + Blog Template** (TypeScript, Next.js, Vercel). To adapt them for a different project:

1. **Change `"project"`** in each file to your project name.
2. **Update `"description"`** to reflect your domain (e.g. SaaS app, CLI tool, mobile app).
3. **Revise domain models** in Skill 02 to match your entities.
4. **Revise the stack** in Skill 03 — swap Next.js for your framework, swap Vercel for your deploy target.
5. **Keep the `guardrails`** — they are largely universal and prevent the most common AI agent mistakes.
6. **Keep the pipeline order** — phases 1→6 are planning phases. Never scaffold code before requirements, architecture, and threat modeling are confirmed.

---

## Principles Behind This Pipeline

**1. Alignment before action.**  
The first six phases produce no code. They exist entirely to align you and the AI on what to build and how. Misalignment at phase 1 costs you a conversation. Misalignment at phase 7 costs you a week of refactoring.

**2. Each phase gates the next.**  
Prerequisites are enforced. The AI will not design APIs (phase 6) before architecture is confirmed (phase 3). This mirrors how senior engineering teams work.

**3. Guardrails > instructions.**  
Instructions tell the AI what to do. Guardrails tell it what never to do. The guardrails in these skills encode hard-won lessons: don't add a database to a static template, don't skip threat modeling because it's "just a portfolio", don't merge PRs without checking for leaked secrets.

**4. Outputs are handoffs.**  
Every skill produces a document in `/docs/`. These documents are not just for humans — they are the context the *next* skill reads. This is how the pipeline maintains coherence across long sessions.

**5. You stay in control.**  
Every skill ends with a confirmation step. The AI proposes; you decide. Nothing moves forward without your sign-off.

---

## File Index

```
portfolio-skills/
├── README.md                        ← You are here
├── 01-clarify-requirements.json
├── 02-domain-decomposition.json
├── 03-architecture-proposal.json
├── 04-threat-modeling.json
├── 05-adr-generation.json
├── 06-api-design.json
├── 07-code-scaffolding.json         ← Coming soon
├── 08-refactoring.json              ← Coming soon
├── 09-test-generation.json          ← Coming soon
├── 10-pr-review.json                ← Coming soon
├── 11-documentation.json            ← Coming soon
├── 12-project-snapshot.json         ← Coming soon
└── 13-release-notes.json            ← Coming soon
```

---

## Contributing & Extending

Found a guardrail that should be stronger? A phase that needs more detail? These skills are living documents.

- To **add a guardrail**, append to the `"guardrails"` array and increment `"version"`.
- To **override an architectural decision**, do not edit the ADR — add a new one marked `"status": "Superseded"` on the old and `"status": "Accepted"` on the new.
- To **create a new skill**, follow the anatomy above and place it in the pipeline at the appropriate phase number.

---

*Generated by the Project Skill Generator · Universal Portfolio + Blog Template · v1.0.0*
