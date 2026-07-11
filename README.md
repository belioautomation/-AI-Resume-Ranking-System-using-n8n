# 📄 AI Resume Ranking System — n8n Automation

An AI-powered recruitment automation workflow built using **n8n**, **Google Gemini AI**, **Google Drive**, **Google Sheets**, and **Telegram Bot API**.

The system automatically monitors a resume upload folder, extracts candidate information from PDF files, evaluates applicants using AI, assigns qualification scores, ranks candidates, stores evaluation results, and notifies recruiters about qualified applicants.

**Stack:**  
n8n · Google Drive · Google Gemini AI · Google Sheets · Telegram Bot · JavaScript · Google Workspace API


---

# 🎯 Project Overview

## Problem

Manual resume screening is time-consuming for recruiters because they need to:

- Review hundreds of resumes
- Extract candidate information manually
- Compare qualifications
- Rank applicants
- Track evaluation results


## Solution

This project automates the recruitment screening process by creating an AI-powered pipeline:

1. Recruiter uploads resumes to Google Drive
2. n8n detects new resume files automatically
3. Resume text is extracted from PDF files
4. Google Gemini AI analyzes candidate qualifications
5. AI generates candidate scores and recommendations
6. Applicants are categorized based on score
7. Results are stored in Google Sheets
8. Telegram sends notifications for qualified candidates


---

# ✨ Features

## Resume Processing

✅ Automatic Google Drive monitoring  
✅ PDF resume detection  
✅ Resume text extraction  
✅ Structured candidate information extraction  


## AI Evaluation

✅ Google Gemini AI resume analysis  
✅ Candidate scoring system  
✅ Qualification ranking  
✅ Interview recommendation generation  
✅ AI-generated candidate summary  


## Automation

✅ n8n trigger-based workflow  
✅ Automated Google Sheets logging  
✅ Telegram recruiter notifications  
✅ JSON-based structured AI output  


---

# 🗺️ System Architecture


```mermaid
flowchart TD

A["📂 Resume Upload"]
--> B["Google Drive Folder"]

B --> C["⚙️ n8n Google Drive Trigger"]

C --> D["📥 Download Resume"]

D --> E["📄 Extract PDF Text"]

E --> F["🤖 Google Gemini AI"]

F --> G["📝 Parse JSON Output"]

G --> H{"⭐ Score >= 80?"}

H -->|Yes| I["🏆 Qualified Candidate"]

H -->|No| J["📌 Needs Review"]

I --> K["📊 Google Sheets"]

J --> K

I --> L["📱 Telegram Notification"]
````

---

# 🏗️ Workflow Implementation

# Workflow 1: AI Resume Evaluation Pipeline

## Node 1 — Google Drive Trigger

### Purpose

Detect newly uploaded resume files.

Configuration:

```
Trigger:
Google Drive Trigger

Event:
File Created

Folder:
Job Applications
```

---

# Node 2 — Download File

### Purpose

Downloads the uploaded resume from Google Drive for processing.

Input:

```
Resume PDF File
```

Output:

```
Binary PDF Data
```

---

# Node 3 — Extract From File

### Purpose

Extracts readable text from PDF resumes.

Example extracted data:

```
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

# Node 4 — Google Gemini AI

### Purpose

Analyze resume information and generate candidate evaluation.

Evaluation Criteria:

* Education
* Technical Skills
* Work Experience
* Certifications
* Overall Candidate Quality

Example AI Response:

```json
{
"name":"John Doe",

"email":"john@example.com",

"education":
"Bachelor of Science in Information Technology",

"experience":
"2 years IT Support",

"skills":[
"Networking",
"Python",
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

# Node 5 — Code Node

### Purpose

Convert AI-generated JSON output into structured n8n data.

Processing:

```
Gemini Response
        |
        ▼
JSON Parser
        |
        ▼
Structured Candidate Data
```

---

# Node 6 — IF Node

### Purpose

Determine candidate qualification status.

Condition:

```javascript
{{$json.score >= 80}}
```

Branches:

## TRUE

Qualified Candidate

Actions:

* Save candidate data
* Send Telegram notification

## FALSE

Needs Review

Actions:

* Save candidate data
* No notification

---

# Node 7 — Google Sheets

Stores evaluated candidate information.

## Qualified Candidates

Candidates with:

```
Score >= 80
```

## Needs Review

Candidates with:

```
Score < 80
```

---

# Node 8 — Telegram Notification

Sends recruiter alerts for qualified candidates.

Example:

```
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


