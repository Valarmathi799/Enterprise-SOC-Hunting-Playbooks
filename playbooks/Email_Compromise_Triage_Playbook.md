# SOP: Phishing & Business Email Compromise (BEC) Investigation Workflow

## 1. Objective
To establish a structured, repeatable framework for investigating, containing, and remediating suspected phishing emails and BEC attempts, ensuring minimal operational disruption and rapid threat eradication.

---

## 2. Initial Triage & Verification
* **Alert Ingestion:** Pick up escalations from L1 or automated user-reported phishing mailboxes (e.g., Cofense, Defender for Office 365).
* **Header Analysis:** Inspect message headers (`Received`, `Authentication-Results`, `Return-Path`) to check for: 
  * SPF, DKIM, and DMARC failures or domain spoofing.
  * Discrepancies between the display name and actual sender address (`From` vs `Reply-To`).
* **URL & Attachment Inspection:**
  * Extract URLs statically. Never click links directly; use URL sandbox results or threat intel lookups (VirusTotal, SOCRadar, Palo Alto WildFire).
  * Check file attachment hashes (SHA-256) against known malicious signatures and sandbox reports for macro execution, credential harvesters, or dropper behavior.

---

## 3. Blast Radius & Scope Assessment
* **Query the Mail Gateway:** Search tenant logs to find all recipients who received the identical email variant.
* **User Interaction Audit:** Determine if any targeted user:
  * **Clicked the link:** Cross-reference proxy and web gateway logs.
  * **Downloaded/Executed attachments:** Check EDR telemetry (SentinelOne, Defender for Endpoint) for anomalous process spawns (e.g., `cmd.exe` or `powershell.exe` spawned from Outlook).
  * **Submitted credentials:** Check Azure AD / Entra ID sign-in logs for suspicious or impossible travel logins immediately following the email timestamp.

---

## 4. Containment & Remediation Actions
* **Mailbox Purge:** Execute a soft-delete / global purge of the malicious email across all user mailboxes using Exchange Online PowerShell or security center explorer.
* **Credential Remediation:** If credential theft or session hijacking is suspected:
  * Revoke all active user session tokens.
  * Force an immediate password reset.
  * Temporarily disable the compromised account pending investigation.
* **Perimeter Blocking:** Add malicious external IP addresses, domains, and sender addresses to email gateway blocklists and perimeter firewalls.

---

## 5. Documentation & Case Closure
* **Ticket Update:** Record all Indicators of Compromise (IOCs), affected user accounts, timelines, and remediation steps in ServiceNow / Jira.
* **Detection Tuning:** Collaborate with detection engineering to refine email filter rules or alert logic to catch iterative attacker variants.
* 
