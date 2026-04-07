# n8n Social Media Automation

> Ready-to-import n8n workflows for LinkedIn and Instagram automation.

Automate your social media presence with AI-powered content generation and posting workflows.

![n8n](https://img.shields.io/badge/n8n-Workflows-EA4B71?style=for-the-badge&logo=n8n&logoColor=white)
![OpenAI](https://img.shields.io/badge/OpenAI-GPT--4-412991?style=for-the-badge&logo=openai&logoColor=white)
![LinkedIn](https://img.shields.io/badge/LinkedIn-Automation-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)
![Instagram](https://img.shields.io/badge/Instagram-DM_Bot-E4405F?style=for-the-badge&logo=instagram&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

---

## Workflows Included

### LinkedIn Automation

| Workflow | Description |
|----------|-------------|
| `SKYNETLABS_LinkedIn_FINAL.json` | Complete LinkedIn auto-posting with AI content |
| `SKYNETLABS_LinkedIn_WORKING.json` | Production-ready daily posting workflow |
| `SKYNETLABS_LinkedIn_VIRAL.json` | Optimized for viral content generation |
| `SKYNETLABS_LinkedIn_SIMPLE.json` | Minimal setup, quick start version |

### Instagram Automation

| Workflow | Description |
|----------|-------------|
| `instagram-dm-automation.json` | AI-powered Instagram DM responses |

---

## Features

- **AI Content Generation** - GPT-4 powered post creation
- **Scheduled Posting** - Automated daily/weekly schedules
- **Multi-Platform** - LinkedIn + Instagram support
- **Customizable Prompts** - Tailor content to your brand voice
- **Google Sheets Integration** - Track and manage content calendar

---

## Quick Start

### Prerequisites

- [n8n](https://n8n.io/) instance (self-hosted or cloud)
- OpenAI API key
- LinkedIn account with API access
- Instagram Business account (for DM automation)

### Installation

1. **Download the workflow**
   ```bash
   git clone https://github.com/waseemnasir2k26/n8n-social-automation.git
   ```

2. **Import to n8n**
   - Open your n8n instance
   - Go to Workflows → Import from File
   - Select the desired `.json` workflow

3. **Configure credentials**
   - Add your OpenAI API key
   - Connect your LinkedIn account
   - Set up Google Sheets (if using)

4. **Activate the workflow**
   - Review all nodes
   - Test with manual execution
   - Enable the schedule trigger

---

## Workflow Structure

```
n8n-social-automation/
├── workflows/
│   ├── linkedin/
│   │   ├── SKYNETLABS_LinkedIn_FINAL.json
│   │   ├── SKYNETLABS_LinkedIn_WORKING.json
│   │   ├── SKYNETLABS_LinkedIn_VIRAL.json
│   │   └── SKYNETLABS_LinkedIn_SIMPLE.json
│   └── instagram/
│       └── instagram-dm-automation.json
├── docs/
│   ├── LINKEDIN_SETUP_GUIDE.md
│   ├── LINKEDIN_SYSTEM_SETUP.md
│   └── GOOGLE_SHEET_TEMPLATE.csv
├── README.md
└── LICENSE
```

---

## Configuration

### LinkedIn Workflow

1. **OpenAI Node**
   - Model: GPT-4 or GPT-4o
   - Temperature: 0.7 (adjustable)
   - System prompt: Customize for your niche

2. **LinkedIn Node**
   - OAuth2 authentication
   - Post visibility: Public/Connections

3. **Schedule Trigger**
   - Default: Daily at 9 AM
   - Adjust timezone as needed

### Instagram DM Workflow

1. **Webhook Trigger**
   - Receives incoming DM notifications

2. **AI Response**
   - Context-aware replies
   - Customizable response templates

---

## Customization Tips

- **Change posting frequency** - Edit the Schedule Trigger node
- **Modify content style** - Update the OpenAI system prompt
- **Add hashtags** - Include hashtag logic in the prompt
- **Multi-language** - Add language parameter to prompts

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| LinkedIn auth fails | Re-authenticate, check API permissions |
| No posts appearing | Verify workflow is active, check execution logs |
| AI content too generic | Refine system prompt with more context |
| Rate limits | Add delay nodes between API calls |

---

## Security Notes

- Never commit API keys to the repository
- Use n8n's built-in credential management
- Rotate keys periodically
- Review AI-generated content before auto-posting

---

## Roadmap

- [ ] Twitter/X automation
- [ ] Facebook page posting
- [ ] TikTok integration
- [ ] Content approval workflow
- [ ] Analytics dashboard

---

## License

MIT License - see [LICENSE](LICENSE) for details.

---

## Author

**Waseem Nasir**
- Website: [skynetjoe.com](https://www.skynetjoe.com)
- LinkedIn: [@waseemnasir2k26](https://linkedin.com/in/waseemnasir2k26)
- GitHub: [@waseemnasir2k26](https://github.com/waseemnasir2k26)

---

<p align="center">
  <b>Built by <a href="https://www.skynetjoe.com">Skynetlabs</a></b><br>
  AI Automation & Systems Studio
</p>

---

<!-- SEO-HIRE-ME-BLOCK -->

## Hire Me

> **Need n8n workflows or social media automation built for you?**

I'm **Waseem Nasir** — founder of [Skynet Labs / SkynetJoe](https://www.skynetjoe.com), an AI Automation Agency. Custom n8n workflows, GoHighLevel automations, multi-platform posting, AI agents.

**50+ live projects across:** Healthcare · Legal · Real Estate · E-Commerce · Logistics · HVAC · SaaS · Consulting

### Hire me
- 📅 **[Book a free strategy call](https://calendly.com/skynetlabs/schedule-a-free-consultation)**
- 💼 **[Hire on Fiverr](https://fiverr.com/agencies/skynetjoellc)**
- 🌐 **[skynetjoe.com](https://www.skynetjoe.com)**
- 📧 **info@skynetjoe.com**
- 💬 **[WhatsApp](https://wa.me/923001001957)**

### Related projects on my GitHub
- [aeo-content-engine](https://github.com/waseemnasir2k26/aeo-content-engine)
- [social-media-dashboard](https://github.com/waseemnasir2k26/social-media-dashboard)
- [ai-motivational-posts](https://github.com/waseemnasir2k26/ai-motivational-posts)
- [→ See all 50+ projects](https://github.com/waseemnasir2k26)

### Tags
`AI automation` · `n8n` · `GoHighLevel` · `Claude Code` · `Next.js` · `React` · `Python` · `freelance` · `hire me` · `agency`
