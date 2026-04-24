# AI Job Application Automation System

An end-to-end intelligent job application pipeline that automates job discovery, evaluates job relevance using AI, customizes resumes per role, generates PDFs, and tracks applications — built using n8n, LLMs, and cloud integrations.


*N8N Image:*

<img width="1193" height="229" alt="image" src="https://github.com/user-attachments/assets/fc4dada8-f752-4fc2-9129-94debdab192e" />



*Output Results:*

<img width="1364" height="662" alt="image" src="https://github.com/user-attachments/assets/06f6f9da-f10f-4400-8122-1f8e2017d15d" />

<img width="1366" height="646" alt="image" src="https://github.com/user-attachments/assets/c5a8cc92-c4ed-43be-b28c-91d9d3a30e8c" />

---

# Table of Contents

1. Overview
2. Features
3. Workflow Architecture
4. System Design Breakdown
5. Folder Structure
6. How to Run Locally
7. Workflow Logic (Step-by-Step)
8. AI Pipeline Design
9. Resume Generation Engine
10. Data Tracking System
11. Challenges & Trade-offs
12. Security & Limitations
13. Performance Considerations
14. Future Improvements

---

# Overview

Modern job hunting suffers from three core inefficiencies:

* Manual application process
* Low-quality resume targeting
* Lack of tracking system

This project solves all three by building a **fully automated job application engine**.

The system:

* Scrapes jobs from LinkedIn
* Filters them using AI
* Customizes resumes per job
* Generates ready-to-send PDFs
* Tracks all applications

---

# Features

## 1. Automated Job Discovery

* Uses Apify LinkedIn scraper
* Filters by:

  * Keywords
  * Location
  * Recency

---

## 2. AI Job Relevance Filtering

* Compares:

  * Resume
  * Job description
* Uses LLM to decide:

  * `true` → apply
  * `false` → skip

---

## 3. Resume Personalization Engine

* Dynamically rewrites resume per job
* Maintains structured format
* Improves ATS compatibility

---

## 4. Resume Rendering Pipeline

* Markdown → structured format → HTML → PDF
* Clean, minimal, recruiter-friendly layout

---

## 5. Cloud Storage Integration

* Uploads resumes to Google Drive
* Auto-naming based on company/job

---

## 6. Application Tracking System

* Logs data into Google Sheets:

  * Job title
  * Company
  * Apply link
  * Resume link
  * Description

Acts as a lightweight ATS.

---

# Workflow Architecture

```id="arch1"
[Manual Trigger]
      ↓
[LinkedIn Search URL Input]
      ↓
[Apify Scraper]
      ↓
[Batch Processing Loop]
      ↓
[Fetch Resume (Google Docs)]
      ↓
[AI Fit Evaluation]
      ↓
[Filter Relevant Jobs]
      ↓
[AI Resume Generation]
      ↓
[HTML Builder (JS Engine)]
      ↓
[PDF Conversion API]
      ↓
[Google Drive Upload]
      ↓
[Google Sheets Logging]
```

---

# System Design Breakdown

### Core Components

| Component       | Role                          |
| --------------- | ----------------------------- |
| n8n             | Workflow orchestration        |
| Apify           | Job scraping                  |
| OpenAI LLM      | Filtering + resume generation |
| Google Docs     | Resume source                 |
| JavaScript Node | HTML rendering                |
| PDF API         | Document conversion           |
| Google Drive    | Storage                       |
| Google Sheets   | Tracking                      |

---

# Folder Structure

```
ai-job-application-automation/
│
├── workflows/
│   └── job-automation.json
│
├── docs/
│   └── architecture.md
│
└── README.md
```

---

# How to Run Locally

## 1. Import Workflow

* Open n8n
* Import JSON from `/workflows`

---

## 2. Configure Credentials

Required:

* Apify API
* OpenAI API
* Google Docs API
* Google Drive API
* Google Sheets API
* PDF API

---

## 3. Update Parameters

Modify:

* LinkedIn search URL
* Resume document
* Drive folder ID
* Sheet ID

---

## 4. Execute Workflow

* Run manually or schedule
* System will process jobs automatically

---

# Workflow Logic (Step-by-Step)

## Step 1: Job Scraping

* Input: LinkedIn search URL
* Output: job listings

---

## Step 2: Batch Processing

* Jobs processed in batches
* Prevents overload

---

## Step 3: Resume Fetch

* Pulls master resume from Google Docs

---

## Step 4: AI Filtering

Prompt logic:

* Compare resume vs job description
* Output boolean decision

---

## Step 5: Conditional Filtering

* Only relevant jobs pass through

---

## Step 6: Resume Customization

LLM rewrites:

* Experience
* Projects
* Skills

Based on job

---

## Step 7: HTML Generation

Custom JS parser:

* Converts structured text → HTML
* Ensures clean formatting

---

## Step 8: PDF Conversion

* HTML → PDF via API

---

## Step 9: Storage

* Upload PDF to Google Drive

---

## Step 10: Tracking

* Append job data into Google Sheets

---

# AI Pipeline Design

## Two-stage intelligence

### Stage 1: Filtering

* Binary classification
* Avoids irrelevant applications

---

### Stage 2: Resume Generation

* Context-aware rewriting
* Improves alignment with job

---

## Key Insight

This mimics a **human recruiter + applicant hybrid system**:

* Evaluate → Decide → Customize → Apply

---

# Resume Generation Engine

### Input:

* Raw resume
* Job description

### Output:

Structured resume:

```
NAME
CONTACT
EXPERIENCE
PROJECTS
SKILLS
EDUCATION
```

---

### Transformation Flow

```
Resume → LLM → Structured Markdown → JS Parser → HTML → PDF
```

---

# Data Tracking System

Google Sheets acts as:

* Application database
* Progress tracker
* Audit log

---

# Challenges & Trade-offs

## 1. Scraping Reliability

* Dependent on LinkedIn + Apify

---

## 2. LLM Accuracy

* May misclassify job fit

---

## 3. Resume Quality

* Prompt-sensitive

---

## 4. API Dependencies

* Multiple external services

---

## 5. No Auto-Apply Yet

* System stops before submission

---

# Security & Limitations

* API keys stored in n8n credentials
* No sensitive data should be hardcoded
* Rate limits may affect execution

---

# Performance Considerations

* Batch processing reduces overload
* LLM calls are main bottleneck
* PDF generation latency present

---

# Future Improvements

## Short-term

* Retry logic for failed jobs
* Better prompt engineering
* Logging system

---

## Medium-term

* Auto-apply integration
* Email alerts
* Resume version control

---

## Long-term

* Dashboard UI
* Multi-profile support
* Skill-gap analysis
* Reinforcement learning for better job matching

---

# Key Insight

This project demonstrates how:

**LLMs + workflow automation = scalable human decision systems**

---

# Author

Deepak Joshi
AI Systems Builder | Automation Engineer

---

