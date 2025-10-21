<!--
AI assistant guidance for contributors working in this repository.
This file is intentionally concise and focused on patterns an AI coding agent needs to be immediately productive.
-->

# Copilot / AI instructions — evaluasi_pekan_3

Purpose: give short, actionable guidance so an AI code assistant can make safe, useful edits to this repo.

1) Project high level
- This repo is a static website / documentation site (HTML, CSS, images) with many auxiliary scripts and docs.
- Primary content lives at the repository root: HTML files (index.html, product.html, etc.), `css/`, `assets/` and `images/`.
- There is no obvious server-side application in the repo. Treat changes as front-end/static-site edits unless you find a clear server/API module.

2) Where to look first
- `index.html` is the canonical front page and contains inlined scripts for UI interactions (smooth scroll, simple alerts). Use it as an example of markup patterns.
- `style.css`, `main.css`, and files under `css/` show styling conventions and utility classes.
- `docs/`, `USER_GUIDE.md`, `DEVELOPER_GUIDE.md`, and `ARCHITECTURE.md` are present but mostly empty — add or update documentation here when adding big features.

3) Build / test / run workflows (concrete)
- This repository uses plain shell and batch scripts for common tasks: `build.sh`/`build.bat`, `deploy.sh`/`deploy.bat`, `start-server.sh`/`start-server.bat`, `run-tests.sh`/`run-tests.bat`, `install.sh`/`install.bat`.
- Most scripts are placeholders. Do not assume they run; inspect the script file before invoking. If empty, propose a safe implementation and add tests or README notes.
- For local preview, open `index.html` directly in a browser or serve the directory with a static server (e.g., Python SimpleHTTPServer / http.server). Example (for maintainers to run manually):
  - PowerShell: python -m http.server 8000 --bind 127.0.0.1

4) Conventions and patterns
- HTML pages tend to include small inline JavaScript for UI (no build toolchain expected). Keep JavaScript minimal and place new scripts in `scripts/` or inline only when trivial.
- CSS is split across multiple files (style.css, main.css, components.css). Follow existing naming and avoid introducing a new global stylesheet unless consolidating intentionally.
- Logs (e.g., `server.log`, `webhook.log`, `deploy.log`) are present for reference. Do NOT commit generated logs back to the repo — keep edits focused on source files.

5) Integration points & external dependencies
- `API.md` and `DATABASE_SCHEMA.md` exist but are empty; there are hints of external integrations through `webhook.log`, `payment.log`, and `email.log`. If implementing integrations, document endpoints in `API.md` and update `DEPLOYMENT.md`.
- Assets are served from `assets/`, `images/`, and `img/`. Preserve existing paths when changing markup to avoid broken images.

6) Safe edit rules for AI
- Prefer small, single-purpose PRs. Each change should include one of: updated HTML/CSS, new static asset, or documentation update.
- When changing visual styles, update only related CSS files and check `index.html` or affected pages for regressions.
- If adding scripts or new CLI workflows, provide cross-platform equivalents (both `.sh` and `.bat`) and update `INSTALL.md` and `DEVELOPER_GUIDE.md`.
- Never introduce runtime secrets, API keys, or embed credentials in files.

7) Examples to reference in edits
- To add a new UI widget: mirror patterns in `index.html` (product cards, `.product-card`, `.btn` classes).
- To add site-wide styles: append to `style.css` or `main.css` and keep media queries consistent with `mobile.css` and `tablet.css`.
- To add a simple static preview server script: create `scripts/serve.sh` and `scripts/serve.bat` that use `python -m http.server` and `python -m http.server --bind 127.0.0.1` respectively.

8) Where to document changes
- Small feature: update `CHANGELOG.md` and `README-backup.md` (or `readme.md`) with a short entry.
- Architectural or workflow changes: update `ARCHITECTURE.md`, `DEVELOPER_GUIDE.md` and `DEPLOYMENT.md`.

9) If you add new code
- Add a short test or manual verification steps in `TESTING.md` (file exists but empty) — list the browser(s) and steps to verify UI changes.

Questions / unknowns to ask the maintainers
- Which script(s) are intended to be runnable? (many are empty)
- Is there a canonical build/deploy process (CI) we should follow or document?

If anything here is unclear or you want more examples, tell me what area to expand (scripts, CSS conventions, docs templates) and I'll iterate.
