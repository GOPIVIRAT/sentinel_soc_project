# 🧩 Attacking & Detecting — Onboarding Phase

## 🔹 Overview
Before starting the attack and detection phase, I first onboarded my machines into Microsoft Sentinel to ensure that all logs and telemetry are centrally collected for monitoring and analysis.

---

### 💻 Onboarding Personal Laptop (Azure Arc) & Azure Virtual Machine
I started by onboarding my **personal Windows laptop** using **Azure Arc**, which connects non-Azure machines to the Azure environment.  
I installed the **Azure Connected Machine Agent** and linked the device to my **Log Analytics Workspace** that is already connected to Microsoft Sentinel.  
After onboarding, I verified that the machine appeared under **Azure Arc → Connected Machines** and that logs were being sent via the **Azure Monitor Agent (AMA)**.  

Next, I onboarded the **Azure Virtual Machine** into the same workspace.  
I enabled **Microsoft Defender for Cloud** and configured **Diagnostic Settings** to send Security Logs, Syslogs, and Performance metrics to Sentinel.  
This ensures that both the personal laptop and Azure VM are monitored in real-time for process, authentication, and network-level activities.  

✅ **Result:**  
Both the personal and Azure VM machines successfully started forwarding logs to Sentinel through the Log Analytics workspace, forming the foundation for later attack simulation and detection.
<img width="942" height="498" alt="image" src="https://github.com/user-attachments/assets/19ecaa5a-faf1-41f8-94c0-20c3b90e0ec4" />
<img width="940" height="499" alt="image" src="https://github.com/user-attachments/assets/1fa68adb-c7d8-48ce-9344-ec1e114711eb" />
<img width="946" height="506" alt="image" src="https://github.com/user-attachments/assets/31fa38dc-deef-4976-b51f-7a76ae3ec1d7" />
<img width="949" height="506" alt="image" src="https://github.com/user-attachments/assets/58c59747-a2e1-418c-8165-5e3bc608a4bc" />
<img width="943" height="449" alt="image" src="https://github.com/user-attachments/assets/b0c4ddae-7470-401b-9dde-c8ea3c0a86b0" />

### 🐧 Onboarding Ubuntu Machine
I also onboarded an **Ubuntu machine** to include a Linux environment for cross-platform visibility.  
I installed the **Azure Monitor Agent (AMA)** and configured **Syslog** and **auditd** to forward authentication and process logs to Microsoft Sentinel.  
Once configured, the Ubuntu system appeared under the **Agents Connected** list in the workspace.  
Additionally, I enabled **OSQuery** for advanced endpoint visibility and tested the integration by generating sample SSH login events.  

✅ **Result:**  
Ubuntu logs such as authentication attempts, process executions, and system activities are now visible in Microsoft Sentinel, enabling Linux-based attack detection.
<img width="948" height="440" alt="image" src="https://github.com/user-attachments/assets/707ff593-1de5-4c84-8e22-8d1a1c74187c" />
<img width="946" height="580" alt="image" src="https://github.com/user-attachments/assets/ec043bca-b35b-41cc-a48a-0b708d052d12" />
<img width="927" height="517" alt="image" src="https://github.com/user-attachments/assets/a35ca97d-b477-48fc-8754-d82f14689b08" />
<img width="933" height="499" alt="image" src="https://github.com/user-attachments/assets/fd325754-d80c-467d-9a03-3a1fdccfb988" />
<img width="935" height="503" alt="image" src="https://github.com/user-attachments/assets/5b69348f-31c8-496c-afc9-b62bcd860ecd" />
<img width="928" height="493" alt="image" src="https://github.com/user-attachments/assets/1604906d-6770-4c74-b07b-17679c4cb037" />
<img width="939" height="498" alt="image" src="https://github.com/user-attachments/assets/5d1f0316-057c-4bbf-9513-3013f5481fca" />


### 🧠 Verification
After completing the onboarding of all three systems:
- All devices (Laptop, Azure VM, Ubuntu) appear in Microsoft Sentinel.  
- Log data is successfully ingested into the **Log Analytics Workspace**.  
- Test queries (e.g., login events, process creation) confirmed that telemetry is flowing correctly.

---

### 🚀 Next Step
With all machines onboarded and sending telemetry, the next phase focuses on **Attack Simulation and Detection** — performing controlled attacks like reconnaissance, brute-force, and privilege escalation to validate Sentinel detections and automation rules.
<img width="1351" height="598" alt="image" src="https://github.com/user-attachments/assets/9b04417b-21d1-413c-88e9-7ce45cc2bd9d" />
<img width="1003" height="299" alt="image" src="https://github.com/user-attachments/assets/38149b43-be04-4de5-8110-6f77aa73c06a" />

