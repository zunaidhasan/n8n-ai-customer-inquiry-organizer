# AI-Powered Customer Inquiry Organizer (n8n)

AI-powered customer inquiry organizer built with **n8n Cloud** for a small digital marketing agency.

The workflow receives website contact form inquiries via Webhook, uses OpenAI to generate a short summary and classify priority (High / Medium / Low), stores the data in Google Sheets, and sends a Gmail notification to the agency team.

## Project Overview

| Item                | Details                                      |
|---------------------|----------------------------------------------|
| Platform            | n8n Cloud (already set up by the client)     |
| AI Provider         | OpenAI API (client provides their own key)   |
| Data Storage        | Google Sheets                                |
| Notifications       | Gmail                                        |
| Input Source        | Existing website contact form via n8n Webhook|
| Priority Levels     | High, Medium, Low                            |
| Deliverables        | Exported n8n workflow JSON + setup guide     |

## Files in this Repository

- **[workflow/n8n-ai-inquiry-organizer.json](workflow/n8n-ai-inquiry-organizer.json)** – Ready-to-import n8n workflow
- **[SETUP-GUIDE.md](SETUP-GUIDE.md)** – Short setup and configuration guide

## Workflow Steps

1. **Webhook** – Receives inquiry data from the website contact form  
2. **Field Extraction** – Standardizes available fields (name, email, message, service)  
3. **OpenAI** – Generates a short summary and assigns High / Medium / Low priority  
4. **Google Sheets** – Saves original inquiry, AI summary, service, priority, and date  
5. **Gmail** – Sends a notification email containing lead details, summary, and priority  
6. **Validation & Error Handling** – Basic checks for missing fields or failed steps  

## Google Sheets Structure

```
Name | Email | Message | Service | AI Summary | Priority | Date
```

Service and Priority are stored in separate columns for easy filtering.

## Scope & Limitations

**Included**
- One n8n workflow
- Webhook input
- OpenAI summary + priority classification
- Google Sheets storage
- Gmail notification (subject includes priority)
- Basic validation & error handling
- Testing with sample inquiries
- Exported workflow JSON + short setup guide

**Excluded**
- WhatsApp / Telegram integration
- CRM integration
- AI voice agents or chatbots
- Website scraping or external lead generation
- Automatic follow-up sequences
- Multiple workflows
- Custom backend / dashboard
- Any paid third-party services beyond the client’s existing accounts

## Quick Start

1. Import `workflow/n8n-ai-inquiry-organizer.json` into your n8n Cloud instance.
2. Follow the steps in **[SETUP-GUIDE.md](SETUP-GUIDE.md)** to connect OpenAI, Google Sheets, and Gmail.
3. Activate the workflow and point your website form to the Webhook URL.

## Notes

- Client maintains their own OpenAI API key, Google Sheets access, and Gmail connection.
- Priority classification is an automated assessment and may not be perfect in every case.
- The workflow is designed to be simple, reliable, and easy to maintain.

## License

Private project – for the client’s internal use.
