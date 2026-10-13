# Setup & Configuration Guide

**Project:** AI-Powered Customer Inquiry Organizer  
**Platform:** n8n Cloud  
**Delivery:** Workflow JSON + this guide

---

## 1. Import the Workflow

1. Open your **n8n Cloud** instance.
2. Go to **Workflows** → **Add workflow** → **Import from File** (or paste JSON).
3. Select the file:  
   `workflow/n8n-ai-inquiry-organizer.json`
4. Click **Import**.

The workflow will appear with these nodes:

- Webhook – Website Inquiry  
- Extract & Standardize Fields  
- Validate Required Fields  
- OpenAI – Summary & Priority  
- Parse AI Response  
- Google Sheets – Save Inquiry  
- Gmail – Send Notification  
- Respond Success / Respond Validation Error

---

## 2. Connect Credentials

### OpenAI
1. In the **OpenAI – Summary & Priority** node, click the credential field.
2. Create or select your OpenAI account.
3. Paste your **OpenAI API key** (you already have one).
4. Recommended model: `gpt-4o-mini` (cost-effective and fast).

### Google Sheets
1. Open the **Google Sheets – Save Inquiry** node.
2. Connect your Google account (OAuth).
3. Replace `YOUR_GOOGLE_SHEET_ID` with the actual ID of your spreadsheet.  
   (You can find it in the sheet URL: `https://docs.google.com/spreadsheets/d/SHEET_ID/edit`)
4. Make sure the sheet has these exact column headers in the first row:

```
Name | Email | Message | Service | AI Summary | Priority | Date
```

### Gmail
1. Open the **Gmail – Send Notification** node.
2. Connect your Gmail account via OAuth.
3. Change the **Send To** address to the email where your agency should receive notifications.

---

## 3. Configure the Webhook

1. Open the **Webhook – Website Inquiry** node.
2. Copy the **Production URL** (it looks like:  
   `https://your-instance.app.n8n.cloud/webhook/website-inquiry`).
3. In your website contact form, set the form submission to send a **POST** request to this URL.
4. Expected payload fields (any of these will work):
   - `name`
   - `email`
   - `message` (or `inquiry`)
   - `service` (or `service_requested`)

Example JSON body:
```json
{
  "name": "John Smith",
  "email": "john@example.com",
  "message": "I need help with SEO for my e-commerce store.",
  "service": "SEO"
}
```

---

## 4. Activate the Workflow

1. Toggle the workflow to **Active** (top right).
2. Test with a sample form submission or by using the **Test** button in the Webhook node.

---

## 5. What the Workflow Does

1. Receives the inquiry via Webhook.
2. Extracts and standardizes the fields.
3. Validates that email and message are present.
4. Sends the inquiry to OpenAI → gets a short summary + High / Medium / Low priority.
5. Appends a new row to your Google Sheet (Service and Priority in separate columns).
6. Sends a Gmail notification with the priority in the subject line, e.g.:  
   `New High-Priority Inquiry – Website Form`
7. Returns a simple success response to the form.

---

## 6. Important Notes

- Keep your OpenAI, Google, and Gmail accounts connected and active.
- Priority classification is an automated assessment — it is helpful but not perfect.
- Basic validation is included: if email or message is missing, the workflow returns an error response and does not process further.
- You can adjust the OpenAI prompt inside the **OpenAI – Summary & Priority** node if you want different priority rules.

---

## Need Help?

If anything does not work after following these steps, reply in the Fiverr order chat with a screenshot of the error and I will assist within the included revision.