# 🔐 Brute-Force Attack — Detection & Response

## Summary
**Attack type:** Brute-force (credential stuffing / repeated login attempts)  
**Goal:** Gain unauthorized access to a user account or host by repeatedly trying credentials.  
**MITRE ATT&CK mapping:** *Credential Access → Brute Force* (T1110)

## How the attack was performed (simulation)
- Generated multiple failed authentication attempts against a target account on a Windows host (Event ID **4625**).   
- other Techniques used for simulation: scripted repeated logon attempts (e.g., a brute force tool or a custom script), or manual repeated invalid password attempts for testing.


## Detection approach
Detect a classic pattern:
1. **Multiple failed logon events** for the same account or from the same source IP within a short timeframe (e.g., ≥ 5 failures in 10 minutes).  
2. **Followed by a successful logon** for the same account or on the same host within a short window (e.g., within 5–10 minutes of the failures).
<img width="1301" height="571" alt="image" src="https://github.com/user-attachments/assets/e65bf7e5-cf28-4896-96c9-01be46e55f93" />

## Analytical rule 
Analytical rules are created to **automate detection** of suspicious activity.  
In this case, the rule continuously monitors for **multiple failed login attempts followed by a successful login**, which indicates a possible brute-force attack.  
When this pattern is detected, **an alert is automatically generated** in Microsoft Sentinel, allowing the SOC analyst to investigate, assign the incident, and take remediation actions.
<img width="1349" height="633" alt="image" src="https://github.com/user-attachments/assets/1eac81c1-3fb9-458d-bae9-a46b92a8713a" />
<img width="1331" height="590" alt="image" src="https://github.com/user-attachments/assets/e9a8fb66-fafb-4725-8a66-51356922e91c" />

# ✅ Successful Login After Brute-Force Attack — Detection & Response

## Summary
**Attack type:** Post-bruteforce successful authentication  
**Goal:** An attacker gains access after repeatedly attempting incorrect passwords.  
**MITRE ATT&CK mapping:** *Credential Access → Brute Force (T1110)* & *Initial Access → Valid Accounts (T1078)*

In this scenario, I monitored and documented a **successful login that occurs immediately after multiple failed login attempts**, indicating a potentially compromised account.

---

## How the attack was performed (simulation)
- First, a brute-force sequence was generated, producing multiple **failed login events (4625)**.
- Shortly after, a **successful login event (4624)** occurred for the same user, confirming the attack succeeded.
- This chain is a strong indicator that credentials were guessed or cracked.

---

## Detection approach
To detect this attack, we look for:

1. **Repeated failed logins by the same user or from the same IP** within a short time window.  
2. **A successful login event immediately after** the failures for the same account.  

This combination signals a possible **account compromise** following a brute-force attempt.
<img width="1307" height="583" alt="image" src="https://github.com/user-attachments/assets/aa2ce828-e71b-48c6-9816-a0428cf42c53" />

---

## Analytical rule  
This analytical rule is created to automatically detect when **a successful login occurs after a burst of failed attempts**, which strongly indicates credential compromise.  
The rule ensures Sentinel raises an alert so the SOC analyst can investigate, assign the incident, and take necessary action.
<img width="1315" height="595" alt="image" src="https://github.com/user-attachments/assets/45155c60-67e8-495e-828a-0b97df59f3ac" />
<img width="1334" height="570" alt="image" src="https://github.com/user-attachments/assets/60e26b12-ece0-40ca-a0ab-02ce8a218250" />
<img width="1116" height="521" alt="image" src="https://github.com/user-attachments/assets/cbdf087a-786f-4339-b965-0f9bd561c133" />
<img width="1122" height="579" alt="image" src="https://github.com/user-attachments/assets/310c4fb5-7e18-4b85-b278-afc183efc2b1" />

## 📨 Macro-Enabled Phishing Attachment — Detection & Response
# Summary:
Attack Type: Phishing email with malicious macro-enabled attachment (.xlsm)
Goal: Trick the user into opening an attachment that executes malicious PowerShell commands
MITRE ATT&CK mapping:

## Initial Access → Phishing: Attachment (T1566.001)

Execution → Command & Scripting Interpreter: PowerShell (T1059.001)

In this scenario, I simulated a phishing attack by downloading and opening a macro-enabled Excel file that, when opened, executed suspicious PowerShell commands. The activity was captured through Windows logs and detected using a custom analytic rule in Sentinel/Defender.

