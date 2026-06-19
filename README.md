# n8n AI Agents — Healthcare

3 production-ready n8n workflow agents for the healthcare domain, built with GPT-4o. Each agent handles complex, multi-step automation with AI decision-making, batch processing, conditional routing, and automated notifications.

---

## HC-1: Patient Discharge & Care Continuity Agent
**Trigger:** Webhook (POST `/webhook/patient-discharge`)
**Workflow:** EHR discharge event → normalize payload → GPT-4o risk assessment → route by risk level (high/medium/low) → urgent physician alert (Gmail + Slack) / patient follow-up email / log routine care plan
**Use Case:** Prevents 30-day readmissions by instantly triaging discharged patients and alerting the care team for high-risk cases.
**n8n:** https://aravind5.app.n8n.cloud/workflow/sTOHb8MdKbJ1w8tS
**Credentials:** OpenAI API Key · Gmail OAuth2 · Slack OAuth2 · Care API Bearer Token

---

## HC-2: Insurance Prior Authorization Automation Agent
**Trigger:** Webhook (POST `/webhook/prior-auth-request`)
**Workflow:** Auth request → check insurance eligibility → GPT-4o medical necessity assessment → if criteria met: submit to payer + notify provider / else: notify provider of missing docs
**Use Case:** Eliminates manual prior auth paperwork. AI evaluates clinical notes against payer guidelines and auto-submits when criteria are met.
**n8n:** https://aravind5.app.n8n.cloud/workflow/PcioiEXandyi4DhB
**Credentials:** OpenAI API Key · Gmail OAuth2 · Payer API Bearer Token

---

## HC-3: Clinical Trial Recruitment & Screening Agent
**Trigger:** Schedule (Daily at 8:00 AM)
**Workflow:** Fetch active patients → split + batch → GPT-4o eligibility screening → send personalized outreach email to eligible / log ineligible to CRM
**Use Case:** Automates patient recruitment for clinical trials by screening entire patient populations against inclusion/exclusion criteria daily.
**n8n:** https://aravind5.app.n8n.cloud/workflow/jnaNp7WZAlQw6v8o
**Credentials:** OpenAI API Key · Gmail OAuth2 · EHR API Bearer Token · Trial CRM Bearer Token

---

## Tech Stack
- **Platform:** n8n (cloud or self-hosted)
- **AI:** OpenAI GPT-4o via `@n8n/n8n-nodes-langchain.agent` v3.1
- **Structured Output:** `@n8n/n8n-nodes-langchain.outputParserStructured` v1.3
- **Notifications:** Gmail v2.2, Slack v2.5
- **Patterns:** SplitInBatches + nextBatch, SplitOut, ifElse, switchCase

## Setup
1. Import each JSON into your n8n instance
2. Replace placeholder URLs (marked `<__PLACEHOLDER_VALUE__...>`) with your actual endpoints
3. Configure credentials listed per agent above
4. Activate the workflow
