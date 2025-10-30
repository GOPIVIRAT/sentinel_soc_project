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


