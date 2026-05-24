# 🔐 Incident Response Playbook: Token Theft

## 📌 Overview
A Token Theft incident occurs when an attacker successfully steals authentication tokens (e.g., session tokens, refresh tokens, or access tokens), allowing them to bypass Multi-Factor Authentication (MFA) and maintain unauthorized access to user accounts.

This playbook outlines the detection, investigation, response, and post-remediation actions for handling such incidents in a cloud environment (Microsoft Entra ID / Microsoft Defender ecosystem).

---

## 🚨 Detection

Token theft incidents may be identified through multiple telemetry sources:

### 👤 User Reporting
- Suspicious account activity reported by the user
- Unexpected MFA prompts or sign-ins
- Unauthorized actions (emails sent, rules created)

### 🔍 Microsoft Entra ID Alerts
- Risky sign-ins (impossible travel, atypical behavior)
- Token replay detections
- Anomalous session activity

### 🛡️ Microsoft Defender Alerts
- Suspicious inbox rules
- Endpoint detections indicating credential/token access
- Email-related alerts (phishing, malicious attachments)

---

## 👤 User Context

Understanding the impacted user is critical:

- **Job Title** – Determines sensitivity of access
- **Roles & Privileges** – Admin vs standard user
  - Global Admin
  - Privileged Role Admin
  - Standard User

---

## ⚠️ Risk Detections

Evaluate risk signals associated with the account:

- ✅ Risk detected: **Yes / No**
- **IP Address / Location**
  - Unfamiliar or high-risk geography
- **Detection Type**
  - Impossible travel
  - Anonymous IP usage
  - Token reuse
- **Device Information**
  - Managed vs unmanaged
  - Known vs unknown device

---

## 🛠️ Containment & Immediate Response

Take rapid action to prevent further access:

- 🔒 Revoke all active sessions
- 🔑 Reset password and enforce MFA re-registration
- ✅ Confirm whether the user account is compromised
- 🚫 Block sign-in (temporarily if needed)

---

## 🕵️ Root Cause Analysis – Initial Access

Determine how the attacker gained access:

### 📧 Phishing Email (If YES)
- Identify scope:
  - Impacted users
  - Malicious URLs clicked
  - Email delivery status
- Extract Indicators of Compromise (IOCs)

### ❌ If NO Phishing Identified
- Use **Microsoft Defender Explorer**
- Perform **Message Trace** in Exchange Online
- Investigate alternative entry points (OAuth abuse, token leakage)

---

## 🔎 Post-Breach Activity Analysis

Investigate attacker actions after compromise:

- 📤 **Emails Sent**
  - Use Message Trace to identify malicious emails

- 📥 **Inbox Rules Created**
  - Review Office Activity Logs
  - Look for forwarding or deletion rules

- 📂 **File Access / Downloads**
  - Identify sensitive data exfiltration via Office logs

- 🔐 **MFA Changes**
  - Check AuditLogs for:
    - Modified authentication methods
    - New MFA registrations

- 🔗 **App Registrations / Consent**
  - Suspicious OAuth apps or delegated permissions
  - Admin/user consent events

- 💻 **Device Registration**
  - New or rogue devices added to Entra ID

- 🔑 **Password Resets**
  - Unauthorized password change attempts

---

## ✅ Post-Remediation Actions

After containment and recovery:

### 🔧 Security Hardening
- Update Conditional Access Policies:
  - Enforce compliant devices
  - Block legacy authentication
  - Require phishing-resistant MFA (e.g., FIDO2)

### 📢 Awareness & Training
- Conduct phishing awareness campaigns
- Educate users on reporting suspicious activity

### 📊 Monitoring & Auditing
- Monitor privileged accounts closely
- Enable continuous auditing of:
  - Admin roles
  - Authentication changes
  - Application consent events

---

## 📎 Key Takeaways

- Token theft bypasses MFA → focus on **session control and behavioral detection**
- Phishing remains the most common entry point
- Post-breach activity often includes **persistence mechanisms (rules, apps, devices)**
- Strong Conditional Access and user awareness are critical defenses

---

## 🧠 Analyst Notes

> Always correlate identity logs (Entra ID), endpoint telemetry (Defender), and email activity to build a complete attack timeline.  
> Prioritize high-privileged users and lateral movement indicators during investigation.