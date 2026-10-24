# Automated SOAR Playbook: Used Shuffle SOAR to Automatically Isolate Endpoints Based on Malicious Events

## Project Description
This project delivers an automated Security Orchestration, Automation, and Response (**SOAR**) playbook implemented with **Shuffle SOAR** to perform zero-touch, automated network isolation of compromised endpoints upon detecting high-severity malicious security events. The solution bridges SIEM/EDR detection signals directly to automated containment playbooks, neutralizing active ransomware execution, Cobalt Strike Command and Control (C2) beaconing, and credential dumping activities within seconds.

---

## Repository Deliverables & Structure
```text
├── YourName_SOAR_Playbook.ipynb         # Main Jupyter Notebook containing playbook workflow execution, API triage, and metrics
├── requirements.txt                     # Python dependencies required to run the analysis and automation scripts
├── README.md                            # Comprehensive project overview, dataset details, and setup instructions
├── YourName_ProjectReport.docx          # Full academic/industry project documentation report
├── shuffle-docker-compose.yml           # Container orchestration stack for Shuffle SOAR (Frontend, Backend, Orborus)
├── shuffle_isolation_playbook.json      # Exported Shuffle SOAR workflow configuration schema
├── soar_malicious_events.json           # Telemetry dataset of malicious endpoint events
└── soar_isolation_metrics.png           # Visual metrics of automated triage decisions and containment thresholds
```

---

## Dataset Reference
* **Dataset Name:** Endpoint Malicious Events & Triage Dataset (`soar_malicious_events.json`)
* **Reference & Origin:** Structured telemetry simulating high-fidelity EDR/SIEM threat alerts, modeled according to the [Atomic Red Team Adversary Simulation Library](https://github.com/redcanaryco/atomic-red-team) and the [MITRE ATT&CK Matrix for Enterprise](https://attack.mitre.org/). Covers techniques:
  - `T1490` (Inhibit System Recovery / Ransomware Volume Shadow Deletion)
  - `T1071.001` (Web Protocols C2 Beaconing)
  - `T1003.001` (OS Credential Dumping via LSASS Memory)
  - `T1059.001` (Malicious Encoded PowerShell Execution)

---

## Technologies Used
* **SOAR Framework:** Shuffle SOAR (Open-Source Security Orchestration)
* **Automation & Scripting:** Python 3.10+, Jupyter Notebook, RESTful Webhooks
* **Data Processing & Analytics:** Pandas, NumPy
* **Visualization:** Matplotlib, Seaborn
* **Reporting:** Tabulate, python-docx
* **Containerization:** Docker, Docker Compose

---

## Setup & Execution Guide

### 1. Prerequisites
- Python 3.10+
- Docker & Docker Compose (optional for hosting live Shuffle SOAR instance)

### 2. Install Python Dependencies
```bash
pip install -r requirements.txt
```

### 3. Deploy Local Shuffle SOAR Stack (Optional Live Lab)
To spin up Shuffle SOAR locally:
```bash
docker compose -f shuffle-docker-compose.yml up -d
```
Access the Shuffle SOAR web builder at `http://localhost:3001` (or HTTPS `https://localhost:3443`).

### 4. Run the SOAR Playbook Pipeline
Open and execute the Jupyter Notebook:
```bash
jupyter notebook YourName_SOAR_Playbook.ipynb
```
Select **Kernel -> Restart and Run All** to simulate incoming webhook alerts, trigger automated endpoint isolation logic, render response dashboards (`soar_isolation_metrics.png`), and export the containment audit log (`soar_containment_audit.csv`).