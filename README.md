# 🛡️ Flagship SOC Lab Microsoft Sentinel, Entra ID & Defender XDR Integration

## 🎯 Overview
This project showcases the design and build of a Flagship SOC Lab that mirrors enterprise-grade security environments.
It was created to demonstrate the ability to integrate firewall, identity, and endpoint telemetry into Microsoft Sentinel, providing full visibility across the SOC stack.

- Setting up and configuring SIEM/XDR pipelines
- Onboarding diverse log sources (pfSense, AD/Entra ID, Microsoft Defender) 
- Validating data sources with **KQL**  
- Documenting architecture and workflows clearly  
- Understanding hybrid identity and endpoint integration  

---

## 🗺️ Architecture

<img width="800" height="600" alt="flagship_soc_architecture_navy_syslogarrow" src="https://github.com/user-attachments/assets/ff5d35a2-a073-4588-8f59-5c21d0cd30ba" />


- **pfSense Firewall** → Syslog forwarded to **Ubuntu (rsyslog + AMA)** → **Microsoft Sentinel**
- **Windows Server 2022 (DC01)** → AD DS + GPO audit → Synced via **Entra Connect** → Entra ID
- **Windows 11 Endpoint** → Sysmon + Microsoft Defender for Endpoint → Sentinel
- **Security Onion** → Zeek/Suricata for NDR visibility
- **Microsoft Sentinel (soc-la)** → Central SIEM/XDR for hunting, detections, and dashboards

---

## 🔹 Phase 1 — Active Directory + Win11 Client
- Built AD DS domain (`lab.local`) on **Windows Server 2022**.  
- Deployed **Audit Baseline GPO** (logon/logoff, policy changes, account management).  
- Joined **Windows 11 client** to domain.  
- Validated security events (4624/4625) in Event Viewer.  

<img width="1021" height="729" alt="Screenshot 2025-08-27 222448" src="https://github.com/user-attachments/assets/37b158ea-dfd9-4e4c-af89-b2c9e7c832ca" />
<img width="746" height="527" alt="Screenshot 2025-08-26 111658" src="https://github.com/user-attachments/assets/8567ed17-c4ba-41fc-bcdd-0c2bdeaa3678" />
<img width="949" height="571" alt="Screenshot 2025-08-26 105932" src="https://github.com/user-attachments/assets/f8fc2728-2912-4578-820e-14ccf579042e" />
<img width="961" height="752" alt="Screenshot 2025-08-26 124518" src="https://github.com/user-attachments/assets/3fab264a-2fd6-43c4-b7f0-56e2ce679967" />

---

## 🔹 Phase 2 — Entra ID + M365 + Entra Connect
- Created **Azure tenant** (`labtenant.onmicrosoft.com`).  
- Enabled **M365 audit logging**.  
- Installed **Entra Connect** → synced on-prem users to Entra ID.  
- Validated hybrid identities across **AD + Entra ID**.  

<img width="880" height="620" alt="Screenshot 2025-08-26 172029" src="https://github.com/user-attachments/assets/9f7b5f9c-c57b-43d2-a064-7876ea74235f" />
<img width="1281" height="650" alt="Screenshot 2025-08-26 172448" src="https://github.com/user-attachments/assets/32e41a06-5685-4013-8565-4b588d59768d" />
<img width="712" height="585" alt="Screenshot 2025-08-26 162655" src="https://github.com/user-attachments/assets/a43f37f7-61ba-4e5c-8155-6626d3fac7d5" />

---

## 🔹 Phase 3 — Microsoft Sentinel + Log Ingestion
- Created **Log Analytics Workspace (`soc-la`)** and enabled Sentinel.  
- Connected data sources:   
  - **Microsoft Defender for Endpoint**  
  - **Entra ID sign-ins**  
  - **pfSense Syslog via Ubuntu forwarder**  
- Built **Data Collection Rule** (Syslog: auth, daemon, local0–7).  
- Verified ingestion with **baseline KQL queries**.  

<img width="1290" height="831" alt="Screenshot 2025-08-27 223650" src="https://github.com/user-attachments/assets/2623b2d3-8592-45f9-bbee-d9641a64d536" />
<img width="1355" height="728" alt="Screenshot 2025-08-27 203626" src="https://github.com/user-attachments/assets/7e191e5f-37a0-4915-b1a5-601d3cb22c43" />

---

## 🔹 Phase 4 — Microsoft Defender for Endpoint (MDE)
- Onboarded **Windows 11 client** to MDE.  
- Enabled **automatic sample submission**.  
- Device appeared in Defender portal and Sentinel.  

<img width="957" height="485" alt="Screenshot 2025-08-26 182552" src="https://github.com/user-attachments/assets/d59e2685-7dbf-4013-b69a-675d817c24ce" />
<img width="1661" height="789" alt="Screenshot 2025-08-27 183703" src="https://github.com/user-attachments/assets/a5ff4576-d824-4947-b376-08e7e6b2c90d" />

---
## 🔹 Phase 7: Key Takeaways

**Microsoft Sentinel Integration**: Built a centralized SIEM/XDR pipeline with Log Analytics, connectors, and Data Collection Rules.

**Firewall Visibility**: Forwarded pfSense syslog through Ubuntu (rsyslog + AMA) into Sentinel for network-level monitoring.

**Hybrid Identity Security**: Linked on-prem Active Directory with Entra ID (Azure AD) and enabled M365 audit logging.

**Endpoint Telemetry**: Deployed Sysmon GPO baseline and onboarded Windows 11 into Microsoft Defender for Endpoint.

**Baseline KQL Queries**: Created ready-to-use queries to validate ingestion and begin threat hunting immediately.

**Repeatable Documentation**: Clear, step-by-step build and validation process designed to mirror real SOC workflows.

---