🤖 Evaluated automatically using Google Gemini.
```

---

# 📊 Database Structure

## Google Sheets — Candidate Evaluation Log

| Field          | Description           |
| -------------- | --------------------- |
| Timestamp      | Evaluation date       |
| Name           | Candidate name        |
| Email          | Candidate email       |
| Phone          | Contact number        |
| Education      | Academic background   |
| Skills         | Technical skills      |
| Experience     | Work experience       |
| Score          | AI evaluation score   |
| Rank           | Candidate category    |
| Recommendation | Hiring recommendation |
| Summary        | AI-generated summary  |

---

# 🔐 Credentials Required

| Service       | Purpose                        |
| ------------- | ------------------------------ |
| Google OAuth2 | Google Drive and Sheets access |
| Gemini API    | AI resume evaluation           |
| Telegram API  | Notifications                  |
| n8n Instance  | Workflow execution             |

---

# ⚙️ Setup Guide

## 1. Create Google Drive Folder

Create a folder:

```
Job Applications
```

Upload resumes inside this folder.

---

## 2. Configure Google Credentials

Enable:

* Google Drive API
* Google Sheets API

Connect OAuth credentials inside n8n.

---

## 3. Configure Gemini AI

Add Gemini API credentials:

```
Google Gemini API Key
```

Test AI response generation.

---

## 4. Configure Telegram Bot

Steps:

1. Open Telegram
2. Search BotFather
3. Create new bot
4. Copy token
5. Add credentials in n8n

---

## 5. Import n8n Workflow

Import:

```
workflow.json
```

Configure:

* Google Drive folder
* Google Sheets spreadsheet
* Gemini API
* Telegram credentials

Activate workflow.

---

# 🧪 Testing Checklist

| Test Case               | Expected Result            |
| ----------------------- | -------------------------- |
| Upload PDF resume       | Workflow starts            |
| PDF extraction runs     | Resume text generated      |
| Gemini evaluates resume | Score generated            |
| Score >= 80             | Telegram notification sent |
| Score < 80              | Saved as review candidate  |
| Google Sheets updated   | Candidate logged           |

---

# 📁 Repository Structure

```
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
│   ├── extract-from-file.png
│   ├── gemini-output.png
│   ├── code-node.png
│   ├── if-node.png
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

* Complete n8n Workflow
* Google Drive Trigger
* Resume Extraction Output
* Gemini AI Evaluation
* JSON Parser Result
* IF Node Branching
* Google Sheets Results
* Telegram Notification
* Workflow Execution

---

# 🚀 Future Improvements

| Feature                | Implementation                   |
| ---------------------- | -------------------------------- |
| DOCX Resume Support    | Add DOCX parser                  |
| AI Interview Generator | Generate questions automatically |
| Candidate Comparison   | AI ranking dashboard             |
| Email Scheduling       | Gmail integration                |
| LinkedIn Extraction    | Profile analysis                 |
| Duplicate Detection    | Resume fingerprinting            |
| HR Dashboard           | Looker Studio integration        |
| ATS Integration        | Connect recruitment platforms    |

---

# 🎓 Skills Applied

## Automation

* n8n Workflow Automation
* Event-driven workflows
* Process automation

## Artificial Intelligence

* Google Gemini AI
* Prompt Engineering
* AI Evaluation Systems

## Programming

* JavaScript
* JSON Processing
* Data Transformation

## APIs

* Google Drive API
* Google Sheets API
* Telegram Bot API

---

# 📚 Learning Objectives

This project demonstrates:

* Building AI-powered business automation
* Integrating AI models into workflows
* Processing documents automatically
* Creating recruitment automation systems
* Designing scalable n8n pipelines

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

This project is part of my **30-Day n8n Automation Portfolio**, showcasing practical AI-powered workflow automation using n8n, APIs, JavaScript, and Google Gemini AI.

---

# 📄 License

MIT License

```

This version now matches your **Smart Attendance Monitoring System README style**, making your repositories look like a consistent automation engineer portfolio.
```
