# Résumé Router

A single-page site that routes visitors to the right résumé for the role they're hiring for. v1: static HTML, links straight out to the live Google Docs (and their auto-generated PDF exports), so the site never goes stale when a doc gets edited.

## Deploy to GitHub Pages (free)

**Option A — user site (`yourname.github.io`), if you don't already have one:**
```bash
# create a new repo on GitHub named exactly: <your-username>.github.io
git init
git add index.html README.md
git commit -m "resume router v1"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-username>.github.io.git
git push -u origin main
```
Live at `https://<your-username>.github.io` within a minute or two, no further config needed.

**Option B — project site (e.g. `yourname.github.io/resume`), if you want to keep it separate from a future portfolio:**
```bash
# create a repo, any name, e.g. "resume-router"
git init
git add index.html README.md
git commit -m "resume router v1"
git branch -M main
git remote add origin https://github.com/<your-username>/resume-router.git
git push -u origin main
```
Then in the repo: **Settings → Pages → Source → Deploy from a branch → `main` / `/ (root)` → Save.**
Live at `https://<your-username>.github.io/resume-router` within a minute or two.

## When you're ready for v2

The routing-table structure here is meant to be a landing layer in front of a fuller portfolio later — same visual language (routes → destinations) could extend naturally into a timeline of your journey (IIT Madras → IMC → UIUC/TTIC research → UChicago → CHPC) without needing a redesign.