## How the attack was performed (simulation)

Downloaded a known malicious test file (PhishingAttachment.xlsm) from the Atomic Red Team repository using Invoke-WebRequest.

Opened the macro-enabled Excel file to simulate a user falling victim to the phishing attempt.

The embedded VBA macro triggered execution of suspicious PowerShell commands.

This generated events such as:

PowerShell operational logs

Process creation events (Sysmon Event ID 1)

Script Block logging (PowerShell Event ID 4104)

⚠️ The file is safe for lab use but should only be executed in an isolated test environment.
<img width="791" height="192" alt="image" src="https://github.com/user-attachments/assets/c87dd491-d8cc-4f82-b5c6-f3e008feee0f" />
<img width="1146" height="85" alt="image" src="https://github.com/user-attachments/assets/908cf98d-5aba-47ff-826e-b2d8c0505589" />

## Detection approach

The detection focuses on identifying behaviors that indicate macro-triggered execution:

A macro-enabled file (.xlsm) is opened → spawning PowerShell

Excel (EXCEL.EXE) launching PowerShell is highly suspicious.

PowerShell executing commands downloaded from the internet
<img width="1013" height="422" alt="image" src="https://github.com/user-attachments/assets/897df4d0-7293-4c2b-981d-a14a446ddd25" />



## Evidence includes:

Unusual command patterns like Invoke-WebRequest, IEX, or encoded commands

Process chain analysis
Example:
EXCEL.EXE → powershell.exe → suspicious command

These signals correlate to typical phishing malware delivery techniques such as initial reconnaissance, payload staging, or lateral movement preparation.

## Analytical Rule

An analytic rule is created to automatically identify when a macro-enabled Office application spawns PowerShell, indicating a likely phishing attack.
<img width="1028" height="341" alt="image" src="https://github.com/user-attachments/assets/bc7ef078-ef48-4557-84e8-4ed8169cab28" />
<img width="851" height="447" alt="image" src="https://github.com/user-attachments/assets/b352d6e9-3ee9-49aa-a3a6-925605ceee82" />
<img width="1343" height="599" alt="image" src="https://github.com/user-attachments/assets/cf3a13ac-7861-43dc-bac5-4197426cf4a9" />

# ⚡ Detection: Suspicious PowerShell Command Execution

## 📌 Overview

Detects execution of high-risk PowerShell commands often used in attacks such as recon, payload download, script obfuscation, and privilege abuse.

Field	Value
Technique	T1059.001 – PowerShell
Data Source	PowerShell Logs, Sysmon Event 1
Severity	High
## 🎯 Purpose

Identify PowerShell commands containing known malicious patterns, including:
DownloadString, Invoke-WebRequest, EncodedCommand, Bypass, IEX, Base64, Invoke-Expression, or obfuscation operators.

## 🧪 Attack Simulation & Detection(Short)
<img width="553" height="94" alt="image" src="https://github.com/user-attachments/assets/cf3ba445-53e9-4e38-9192-218976a0d5c1" />
<img width="1207" height="387" alt="image" src="https://github.com/user-attachments/assets/5ab720ad-70ee-4de7-9848-32ddb1e2d93b" />
<img width="849" height="69" alt="image" src="https://github.com/user-attachments/assets/820fc99a-a396-4580-ba85-5ab5924bda41" />
<img width="960" height="312" alt="image" src="https://github.com/user-attachments/assets/39f8579e-c102-4334-80b2-51cc462bdfcd" />

## Analytical rule
📎 Screenshots
<img width="844" height="502" alt="image" src="https://github.com/user-attachments/assets/650c2e79-90ef-4a75-ab2b-ef4ccd1da604" />
<img width="1014" height="382" alt="image" src="https://github.com/user-attachments/assets/73e6e096-a95e-42db-b2e3-a71aa5c871f3" />
<img width="1012" height="380" alt="image" src="https://github.com/user-attachments/assets/45f37753-e383-4e82-b13e-9d29ba4fca03" />
<img width="1298" height="527" alt="image" src="https://github.com/user-attachments/assets/0c6b4404-80c9-4153-b736-dad02cb93850" />
<img width="1117" height="497" alt="image" src="https://github.com/user-attachments/assets/fa31e1ea-4e17-40ae-80e9-0a5b93e57a33" />
<img width="1119" height="571" alt="image" src="https://github.com/user-attachments/assets/aa29be95-3869-4181-a3a8-dafb95dc3bd0" />
<img width="1137" height="605" alt="image" src="https://github.com/user-attachments/assets/9efa32bd-5565-4494-828f-8d25f76b0534" />
## 🚨 Alert Trigger
Alert when any PowerShell script block contains known malicious keywords or encoding/obfuscation techniques.
🛡 SOC Actions
Retrieve full script block

