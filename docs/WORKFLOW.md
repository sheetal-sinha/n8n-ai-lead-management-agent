# ⚙️ Workflow Architecture & Node Breakdown

This document provides a technical deep-dive into the **AI Lead Management & Problem Analysis Agent** built on n8n.

---

## 📐 System Flow Diagram

```text in this
[ User Form Submission ]
           │
           ▼
┌──────────────────────┐
│  On Form Submission  │  <-- (Form Trigger Node) given flow diagram
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│       AI Agent       │  <-- (LangChain Agent Core)
└──────┬───┬───┬───────┘
       │   │   │
       │   │   └────────────────────────────────┐
       │   └────────────────────┐               │
       ▼                        ▼               ▼
┌──────────────┐     ┌──────────────────┐  ┌──────────┐
│ Gemini LLM   │     │ Google Sheets    │  │ Notify   │
│ (Chat Model) │     │ (Data Storage)   │  │ (Gmail)  │
└──────────────┘     └──────────────────┘  └──────────┘
```

---

## 🧩 Node Breakdown

### 1. On Form Submission (`n8n-nodes-base.formTrigger`)
- **Purpose**: Collects input directly from users via an auto-generated n8n form web link.
- **Fields**:
  - `What is your email address?` (Required, String)
  - `What is your required problem statement ?` (Required, Text Area)
- **Output**: Transmits user submission payload (`email`, `problem`, `submittedAt`) to the downstream AI Agent.

### 2. AI Agent (`@n8n/n8n-nodes-langchain.agent`)
- **Purpose**: Acts as the central reasoning engine. It executes system prompts, enforces strict data validation rules, evaluates priority scores, and orchestrates tool invocations.
- **Core Responsibilities**:
  1. Parse problem input and lead email.
  2. Compute an **Importance Score (1–10)**.
  3. Generate actionable, non-hallucinated **AI Suggestions**.
  4. Perform data validation on email format and numerical scores.
  5. Call **Google Sheets Tool** to record lead data.
  6. Call **Notify Tool** to send email alerts to responders/doctors.

### 3. Google Gemini Chat Model (`@n8n/n8n-nodes-langchain.lmChatGoogleGemini`)
- **Model**: `gemini-pro-latest` / `gemini-1.5-pro`
- **Role**: Provides the underlying large language model (LLM) reasoning capacity for natural language understanding and priority evaluation.

### 4. Google Sheet Tool (`n8n-nodes-base.googleSheetsTool`)
- **Action**: `appendOrUpdate`
- **Target Sheet**: `Lead Spreadsheet` (`Sheet1`)
- **Mapped Columns**:
  - **Lead Email**: `{{ $fromAI('Email') }}`
  - **Problem**: `{{ $fromAI('Problem_') }}`
  - **Score**: `{{ $fromAI('Score') }}` (Pure numeric integer 1–10)
  - **AI Suggestion**: `{{ $fromAI('AI_Suggestion') }}`

### 5. Notify Tool (`n8n-nodes-base.gmailHitlTool` / `gmailTool`)
- **Action**: Sends structured email via Gmail OAuth2.
- **Recipient**: Team/Doctor notification address.
- **Priority Escalation**:
  - **Score ≥ 8**: Escalated with `PRIORITY: HIGH — Prompt attention required.`
  - **Score = 10**: Escalated with `PRIORITY: CRITICAL — Immediate attention required.`

---

## 📊 Priority Scoring System

| Score | Priority Level | Criteria & Description | Action Required |
|:---:|:---|:---|:---|
| **1 – 2** | Low | Minor inquiry or general question. | Standard logging |
| **3 – 4** | Moderate-Low | Non-urgent request or feedback. | Queue for review |
| **5 – 6** | Moderate | Operational issue causing mild inconvenience (e.g. 3-day headache, minor bug). | Log & send standard guidance |
| **7 – 8** | High | Severe issue causing operational blocking or significant distress. | Priority notification to team |
| **9 – 10** | Critical | Emergency / Outage / Severe medical or system threat. | Immediate alert & escalation |

---

## 🔒 Validation Rules

Before tools are invoked, the AI Agent executes internal checks:
- **Email Validation**: Must follow valid pattern `@domain.extension` and non-empty.
- **Score Validation**: Must be strictly an integer between `1` and `10` (no text suffixes like "8/10").
- **Sequence Guarantee**: Google Sheets entry **MUST** complete successfully before the Notify Tool is called.
