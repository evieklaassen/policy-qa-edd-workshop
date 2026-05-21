# IT Security & Acceptable Use Policy
**Effective Date:** March 1, 2024  
**Document Owner:** Information Security (InfoSec)  
**Policy ID:** IT-SEC-001

---

## 1. Overview

This policy governs the acceptable use of Acme Corp's IT systems, networks, and data. It applies to all employees, contractors, and third-party vendors with access to Acme Corp systems.

---

## 2. Device Policy

### Standard Employees (Individual Contributor – Manager)
- All employees are issued a company-managed MacBook Pro or Windows laptop.
- Personal devices **may not** be used to access company data unless enrolled in the Mobile Device Management (MDM) program via IT ServiceDesk (ticket required).
- USB storage devices are **disabled by default** on all managed endpoints. Exceptions require IT Security approval via an InfoSec waiver (form IT-WAIVER-03).

### Senior Manager and Director Level
- Directors and above may request a second company device (tablet or secondary laptop) for travel purposes. Requests must be approved by their VP.
- Directors have read access to the IT Security audit logs for their cost center.

### Engineering & DevOps Roles (All Levels)
- Engineers may request elevated local admin rights via IT ServiceDesk. Requests are reviewed within 2 business days and require manager countersignature.
- Engineers working on production infrastructure are issued a **hardware security key (YubiKey)** and are required to use it for all production environment access.
- SSH access to production systems requires a hardware key; password-only SSH is disabled in production.

### Executive (VP and Above)
- Executives receive dedicated IT concierge support (concierge@acme-it.com, response SLA: 2 hours business hours).
- Executives are exempt from the standard MDM enrollment requirement for personal mobile devices but are strongly encouraged to enroll.
- Executive laptops are encrypted with a separate key escrow held by the CISO's office, not the standard IT key management system.

---

## 3. Password & Authentication Policy

- **Minimum password length:** 14 characters (enforced via SSO provider).
- **Multi-Factor Authentication (MFA):** Required for all employees on all company systems. Authenticator app (Okta Verify or Google Authenticator) is the standard second factor.
- **Hardware key (YubiKey):** Required for Engineering and DevOps roles for production access. Optional (but encouraged) for all other employees.
- **Password manager:** All employees are provided a 1Password Teams license. Using a personal password manager for company credentials is a policy violation.
- Passwords may **not** be shared under any circumstances. Shared service accounts must be managed via the IT Service Account process (form IT-SVC-01).

---

## 4. Data Classification and Handling

| Classification | Definition | Handling Requirements |
|---------------|-----------|----------------------|
| Public | Intentionally public info | No special handling |
| Internal | General business info | Must stay on company systems |
| Confidential | Business-sensitive (financials, HR data, customer data) | Encryption required at rest and in transit; no personal device storage |
| Restricted | Highly sensitive (source code, M&A, PII, PHI) | Need-to-know access; DLP monitoring active; VP approval required to share externally |

- Employees must classify documents when creating them using the Acme Data Classification labels in Google Workspace or Microsoft 365.
- Sending Confidential or Restricted data via personal email is a **Level 2 policy violation** (see Section 7).

---

## 5. Remote Access & VPN

- VPN (Acme GlobalConnect) is required when accessing Internal or above resources from non-corporate networks.
- VPN is **not** required for Public resources or SSO-gated SaaS tools (e.g., Slack, Google Workspace, Salesforce) which use Okta-enforced device trust.
- Split-tunnel VPN is enabled by default; all traffic to `10.0.0.0/8` and `172.16.0.0/12` routes through VPN; general internet traffic does not.

---

## 6. AI & Generative AI Tools

- Employees may use approved AI tools listed on the [AI Tools Registry](https://intranet.acme.com/ai-tools).
- **Prohibited:** Inputting Confidential or Restricted data into any AI tool not on the approved registry, including publicly available LLMs (e.g., ChatGPT, Claude.ai, Gemini) in their free or personal tiers.
- Approved enterprise tools (e.g., Microsoft Copilot with tenant isolation, Acme internal LLM gateway) may process Internal data only; Restricted data requires CISO approval.
- Engineers building AI features in Acme products must follow the AI Development Security Standards (IT-AI-002).

---

## 7. Policy Violations

| Level | Examples | Consequence |
|-------|---------|-------------|
| Level 1 (Minor) | Forgetting to lock screen, using unapproved browser extension | Mandatory security training |
| Level 2 (Moderate) | Sharing credentials, emailing Confidential data externally, unauthorized USB use | Written warning, additional training, possible access restrictions |
| Level 3 (Severe) | Data exfiltration, sharing Restricted data externally without approval, circumventing DLP | Immediate suspension pending investigation; possible termination and legal action |

---

## 8. Incident Reporting

All suspected security incidents must be reported to security@acme.com within **1 hour** of discovery. Employees who discover a potential incident and fail to report it may be subject to disciplinary action regardless of whether they caused the incident.

Phishing emails should be reported using the "Report Phishing" button in Gmail/Outlook. Do not forward phishing emails.
