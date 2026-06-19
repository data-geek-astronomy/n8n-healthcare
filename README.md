# n8n Healthcare AI Agents

> 3 production-ready n8n workflow agents that automate patient discharge management, insurance prior authorization, and clinical trial recruitment.

![status](https://img.shields.io/badge/status-production--ready-brightgreen)
![license](https://img.shields.io/badge/license-MIT-blue)
![built with](https://img.shields.io/badge/built%20with-n8n%20%2B%20GPT--4o-orange)

---

## 🎯 Problem Statement

Healthcare teams spend hours on manual tasks that delay patient care:
- Reviewing discharge risk and coordinating follow-ups
- Filling out prior authorization forms for insurance
- Manually screening patients for clinical trials

These agents automate all three workflows end-to-end.

---

## ✨ Agents

### HC-1: Patient Discharge & Care Continuity
**Trigger:** Webhook POST → EHR fires on discharge

```
EHR Discharge Event
      ↓
Normalize Payload
      ↓
GPT-4o Risk Assessment (30-day readmission score)
      ↓
    Router
   /  |  \
High  Med  Low
 ↓         ↓
Alert     Log
Physician  Care Plan
+ Slack
```

✅ Risk-stratifies every discharge in real-time
✅ Alerts physician + Slack for high-risk patients
✅ Sends follow-up email to medium-risk patients

**n8n:** https://aravind5.app.n8n.cloud/workflow/sTOHb8MdKbJ1w8tS

---

### HC-2: Insurance Prior Authorization Automation
**Trigger:** Webhook POST → from EHR/provider portal

```
Auth Request Webhook
      ↓
Normalize Request
      ↓
Check Insurance Eligibility (API)
      ↓
GPT-4o Medical Necessity Assessment
      ↓
  Criteria Met?
   Yes      No
    ↓        ↓
Submit    Notify Provider
to Payer  (missing docs)
+ Notify
Provider
```

✅ Evaluates clinical notes against payer guidelines
✅ Auto-submits when criteria are met
✅ Returns missing documentation checklist to provider

**n8n:** https://aravind5.app.n8n.cloud/workflow/PcioiEXandyi4DhB

---

### HC-3: Clinical Trial Recruitment & Screening
**Trigger:** Schedule → runs daily at 8:00 AM

```
Daily Scheduler
      ↓
Fetch Active Patients (EHR)
      ↓
Split + Batch (1 at a time)
      ↓
GPT-4o Eligibility Screening
(INNOVATE-DM2 Phase III criteria)
      ↓
  Eligible?
  Yes    No
   ↓      ↓
Send    Log to
Outreach  CRM
Email   (screened out)
+ Log CRM
```

✅ Screens full patient population daily
✅ Sends personalized outreach to eligible patients
✅ Logs all results (eligible + ineligible) to trial CRM

**n8n:** https://aravind5.app.n8n.cloud/workflow/jnaNp7WZAlQw6v8o

---

## 🚀 Quick Start

### Prerequisites
- n8n cloud account (free tier works)
- OpenAI API key (GPT-4o)
- Gmail account for notifications
- Slack workspace (HC-1 only)

### Deploy
1. Import the relevant JSON file into your n8n instance
2. Replace placeholder URLs (`<__PLACEHOLDER_VALUE__...>`) with your API endpoints
3. Add credentials (see below)
4. Activate the workflow

### Credentials Required

| Agent | Credentials |
|-------|-------------|
| HC-1  | OpenAI, Gmail, Slack, Care API |
| HC-2  | OpenAI, Gmail, Payer API |
| HC-3  | OpenAI, Gmail, EHR API, Trial CRM API |

---

## 🧑‍💻 Author
**Aravind Kumar** · GitHub: [@data-geek-astronomy](https://github.com/data-geek-astronomy)

## 📄 License
MIT
