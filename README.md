# Telegram Job Application Bot 🤖

An AI-powered Telegram bot built with **n8n** that automates the entire job application process. Drop a job link or paste job details into Telegram — the bot picks the right CV, writes a tailored application email, and sends it automatically.

---

## What It Does

1. **Receives input via Telegram** — accepts a job URL or raw job description text
2. **Detects input type** — checks if the message is a URL or plain text and routes accordingly
3. **Scrapes job details** — if a URL is provided, fetches the page content automatically
4. **Selects the right CV** — picks the most relevant CV from Google Drive based on the role:
   - AI Automation Engineer
   - AI Data Trainer
   - Data Analyst
5. **Writes a tailored application email** — Groq (LLaMA 3.3-70b-versatile) crafts a professional, recruitment-standard email based on the job requirements and selected CV
6. **Sends the application** — dispatches the email with the CV attached via Gmail
7. **Confirms via Telegram** — sends a confirmation message with role, CV used, and recipient email

---

## Tech Stack

| Tool | Purpose |
|------|---------|
| n8n | Workflow orchestration |
| Telegram Bot API | User interface / trigger |
| Groq (LLaMA 3.3-70b-versatile) | AI email generation |
| Google Drive | CV storage and retrieval |
| Gmail | Sending application emails |

---

## Workflow Architecture

```
Telegram Trigger
      │
      ▼
Parse Input (Code Node)
      │
      ▼
Is it a URL? (IF Node)
   │         │
  YES        NO
   │         │
   ▼         ▼
Fetch URL   Use raw text
   │         │
   └────┬────┘
        ▼
  Select CV (Code Node)
        │
        ▼
  Extract Application Email (Groq via Information Extractor)
        │
        ▼
  Build Output (Code Node)
        │
        ▼
  Download CV from Google Drive
        │
        ▼
  Send Email via Gmail
        │
        ▼
  Confirm via Telegram
```

---

## Prerequisites

- n8n instance (self-hosted or cloud)
- Telegram Bot (create via [@BotFather](https://t.me/BotFather))
- Groq API key ([console.groq.com](https://console.groq.com))
- Google Drive OAuth2 credentials
- Gmail OAuth2 credentials

---

## Setup

See [SETUP.md](./SETUP.md) for full step-by-step configuration instructions.

---

## Importing the Workflow

1. Open your n8n instance
2. Go to **Workflows → Import from File**
3. Select `workflow.json`
4. Configure credentials for each node (see SETUP.md)
5. Activate the workflow

---

## Deployment

This bot is self-hosted on [Render.com](https://render.com). For deployment instructions, refer to the n8n self-hosting docs and configure your Telegram webhook URL to point to your Render instance.

---

## Author

Built by **Precious Agu** — AI Automation Engineer  
Part of a 7-project n8n automation portfolio.

