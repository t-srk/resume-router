# Résumé Router

Single-page landing site that routes visitors to the right résumé for the role they're hiring for. One `index.html`, no build step; links go straight out to the live Google Docs (and their `/export?format=pdf` variants) so the site never goes stale when a doc gets edited.

**Live:** https://resume-router.pages.dev/

## Hosting

Deployed on **Cloudflare Pages**. Any push to `main` auto-deploys in ~10 seconds.

- Build command: *(empty)*
- Build output directory: `/`
- Framework preset: `None`

The project was originally set up on GitHub Pages but migrated after persistent Actions-runner failures. Don't re-enable GitHub Pages.

## Editing

Edit `index.html` directly. Commit and push — Cloudflare picks up the change automatically.

The résumés themselves are **Google Docs**, not files in this repo. Their sharing must stay set to "Anyone with the link → Viewer" or the view/PDF buttons will 403.

## See also

- [`PLANNING.md`](./PLANNING.md) — full context, design decisions, and v2 plans for a fresh Claude Code session to pick up from.
