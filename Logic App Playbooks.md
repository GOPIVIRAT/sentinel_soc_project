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

# 🔐 User Creation Detection + Entra ID Disable/Enable Playbook
**📌 Overview**

This workflow detects when a specific user account is created (example: virat@gopisid…) and automatically disables or enables the user using a Logic App playbook.
Simple, clear, and useful for SOC identity response.

**🔄 Workflow Summary (Easy to Understand)**

**1️⃣ User Created in Entra ID**

A new user is created.
Example detected in logs:

Operation: Add user

Target User: virat@…

Created By: gopisiddams@…

Result: success

**2️⃣ Analytics Rule – Detect User Creation**

A custom Analytics Rule runs a KQL query to detect when a user named Virat (or any new user) is added.

Sample KQL:
<img width="983" height="359" alt="image" src="https://github.com/user-attachments/assets/388f2b93-fdf2-49e5-bb1f-e15175e71f67" />

If the TargetUser matches the condition, the rule triggers an incident.

**3️⃣ Playbook – Disable or Enable the User**

The Logic App playbook performs:

Disable user → accountEnabled = false

Enable user → accountEnabled = true

Adds a comment to the incident

Updates SOC team

Uses Managed Identity + Graph API

This helps automate response to suspicious or unwanted user creation.

**Screenshot with Explanation:**

**First in entra id i am creating the new user virat you can see that in the screenshot**
 <img width="480" height="529" alt="image" src="https://github.com/user-attachments/assets/160fe122-a316-4a82-bab9-8da3811af41b" />
 
**Then i was able to write a kql query that will effectiverly detect these type of attacks**
<img width="963" height="344" alt="image" src="https://github.com/user-attachments/assets/76abad64-7aac-4095-9709-29a3b8abb8be" />

**I am saving the rule New User created**
<img width="1084" height="558" alt="image" src="https://github.com/user-attachments/assets/e9db0514-ee6a-4c7d-8d0a-c20351f1db73" />


**we can see in the incident page the rule was triggered**
<img width="1114" height="336" alt="image" src="https://github.com/user-attachments/assets/efbdad9c-b1e2-4a89-a43a-936e1e7a6cf5" />

**Then i was able to build a playbook to enable or disable these type of incidents**
<img width="1110" height="483" alt="image" src="https://github.com/user-attachments/assets/1943d41e-c8ac-4886-b851-77ef85a03376" />

<img width="387" height="464" alt="image" src="https://github.com/user-attachments/assets/034f6463-ab54-458b-b0c5-bf0a473cb3dc" />

**its time to run our playbook on the incident**
<img width="1349" height="473" alt="image" src="https://github.com/user-attachments/assets/f7b4efae-d482-49c9-8747-90bc08b1d3f5" />

**After running the playbooks we can be able to enable and disable the users**
<img width="1362" height="556" alt="image" src="https://github.com/user-attachments/assets/98e37302-a5e9-4948-922d-36a91ed34533" />
<img width="1169" height="456" alt="image" src="https://github.com/user-attachments/assets/fe4c7889-5e97-44f3-b465-0fcfd688f6f3" />






