Check for payload download or persistence creation

Block external domain or IP

Isolate endpoint if needed

# ⏰ Detection: Suspicious Scheduled Task Creation

## 📌 Overview

Detects creation or modification of Windows Scheduled Tasks, a common persistence technique used by attackers to execute payloads at logon, startup, or at scheduled intervals.

Field	Value
Technique	T1053.005 – Scheduled Task
Data Source	Security Logs, Sysmon (Event ID 1), TaskScheduler logs
Severity	High
## 🧪 Attack Simulation (Based on Screenshot)

In this test, two malicious scheduled tasks were created:
Commands used:
<img width="977" height="243" alt="image" src="https://github.com/user-attachments/assets/70c15805-d3bc-4612-a205-357b7cc01931" />
This technique is frequently used for persistence and privilege escalation.

## 🔍 Detection Approach

To detect scheduled task creation, look for:

New task registration events

Event ID 4698 – A scheduled task was created.

Event ID 4699 – A scheduled task was deleted.

Event ID 4702 – A scheduled task was updated.

Sysmon process execution (Event ID 1)

## Command lines containing:

schtasks /create

schtasks /change

schtasks /run

Suspicious actions

Tasks running as SYSTEM

Tasks executing cmd.exe, PowerShell, scripts, or unknown binaries

Tasks triggered at logon, startup, or repeated intervals

## 📘 Analytical Rule
<img width="977" height="243" alt="image" src="https://github.com/user-attachments/assets/70c15805-d3bc-4612-a205-357b7cc01931" />
<img width="1012" height="436" alt="image" src="https://github.com/user-attachments/assets/7c79b2fe-9dd8-4cd7-a699-7c5e4ec82eb6" />
<img width="1025" height="437" alt="image" src="https://github.com/user-attachments/assets/1da59b88-9ba5-4e2a-8e06-a84d3e2237ed" />
<img width="1346" height="641" alt="image" src="https://github.com/user-attachments/assets/40dadf96-90e7-49f5-8af0-c5c6e6501df9" />
This analytic rule is created to automatically alert when a new or modified scheduled task is detected, especially when associated with suspicious commands or SYSTEM-level execution.

## After detecting the scduled tasks running in the machine i was manually able to delete the tasks running 
<img width="1048" height="341" alt="image" src="https://github.com/user-attachments/assets/58d01f70-1ee4-4328-84c9-51f855be34ba" />

# 🛠️ System Enumeration via Command-Line Utilities — Detection & Response
## 📌 Summary

Attack type: Reconnaissance / System Enumeration
Goal: Gather information about logged-in users, sessions, and system configuration using built-in Windows command-line tools.
MITRE ATT&CK:

T1033 – System Owner/User Discovery

T1426 – System Information Discovery

Adversaries often perform enumeration after gaining initial access to understand the system, identify valuable accounts, and plan privilege escalation or lateral movement.

## 🔥 How the attack was performed (simulation)

Using built-in Windows utilities commonly abused by attackers:

<img width="944" height="261" alt="image" src="https://github.com/user-attachments/assets/b678685e-7ccd-41c1-b4d1-9da3dcc3d7d8" />

## These commands reveal:

Current user

Logged-in sessions

RDP/terminal sessions

All system users

Active/disconnected sessions

This type of enumeration is standard during post-compromise reconnaissance.

## 🎯 Detection approach

The analytic rule monitors for suspicious execution of enumeration utilities:

whoami.exe

quser.exe

qwinsta.exe

wmic.exe

Any output files generated by these commands

These tools are uncommon in normal user activity but very common in attack chains.

