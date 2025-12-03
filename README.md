# ServiceNow & n8n Integration: VIP Lead Escalation

This project demonstrates a **Low-Code Automation Workflow** designed to bridge the gap between Marketing Operations (CRM) and IT Service Management (ServiceNow).

## 🎯 Business Problem
High-value clients often report critical issues via marketing forms (HubSpot/Pipedrive) rather than the official Support Portal. These emails often get lost in the Sales inbox, leading to delayed response times and SLA breaches.

## 🛠️ The Solution
I architected an automated workflow using **n8n** that listens for incoming high-priority leads and instantly creates a tracked Incident in ServiceNow.

### Tech Stack
- **ServiceNow REST Table API**: For creating Incident records (`incident` table).
- **n8n (Workflow Automation)**: To orchestrate the logic.
- **JSON/Webhooks**: To parse the incoming data payload.

### Workflow Logic
1.  **Webhook Trigger**: Receives payload from CRM form submission.
2.  **Condition Logic**: Checks if `priority == 'high'`.
3.  **API Action**:
    - POST to `https://instance.service-now.com/api/now/table/incident`
    - Maps `email` -> `caller_id`
    - Maps `message` -> `short_description`
    - Sets `urgency` -> `1` (Critical)
4.  **Slack Notification**: Alerts the Account Manager instantly.

## 🚀 How to Use
Import the `workflow.json` file directly into your n8n instance to see the node configuration.
