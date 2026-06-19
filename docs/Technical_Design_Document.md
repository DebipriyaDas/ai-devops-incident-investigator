# Technical Design Document (TDD)

# AI-Powered DevOps Incident Investigator

Version: MVP v1.0
Author: Debipriya Das
Date: June 2026

---

# 1. Overview

AI-Powered DevOps Incident Investigator is an AI-assisted platform that automates incident triage and postmortem generation by analyzing deployment logs and application failures.

The platform helps DevOps and SRE teams:

* Reduce Mean Time to Resolution (MTTR)
* Identify probable root causes
* Reuse historical knowledge
* Generate postmortems automatically

---

# 2. Technology Stack

## Frontend

* React
* TypeScript
* TanStack Start
* TailwindCSS
* Lovable

## Workflow Engine

* n8n

## AI Layer

* Gemini 2.5 Flash

## Database

* Supabase

## Storage

* Supabase Tables

## PDF Generation

* jsPDF

---

# 3. High-Level Architecture

User Upload

↓

React Frontend

↓

Server Function

↓

n8n Webhook

↓

Gemini AI

↓

Supabase

↓

Response to UI

↓

PDF Generation

---

# 4. Components

## Frontend

Responsibilities:

* Upload logs
* Display AI analysis
* Show history
* Download postmortem PDF

Pages:

### Home

Features:

* Upload log file
* Analyze Incident

### Investigation History

Features:

* List previous investigations
* View details
* Download postmortem

### Incident History

Features:

* Incident repository

---

## Server Functions

### analyzeIncident()

Purpose:

Invoke n8n webhook.

Input:

```json
{
"log": "...",
"file_name": "error.txt"
}
```

Output:

```json
{
"id":"",
"incident_summary":"",
"root_cause":"",
"severity":"",
"recommended_actions":[],
"postmortem":""
}
```

---

## n8n Workflow

Steps:

1. Receive Webhook

↓

2. Parse Log

↓

3. Send Prompt to Gemini

↓

4. Parse JSON Response

↓

5. Insert Into Supabase

↓

6. Fetch Complete Row

↓

7. Respond to Webhook

---

## Gemini AI

Generates:

* Incident Summary
* Category
* Root Cause
* Severity
* Confidence Score
* Historical Insights
* Recommended Resolution
* Recommended Actions
* Full Postmortem

---

# 5. Database Schema

Table:

investigations

Columns:

| Column                 | Type      |
| ---------------------- | --------- |
| id                     | UUID      |
| created_at             | Timestamp |
| file_name              | Text      |
| file_type              | Text      |
| uploaded_log           | Text      |
| incident_summary       | Text      |
| incident_category      | Text      |
| root_cause             | Text      |
| severity               | Text      |
| confidence_score       | Float     |
| recommended_resolution | Text      |
| historical_insights    | Text      |
| recommended_actions    | JSON      |
| postmortem             | Text      |

---

# 6. API Contract

POST

Webhook

Input:

```json
{
"log":"...",
"file_name":"..."
}
```

Output:

```json
{
"id":"uuid",
"incident_summary":"...",
"incident_category":"...",
"root_cause":"...",
"severity":"...",
"confidence_score":0.85,
"recommended_resolution":"...",
"historical_insights":"...",
"recommended_actions":[...],
"postmortem":"..."
}
```

---

# 7. PDF Generation

Sections:

## Metadata

* Incident ID
* Source
* Date
* Severity
* Confidence

## Incident Summary

## Root Cause

## Recommended Resolution

## Recommended Actions

## Historical Insights

## Full Postmortem

---

# 8. Error Handling

### Invalid File

Expected:

Unsupported file error

---

### Empty Log

Expected:

Graceful failure

---

### Gemini Timeout

Expected:

Retry mechanism

---

### Supabase Insert Failure

Expected:

Rollback and error message

---

# 9. Test Scenarios

## Database Timeout

Input

```text
ERROR: Database connection timeout after 30 seconds
```

Expected

Category:

Database

Severity:

Critical

---

## Disk Space Failure

Input

```text
Node out of disk space. Rollout failed.
```

Expected

Category:

Infrastructure

---

## CPU Saturation

Input

```text
Worker node CPU reached 99%
```

Expected

Category:

Performance

---

## Memory Leak

Input

```text
OOMKilled
Container restarted
```

Expected

Category:

Application

---

## Kubernetes CrashLoopBackOff

Input

```text
CrashLoopBackOff
```

Expected

Category:

Container

---

## Redis Connection Failure

Input

```text
Redis connection refused
```

Expected

Category:

Database

---

# 10. Setup Instructions

## Frontend

```bash
npm install
npm run dev
```

---

## n8n

Import workflow

Configure:

* Gemini API key
* Supabase credentials

Activate workflow

---

## Supabase

Create:

investigations table

---

# 11. Security

Current MVP:

* No authentication

Future:

* Supabase Auth
* Row Level Security
* User-specific investigations

---

# 12. Future Enhancements

## Authentication

Google Login

---

## Slack Integration

Incident notifications

---

## Jira Integration

Auto-ticket generation

---

## RAG Search

Similar incidents

---

## Multi-Agent Framework

Specialized agents:

* Log Agent
* Root Cause Agent
* Remediation Agent
* Postmortem Agent

---

## Predictive Intelligence

Deployment risk scoring

---

# 13. Limitations

Current MVP:

* Shared workspace
* No RBAC
* No live monitoring
* No Slack integration
* No real-time alerts

---

# 14. Demo Flow

1. Upload error log

↓

2. Analyze Incident

↓

3. AI generates summary

↓

4. Store investigation

↓

5. Open History

↓

6. Download PDF

---

# 15. Repository Structure

```
src/
public/

docs/
Technical_Design_Document.md

README.md

n8n/
workflow.json

samples/
database_timeout.log
disk_space_error.log
cpu_saturation.log
oom_killed.log
crashloopbackoff.log
redis_failure.log
```