## 📘 Analytical Rule
<img width="944" height="261" alt="image" src="https://github.com/user-attachments/assets/f0eb1f7b-c922-4d2e-af33-d6a6c12ba642" />
<img width="650" height="658" alt="image" src="https://github.com/user-attachments/assets/d86697c9-8a5c-443a-98aa-8294b49336f6" />
<img width="783" height="209" alt="image" src="https://github.com/user-attachments/assets/e2d7059f-1100-4d09-8a2e-7f932c78ad37" />
<img width="1031" height="438" alt="image" src="https://github.com/user-attachments/assets/58c9403b-f12f-44b8-a887-d29a450a86dd" />
<img width="1029" height="439" alt="image" src="https://github.com/user-attachments/assets/769d5b71-0574-41f5-8491-a356c647f87d" />
<img width="1027" height="436" alt="image" src="https://github.com/user-attachments/assets/72d6e8f3-1514-4649-8ee3-976aa8503e3f" />
<img width="1359" height="656" alt="image" src="https://github.com/user-attachments/assets/58ae3d43-1de4-4c19-99d8-b53666cf8f2a" />
<img width="1272" height="642" alt="image" src="https://github.com/user-attachments/assets/4f01a908-014f-45b0-8412-8c216096cb8c" />


This analytic rule is designed to detect reconnaissance behavior executed through system command-line utilities.
Once triggered, the rule alerts the SOC team to investigate suspicious enumeration, assign the incident, and take appropriate action.

# 🗂️ Registry Persistence — Run / RunOnce / Services
Detection & Response Documentation
## 📌 Summary

Attack type: Persistence via Registry Modification
Goal: Ensure malicious programs run automatically at system startup or user logon.
MITRE ATT&CK:

T1547 – Boot or Logon Autostart Execution

T1547.001 – Registry Run Keys / Startup Folder

Attackers commonly modify registry keys like Run, RunOnce, and RunOnceEx to maintain persistence even after reboots.

## 🔥 How the attack was performed (simulation)
## 1️⃣ User-Level Persistence (HKCU – No Admin Required)

The attacker adds a malicious command to the Run key under the Current User hive:
REG ADD "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "Atomic Red Team" /T REG_SZ /F /D "{command_to_execute}"
<img width="1147" height="230" alt="image" src="https://github.com/user-attachments/assets/670496e6-06ab-42d6-8ae7-dc50f1c469d7" />
This causes the payload to execute every time the user logs in.

## 2️⃣ System-Level Persistence (HKLM – Admin Required)

The attacker performs a high-privilege persistence modification using RunOnceEx:

REG ADD "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnceEx\0001\Depend" /V 1 /D "{thing_to_execute}"
<img width="1216" height="210" alt="image" src="https://github.com/user-attachments/assets/ca2cb242-9220-42e4-8ce9-1427b47bc4be" />

This executes the payload on next system startup, impacting all users.

These techniques are widely used by malware, RATs, and threat actors to maintain access.

## 🎯 Detection approach

The analytic rule monitors for:

Sysmon Event ID 13 — Registry value writes

Sysmon Event ID 1 — Process creation that touches persistence-related registry paths

## Registry paths monitored include:

HKCU\...\Run

HKCU\...\RunOnce

HKLM\...\Run

HKLM\...\RunOnceEx

Services keys used to configure malicious service persistence

Suspicious entries in these locations are highly indicative of malicious persistence.

## 📘 Analytical Rule detection
<img width="1147" height="230" alt="image" src="https://github.com/user-attachments/assets/c267f6db-99ea-40dc-a9e6-4e6fa5d83b1b" />
<img width="1216" height="210" alt="image" src="https://github.com/user-attachments/assets/9fe71da2-e60d-46ff-9213-b5131b637045" />
<img width="1036" height="444" alt="image" src="https://github.com/user-attachments/assets/54faf194-7b80-43c2-bc63-c8c962f5b2b9" />
<img width="1029" height="439" alt="image" src="https://github.com/user-attachments/assets/f14f3c64-0783-4e69-b3ba-e1caff2084dd" />
<img width="1034" height="444" alt="image" src="https://github.com/user-attachments/assets/e034bcbb-464f-4bd1-b5e8-826685e877b2" />
<img width="1253" height="437" alt="image" src="https://github.com/user-attachments/assets/a45626fb-67c1-4349-9bb7-a68360e39e49" />
<img width="1118" height="615" alt="image" src="https://github.com/user-attachments/assets/6b3a3590-4b0e-428f-a513-10217acb8818" />
This analytic rule detects registry modification attempts targeting startup/persistence keys.
When triggered, it alerts the SOC analyst to investigate any unexpected autoruns, validate processes, and remove malicious registry entries.

## After detecting the REG keys running in the machine i was manually able to delete the REG keys running 
<img width="1126" height="400" alt="image" src="https://github.com/user-attachments/assets/73f66062-6108-4a63-8a91-4325ad71006a" />
<img width="1243" height="511" alt="image" src="https://github.com/user-attachments/assets/9bf3acc7-e7a1-424b-8164-70a999d2dff5" />



























