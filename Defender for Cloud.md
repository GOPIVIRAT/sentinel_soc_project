
## 🛡️ Step 2: Configuring Microsoft Defender for Cloud

After setting up the Azure environment, I configured **Microsoft Defender for Cloud** to strengthen the overall security posture and enable continuous threat protection for cloud resources.

Microsoft Defender for Cloud is a **Cloud-Native Application Protection Platform (CNAPP)** that combines **CSPM (Cloud Security Posture Management)** and **CWPP (Cloud Workload Protection Platform)** capabilities.  
It helps organizations **monitor, assess, and protect** their cloud assets across **Azure, hybrid, and multi-cloud** environments.

---

### 🔍 CSPM – Cloud Security Posture Management

I enabled **CSPM** to continuously evaluate the security posture of my Azure environment.  
It helps identify **misconfigurations, compliance gaps, and potential risks** in cloud services.

**Key Capabilities:**
- 🧭 Provides **Security Recommendations** to harden resources.
- 📊 Tracks **Regulatory Compliance** against standards like **CIS**, **ISO**, and **NIST**.
- 🧮 Helps visualize the **Secure Score**, representing the overall cloud security posture.
- ⚠️ Detects risky configurations such as **publicly exposed storage accounts** or **weak network controls**.


<img width="938" height="455" alt="image" src="https://github.com/user-attachments/assets/88e3ff8c-aa95-4c53-bbd1-2940d9c4c9c6" />

### 🧩 CWPP – Cloud Workload Protection Platform

**CWPP** was enabled to protect workloads running in the cloud, such as servers, applications, and databases.  
This feature integrates **real-time protection** using Defender plans across multiple workloads.


<img width="956" height="507" alt="image" src="https://github.com/user-attachments/assets/1115c0e3-4be8-4440-9e3b-b94d1ff8fa74" />
<img width="942" height="436" alt="image" src="https://github.com/user-attachments/assets/7e2330ea-d746-45b9-8ad4-b4073d0d5908" />

**Defender Plan Coverage:**
- 💻 **Servers:** Enables vulnerability assessment and endpoint protection for virtual machines.  
- 🌐 **App Services:** Secures application code, containers, and dependencies.  
- 🗄️ **Databases:** Monitors for data exposure, SQL injection risks, and configuration weaknesses.  
- 🔔 Provides **Threat Detection Alerts** in the Defender portal for immediate investigation.



### ⚙️ Outcome

By enabling both **CSPM** and **CWPP**, the **Defender for Cloud dashboard** now provides a **unified view of cloud security posture**, along with:
- Actionable insights  
- Continuous monitoring  
- Integration with **Microsoft Defender XDR** for incident detection and response  

> 💡 *This configuration ensures that all workloads in the Azure environment are protected and continuously monitored for vulnerabilities, threats, and misconfigurations — forming the foundation for proactive cloud threat detection in this SOC project.*



