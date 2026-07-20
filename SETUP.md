# Setup Guide

## 1. Telegram Bot

1. Open Telegram and search for **@BotFather**
2. Send `/newbot` and follow the prompts
3. Copy your **Bot Token**
4. In n8n, create a **Telegram credential** and paste the token

## 2. Groq API

1. Go to [console.groq.com](https://console.groq.com) and sign up
2. Navigate to **API Keys** and generate a new key
3. In n8n, create a **Header Auth credential**:
   - Name: `Authorization`
   - Value: `Bearer YOUR_GROQ_API_KEY`

## 3. Google Drive

1. Go to [Google Cloud Console](https://console.cloud.google.com)
2. Create a new project and enable the **Google Drive API**
3. Create **OAuth2 credentials** (Desktop app)
4. In n8n, create a **Google Drive OAuth2** credential and authenticate
5. Upload your CVs to Google Drive and note their **File IDs**

## 4. Update CV File IDs

Open `workflow.json` and locate the Code node labelled **"Select CV"**. Replace the placeholder File IDs with your actual Google Drive file IDs:

```javascript
const CV_MAP = {
  "AI Automation Engineer": "YOUR_AUTOMATION_CV_FILE_ID",
  "AI Data Trainer": "YOUR_DATA_TRAINER_CV_FILE_ID",
  "Data Analyst": "YOUR_DATA_ANALYST_CV_FILE_ID"
};
```

To find a file ID in Google Drive:
- Right-click the file → **Get link**
- The ID is the long string in the URL between `/d/` and `/view`

## 5. Gmail

1. In n8n, create a **Gmail OAuth2** credential
2. Authenticate with the Google account you want to send applications from
3. Update the **Gmail node** with your sender email

## 6. Update System Prompt Email

In the **Information Extractor** node, update the placeholder email in the system prompt:

```
Replace: your-email@gmail.com
With: your actual application email address
```

## 7. Activate the Workflow

1. Import `workflow.json` into n8n
2. Assign all credentials to their respective nodes
3. Toggle the workflow to **Active**
4. Send a job link or description to your Telegram bot to test

---

## Testing

Send a message to your bot in this format:

```
https://www.linkedin.com/jobs/view/some-job-id
```

Or paste raw job description text directly. The bot will respond with a confirmation once the application is sent.

