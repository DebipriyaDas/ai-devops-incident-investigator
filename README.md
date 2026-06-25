![React](https://img.shields.io/badge/Frontend-React-blue)
![TypeScript](https://img.shields.io/badge/Language-TypeScript-blue)
![Supabase](https://img.shields.io/badge/Database-Supabase-green)
![n8n](https://img.shields.io/badge/Automation-n8n-orange)
![Gemini](https://img.shields.io/badge/LLM-Gemini-red)
![Status](https://img.shields.io/badge/Status-MVP-success)

## Demo Link- https://drive.google.com/file/d/1z6N9eqD15d47l0vuIsuoWxte0bSaque5/view?usp=drive_link

# AI-Powered DevOps Incident Investigator

An AI-assisted DevOps and SRE incident investigation platform that analyzes deployment logs, identifies probable root causes, surfaces historical incidents, recommends remediation actions, and automatically generates postmortem reports.

---

## Overview

Modern DevOps teams spend significant time manually investigating deployment failures and production incidents.

The AI-Powered DevOps Incident Investigator automates:

* Log analysis
* Root cause identification
* Historical incident retrieval
* Remediation recommendations
* Postmortem generation

The system reduces Mean Time to Resolution (MTTR) and provides a reusable incident knowledge base.

---

## Features

### Incident Analysis

* Upload log files (.txt, .log, .xml)
* AI-generated incident summary
* Root cause analysis
* Severity classification
* Confidence score

### Historical Incident Intelligence

* Stores investigations in Supabase
* Investigation History page
* Incident History page
* Searchable incident repository

### Recommended Actions

* AI-generated remediation suggestions
* Preventive actions
* Operational recommendations

### Automated Postmortem Generation

Generates:

* Summary
* Timeline
* Root Cause
* Resolution
* Preventive Actions

### PDF Export

Download a professional postmortem report including:

* Incident metadata
* Root cause
* Recommendations
* Historical insights
* Complete postmortem document

---

# Architecture

```
User
  |
  v
Lovable Frontend
(React + TanStack)
  |
  v
Server Functions
  |
  v
n8n Workflow
  |
  v
Google Gemini 2.5 Flash
  |
  v
Supabase
(investigations table)
```

---

# Tech Stack

## Frontend

* Lovable
* React
* TanStack Start
* TypeScript

## Workflow Engine

* n8n

## AI Model

* Google Gemini 2.5 Flash

## Database

* Supabase

## Export

* jsPDF

---

# Project Structure

```
src/
├── routes/
│   ├── index.tsx
│   ├── history.tsx
│   └── incidents.tsx
│
├── lib/
│   ├── incidents.functions.ts
│   ├── investigations.functions.ts
│   ├── normalize.ts
│   └── postmortem.ts
│
├── integrations/
│   └── supabase/
│
└── components/
```

---

# Workflow

## 1. Upload Log

User uploads:

```
ERROR.txt
```

Example:

```
ERROR: Database connection timeout after 30 seconds
```

---

## 2. n8n Workflow

Performs:

1. Receive log
2. Call Gemini
3. Generate:

* Incident summary
* Root cause
* Severity
* Recommendations
* Postmortem

4. Insert into Supabase
5. Return inserted row to UI

---

## 3. Display Analysis

UI shows:

* Incident Summary
* Root Cause
* Severity
* Confidence Score
* Historical Insights
* Recommended Actions

---

## 4. Store Investigation

Saved inside:

```
investigations
```

table in Supabase.

---

## Database Schema

Table:

```
investigations
```

Columns:

| Column                 | Type      |
| ---------------------- | --------- |
| id                     | uuid      |
| created_at             | timestamp |
| file_name              | text      |
| file_type              | text      |
| uploaded_log           | text      |
| incident_summary       | text      |
| incident_category      | text      |
| root_cause             | text      |
| severity               | text      |
| confidence_score       | numeric   |
| recommended_resolution | text      |
| historical_insights    | text      |
| recommended_actions    | jsonb     |
| postmortem             | text      |

---

# Pages

## Home

Upload logs and analyze incidents.

---

## Investigation History

Displays all investigations stored in Supabase.

Capabilities:

* View details
* Download postmortem PDF

---

## Incident History

Alternative incident-centric view of the same investigation repository.

---

# Example Input

```
ERROR: Database connection timeout after 30 seconds
```

---

# Example Output

### Incident Summary

Deployment aborted due to database connection timeout.

### Root Cause

Database server unresponsiveness.

### Severity

Critical

### Recommended Resolution

Investigate database health and connectivity.

### Recommended Actions

* Verify database availability.
* Check network connectivity.
* Review database logs.
* Implement monitoring.
* Add pre-deployment health checks.

---

# Sample Postmortem

```
Summary

Timeline

Root Cause

Resolution

Preventive Actions
```

---

# Future Enhancements

### V2

* Slack integration
* Jira ticket creation
* Advanced RAG search
* Confidence explanations

### V3

* Multi-agent incident investigation
* Trend analysis
* Incident clustering

### V4

* Auto-remediation
* Deployment risk prediction
* AI Incident Command Center

---

# Success Metrics

Target outcomes:

* 50% reduction in investigation time
* <30 seconds analysis latency
* 80% root cause accuracy
* Improved MTTR

---

# Author

Debipriya Das

Product Manager | AI Enthusiast | DevOps AI Solutions
