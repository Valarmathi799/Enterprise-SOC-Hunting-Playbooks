# Enterprise SOC Threat Hunting & Incident Response Playbooks

Welcome to my security operations repository. This collection showcases practical, production-ready threat hunting methodologies, incident response standard operating procedures (SOPs), and detection queries designed for Layer 2 (L2) Security Operations Center (SOC) analysts. 

As a cybersecurity analyst specializing in **Incident Response, Phishing/BEC analysis, and SIEM/EDR log correlation**, this repository highlights my hands-on approach to threat detection, alert triage, and adversary tracking.

---

## 📂 Repository Structure

```text
Enterprise-SOC-Hunting-Playbooks/
│
├── playbooks/
│   └── Email_Compromise_Triage_Playbook.md   # End-to-end IR workflow for Phishing & BEC
│
└── queries/
    ├── KQL_Sentinel_Hunting.kql              # Microsoft Sentinel hunting queries (Cloud/Identity)
    └── Splunk_SPL_Detections.spl             # Splunk SPL detection rules (Endpoint/Network)
