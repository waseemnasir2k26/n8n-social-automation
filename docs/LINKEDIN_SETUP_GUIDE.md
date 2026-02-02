# LinkedIn Auto-Posting Setup for n8n

---

## What You Need

1. **LinkedIn OAuth2 Credentials** in n8n
2. **LinkedIn Person URN** (your profile ID)
3. **New Airtable field** for tracking posted content

---

## Step 1: Add LinkedIn Credential in n8n

### 1.1 In n8n
1. Go to **Credentials** → **Add Credential**
2. Search for **"LinkedIn OAuth2 API"**
3. You'll see fields for:
   - Client ID
   - Client Secret

### 1.2 Get LinkedIn API Credentials

**Option A: If you already have a LinkedIn App (working for you)**
- Use your existing Client ID and Client Secret

**Option B: Create LinkedIn App**
1. Go to: https://www.linkedin.com/developers/apps
2. Click **Create App**
3. Fill in:
   - App name: `SkynetLabs Content Engine`
   - LinkedIn Page: Select your company page
   - Privacy policy URL: Your website URL
   - App logo: Upload any logo
4. Click **Create app**

### 1.3 Configure App Permissions
1. In your LinkedIn App → **Auth** tab
2. Under **OAuth 2.0 scopes**, request:
   - `w_member_social` (Share, comment, and like posts)
3. Under **Authorized redirect URLs**, add:
   ```
   https://your-n8n-url.com/rest/oauth2-credential/callback
   ```

   For n8n Cloud:
   ```
   https://your-instance.app.n8n.cloud/rest/oauth2-credential/callback
   ```

   For local:
   ```
   http://localhost:5678/rest/oauth2-credential/callback
   ```

### 1.4 Copy Credentials
1. Go to **Auth** tab
2. Copy **Client ID**
3. Copy **Client Secret**
4. Paste both into n8n

### 1.5 Connect in n8n
1. Click **Sign in with LinkedIn**
2. Authorize the app
3. Save credential as **"LinkedIn"**

---

## Step 2: Get Your LinkedIn Person URN

Your Person URN is your LinkedIn profile ID in this format:
```
urn:li:person:ABC123xyz
```

### How to Find It:

**Method 1: From LinkedIn Profile URL**
1. Go to your LinkedIn profile
2. Look at URL: `https://www.linkedin.com/in/yourname/`
3. The URN format is different - you need the ID

**Method 2: Use n8n to Get It**
1. Create a test workflow with HTTP Request node
2. URL: `https://api.linkedin.com/v2/me`
3. Authentication: Use your LinkedIn OAuth2 credential
4. Run it - response will contain your `id`
5. Your URN is: `urn:li:person:{id}`

**Method 3: Quick Test**
1. In your workflow, temporarily use the LinkedIn node
2. Set operation to "Get Profile"
3. Run it
4. Check output for your ID

---

## Step 3: Add Environment Variable

In n8n **Settings** → **Variables**, add:

```
LINKEDIN_PERSON_URN = urn:li:person:YOUR_ID_HERE
```

---

## Step 4: Update Airtable Schema

Add this field to your **ContentDrafts** table:

| Field Name | Type |
|------------|------|
| LinkedIn_Post_ID | Single line text |

This tracks which posts have been published.

---

## Step 5: Test the LinkedIn Node

1. Open the workflow
2. Click on **"Post to LinkedIn"** node
3. Select your LinkedIn credential
4. Click **Test step** (after running previous nodes)
5. Check your LinkedIn profile for the post

---

## Flow After Adding LinkedIn

```
RSS → Filter → Draft → Airtable → Gmail
                                    ↓
                              Post to LinkedIn
                                    ↓
                           Update Status = "Published"
```

**What happens:**
1. Draft is created and saved to Airtable (Status: "Draft")
2. Gmail notification sent
3. **Version A (Story)** is auto-posted to LinkedIn
4. Airtable status updated to "Published"

---

## Which Draft Gets Posted?

By default: **Version A (Story-driven)** is posted.

To change this, edit the LinkedIn node text field:

| Draft | Code |
|-------|------|
| Version A (Story) | `{{ $('Parse Drafts').item.json.drafts.version_a }}` |
| Version B (Contrarian) | `{{ $('Parse Drafts').item.json.drafts.version_b }}` |
| Version C (Analytical) | `{{ $('Parse Drafts').item.json.drafts.version_c }}` |

---

## Rate Limiting

LinkedIn has posting limits:
- ~50 shares per day (personal accounts)
- Don't post too frequently (wait 1+ hours between posts)

The workflow runs every 6 hours, so you're safe.

---

## Troubleshooting

### "Unauthorized" Error
- Re-authenticate LinkedIn credential
- Check `w_member_social` scope is enabled

### "Invalid Person URN"
- Make sure format is `urn:li:person:XXXXXX`
- Get fresh ID using Method 2 above

### "Post not appearing"
- Check LinkedIn activity feed (not main feed)
- May take a few minutes to appear

### "Rate limit exceeded"
- You've hit LinkedIn's daily limit
- Wait 24 hours

---

## Files

**New workflow file:**
```
SKYNETLABS_OpenAI_Gmail_LinkedIn_Workflow.json
```

This is the complete workflow with:
- OpenAI (GPT-4o-mini + GPT-4o)
- Airtable
- Gmail notifications
- LinkedIn auto-posting

---

## Your Final Stack

| Component | Service | Purpose |
|-----------|---------|---------|
| AI Filtering | GPT-4o-mini | Score content relevance |
| AI Drafting | GPT-4o | Write 3 post variations |
| Database | Airtable | Store drafts & track status |
| Notifications | Gmail | Alert when drafts ready |
| Publishing | LinkedIn | Auto-post Version A |

**Fully automated content pipeline!**
