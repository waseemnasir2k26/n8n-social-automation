# n8n-social-automation

Five importable n8n workflows: four ways to auto-draft and post to LinkedIn from RSS news, and one Instagram DM agent with human handoff. Import the JSON, add your credentials, test by hand, then switch on the schedule.

## What is in the box

| File | What it does |
| --- | --- |
| `workflows/linkedin/SKYNETLABS_LinkedIn_FINAL.json` | Every 8 hours reads 10 RSS feeds, picks the best item, has OpenAI draft a post, saves it to a Google Sheet. A row you mark approved gets posted to LinkedIn and marked as posted. |
| `workflows/linkedin/SKYNETLABS_LinkedIn_SIMPLE.json` | 4 RSS feeds, de-duplicated against an Airtable log, scored by GPT-4o-mini (keeps 7 and up), written by GPT-4o, saved to Airtable, posted to LinkedIn. |
| `workflows/linkedin/SKYNETLABS_LinkedIn_WORKING.json` | Picks one random item from 2 feeds, scores it, makes an image through an HTTP call to Reve AI, writes the post, posts with image or text only. |
| `workflows/linkedin/SKYNETLABS_LinkedIn_VIRAL.json` | Same shape as WORKING with a "viral score" gate (6 and up). |
| `workflows/instagram/instagram-dm-automation.json` | Instagram webhook into an AI agent with conversation memory, a Google Sheets lookup tool, human-takeover detection, Telegram alert on handoff, and a scheduled sync that refills the sheet from an API. |

`docs/` has a LinkedIn setup guide, a LinkedIn system setup note and a Google Sheet template (`GOOGLE_SHEET_TEMPLATE.csv`).

## Quickstart

```bash
git clone https://github.com/waseemnasir2k26/n8n-social-automation.git
```

1. In n8n: Workflows, Import from File, pick one JSON from `workflows/`.
2. Create the credentials the nodes ask for: OpenAI, LinkedIn OAuth2, and Google Sheets or Airtable depending on the workflow. Follow `docs/LINKEDIN_SETUP_GUIDE.md` for the LinkedIn side.
3. Replace placeholder values (for example the `Bearer YOUR_...` header in the image-generation node) with your own, kept in n8n credentials.
4. Run once manually and read every output before enabling the Schedule Trigger.

## For you if

You run n8n yourself, want a human-reviewable LinkedIn pipeline (FINAL has an approval step), and are comfortable editing prompts and feed lists.

## Status and limits

- LinkedIn and Instagram only. There is no X, Facebook, Pinterest or YouTube workflow in this repo.
- Workflows were exported as they were used, so names and prompts are SkynetLabs-flavoured. Rewrite the system prompts for your own voice.
- `instagram-dm-automation.json` is built around a vehicle inventory (`search_vehicles` tool and a vehicle API sync). Treat it as a pattern for an inventory-aware DM agent, not a generic bot.
- WORKING, VIRAL and SIMPLE post without a review step. Add an approval gate before pointing them at a real account.
- Review AI-written posts before they go public, and respect each platform's automation rules.

## License

MIT, see [LICENSE](LICENSE).

---

Built by SkynetLabs. Contact: waseem@skynetjoe.com

Need this wired into your business? SkynetLabs builds voice agents, n8n back offices and sites that convert → https://skynetjoe.com
