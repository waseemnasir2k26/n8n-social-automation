# Changelog

All notable changes to this project are documented in this file.

## [2026.10] - 2026-10-12

- Public MIT pack of importable n8n workflows: four LinkedIn auto-posting variants (FINAL, WORKING, VIRAL, SIMPLE) and one Instagram DM automation, plus setup docs and a content-calendar CSV template.
- Reviewed October 2026: README links checked (Calendly, Fiverr, LinkedIn profile, n8n.io, sibling repos, WhatsApp all respond 200); no dead links. No workflow JSON or doc changes; last functional commit 2026-04-07.
- Hire section links normalised to the three canonical SkynetLabs destinations (Fiverr agency, Upwork profile, Calendly).
- Known gaps: four near-duplicate LinkedIn workflows with no stated rule for which to import; no JSON validation or CI; roadmap items (X, Facebook, TikTok, approvals, analytics) still unchecked; workflows have no spend or iteration caps of their own.

## [2026.09] - 2026-09-16

- Maintenance review of n8n-social-automation — a pack of ready-to-import n8n workflow JSONs for LinkedIn auto-posting and Instagram DM handling, with GPT-4 content generation and a Google Sheets content calendar.
- Contents: four LinkedIn variants in `workflows/linkedin/` (FINAL, WORKING, VIRAL, SIMPLE), one `instagram-dm-automation.json`, and `docs/` with two LinkedIn setup guides plus a Google Sheet CSV template. MIT licensed.
- Status: JSON + docs only — no code, no build, no package manifest, no tests. Last change April 2026 (SEO "Hire Me" block). The README's roadmap items (Twitter/X, Facebook, TikTok, approval workflow, analytics) are all still unchecked.
- Reviewed September 2026: docs refreshed, CHANGELOG started, versioned as v2026.09. No workflow JSON or setup guides changed.
- Known gaps: four near-duplicate LinkedIn workflows with no stated rule for which one to import; no validator or CI to catch a malformed workflow JSON before import; no CHANGELOG before this release; the workflows carry no spend, iteration or kill-switch caps of their own.
