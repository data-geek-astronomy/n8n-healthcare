# n8n Healthcare AI Agents

> 3 production-ready n8n workflow agents that automate patient discharge management, insurance prior authorization, and clinical trial recruitment.

![status](https://img.shields.io/badge/status-production--ready-brightgreen)
![license](https://img.shields.io/badge/license-MIT-blue)
![built with](https://img.shields.io/badge/built%20with-n8n%20%2B%20GPT--4o-orange)

---

## ✨ Agents

### HC-1: Patient Discharge & Care Continuity
**Trigger:** Webhook POST → EHR fires on discharge

> **Problem:** Hospitals like Mayo Clinic and Kaiser Permanente manually triage thousands of discharged patients daily, missing high-risk cases until readmission occurs.
> **Built:** A real-time webhook agent that scores every discharge using GPT-4o and routes alerts to physicians, patients, and care teams automatically.
> **Solved:** Reduces 30-day readmission rates by ensuring high-risk patients receive a physician call within hours, not days.

```
EHR Discharge Event
      ↓
Normalize Payload
      ↓
GPT-4o Risk Assessment
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

**Use Cases:**
- **Kaiser Permanente** — automate post-discharge follow-up for cardiac patients
- **HCA Healthcare** — flag CHF and COPD patients for same-day nurse callback
- **Telehealth platforms (Teladoc)** — trigger virtual follow-up scheduling on discharge

**n8n:** https://aravind5.app.n8n.cloud/workflow/sTOHb8MdKbJ1w8tS

---

### HC-2: Insurance Prior Authorization Automation
**Trigger:** Webhook POST → from EHR/provider portal

> **Problem:** Providers at hospitals like Cleveland Clinic spend 2+ hours per day submitting prior auth requests manually, delaying patient procedures by days.
> **Built:** A webhook agent that evaluates clinical notes against payer criteria using GPT-4o and auto-submits approvals to the insurance API.
> **Solved:** Cuts prior auth turnaround from 2–3 days to under 30 seconds for eligible requests.

```
Auth Request Webhook
      ↓
Normalize + Check Eligibility
      ↓
GPT-4o Medical Necessity Assessment
      ↓
  Criteria Met?
   Yes      No
    ↓        ↓
Submit    Notify Provider
to Payer  (missing docs)
```

✅ Evaluates clinical notes against payer guidelines
✅ Auto-submits when criteria are met
✅ Returns missing documentation checklist to provider

**Use Cases:**
- **UnitedHealth Group** — auto-process high-volume ortho and imaging prior auths
- **Aetna / CVS Health** — reduce manual review queue for routine outpatient procedures
- **Epic-integrated clinics** — trigger from Epic SmartForms directly into payer APIs

**n8n:** https://aravind5.app.n8n.cloud/workflow/PcioiEXandyi4DhB

---

### HC-3: Clinical Trial Recruitment & Screening
**Trigger:** Schedule → runs daily at 8:00 AM

> **Problem:** Research teams at Pfizer and Moderna manually screen patient charts to find trial candidates, a process that takes weeks and misses eligible patients.
> **Built:** A daily batch agent that screens the entire active patient population against trial inclusion/exclusion criteria using GPT-4o.
> **Solved:** Compresses weeks of manual chart review into a nightly run, surfacing eligible candidates with personalized outreach the next morning.

```
Daily Scheduler
      ↓
Fetch Active Patients (EHR)
      ↓
Split + Batch
      ↓
GPT-4o Eligibility Screening
      ↓
  Eligible?
  Yes    No
   ↓      ↓
Send    Log to
Outreach  CRM
Email
```

✅ Screens full patient population daily
✅ Sends personalized outreach to eligible patients
✅ Logs all results (eligible + ineligible) to trial CRM

**Use Cases:**
- **Pfizer** — automate Phase III diabetes trial recruitment across partner clinics
- **Medidata / Veeva** — integrate screening output directly into CTMS platforms
- **Academic Medical Centers (Johns Hopkins)** — run nightly screens across multiple concurrent trials

**n8n:** https://aravind5.app.n8n.cloud/workflow/jnaNp7WZAlQw6v8o

---

## 🚀 Quick Start

### Prerequisites
- n8n cloud account
- OpenAI API key (GPT-4o)
- Gmail OAuth2 credentials
- Slack OAuth2 credentials (HC-1 only)

### Deploy
1. Import the JSON file into your n8n instance
2. Replace `<__PLACEHOLDER_VALUE__...>` URLs with your actual API endpoints
3. Configure credentials per the table below
4. Activate the workflow

| Agent | Credentials |
|-------|-------------|
| HC-1  | OpenAI · Gmail · Slack · Care API |
| HC-2  | OpenAI · Gmail · Payer API |
| HC-3  | OpenAI · Gmail · EHR API · Trial CRM API |

---

## 🧑‍💻 Author
**Aravind Kumar** · GitHub: [@data-geek-astronomy](https://github.com/data-geek-astronomy)
Portfolio: Building AI agents for enterprise automation

## 📄 License
MIT
