# 🤖 AI Lead Management & Problem Analysis Agent

An intelligent and  end-to-end lead ingestion, issue analysis, priority scoring, Google Sheets logging, and automated notification workflow built with **n8n**, **Google Gemini AI**, and **Gmail**.

[![n8n](https://img.shields.io/badge/Automation-n8n-FF6D5A?style=for-the-badge&logo=n8n)](https://n8n.io)
[![Google Gemini](https://img.shields.io/badge/AI%20Engine-Google%20Gemini-4285F4?style=for-the-badge&logo=googlegemini)](https://ai.google.dev/)
[![Google Sheets](https://img.shields.io/badge/Database-Google%20Sheets-34A853?style=for-the-badge&logo=googlesheets)](https://docs.google.com/spreadsheets)
[![Gmail](https://img.shields.io/badge/Notifications-Gmail-EA4335?style=for-the-badge&logo=gmail)](https://mail.google.com)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](LICENSE)

---

## 📌 Table of Contents

- [Overview](#-overview)
- [Project Folder Structure](#-project-folder-structure)
- [Screenshots & Visual Demos](#-screenshots--visual-demos)
- [Workflow Architecture](#-workflow-architecture)
- [Key Features](#-key-features)
- [AI Priority Scoring Matrix](#-ai-priority-scoring-matrix)
- [Quick Start & Setup](#-quick-start--setup)
- [Documentation](#-documentation)
- [License](#-license)

---

## 🔎 Overview

The **AI Lead Management & Problem Analysis Agent** eliminates manual review overhead for incoming customer/patient inquiries. 

When a user submits a problem statement through an n8n form, the system automatically:
1. **Parses & Validates** user input payload (Email & Problem Statement).
2. **Analyzes Issue Complexity** using a LangChain-powered AI Agent with Google Gemini LLM..
3. **Assigns a Priority Score (1–10)** based on urgency, impact, and risk.
4. **Generates Practical AI Suggestions** tailored specifically to the problem.
5. **Appends Validated Lead Data** directly into a master **Google Sheets** database.
6. **Triggers Email Alerts** via **Gmail** to notify responding teams/doctors for high-priority items.
7. 

---

## 📁 Project Folder Structure

```text
n8n-ai-lead-management-agent/
│
├── 📂 workflows/
│   └── ai_lead_management_workflow.json  # Complete n8n workflow export (Ready to import)
│
├── 📂 screenshots/
│   ├── 01_n8n_workflow_canvas.png        # Screenshot of the active n8n workflow canvas
│   ├── 02_lead_capture_form.png          # Screenshot of the customer-facing lead capture form
│   └── 03_google_sheets_output.png       # Screenshot of populated Google Sheets database
│
├── 📂 docs/
│   ├── WORKFLOW.md                       # Detailed node architecture & execution rules
│   └── SETUP_GUIDE.md                    # Step-by-step setup, OAuth, & credential guide
│
├── .gitignore                            # Standard git ignore rules
├── LICENSE                               # MIT License file
└── README.md                             # Project documentation & overview
```

---

## 📸 Screenshots & Visual Demos

### 1. n8n Workflow Canvas
*Visual representation of the end-to-end node architecture combining Form Trigger, LangChain AI Agent, Gemini Chat Model, Google Sheets Tool, and Notify Tool.*

![n8n Workflow Canvas](./screenshots/01_n8n_workflow_canvas.png)

---

### 2. Lead Capture Form
*The clean user submission form collecting the lead's email and issue details.*

![Lead Capture Form](./screenshots/02_lead_capture_form.png)

---

### 3. Google Sheets Output
*Master lead log updating automatically with Lead Email, Problem Statement, Priority Score (1-10), and AI Suggestion.*

![Google Sheets Output](./screenshots/03_google_sheets_output.png)

---

## ⚙️ Workflow Architecture

```text
[ User Submission ] 
       │
       ▼
 ┌───────────────┐
 │ n8n Form      │ (Lead Email & Problem)
 └───────┬───────┘
         │
         ▼
 ┌───────────────┐      ┌─────────────────────────┐
 │ AI Agent Core │ ◄──► │ Google Gemini Chat Model│
 └───────┬───────┘      └─────────────────────────┘
         │ (Analyzes & Scores 1-10)
         ├────────────────────────┐
         ▼                        ▼
 ┌───────────────┐        ┌───────────────┐
 │ Google Sheets │        │  Gmail Notify │
 │ (Store Lead)  │ ──►──► │  (Team Alert) │
 └───────────────┘        └───────────────┘
```

---

## 🎯 AI Priority Scoring Matrix

| Priority Score | Severity Level | System Response & Escalation |
|:---:|:---|:---|
| **1 – 4** | Low / Moderate-Low | Logged to Google Sheets; normal response queue. |
| **5 – 6** | Moderate | Logged to Google Sheets; standard guidance generated. |
| **7 – 8** | High | Logged to Google Sheets; **HIGH PRIORITY** email alert sent to team. |
| **9 – 10** | Critical / Emergency | Logged to Google Sheets; **CRITICAL ALERT** instant notification triggered. |

---

## 🚀 Quick Start & Setup

1. **Clone the repository**:
   ```bash
   git clone https://github.com/your-username/n8n-ai-lead-management-agent.git
   cd n8n-ai-lead-management-agent
   ```
2. **Import the workflow into n8n**:
   - Open n8n → **Workflows** → **Import from File**.
   - Choose `workflows/ai_lead_management_workflow.json`.
3. **Configure Credentials**:
   - Set up your **Google Gemini API Key**.
   - Connect **Google Sheets OAuth2** credential and set your Google Sheet ID.
   - Connect **Gmail OAuth2** credential for notification delivery.
4. For detailed step-by-step setup instructions, check out [docs/SETUP_GUIDE.md](./docs/SETUP_GUIDE.md).

---

## 📚 Documentation

- 📄 **[Workflow & Node Breakdown](./docs/WORKFLOW.md)**: In-depth technical specifications of prompt engineering, validation logic, and execution order.
- 🛠️ **[Setup & Deployment Guide](./docs/SETUP_GUIDE.md)**: Prerequisites, OAuth connection, and testing guide.

---

## 📜 License

Distributed under the MIT License. See [`LICENSE`](./LICENSE) for more information.
