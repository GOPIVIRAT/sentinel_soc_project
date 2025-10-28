## 🛰️ Step 4: Exploring Microsoft Sentinel for SOC Operations

After integrating Microsoft Defender for Cloud, I explored Microsoft Sentinel to perform real-world SOC operations such as monitoring incidents, analyzing logs, and automating response workflows.

Microsoft Sentinel acts as the **central SIEM and SOAR platform**, providing visibility across cloud and on-premises environments, enabling proactive threat detection and automated security response.

i have created the workspace and then created the retention period to 180 days in the workspace this is where all the logs will be stroed 
<img width="960" height="481" alt="image" src="https://github.com/user-attachments/assets/c7426a8d-3e82-467d-84e3-485cff8f307a" />
<img width="964" height="528" alt="image" src="https://github.com/user-attachments/assets/697e5c01-1213-45be-8bc0-a5aa2ce41f5a" />
<img width="961" height="478" alt="image" src="https://github.com/user-attachments/assets/78677c55-ed22-4195-b5d6-9b7ee4217880" />



### 📊 1. Tables (Log Analytics Workspace)
In Microsoft Sentinel, data is stored in tables within the Log Analytics workspace.  
Each data connector (like Defender for Cloud or Office 365) sends its logs to specific tables.

- Explored log tables such as **SecurityAlert**, **SecurityEvent**, and **Heartbeat**.  
- Used **KQL queries** to analyze alert trends, login patterns, and suspicious activities.  
- Verified that logs from connected resources (Defender for Cloud, Entra ID, etc.) were successfully ingested.

📸 *Screenshot suggestion:* Add image showing “Logs” tab and a query result using `SecurityAlert | take 10`
<img width="962" height="536" alt="image" src="https://github.com/user-attachments/assets/1de76a7a-1a6e-43d2-94e9-0c6c4ef9ab12" />
<img width="969" height="535" alt="image" src="https://github.com/user-attachments/assets/e6c1ae98-7588-4b2d-a0d7-9920dc8738a3" />
<img width="966" height="541" alt="image" src="https://github.com/user-attachments/assets/c12ef834-d61a-4289-93b0-92a8da4b1602" />


### 🧠 2. Threat Intelligence
Configured **Threat Intelligence** to integrate external IoC (Indicators of Compromise) feeds into Sentinel.  
This helps correlate alerts with known malicious IPs, domains, or file hashes.

- Added sample threat indicators manually.  
- Verified correlation between Defender alerts and imported threat indicators.  
- Used KQL queries to match alerts with known IoCs.

📸 *Screenshot suggestion:* Add image showing “Threat Intelligence” blade with IoCs listed.
<img width="960" height="531" alt="image" src="https://github.com/user-attachments/assets/f475ae75-c2f2-4c13-ad42-13deeb10a1a4" />
<img width="964" height="537" alt="image" src="https://github.com/user-attachments/assets/bbefe48d-aabd-41d1-8f37-6e3662893a3e" />



### 📋 3. Watchlists
Created **Watchlists** in Sentinel to store and reuse reference data during investigations.

- Uploaded custom CSV files containing high-value assets and user accounts.  
- Used these watchlists in KQL queries to filter incidents related to critical systems.  
- Helped enrich alert context and prioritize incidents.

📸 *Screenshot suggestion:* Add Watchlist creation screen and an example query referencing the watchlist.

<img width="965" height="528" alt="image" src="https://github.com/user-attachments/assets/4cee5971-352d-414a-981e-105e00ae01a2" />
<img width="962" height="560" alt="image" src="https://github.com/user-attachments/assets/22e67329-b2aa-4228-94c2-45ad836cd446" />
<img width="966" height="533" alt="image" src="https://github.com/user-attachments/assets/61a5c6b7-114d-433b-a520-dcf267fb71bd" />
<img width="958" height="524" alt="image" src="https://github.com/user-attachments/assets/ff81c0ad-99f9-45ee-a185-5724e0e8f110" />



### 🧩 4. Analytics Rules
Configured **Analytic Rules** to automatically detect suspicious behavior patterns.

- created a analytical rule such as *“Possible Brute Force Attack”* and *“Multiple Failed Sign-ins”*.  
- Customized rule logic using KQL to match my environment. 
- Enabled **alert grouping** and **automation rules** for better incident management.

📸 *Screenshot suggestion:* Add image showing Analytics Rule configuration and detection results.
<img width="1301" height="571" alt="image" src="https://github.com/user-attachments/assets/f431d089-7aad-46a1-bba2-f68684147f2d" />
<img width="1349" height="633" alt="image" src="https://github.com/user-attachments/assets/f2a093b4-31ee-49cd-8c2c-c21636efbac0" />
<img width="1331" height="590" alt="image" src="https://github.com/user-attachments/assets/a131df4d-bcfe-485f-b867-9d207b77ea25" />



### ⚙️ 5. Playbooks (SOAR Automation)
Created **Playbooks** to automate incident response tasks using **Logic Apps**.

- Designed automation to send email notifications when new incidents are created.  
- Integrated Microsoft Teams alerting for real-time SOC collaboration.  
- Verified successful trigger execution via incident automation.

📸 *Screenshot suggestion:* Add Logic App Designer image showing automation workflow.

### Content hub
<img width="1294" height="563" alt="image" src="https://github.com/user-attachments/assets/8bcf63f2-ef2a-411e-ad96-441a997757c8" />
<img width="1130" height="554" alt="image" src="https://github.com/user-attachments/assets/c54fa13e-4a16-460a-80fe-57483fea904e" />


### 🧾 Outcome
Through this exploration, Microsoft Sentinel served as a **unified SOC platform**, enabling:
- Continuous monitoring and alert correlation.  
- Integration of intelligence and reference data.  
- Automated and efficient incident response through playbooks.

This phase demonstrated practical SOC workflows — from detection to response — across the Microsoft security ecosystem.

