# Changelog

All notable changes to this project are documented in this file.

## [2026.09] - 2026-09-16

- Maintenance review of n8n-social-automation — a pack of ready-to-import n8n workflow JSONs for LinkedIn auto-posting and Instagram DM handling, with GPT-4 content generation and a Google Sheets content calendar.
- Contents: four LinkedIn variants in `workflows/linkedin/` (FINAL, WORKING, VIRAL, SIMPLE), one `instagram-dm-automation.json`, and `docs/` with two LinkedIn setup guides plus a Google Sheet CSV template. MIT licensed.
- Status: JSON + docs only — no code, no build, no package manifest, no tests. Last change April 2026 (SEO "Hire Me" block). The README's roadmap items (Twitter/X, Facebook, TikTok, approval workflow, analytics) are all still unchecked.
- Reviewed September 2026: docs refreshed, CHANGELOG started, versioned as v2026.09. No workflow JSON or setup guides changed.
- Known gaps: four near-duplicate LinkedIn workflows with no stated rule for which one to import; no validator or CI to catch a malformed workflow JSON before import; no CHANGELOG before this release; the workflows carry no spend, iteration or kill-switch caps of their own.
