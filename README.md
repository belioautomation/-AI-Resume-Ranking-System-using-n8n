# 📄 AI Resume Ranking System — n8n Automation

![n8n](https://img.shields.io/badge/n8n-Automation-orange)
![Google Gemini](https://img.shields.io/badge/AI-Google%20Gemini-blue)
![JavaScript](https://img.shields.io/badge/Code-JavaScript-yellow)
![License](https://img.shields.io/badge/license-MIT-green)

An AI-powered recruitment automation workflow built using **n8n**, **Google Gemini AI**, **Google Drive**, **Google Sheets**, and **Telegram Bot API**.

This system automatically monitors uploaded resumes, extracts candidate information from PDF files, evaluates applicants using artificial intelligence, assigns qualification scores, ranks candidates, stores evaluation results, and sends recruiter notifications for qualified applicants.

**Stack:**  
n8n · Google Drive · Google Gemini AI · Google Sheets · Telegram Bot · JavaScript · Google Workspace API · AI Automation


---

# 🎯 Project Overview


## Problem

Manual resume screening creates several challenges for recruiters:

- Reviewing hundreds of resumes takes significant time
- Candidate information must be extracted manually
- Comparing applicant qualifications is difficult
- Ranking candidates requires repetitive evaluation
- Tracking applicant results becomes complicated


Common recruitment tasks affected:

- Resume filtering
- Candidate ranking
- Interview selection
- Applicant tracking
- Hiring decisions


---

## Solution

This project creates an AI-powered resume screening pipeline that automatically:


1. Monitors a Google Drive resume folder
2. Detects newly uploaded PDF resumes
3. Extracts resume text automatically
4. Analyzes candidate information using Google Gemini AI
5. Generates candidate scores and recommendations
6. Classifies applicants based on qualification level
7. Stores evaluation results in Google Sheets
8. Sends Telegram notifications for qualified candidates


The workflow works as an automated AI recruitment assistant that helps recruiters identify strong candidates faster.


---

# ✨ Features


## Resume Processing

✅ Automatic Google Drive monitoring  
✅ Resume upload detection  
✅ PDF document processing  
✅ Resume text extraction  
✅ Candidate information extraction  


## Artificial Intelligence

✅ Google Gemini AI resume analysis  
✅ Candidate qualification scoring  
✅ Skill and experience evaluation  
✅ AI-generated candidate summaries  
✅ Interview recommendation generation  


## Data Management

✅ Google Sheets candidate database  
✅ Structured evaluation records  
✅ JSON-based AI output processing  
✅ Automated candidate ranking  


## Notifications

✅ Telegram recruiter alerts  
✅ Qualified candidate notifications  
✅ Real-time workflow updates  


---

# 🗺️ System Architecture


```mermaid
flowchart TD

A["📂 Resume Upload"]

--> B["📁 Google Drive Folder"]

B --> C["⚙️ Google Drive Trigger"]

C --> D["📥 Download Resume PDF"]

D --> E["📄 Extract Resume Text"]

E --> F["🤖 Google Gemini AI"]

F --> G["📝 JavaScript JSON Parser"]

G --> H{"⭐ Score >= 80?"}

H -->|YES| I["🏆 Qualified Candidate"]

H -->|NO| J["📌 Needs Review"]

I --> K["📊 Google Sheets"]

J --> K

I --> L["📱 Telegram Notification"]

````

---

# 🏗️ Workflow Implementation

# Workflow 1: AI Resume Evaluation Pipeline

## Node 1 — Google Drive Trigger

### Purpose

Monitor a Google Drive folder and detect newly uploaded resume files.

Configuration:

```text
Trigger:

Google Drive Trigger


Event:

File Created


Folder:

Job Applications
```

Captured Information:

| Field       | Description             |
| ----------- | ----------------------- |
| File Name   | Resume filename         |
| File ID     | Google Drive identifier |
| File Type   | PDF document            |
| Upload Time | Creation timestamp      |

---

# Node 2 — Download Resume File

### Purpose

Retrieve the uploaded resume file from Google Drive for processing.

Input:

```text
Resume PDF File
```

Output:

```text
Binary PDF Data
```

The downloaded file is passed to the extraction stage.

---

# Node 3 — Extract Resume Text

### Purpose

Convert PDF resume documents into readable text data.

Extracted Information:

| Field          | Description              |
| -------------- | ------------------------ |
| Name           | Candidate name           |
| Email          | Contact email            |
| Education      | Academic background      |
| Skills         | Technical abilities      |
| Experience     | Previous work experience |
| Certifications | Professional credentials |

Example:

```text
Name:

John Doe


Education:

BS Information Technology


Skills:

Python, Networking, Windows


Experience:

2 Years IT Support
```

---

# Node 4 — Google Gemini AI Agent

### Purpose

Analyze extracted resume information and evaluate candidate suitability.

Evaluation Criteria:

* Educational background
* Technical skills
* Professional experience
* Certifications
* Overall candidate quality

Example AI Output:

```json
{
"name":"John Doe",

"email":"john@example.com",

"education":
"BS Information Technology",

"experience":
"2 Years IT Support",

"skills":[
"Python",
"Networking",
"Windows"
],

"certifications":[
"CompTIA A+"
],

"score":88,

"rank":
"Qualified Candidate",

"recommendation":
"Interview",

"summary":
"Strong IT support candidate with relevant technical skills."
}
```

---

# Node 5 — Code Node (JSON Parser)

### Purpose

Convert Gemini AI response into structured workflow data.

Processing:

```text
Gemini AI Response

        ↓

JavaScript JSON Parsing

        ↓

Structured Candidate Data
```

Output:

```json
{
"name":"John Doe",
"score":88,
"rank":"Qualified Candidate",
"recommendation":"Interview"
}
```

---

# Node 6 — IF Node

### Purpose

Determine whether the candidate qualifies for recruiter notification.

Condition:

```javascript
{{$json.score >= 80}}
```

## TRUE Branch

Qualified Candidate:

Actions:

* Save candidate evaluation
* Send Telegram notification

## FALSE Branch

Needs Review:

Actions:

* Save candidate evaluation
* Wait for manual review

---

# Node 7 — Google Sheets

### Purpose

Store candidate evaluation results.

Database Structure:

| Field          | Description          |
| -------------- | -------------------- |
| Timestamp      | Evaluation date      |
| Name           | Candidate name       |
| Email          | Candidate email      |
| Education      | Academic background  |
| Skills         | Technical skills     |
| Experience     | Work history         |
| Score          | AI evaluation score  |
| Rank           | Candidate category   |
| Recommendation | Hiring suggestion    |
| Summary        | AI-generated summary |

Example:

| Name     | Score | Rank                |
| -------- | ----- | ------------------- |
| John Doe | 88    | Qualified Candidate |

---

# Node 8 — Telegram Notification

### Purpose

Notify recruiters when highly qualified candidates are detected.

Example:

```text
📄 Qualified Candidate Detected


👤 Name:

John Doe


⭐ Score:

88 / 100


🏆 Rank:

Qualified Candidate


📌 Recommendation:

Interview


📝 Summary:

Strong IT support candidate with relevant technical skills.


🤖 Evaluated automatically using Google Gemini AI.
```

---

# 🔐 Credentials Required

| Service           | Purpose                        |
| ----------------- | ------------------------------ |
| Google OAuth2     | Google Drive and Sheets access |
| Google Gemini API | AI resume evaluation           |
| Telegram Bot API  | Recruiter notifications        |
| n8n Instance      | Workflow execution             |

---

# ⚙️ Setup Guide

## 1. Create Google Drive Resume Folder

Create:

```text
Job Applications
```

Upload resume PDF files inside this folder.

---

## 2. Configure Google Credentials

Enable:

```text
Google Drive API

Google Sheets API
```

Connect OAuth credentials inside n8n.

---

## 3. Configure Google Gemini AI

Add Gemini credentials:

```text
Google Gemini API Key
```

Test AI resume evaluation response.

---

## 4. Configure Telegram Bot

Steps:

1. Open Telegram
2. Search BotFather
3. Create a new bot
4. Copy bot token
5. Add Telegram credentials in n8n
6. Configure recruiter chat ID

---

## 5. Import Workflow

Import:

```text
workflow.json
```

Configure:

* Google Drive folder
* Google Sheets database
* Gemini credentials
* Telegram credentials

Activate workflow.

---

# 🧪 Testing Checklist

| Test Case              | Expected Result            |
| ---------------------- | -------------------------- |
| Upload PDF resume      | Workflow starts            |
| Resume extraction runs | Text generated             |
| Gemini analyzes resume | Candidate score created    |
| Score >= 80            | Telegram notification sent |
| Score < 80             | Saved for review           |
| Google Sheets updated  | Candidate logged           |

---

# 📁 Repository Structure

```text
AI-Resume-Ranking-System/

│
├── README.md
│
├── workflow.json
│
├── screenshots/
│   │
│   ├── workflow.png
│   ├── google-drive-trigger.png
│   ├── resume-extraction.png
│   ├── gemini-output.png
│   ├── code-node-output.png
│   ├── if-node-execution.png
│   ├── google-sheets.png
│   ├── telegram-notification.png
│   └── execution-result.png
│
└── assets/
    │
    └── sample-output.json
```

---

# 📸 Screenshots

Recommended screenshots:

* Complete n8n workflow
* Google Drive Trigger configuration
* Resume extraction output
* Gemini AI evaluation result
* JSON parser output
* IF Node branching
* Google Sheets records
* Telegram notification
* Workflow execution

---

# 🚀 Future Improvements

| Feature                | Implementation                         |
| ---------------------- | -------------------------------------- |
| DOCX Resume Support    | Add Word document parser               |
| AI Interview Generator | Generate technical interview questions |
| Candidate Comparison   | AI ranking dashboard                   |
| Email Scheduling       | Gmail interview invitations            |
| LinkedIn Integration   | Candidate profile analysis             |
| Duplicate Detection    | Resume fingerprinting                  |
| HR Dashboard           | Looker Studio analytics                |
| ATS Integration        | Recruitment platform connection        |

---

# 🎓 Skills Applied

## Automation

* n8n Workflow Automation
* Event-driven workflows
* Recruitment process automation

## Artificial Intelligence

* Google Gemini AI
* Prompt Engineering
* AI evaluation systems
* Structured AI outputs

## APIs

* Google Drive API
* Google Sheets API
* Telegram Bot API

## Programming

* JavaScript
* JSON processing
* Data transformation
* Conditional workflow logic

## Business Automation

* Applicant tracking automation
* Recruitment workflow optimization
* AI-assisted decision systems

---

# 📚 Learning Objectives

This project demonstrates:

* Building AI-powered recruitment automation
* Integrating document processing workflows
* Using LLMs for candidate evaluation
* Creating structured AI outputs
* Designing scalable n8n automation systems

---

# 🙌 Acknowledgements

* n8n
* Google Gemini AI
* Google Drive API
* Google Sheets API
* Telegram Bot API

---

# 👨‍💻 Author

**Belio C. Sinangote**

BS Information Technology Student
Cebu Technological University (CTU)

GitHub:

[https://github.com/belioautomation](https://github.com/belioautomation)

This project is part of my **30-Day n8n Automation Portfolio**, showcasing practical AI-powered automation solutions using **n8n, APIs, JavaScript, and Google Gemini AI**.

---

# 📄 License

MIT License

```
```
