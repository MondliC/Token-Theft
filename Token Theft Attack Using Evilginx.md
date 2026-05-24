# Token Theft Attack Using Evilginx

## Overview
Token theft is a modern attack technique used to bypass Multi-Factor Authentication (MFA) by stealing session cookies instead of credentials alone. This allows attackers to hijack authenticated sessions without needing to re-enter credentials or MFA codes.

One of the most widely used tools for this attack is **Evilginx**, which enables adversary-in-the-middle (AiTM) phishing attacks.

---

## What is Evilginx?

**Evilginx** is an open-source adversary-in-the-middle (AiTM) framework used for phishing attacks. It acts as a reverse proxy between the victim and the legitimate website, capturing authentication data in real time.

### Key Characteristics:
- Operates as a **reverse proxy** between victim and target site
- Captures:
  - User credentials (username/password)
  - Session cookies (authentication tokens)
- Enables **MFA bypass**
- Uses **phishing domains** that mimic legitimate login pages
- Supports platforms like:
  - Microsoft 365
  - Google
  - Facebook
  - Other SSO providers

---

## Attack Flow: Token Theft via Evilginx

### Step 1: Infrastructure Setup
- Attacker registers a lookalike domain (e.g., `micr0soft-login[.]com`)
- Configures DNS to point to Evilginx server
- Loads a **phishlet** (preconfigured template for target service)

---

### Step 2: Luring the Victim
- Victim receives phishing email/link
- Link directs to Evilginx proxy site
- The page appears identical to legitimate login portal

---

### Step 3: Credential Harvesting
- Victim enters:
  - Username
  - Password
- Data is captured by Evilginx before being forwarded to the legitimate service

---

### Step 4: MFA Challenge
- Victim completes MFA (SMS, Authenticator app, etc.)
- The request passes through the Evilginx proxy
- Authentication succeeds on the real service

---

### Step 5: Session Cookie Capture (Critical Step)
- After successful login, the legitimate service issues **session cookies**
- Evilginx intercepts and stores these cookies
- These cookies represent an already authenticated session

---

### Step 6: Session Hijacking
- Attacker imports stolen cookies into their browser
- Gains **authenticated access without MFA**
- Can:
  - Access email
  - Create inbox rules
  - Exfiltrate data
  - Maintain persistence

---

## Indicators of Compromise (IoCs)

### Identity & Authentication
- Sign-ins from:
  - Different geographic locations within short timeframe
  - Anonymous proxies or VPS providers
- Suspicious **User-Agent strings**
- Token reuse from unusual IPs
- Successful login after phishing-related alerts

---

### Email & Account Activity
- Creation of **inbox forwarding rules**
- Suspicious mailbox access from new locations
- Unusual sending behavior

---

### Network Indicators
- Connections to:
  - Newly registered domains
  - Typosquatted domains
- TLS certificates with short validity periods

---

### Endpoint & Logs
- No malware present (attack is session-based)
- Legitimate browser activity but from:
  - Abnormal IP addresses
- Sign-in logs show:
  - MFA success followed by anomalous behavior

---
