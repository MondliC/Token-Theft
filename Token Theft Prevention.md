# 🛡️ Token Theft Prevention Playbook

## 📌 Overview
Token theft attacks (especially Adversary-in-the-Middle - AiTM) allow attackers to capture session tokens and bypass Multi-Factor Authentication (MFA). Preventing these attacks requires a combination of **licensing, identity protection controls, and strong Conditional Access policies**.

This guide outlines the key preventive measures within Microsoft Entra ID and associated security controls.

---

## 🔑 Microsoft Entra Licensing Requirements

Effective prevention relies heavily on the correct licensing tier:

### 🟦 Entra ID P1

**Capabilities:**

- 🔐 **Security**
  - Basic Conditional Access policies
  - Multi-Factor Authentication (MFA)

- 📊 **Compliance**
  - Standard reporting and logging

- ⚙️ **Administrative Control**
  - Single Sign-On (SSO)
  - Hybrid identity monitoring

✅ **Use Case:**
- Baseline identity protection
- Foundational defense against token theft via policy enforcement

---

### 🟪 Entra ID P2

**Capabilities:**

- 🛡️ **Security**
  - Risk-based Conditional Access
  - Entra ID Protection (user risk + sign-in risk)

- 📋 **Compliance**
  - Advanced reporting
  - Access reviews
  - Full audit trails

- 👑 **Administrative Control**
  - Privileged Identity Management (PIM)
  - Automated access governance

✅ **Use Case:**
- Advanced threat detection and automated response
- Required for **token replay protection and identity risk scoring**

---

## 🚧 Conditional Access Policies (Core Defense Layer)

Conditional Access is the **most effective control** for preventing token theft and replay attacks.

---

### 💻 Require Managed / Compliant Device  
**License:** Entra P1 + Intune  
**Protection:** Prevents Token Theft via AiTM

**Pros:**
- ✅ Most achievable control in enterprise environments
- ✅ Flexible across different device types
- ✅ Protects against token harvesting (AiTM phishing)

**Cons:**
- ❌ Does NOT prevent token replay attacks
- ❌ Requires device onboarding and management overhead

---

### 🔐 Require Phishing-Resistant MFA  
**License:** Entra P1  
**Protection:** Prevents Token Theft via AiTM

**Examples:**
- FIDO2 keys  
- Windows Hello for Business  
- Certificate-based authentication  

**Pros:**
- ✅ Strongest form of authentication
- ✅ Passwordless → eliminates credential theft
- ✅ Highly effective against phishing attacks

**Cons:**
- ❌ May introduce end-user friction
- ❌ Does NOT prevent token replay

---

### 🖥️ Require Hybrid Azure AD Joined Device  
**License:** Entra P1  
**Protection:** Prevents Token Theft via AiTM

**Pros:**
- ✅ Ensures only corporate-managed devices can authenticate
- ✅ Limits exposure from unmanaged endpoints

**Cons:**
- ❌ Less flexible in BYOD environments
- ❌ Does not mitigate token replay

---

### 🌍 Require Trusted Location / Network  
**License:** Entra P1  
**Protection:** Prevents AiTM + Token Replay

**Pros:**
- ✅ Helps block token replay from unknown IPs/geographies
- ✅ Adds strong contextual access validation

**Cons:**
- ❌ Difficult to maintain (dynamic IPs, remote work)
- ❌ Can impact user productivity if too restrictive

---

### 🔗 Require Device-Bound Token Protection  
**License:** Entra P2  
**Protection:** Prevents Token Replay

**Pros:**
- ✅ Binds tokens to a specific device
- ✅ Prevents attacker reuse of stolen tokens
- ✅ Low user friction

**Cons:**
- ❌ Limited browser support
- ❌ Not fully supported across all apps/services

---

### 🌐 Require Global Secure Access (GSA)  
**License:** Entra P1 + Add-on  
**Protection:** Prevents AiTM + Token Replay

**Pros:**
- ✅ Strong protection against both phishing and replay attacks
- ✅ Enables secure access from anywhere
- ✅ Flexible access control model

**Cons:**
- ❌ Additional cost
- ❌ Implementation and operational overhead

---

## 🧠 Defense Strategy (Best Practice Approach)

For **maximum protection against token theft**, combine the following:

### ✅ Recommended Baseline
- Entra ID P1 licensing
- MFA enforced for all users
- Conditional Access:
  - Require compliant devices
  - Block legacy authentication

### 🔥 Advanced Protection (SOC-Level)
- Entra ID P2 licensing
- Risk-based Conditional Access
- Phishing-resistant MFA (FIDO2 / WHfB)
- Device-bound token protection
- Continuous monitoring of sign-in risk

---

## ⚠️ Key Security Insights

- MFA alone is **NOT sufficient** → tokens can bypass MFA
- AiTM attacks target **session tokens, not credentials**
- Token replay is a **post-authentication attack**
- Strong defense = **Identity + Device + Context**

---

## 📊 Mapping to Attack Techniques

| Attack Type          | Prevented By |
|---------------------|-------------|
| Phishing (AiTM)     | MFA + Compliant Device + Phishing-resistant MFA |
| Token Harvesting    | Conditional Access + Device Compliance |
| Token Replay        | Device-bound tokens + Trusted Locations + GSA |

---

## 🧠 Analyst Notes

> Always assume that once a token is stolen, the attacker may maintain access **even after password reset** unless sessions are revoked and token protections are enforced.

> Focus on **reducing token usability** (device binding, location controls) rather than only strengthening authentication.