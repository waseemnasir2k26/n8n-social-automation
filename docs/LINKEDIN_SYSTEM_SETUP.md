# LinkedIn Automated Content System
## Production Setup Guide

---

## System Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                    TWO-WORKFLOW ARCHITECTURE                    │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  WORKFLOW 1: Daily Content Generator                           │
│  ├── Runs: Daily at 6 AM                                       │
│  ├── Sources: 5 RSS feeds (AI/automation niche)                │
│  ├── Output: New posts added to Google Sheet                   │
│  └── Status: Unapproved (requires manual review)               │
│                                                                 │
│  WORKFLOW 2: LinkedIn Publisher                                 │
│  ├── Runs: Every hour                                          │
│  ├── Checks: Approved posts with 8-hour gap                    │
│  ├── Posts: Text-only to LinkedIn                              │
│  └── Updates: Marks as posted with timestamp                   │
│                                                                 │
│  CONTROL PANEL: Google Sheet                                   │
│  ├── Review generated posts                                    │
│  ├── Type "Approved" to queue for publishing                   │
│  └── Track all posted content                                  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## Quick Start Checklist

```
□ 1. Set up Google Sheet with correct columns
□ 2. Import LinkedIn_Daily_Content_Generator.json
□ 3. Import LinkedIn_Publisher.json
□ 4. Configure credentials (Google Sheets, OpenAI, LinkedIn)
□ 5. Test Daily Generator with manual trigger
□ 6. Review posts in sheet, approve one
□ 7. Test Publisher with manual trigger
□ 8. Enable scheduled triggers
```

---

## Google Sheet Setup

### Required Columns (in this exact order)

| Column | Header | Purpose |
|--------|--------|---------|
| A | `date_added` | When post was generated |
| B | `source_feed` | RSS feed origin |
| C | `original_topic` | Core topic extracted |
| D | `content_hash` | Duplicate detection hash |
| E | `linkedin_post` | **THE POST TEXT** |
| F | `word_count` | Post length |
| G | `approval_status` | **Type "Approved" here** |
| H | `posted_status` | "No" or "Yes" |
| I | `scheduled_time` | (optional) |
| J | `posted_time` | When actually posted |
| K | `linkedin_post_id` | LinkedIn API response |
| L | `notes` | Your notes |

### How Approval Works

1. Generator adds new rows with `approval_status` = empty
2. You review the `linkedin_post` column
3. Type **Approved** (exactly) in `approval_status`
4. Publisher picks it up on next hourly run

---

## Workflow 1: Daily Content Generator

### What It Does

1. Fetches RSS feeds at 6 AM daily
2. Filters to last 24 hours only
3. Limits to 10 items max
4. AI extracts core insights (GPT-4o-mini)
5. Filters by relevance score (>= 6)
6. AI generates LinkedIn post (GPT-4o)
7. Checks for duplicates (hash + text similarity)
8. Adds unique posts to Google Sheet

### RSS Sources Included

| Source | Focus |
|--------|-------|
| n8n Blog | Automation tutorials |
| Anthropic News | Claude/AI updates |
| LangChain Blog | AI agents/chains |
| Simon Willison | AI dev tools |
| Latent Space | AI engineering |

### To Add More RSS Feeds

1. Duplicate any RSS node
2. Change the URL
3. Connect to "Merge All Feeds" node

---

## Workflow 2: LinkedIn Publisher

### What It Does

1. Runs every hour
2. Checks for approved, unposted rows
3. Enforces 8-hour gap between posts
4. Enforces 3 posts/day maximum
5. Posts oldest approved first
6. Updates sheet with posted status

### Publishing Rules

| Rule | Value |
|------|-------|
| Minimum gap | 8 hours |
| Max per day | 3 posts |
| Order | Oldest approved first |
| Format | Text only (no images) |

---

## Credentials Required

### 1. Google Sheets OAuth2

```
Credential ID: saZ3kdmtxT2N7QN5
Name: waseemhome8
Scopes: spreadsheets (read/write)
```

### 2. OpenAI API

```
Credential ID: AevMS99UaDEkMJw8
Name: OpenAi account
Models used: gpt-4o-mini, gpt-4o
```

### 3. LinkedIn OAuth2

```
Credential ID: o3O2LKk7w9epRLKv
Name: LinkedIn account
Person URN: fbb-chs7WH
```

---

## Duplicate Prevention

### Two-Layer System

**Layer 1: Exact Hash**
- SHA-256 hash of normalized post text
- Catches exact duplicates instantly

**Layer 2: Text Similarity**
- Jaccard similarity on word sets
- Threshold: 0.6 (60% similar = duplicate)
- Catches paraphrased duplicates

### How It Works

```
New Post → Hash Check → [Match?] → DISCARD
                ↓
              [No Match]
                ↓
         Similarity Check → [>= 60%?] → DISCARD
                ↓
              [< 60%]
                ↓
           ADD TO SHEET
```

---

## Post Quality Rules

### AI Prompt Enforces

- 80-150 words
- No emojis
- No questions as hooks
- No engagement bait
- Statement-based hooks only
- 2-3 hashtags max (at end)
- Founder voice, not content creator

### Banned Phrases

```
❌ "Here's the thing..."
❌ "Let that sink in"
❌ "Game-changer"
❌ "This changes everything"
❌ "Thoughts?"
❌ "Agree?"
```

---

## Troubleshooting

### No Posts Generated

1. Check RSS feeds are returning items
2. Check items have pubDate in last 24h
3. Check relevance score threshold (must be >= 6)
4. Check duplicate detection isn't too aggressive

### Posts Not Publishing

1. Check `approval_status` says exactly "Approved"
2. Check `posted_status` is "No"
3. Check 8-hour gap from last post
4. Check daily limit (3 posts)
5. Check LinkedIn credentials are valid

### Duplicate False Positives

Lower the similarity threshold in "Check Duplicates" node:
```javascript
const SIMILARITY_THRESHOLD = 0.6; // Lower to 0.5 or 0.4
```

---

## File List

| File | Purpose |
|------|---------|
| `LinkedIn_Daily_Content_Generator.json` | Daily RSS → AI → Sheet workflow |
| `LinkedIn_Publisher.json` | Hourly approval → LinkedIn workflow |
| `LINKEDIN_SYSTEM_SETUP.md` | This setup guide |

---

## Manual Testing

### Test Content Generator

1. Open workflow in n8n
2. Click "Execute Workflow" (don't wait for schedule)
3. Check Google Sheet for new rows
4. Verify posts are readable and on-brand

### Test Publisher

1. In Google Sheet, type "Approved" for one row
2. Open Publisher workflow
3. Click "Execute Workflow"
4. Check LinkedIn for new post
5. Verify sheet row updated to "Yes"

---

## Production Schedule

| Time | Event |
|------|-------|
| 6:00 AM | Content Generator runs |
| 7:00 AM | Publisher checks (posts if approved) |
| 8:00 AM | Publisher checks |
| ... | Every hour |
| 11:00 PM | Publisher checks |

**You should review and approve posts between 6 AM - 10 AM for same-day publishing.**

---

## Support

- n8n Docs: https://docs.n8n.io
- OpenAI API: https://platform.openai.com/docs
- LinkedIn API: https://docs.microsoft.com/linkedin
