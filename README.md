# n8n AI Agents — Healthcare, Transportation & Construction

9 production-ready n8n workflow agents built with GPT-4o across three domains. Each agent handles complex, multi-step automation with AI decision-making, batch processing, conditional routing, and automated notifications.

---

## Healthcare Agents

### HC-1: Patient Discharge & Care Continuity Agent
**Trigger:** Webhook (POST `/webhook/patient-discharge`)  
**Workflow:** EHR discharge event → normalize payload → GPT-4o risk assessment → route by risk level (high/medium/low) → urgent physician alert (Gmail + Slack) / patient follow-up email / log routine care plan  
**Use Case:** Prevents 30-day readmissions by instantly triaging discharged patients and alerting the care team for high-risk cases.  
**n8n:** https://aravind5.app.n8n.cloud/workflow/sTOHb8MdKbJ1w8tS

### HC-2: Insurance Prior Authorization Automation Agent
**Trigger:** Webhook (POST `/webhook/prior-auth-request`)  
**Workflow:** Auth request → check insurance eligibility → GPT-4o medical necessity assessment → if criteria met: submit to payer + notify provider / else: notify provider of missing docs  
**Use Case:** Eliminates manual prior auth paperwork. AI evaluates clinical notes against payer guidelines and auto-submits when criteria are met.  
**n8n:** https://aravind5.app.n8n.cloud/workflow/PcioiEXandyi4DhB

### HC-3: Clinical Trial Recruitment & Screening Agent
**Trigger:** Schedule (Daily at 8:00 AM)  
**Workflow:** Fetch active patients → split + batch → GPT-4o eligibility screening (INNOVATE-DM2 Phase III criteria) → send personalized outreach email to eligible / log ineligible to CRM  
**Use Case:** Automates patient recruitment for clinical trials by screening entire patient populations against inclusion/exclusion criteria daily.  
**n8n:** https://aravind5.app.n8n.cloud/workflow/jnaNp7WZAlQw6v8o

---

## Transportation Agents

### TR-4: Fleet Predictive Maintenance Agent
**Trigger:** Schedule (Every hour)  
**Workflow:** Fetch fleet telematics → split vehicles → batch → GPT-4o analyze DTC codes + sensor readings → if maintenance needed: schedule service + Slack alert / else: log healthy status  
**Use Case:** Predicts vehicle failures before they happen using real-time telemetry (engine temp, oil pressure, brake wear, DTC codes).  
**n8n:** https://aravind5.app.n8n.cloud/workflow/WXXRgxylUgXEykTx

### TR-5: Dynamic Route Optimization & Exception Agent
**Trigger:** Schedule (Every 15 minutes)  
**Workflow:** Fetch active deliveries → batch → fetch live traffic/weather → GPT-4o assess delay impact → if significant delay: update route + notify driver (Gmail) + notify customer / else: log on-time  
**Use Case:** Real-time delivery monitoring that auto-reroutes drivers and proactively notifies customers when traffic or weather causes delays.  
**n8n:** https://aravind5.app.n8n.cloud/workflow/Z1WNtgrFm3DesCmj

### TR-6: Freight Exception & Carrier Resolution Agent
**Trigger:** Schedule (Every hour)  
**Workflow:** Fetch in-transit shipments → batch → GPT-4o classify exception severity (critical/standard/low) → critical: create case + alert account manager + notify customer / standard: create case + notify customer / low: log  
**Use Case:** Automatically manages freight exceptions by severity. High-value shipments get immediate account manager escalation; low-priority issues are silently logged.  
**n8n:** https://aravind5.app.n8n.cloud/workflow/trGcBqL5lylqqmjF

---

## Construction Agents

### C-7: Site Safety Compliance & OSHA Reporting Agent
**Trigger:** Schedule (Daily)  
**Workflow:** Fetch inspection reports → batch → GPT-4o analyze violations against 29 CFR 1926 → if OSHA reportable: file incident report + alert PM / else: log minor violation + notify PM  
**Use Case:** Automates OSHA compliance by classifying violations, calculating fines, determining required forms (300/301/300A), and auto-filing incident reports with corrective action plans.  
**n8n:** https://aravind5.app.n8n.cloud/workflow/yV1moFLC09gC4g6C

### C-8: Subcontractor Invoice Reconciliation & Payment Agent
**Trigger:** Schedule (Weekly)  
**Workflow:** Fetch pending invoices → batch → fetch contract SOV → GPT-4o reconcile line items + check compliance docs + calculate retainage → if approved: create ERP payment voucher + notify sub / else: flag + notify sub of discrepancies  
**Use Case:** Eliminates manual invoice review. AI checks every line item against the Schedule of Values, validates lien waivers and certified payroll, and calculates correct retainage.  
**n8n:** https://aravind5.app.n8n.cloud/workflow/lQhFarz4A38f2flj

### C-9: Material Procurement & Supply Forecasting Agent
**Trigger:** Schedule (Daily)  
**Workflow:** Fetch project schedules + inventory levels → split projects → batch → GPT-4o analyze material requirements vs stock + supplier lead times → if shortages: create bulk POs + alert PM / else: log adequate supply + send daily summary  
**Use Case:** Prevents schedule delays by daily cross-referencing upcoming material needs against inventory, factoring in supplier lead times and auto-generating urgent purchase orders.  
**n8n:** https://aravind5.app.n8n.cloud/workflow/aby1Dzm36hwcWkHM

---

## Tech Stack

- **Platform:** n8n (self-hosted or cloud)
- **AI:** OpenAI GPT-4o via `@n8n/n8n-nodes-langchain.agent` v3.1
- **Structured Output:** `@n8n/n8n-nodes-langchain.outputParserStructured` v1.3
- **Notifications:** Gmail v2.2, Slack v2.5
- **Integrations:** HTTP Request v4.4 (configurable API endpoints via placeholder URLs)
- **Patterns:** SplitInBatches + nextBatch, SplitOut, ifElse, switchCase

## Setup

1. Import each workflow JSON into your n8n instance
2. Replace placeholder API URLs (marked `<__PLACEHOLDER_VALUE__...>`) with your actual endpoints
3. Configure credentials: OpenAI API Key, Gmail OAuth2, Slack OAuth2, and any domain-specific API keys
4. Activate workflows

## Credentials Required (per agent — see individual files)

- `OpenAI API Key` — all agents
- `Gmail OAuth2` — all agents
- `Slack OAuth2` — HC-1, TR-4
- Domain-specific API keys for EHR, TMS, CRM, ERP, fleet telematics, safety platforms, etc.
