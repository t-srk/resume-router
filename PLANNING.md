# Résumé Router — Planning & Handoff

Last updated: 2026-07-03. Written for a fresh Claude Code session to pick up from cold.

---

## Where things stand

**v1 is shipped and live at https://resume-router.pages.dev/**

A single-page landing site (one `index.html`, no build step) that routes recruiters to the right résumé for the role they're hiring for. Four role-specific Google Docs plus a master:

| Role family | Doc handle | Google Doc ID |
|---|---|---|
| Quant Trader / Researcher | `quant_r2` | `1aWWNX7bI2ZkGq6YzwX_3SEZ-LRSLGXqKTbdpr3HJguA` |
| Quant Developer / Fintech SWE | `swe_q1` | `1CW3jFtjJx0irKW4xIKRWqKyug3FinPvvsRTN2nBqTV8` |
| AI Engineer / SWE | `swe_s1` | `1pJeEzl80o9TVK9luFNPL72oYMHX0YSA4lYEp-Iw-JFw` |
| ML / Research | `ml_a1` | `1LdYSe2Sm38G_xNWBDfOiePo5r-HQMpvrAYkbJ0GpnPE` |
| Master (source of truth) | `master` | `1HTrf1bq_PTgw4W_aQKSKr66azMPjzF5yYmL71wQjBg8` |

Each card links to the doc's `/edit` view and `/export?format=pdf` — so nothing goes stale when Shiva edits a résumé.

**All 5 docs are set to "Anyone with the link → Viewer"** (verified with Shiva 2026-07-03). If a view/PDF button ever 403s, sharing on that specific doc has been changed back to restricted — that's the first thing to check.

---

## Deploy pipeline (current)

- Repo: `github.com/t-srk/resume-router`
- Hosting: **Cloudflare Pages** (project name: `resume-router`)
- Trigger: any push to `main` → auto-deploy in ~10s
- Build settings: framework preset `None`, build command empty, output directory `/`

**Do not** touch GitHub Pages. It was tried first, hit persistent transient `actions/deploy-pages@v5` failures and 2-hour runner queues on this account, and got abandoned. The old `t-srk.github.io/resume-router` URL still resolves but should not be shared.

---

## Design decisions

Went through two visual iterations:

1. **First pass (rejected):** Dark navy background (`#0B1220`) with amber/teal accents, terminal-prompt eyebrow, monospace `role.match(...) → target` syntax on each card. Kept a "routing table" metaphor throughout.
2. **Current (shipped):** White background, near-black text (`#0f172a`), single blue accent (`#2563eb`) on links only. Fraunces serif for h1 and résumé titles, Inter for body. No terminal metaphor. Résumés are a plain list separated by thin `#e5e7eb` dividers. Master is a single sentence at the bottom, not a boxed callout. All copy in first person.

**Type stack requires Google Fonts** (`Fraunces` + `Inter`) — CSS `<link>` at the top of `index.html`. If Shiva ever wants offline reliability, self-host the WOFF2s.

**Responsive**: single breakpoint at `@media (max-width: 520px)` in the CSS. h1 uses `clamp(40px, 6vw, 56px)`.

---

## v2 — not started

Shiva mentioned two inputs sitting in the parent `Resume/` folder that were **intentionally not touched during v1**:

- Résumé PDFs (source material)
- Job-history context from a prior Claude.ai conversation

These are for a **timeline / portfolio section** to be added below the current routing table. Shiva's stated intent: same visual language as v1 (list of destinations with thin dividers) should extend naturally into a career timeline — no redesign required. Ordering per the résumé router content: IIT Madras → IMC → UIUC/TTIC computer-vision research → UChicago → CHPC.

When Shiva opens the next session and says "let's do v2," the starting move is:
1. Ask him to point to the résumé PDFs and job-history file paths (don't assume filenames)
2. Read the job-history context to get accurate dates, titles, and 1-2 line summaries per role
3. Design a timeline section that lives below the résumé list, using the same Fraunces/Inter type and blue accent
4. Preserve the top-of-page "route to a résumé" flow — the router is the primary call to action; the timeline is context that lives below it

---

## File map

```
portfolio-website/
├── index.html      # the entire site
├── README.md       # short public-facing deploy notes (reflects Cloudflare)
└── PLANNING.md     # this file
```

That's it. No build tools, no npm, no framework. Every change is a hand-edit to `index.html`.

---

## Working-style notes for the next session

- Shiva prefers tight, numbered step-by-step instructions for anything he has to do himself in a browser (GitHub, Cloudflare, Google Docs sharing). Include exact URLs and exact button names. Skip exploratory prose.
- `gh` CLI is **not installed** on this machine. Any GitHub operation the user can't do via `git` needs to be walked through in the browser.
- Windows Git will show CRLF/LF warnings on commit — ignore, they're not errors.
- User email for commits: `shivatipireddy@uchicago.edu`. Personal email (in the site): `shivatippireddy@gmail.com` (note the double p — genuinely two different addresses).
