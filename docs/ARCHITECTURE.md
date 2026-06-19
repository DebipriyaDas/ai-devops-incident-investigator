# Architecture

## Overview

AI-Powered DevOps Incident Investigator helps DevOps and SRE teams analyze deployment failures and generate incident reports automatically.

The solution consists of:

* Frontend (Lovable + React)
* Workflow Orchestration (n8n)
* AI Analysis (Gemini 2.5 Flash)
* Database (Supabase)
* PDF Postmortem Generator

---

## High-Level Flow

```
User uploads log
        ↓
Frontend (Lovable)
        ↓
Server Function
        ↓
n8n Webhook
        ↓
Gemini AI Analysis
        ↓
Supabase investigations table
        ↓
Respond to Webhook
        ↓
Frontend renders analysis
        ↓
Generate PDF Postmortem
```

---

## Components

### Frontend

Built using:

* Lovable
* React
* TypeScript

Pages:

* Home
* Investigation History
* Incident History
* Details Modal

---

### n8n Workflow

Nodes:

1. Webhook
2. Parse Input
3. Gemini Prompt
4. JSON Parser
5. Supabase Insert
6. Respond to Webhook

---

### AI Layer

Gemini 2.5 Flash generates:

* Incident Summary
* Root Cause
* Severity
* Confidence Score
* Historical Insights
* Recommended Actions
* Full Postmortem

---

### Database

Supabase table:

```
investigations
```

Stores:

* uploaded_log
* incident_summary
* root_cause
* severity
* confidence_score
* recommended_resolution
* historical_insights
* recommended_actions
* postmortem

---

### PDF Generator

Produces:

* Summary
* Root Cause
* Resolution
* Recommendations
* Historical Insights
* Full Postmortem
