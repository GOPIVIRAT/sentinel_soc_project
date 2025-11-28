## 📘 Auto-Close Informational & Low Incidents Playbook
## 📌 Overview ##

This Logic App playbook is designed to automatically close Informational & Low incidents in Microsoft Sentinel.
It works together with an Automation Rule that triggers the playbook whenever a new incident with Severity = Informational is created.

This reduces noise, removes non-actionable alerts, and helps SOC analysts focus on high-value incidents.

## 🎯 Purpose ##

Automatically close low-value Informational incidents

Reduce manual workload for SOC analysts

Maintain a clean incident queue

Improve SOC efficiency and response time

## ⚙️ How It Works (Workflow) ##

An Automation Rule checks each newly created incident.

If the severity is Informational, the rule triggers this playbook.

## The playbook: ##

Retrieves the incident details

Updates the incident status → Closed

Adds a closing comment

Tags the incident (optional)

No manual action required by the SOC team.

## 🧩 Playbook Logic (Steps Inside Logic App) ##

Trigger: “When an incident is created”

Get Incident Details

Update Incident

Status → Closed

Closing Reason → Benign Positive / Resolved

Comment → “Automatically closed: Informational incident (noise reduction).”

## Screenshots ##

in the incident page you can see there was alert which is informational 
<img width="1116" height="396" alt="image" src="https://github.com/user-attachments/assets/957fca61-d59a-4b15-9178-f783bf4eba96" />
Then i was able to create a playbook in the logic app to close the incident
<img width="951" height="465" alt="image" src="https://github.com/user-attachments/assets/cb28b626-e641-4a6c-ab37-0c2689633597" />
Then i was able to write a automation rule when ever new incident came with severity low & Information close that incident 
<img width="1110" height="594" alt="image" src="https://github.com/user-attachments/assets/0f2fa7e9-58fe-4702-8f7c-e5009dc97655" />
Then i have written a query to attach this automation rule you can see that in the screenshot
<img width="1040" height="434" alt="image" src="https://github.com/user-attachments/assets/e0d8feda-9ef6-44fe-a0e1-dfbeffa32e57" />
Then you can see That my incident was automatically investigated and resolved by the automation rule
<img width="406" height="125" alt="image" src="https://github.com/user-attachments/assets/f9d6940c-eeea-4bcb-9b2b-9502ad889afb" />


