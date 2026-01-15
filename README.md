[README.md](https://github.com/user-attachments/files/24642319/README.md)
# Consultant / Clinical Claim Form — Monthly (Multi-session) Prototype (V3)

This is a static, client-side prototype that captures a clinician's monthly claim with multiple sessions per month. It is accessible (WCAG 2.2 AA conscious), responsive, and stores data in-browser (localStorage). No network calls are made.

Files
- index.html — main application (open locally in a modern browser)
- assets/styles.css — NHS-aligned styles (accent #005EB8)
- assets/app.js — application logic (sessions, specimens, validation, persistence, export)
- schema/claim.schema.json — JSON Schema for the exported payload
- README.md — this file
- .github/workflows/pages.yml (optional) — deploy on push to `main`

How to run locally
1. Download or clone the repository.
2. Open `index.html` in a modern browser (Chrome, Edge, Firefox).
   - No server required.
   - Note: the app uses `crypto.randomUUID()` where available; a secure fallback is provided.

Primary behaviours
- Add one or more sessions; each session has a unique UUID v4 Session ID (read-only).
- Each session contains a specimen list; add one or more specimens per session.
- Cases reported and total points are calculated per session.
- KPI badge per session shows Red (<36), Green (=36), Orange (>36).
- All fields are required (except budget email).
- Submit is disabled until the entire form (including all sessions/specimens) is valid.
- Save draft persists the full payload in localStorage; Load draft restores it.
- On submit, two files are downloaded:
  - `claim_<ESR>_<YYYY-MM>.json`
  - `claim_<ESR>_<YYYY-MM>.csv` (one row per specimen, repeating session context)
- If budget email is provided, the "Prepare email" button opens a mailto: draft with a prefilled subject and message; user attaches exported files manually.

Data privacy & security
- Drafts and used Session IDs are stored in localStorage only.
- No data leaves your browser in this prototype.
- For production, implement authenticated backend storage, server-side validation, and NHS IG-compliant data handling.

Extensibility notes
- Validation is performed client-side in `assets/app.js`. Replace or augment with a server-side validator upon integration.
- To change KPI target, update `KPI_TARGET` in `assets/app.js` and the schema.
- The JSON schema in `schema/claim.schema.json` documents the expected payload shape for integration.

Deploy to GitHub Pages
1. Push this repository to GitHub.
2. Enable GitHub Pages in repository settings (serve from the `main` branch or `gh-pages`).
3. Optionally use the included workflow to auto-deploy on push to `main`.

Contact / Next steps
- I can add a printable summary view, replace CSV builder with more advanced spreadsheet-friendly output, or wire a sample secure backend endpoint for server-side storage.
