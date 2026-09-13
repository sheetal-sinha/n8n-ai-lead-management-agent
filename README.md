# n8n-ai-lead-management-agent
# 🤖 AI Lead Management & Problem Analysis Agent

An AI-powered lead management and problem analysis automation built with **n8n**.

This workflow accepts a user's problem through an n8n form, analyzes the submitted issue using an AI Agent, assigns an importance score from **1–10**, generates a contextual AI suggestion, validates the information, stores the lead in **Google Sheets**, and automatically notifies the responsible team.

The workflow is designed to demonstrate how **AI Agents, workflow automation, data validation, Google Sheets, and automated notifications** can be combined into a practical end-to-end automation system.

---

## 📌 Table of Contents

- [Overview](#-overview)
- [Problem Statement](#-problem-statement)
- [Solution](#-solution)
- [Key Features](#-key-features)
- [Workflow Architecture](#-workflow-architecture)
- [How It Works](#-how-it-works)
- [AI Agent Responsibilities](#-ai-agent-responsibilities)
- [Priority Scoring System](#-priority-scoring-system)
- [Google Sheets Integration](#-google-sheets-integration)
- [Notification System](#-notification-system)
- [Input and Output](#-input-and-output)
- [Example](#-example)
- [Technology Stack](#-technology-stack)
- [Project Structure](#-project-structure)
- [Installation](#-installation)
- [n8n Configuration](#-n8n-configuration)
- [Importing the Workflow](#-importing-the-workflow)
- [Environment & Credentials](#-environment--credentials)
- [Testing](#-testing)
- [Error Handling](#-error-handling)
- [Security](#-security)
- [Limitations](#-limitations)
- [Future Improvements](#-future-improvements)
- [Use Cases](#-use-cases)
- [Learning Outcomes](#-learning-outcomes)
- [Screenshots](#-screenshots)
- [Contributing](#-contributing)
- [License](#-license)
- [Author](#-author)

---

# 🔎 Overview

The **AI Lead Management & Problem Analysis Agent** is an automation workflow created using **n8n**.

The system is designed to reduce manual work involved in receiving, analyzing, prioritizing, recording, and forwarding user problems.

Instead of manually reviewing every incoming request, the workflow automatically:

1. Receives the user's submission.
2. Extracts the user's email and problem.
3. Sends the information to an AI Agent.
4. Analyzes the problem.
5. Assigns a priority score.
6. Generates an AI-based suggestion.
7. Validates the generated information.
8. Stores the lead in Google Sheets.
9. Notifies the appropriate team.
10. Returns a structured execution result.

---

# 🎯 Problem Statement

Organizations often receive user requests through forms, emails, or support channels.

Manually processing every request can result in:

- Delayed responses
- Inconsistent prioritization
- Repetitive manual work
- Difficulty tracking incoming leads
- Missed high-priority requests
- Lack of centralized lead information
- Time-consuming communication between teams

A simple form submission does not provide enough structure for a team to immediately understand:

> "How important is this problem, what should be done next, and who needs to know about it?"

This project addresses that problem by introducing an **AI-powered automated analysis and lead-management layer**.

---

# 💡 Solution

The workflow combines:

- **n8n Forms** for collecting user submissions
- **AI Agent** for problem analysis
- **LLM** for reasoning and suggestion generation
- **Validation logic** for data quality
- **Google Sheets** for lead storage
- **Notification Tool** for automated team communication

The result is an end-to-end automated pipeline:

```text
User Submission
       ↓
n8n Form
       ↓
AI Agent
       ↓
Problem Analysis
       ↓
Priority Score
       ↓
AI Suggestion
       ↓
Validation
       ↓
Google Sheets
       ↓
Notification
       ↓
Team / Doctor


<img width="1102" height="525" alt="image" src="https://github.com/user-attachments/assets/bff80e49-4da7-4a99-aeeb-339a7f479fa0" />

