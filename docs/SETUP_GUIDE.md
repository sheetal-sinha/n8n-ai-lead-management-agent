# 🛠️ Setup & Installation Guide

This guide will help you set up and deploy the **AI Lead Management & Problem Analysis Agent** in your own n8n instance.

---

## 📋 Prerequisites

Before starting, ensure you have:
1. An active **n8n** instance (Cloud or Self-Hosted version 1.0+).
2. A **Google Gemini API Key** (from Google AI Studio).
3. A **Google Cloud Platform (GCP)** project with Google Sheets API and Gmail API enabled (for OAuth credentials).

---

## 🚀 Step-by-Step Setup

### Step 1: Import the Workflow
1. Open your n8n dashboard.
2. Click **Workflows** → **Add Workflow**.
3. Click the top-right **⋮ (Menu)** → **Import from File**.
4. Select `workflows/ai_lead_management_workflow.json` from this repository.

### Step 2: Configure Credentials

#### 1. Google Gemini API Account
- Click on the **Google Gemini Chat Model** node.
- Under **Credential for Google Gemini(PaLM) Api**, select **Create New Credential**.
- Enter your **API Key** obtained from Google AI Studio.
- Save credential.

#### 2. Google Sheets OAuth2 Account
- Click on the **Google Sheet Tool** node.
- Under **Credential for Google Sheets OAuth2 API**, create/select your credential.
- Create a target Google Sheet named `Lead Spreadsheet` with the following column headers in Row 1:
  - `Lead Email`
  - `Problem`
  - `Score`
  - `AI Suggestion`
- Copy your Spreadsheet ID from the URL and update the `Document ID` field in the node properties.

#### 3. Gmail OAuth2 Account
- Click on the **Notify Tool** node.
- Select/Create your Gmail OAuth2 credential.
- Set the default recipient email address for notification delivery.

### Step 3: Test and Activate
1. Click **Test Workflow** in n8n.
2. Open the form URL provided by the **On Form Submission** trigger node.
3. Fill out a sample email and problem statement, then click **Submit**.
4. Verify that:
   - The lead appears in your Google Sheet.
   - An email notification is sent via Gmail.
5. Switch the workflow toggle to **Active** for live production use.
