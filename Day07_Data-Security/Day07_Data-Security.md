# Day 07 — Data Security
## DAMA-DMBOK2 Chapter 7 | CDMP Exam Weight: ~11%

**Study Plan:** Day 7 of 17 | One of the highest-weighted chapters — tied with Data Governance and Data Modelling
**Malaysian Context:** PDPA 2010 (Act 709), BNM RMIT 2020, Cybersecurity Act 2018, NACSA, MyDIGITAL Blueprint
**Connections:** Builds on Chapter 6 (Storage) | Enforced through Chapter 3 (Governance) | Measured by Chapter 13 (Quality)

---

## Section 1: Core Summary — What Is Data Security

Data Security encompasses the policies, procedures, and technical controls that protect data assets from unauthorised access, use, disclosure, disruption, modification, or destruction. DAMA-DMBOK2 positions data security as a cross-cutting discipline — it is not the exclusive responsibility of the IT security team. Every data management activity, from data collection through disposal, has a security dimension that requires governance, technical enforcement, and human accountability.

### DAMA Definition

DAMA defines Data Security as: *"the planning, development, and execution of security policies and procedures to provide proper authentication, authorisation, access, and auditing of data and information assets."* The emphasis on all four elements — authentication, authorisation, access, and auditing — reflects that security is a lifecycle of controls, not a single technical measure.

### Why This Chapter Is Critical for the CDMP Exam

Chapter 7 carries approximately **11% of exam weight** — one of the highest-weighted chapters alongside Data Governance and Data Modelling. The exam tests: understanding of the CIA triad, the ability to classify data by sensitivity, the selection of appropriate access control models for given scenarios, knowledge of privacy-preserving techniques (masking, tokenisation, anonymisation), and the governance structures that sustain a data security programme. This chapter also connects directly to every other chapter — security must be built into data architecture, modelling, storage, integration, and quality management.

### The CIA Triad — The Foundation of Data Security

```
CIA TRIAD — THREE SECURITY PROPERTIES

  ┌──────────────────────────────────────────────────────┐
  │  CONFIDENTIALITY                                     │
  │  "Data is accessible only to those authorised"      │
  │                                                      │
  │  Protects against: Unauthorised disclosure,          │
  │  eavesdropping, data breaches, insider threats       │
  │                                                      │
  │  Controls: Encryption, access control, data          │
  │  masking, classification, need-to-know principle     │
  └──────────────────────────────────────────────────────┘
  ┌──────────────────────────────────────────────────────┐
  │  INTEGRITY                                           │
  │  "Data is accurate, complete, and unaltered"        │
  │                                                      │
  │  Protects against: Unauthorised modification,        │
  │  data tampering, corruption, accidental errors       │
  │                                                      │
  │  Controls: Checksums, hashing, digital signatures,  │
  │  referential integrity, change audit logs            │
  └──────────────────────────────────────────────────────┘
  ┌──────────────────────────────────────────────────────┐
  │  AVAILABILITY                                        │
  │  "Data is accessible to authorised users when        │
  │   needed"                                            │
  │                                                      │
  │  Protects against: DoS attacks, system failures,    │
  │  ransomware, data loss, excessive access controls    │
  │                                                      │
  │  Controls: Redundancy, backups, DR, capacity        │
  │  planning, anti-DDoS, access control (balanced)     │
  └──────────────────────────────────────────────────────┘

  Note: Over-controlling for Confidentiality can threaten
  Availability. Security design requires BALANCING all three.
```

### Three Core Business Drivers

**Regulatory compliance** — PDPA 2010, BNM RMIT 2020, the Cybersecurity Act 2018, PCI DSS, and sector-specific regulations mandate specific data security controls with legal consequences for non-compliance. Data security is not optional — it is a legal obligation with financial penalties, licence revocation risk, and reputational consequences.

**Protecting organisational and customer assets** — Customer personal data, intellectual property, financial records, and competitive information have direct business value. Unauthorised disclosure or destruction of these assets causes measurable financial harm (fraud losses, litigation, regulatory fines) and intangible harm (brand damage, customer trust erosion).

**Enabling trusted data sharing** — Internal teams, business partners, regulators, and customers can only share data safely when security controls are established and verifiable. Without a data security framework, data sharing creates unacceptable risk and must be constrained — limiting analytics capability, operational efficiency, and regulatory reporting.

---

## Section 2: DAMA Framework View — Concepts, Activities, Controls

### 2.1 Data Classification — The Foundation of Security Design

Data classification assigns a sensitivity level to data based on the potential harm of unauthorised disclosure. Classification is the first step in security design — without knowing how sensitive data is, no rational security control can be selected.

```
DATA CLASSIFICATION FRAMEWORK — FOUR-TIER MODEL

  ┌─────────────────────────────────────────────────────────┐
  │  TIER 1: RESTRICTED / HIGHLY CONFIDENTIAL               │
  │                                                         │
  │  Definition: Data whose unauthorised disclosure would   │
  │  cause severe harm — legal liability, regulatory        │
  │  sanction, significant financial loss, or personal      │
  │  safety risk.                                           │
  │                                                         │
  │  Examples:                                              │
  │  • Customer NRIC numbers, biometric data                │
  │  • Patient medical records, HIV/mental health status    │
  │  • Bank account numbers, credit card PANs (full)        │
  │  • Encryption keys, authentication credentials          │
  │  • Classified government information                    │
  │                                                         │
  │  Controls required: Encryption at rest + in transit;   │
  │  strict RBAC; access logs; masking in non-prod;         │
  │  contractual restrictions on transfer                   │
  └─────────────────────────────────────────────────────────┘
  ┌─────────────────────────────────────────────────────────┐
  │  TIER 2: CONFIDENTIAL                                   │
  │                                                         │
  │  Definition: Internal business data whose disclosure    │
  │  would harm competitive position or customer trust      │
  │  but does not meet the highest threshold.               │
  │                                                         │
  │  Examples:                                              │
  │  • Customer names + contact details (combined)          │
  │  • Employee salaries, performance reviews               │
  │  • Unpublished financial results                        │
  │  • Business strategies, pricing models                  │
  │                                                         │
  │  Controls required: Access control; encrypted transit;  │
  │  NDA for third-party sharing; audit logging             │
  └─────────────────────────────────────────────────────────┘
  ┌─────────────────────────────────────────────────────────┐
  │  TIER 3: INTERNAL                                       │
  │                                                         │
  │  Definition: Data for internal use only; not harmful    │
  │  if disclosed internally but should not be shared       │
  │  publicly without authorisation.                        │
  │                                                         │
  │  Examples:                                              │
  │  • Internal policies and procedures                     │
  │  • Project plans, meeting minutes                       │
  │  • Aggregated (non-personal) operational reports        │
  │                                                         │
  │  Controls required: Basic access control;               │
  │  no public sharing without approval                     │
  └─────────────────────────────────────────────────────────┘
  ┌─────────────────────────────────────────────────────────┐
  │  TIER 4: PUBLIC                                         │
  │                                                         │
  │  Definition: Data approved for public disclosure —      │
  │  no harm from unrestricted access.                      │
  │                                                         │
  │  Examples:                                              │
  │  • Published financial reports                          │
  │  • Product brochures, price lists                       │
  │  • Press releases, regulatory filings (public)          │
  │                                                         │
  │  Controls required: Integrity only (prevent tampering); │
  │  no access restriction needed                           │
  └─────────────────────────────────────────────────────────┘
```

### 2.2 Access Control Models

Access control defines who can access what data, under what conditions. DAMA recognises four primary access control models — each with different strengths and appropriate use cases.

```
ACCESS CONTROL MODELS — COMPARISON

  ┌───────────────────────────────────────────────────────┐
  │  DAC — Discretionary Access Control                   │
  │                                                       │
  │  Who controls access: The DATA OWNER decides who      │
  │  can access their data and delegates permissions.     │
  │                                                       │
  │  How it works: Owner grants READ/WRITE/EXECUTE        │
  │  permissions to specific users or groups.             │
  │                                                       │
  │  Strength: Flexible; owner-controlled                 │
  │  Weakness: Hard to audit at scale; owner may          │
  │  grant excessive access; no central oversight         │
  │                                                       │
  │  Malaysian example: SharePoint folders where the      │
  │  document owner manually grants access to teammates   │
  └───────────────────────────────────────────────────────┘
  ┌───────────────────────────────────────────────────────┐
  │  MAC — Mandatory Access Control                       │
  │                                                       │
  │  Who controls access: The SYSTEM enforces a           │
  │  classification-based policy; individuals cannot      │
  │  override it.                                         │
  │                                                       │
  │  How it works: Data is labelled with a security       │
  │  level (Restricted / Confidential / Internal /        │
  │  Public). Users have a clearance level. Access        │
  │  granted only if user clearance ≥ data classification.│
  │                                                       │
  │  Strength: Centrally enforced; consistent; auditable  │
  │  Weakness: Rigid; complex to implement commercially   │
  │                                                       │
  │  Malaysian example: Government / defence systems;     │
  │  NACSA-classified national security data              │
  └───────────────────────────────────────────────────────┘
  ┌───────────────────────────────────────────────────────┐
  │  RBAC — Role-Based Access Control                     │
  │                                                       │
  │  Who controls access: Permissions are assigned to     │
  │  ROLES; users are assigned to roles.                  │
  │                                                       │
  │  How it works:                                        │
  │  ROLE: Loan_Officer → can VIEW loan applications,    │
  │                        APPROVE loans < MYR 500K      │
  │  USER: Ahmad → assigned ROLE: Loan_Officer           │
  │  Ahmad inherits all Loan_Officer permissions.         │
  │                                                       │
  │  Strength: Scalable; easy to manage; audit-friendly   │
  │  Weakness: Role explosion if not governed carefully   │
  │                                                       │
  │  Malaysian example: Core banking RBAC; ERP roles      │
  │  (most common model in Malaysian enterprise)          │
  └───────────────────────────────────────────────────────┘
  ┌───────────────────────────────────────────────────────┐
  │  ABAC — Attribute-Based Access Control                │
  │                                                       │
  │  Who controls access: Policies evaluate multiple      │
  │  ATTRIBUTES of the user, the data, and the context   │
  │  to make dynamic access decisions.                    │
  │                                                       │
  │  How it works:                                        │
  │  Policy: "Allow access IF user.department = 'Risk'   │
  │           AND data.classification ≤ 'Confidential'   │
  │           AND context.time BETWEEN 08:00 AND 18:00   │
  │           AND context.location = 'Malaysia'"          │
  │                                                       │
  │  Strength: Highly granular; context-aware; flexible  │
  │  Weakness: Complex to design; harder to audit         │
  │                                                       │
  │  Malaysian example: Cloud-native platforms; zero-     │
  │  trust architecture; MyGovID federated access         │
  └───────────────────────────────────────────────────────┘
```

### 2.3 Privacy-Preserving Techniques — Masking, Tokenisation, Anonymisation

These techniques protect sensitive data while preserving its utility for non-production use cases (testing, analytics, development, external sharing).

```
PRIVACY-PRESERVING TECHNIQUES — COMPARISON

  TECHNIQUE        REVERSIBLE?   USE CASE              Malaysian Example
  ────────────────────────────────────────────────────────────────────────
  Data Masking     No (static)   Non-prod environments  Mask NRIC in UAT:
  (Static)                       Test data generation   620514-**-**** 
                                                         → format preserved

  Data Masking     No (dynamic)  Production queries by  Customer service rep
  (Dynamic)                      lower-privilege users   sees only last 4 digits
                                                         of card number in UI

  Tokenisation     Yes           Payment processing;     Card PAN replaced
                  (with vault)   high-value identifiers  by token in merchant
                                                         system; real PAN in
                                                         secure vault (PCI DSS)

  Pseudonymisation Yes           Analytics; research;    Replace NRIC with
                  (with key)     data sharing            consistent pseudoID
                                                         (same person = same
                                                         pseudo ID across records)

  Anonymisation    No            Public datasets;        Remove all direct +
                  (irreversible) open data publication   quasi-identifiers;
                                                         k-anonymity applied

  Encryption       Yes           Data at rest/transit    AES-256 for customer
                  (with key)     (not a de-id technique) data files; TLS 1.3
                                                         for API calls
  ────────────────────────────────────────────────────────────────────────
  PDPA 2010 Note:
  "Anonymous" data is outside PDPA scope — it is no longer personal data.
  "Pseudonymised" data IS still personal data — re-identification is possible.
  This distinction is tested on the exam.
```

### 2.4 Encryption — At Rest, In Transit, In Use

**Encryption at Rest** — Data stored on disk, in databases, in backup files, or in cloud object storage is encrypted so that physical access to storage media does not expose readable data. Standard: AES-256 (Advanced Encryption Standard, 256-bit key).

**Encryption in Transit** — Data moving across networks (client-server, server-server, API calls) is encrypted so that network eavesdropping does not expose readable data. Standard: TLS 1.2 minimum; TLS 1.3 preferred. Older: SSL (deprecated, do not use).

**Encryption in Use** — An emerging capability (Homomorphic Encryption, Trusted Execution Environments) where data remains encrypted even while being processed. Still largely research-stage for most production use cases.

**Key Management** — Encryption is only as strong as key management. If encryption keys are lost, data is permanently inaccessible. If keys are stolen, encryption provides no protection. Key management requirements include: secure key generation, key rotation policies, separation of key custody from data custody, and hardware security modules (HSMs) for high-value keys.

### 2.5 Authentication and Authorisation

**Authentication** — Verifying *who* is accessing the system (identity verification).

```
AUTHENTICATION FACTORS — MFA

  Something you KNOW     → Password, PIN, security question
  Something you HAVE     → Token, smart card, mobile authenticator (TOTP)
  Something you ARE      → Fingerprint, face recognition, iris scan
  Something you DO       → Typing rhythm, gait analysis (behavioural)

  MFA (Multi-Factor Authentication): Requires ≥ 2 factors
  BNM RMIT 2020: MFA is required for all privileged access
  and remote access to critical systems in Malaysian banks.
```

**Authorisation** — Determining *what* an authenticated user is permitted to do (access control, as described in 2.2).

**Principle of Least Privilege** — Every user, system, and process should have only the minimum access required to perform their function — nothing more. Over-privileged accounts are one of the most common vectors for insider threats and compromised credential misuse.

**Segregation of Duties (SoD)** — No single person should have end-to-end control over a sensitive process. In banking: the person who initiates a payment should not also be the person who approves it. In data management: the DBA who manages production data should not also be the person who approves their own access requests.

### 2.6 Data Security Activities (DAMA Chapter 7)

| Activity | Description |
|---|---|
| **Identify data security requirements** | Determine what data exists, its classification, regulatory obligations, and applicable security standards |
| **Define data security policy** | Document what security controls apply to each data classification level; align with organisational risk appetite |
| **Define data security standards** | Specify the technical implementation standards (encryption algorithms, key lengths, authentication protocols, audit log retention) |
| **Implement data security controls** | Deploy technical controls: access management, encryption, masking, monitoring, DLP tools |
| **Perform data security audits** | Regularly review actual access against entitlements; review audit logs; test controls; conduct penetration testing |
| **Manage data security incidents** | Detect, contain, investigate, and remediate breaches; notify affected parties and regulators per legal obligation |
| **Provide data security training** | Ensure all staff with data access understand their security obligations; phishing awareness; data handling procedures |

### 2.7 Monitoring, Auditing, and Incident Response

**Security Monitoring** — Continuous surveillance of data access events to detect anomalies. Tools include SIEM (Security Information and Event Management) systems that aggregate logs from databases, applications, network devices, and identity systems, applying rules and ML models to detect suspicious patterns.

**Access Audit Logs** — Every access event to sensitive data should be logged: who accessed what, when, from where, and what action was performed (read/write/delete). Logs must be tamper-proof (write-once), retained for the audit period (typically 1–3 years per BNM RMIT), and reviewed regularly.

```
DATA BREACH INCIDENT RESPONSE — PROCESS

  DETECTION
  → Anomaly detected in SIEM / reported by staff / external notification
       │
       ▼
  CONTAINMENT
  → Isolate affected systems; revoke compromised credentials;
    block exfiltration paths; preserve evidence
       │
       ▼
  INVESTIGATION
  → Determine: What data was accessed? How many records?
    Which individuals? What was the attack vector?
    Is the breach contained?
       │
       ▼
  NOTIFICATION (PDPA 2010 + BNM RMIT)
  → Notify affected data subjects if personal data breached
  → Notify BNM within 24 hours for significant incidents
  → Notify NACSA for critical infrastructure incidents
  → Notify MCMC per Cybersecurity Act 2018 requirements
       │
       ▼
  REMEDIATION
  → Patch vulnerability; update controls; reset credentials;
    implement additional monitoring
       │
       ▼
  POST-INCIDENT REVIEW
  → Root cause analysis; lessons learned; control improvements;
    update incident response plan
```

### 2.8 Data Loss Prevention (DLP)

DLP tools monitor, detect, and block the unauthorised transfer of sensitive data out of the organisation. DLP operates across three vectors:

- **Network DLP**: Monitors outbound network traffic (email, web, FTP) for sensitive data patterns (e.g., blocks emails containing NRIC numbers or card numbers to external addresses)
- **Endpoint DLP**: Monitors data copied to USB drives, printed, or transferred from endpoint devices
- **Storage DLP**: Scans data at rest to identify sensitive data stored in unauthorised locations

In Malaysian financial institutions, DLP is increasingly mandated — BNM RMIT requires banks to implement controls preventing unauthorised data exfiltration, and regulators have cited DLP as a specific expected control in technology risk assessments.

---

## Section 3: Real-World Scenarios — Malaysian Context

### Scenario 1: RHB Bank — Implementing RBAC for a Core Banking System Migration

**Business Context:**
RHB Bank is migrating from a legacy core banking system to a modern cloud-native platform. The legacy system had 847 user accounts, most with "full access" permissions granted historically on an ad-hoc basis — a common pattern in Malaysian banks that grew through acquisition. The migration is an opportunity to implement proper Role-Based Access Control aligned with BNM RMIT 2020 requirements.

**The Security Challenge:**
An access review reveals that 68% of users have access to data they have not touched in 12 months. Three tellers have SQL-level database access (they should only use the application UI). Two IT contractors from 2019 still have active credentials. The Head of Retail Banking has system administrator privileges from a project three years ago that was never revoked.

**RBAC Implementation Design:**

```
RHB RBAC DESIGN — ROLE HIERARCHY

  SYSTEM ROLES (coarse-grained)
  ─────────────────────────────────────────────────────
  ROLE: Branch_Teller
  PERMISSIONS:
    ✓ VIEW: Customer profile (masked NRIC, name, address)
    ✓ VIEW: Account balance (own branch customers only)
    ✓ CREATE: Cash deposit/withdrawal transactions < MYR 10K
    ✓ VIEW: Transaction history (last 90 days)
    ✗ VIEW: Credit score, full account history
    ✗ APPROVE: Any transaction
    ✗ ACCESS: Backend database directly

  ROLE: Loan_Officer
  PERMISSIONS:
    ✓ VIEW: Full customer profile (unmasked, with business need)
    ✓ VIEW: Credit history, scoring
    ✓ CREATE: Loan applications
    ✓ APPROVE: Loans < MYR 500K
    ✗ APPROVE: Own loan applications (SoD control)
    ✗ ACCESS: Systems outside loan origination module

  ROLE: Compliance_Analyst
  PERMISSIONS:
    ✓ VIEW: Aggregated transaction reports (anonymised)
    ✓ VIEW: AML alert queue
    ✓ ACCESS: Regulatory reporting module (read-only)
    ✗ MODIFY: Any customer record
    ✗ VIEW: Individual customer data without case basis

  ROLE: DBA_Production
  PERMISSIONS:
    ✓ MANAGE: Database schema changes (via approved change request)
    ✓ VIEW: Performance metrics, query plans
    ✗ VIEW: Customer personal data (data masking applied to DBA queries)
    ✗ APPROVE: Own access changes (SoD control)

  SEPARATION OF DUTIES CONTROLS:
  ─────────────────────────────────────────────────────
  • No user can both initiate AND approve a payment
  • No DBA can view unmasked customer personal data
  • No IT admin can approve their own access requests
  • No single user can both create and release a regulatory report
```

**Access Certification Programme:**
Every 90 days, each role owner receives an access certification report listing all users in their role. They must actively recertify each user — "yes, this person still needs this access" — or initiate removal. Unused access is automatically flagged for review after 60 days of inactivity.

**BNM RMIT Link:** RMIT Principle 5 requires banks to implement access management controls proportionate to the risk of the data being accessed. The RBAC design, quarterly access certification, and DBA data masking directly satisfy this requirement.

---

### Scenario 2: Hospital Kuala Lumpur — Patient Data Classification and De-identification

**Business Context:**
Hospital Kuala Lumpur (HKL) is partnering with UM (University of Malaya) to share patient data for medical research on diabetes prevalence in Malaysian Chinese, Malay, and Indian populations. The research team needs demographic and clinical data. The hospital's Data Protection Officer (DPO) must ensure that sharing complies with PDPA 2010 and the Ministry of Health's data sharing guidelines.

**The Privacy Challenge:**
Full patient records contain: NRIC, name, address, date of birth, diagnosis codes, medication history, lab results, physician notes, and ethnicity. Sharing this in full would be a PDPA violation and an ethical breach. The research team needs enough data to conduct population-level analysis but does not need any information that identifies individual patients.

**De-identification Design:**

```
HKL → UM DATA DE-IDENTIFICATION PIPELINE

  ORIGINAL PATIENT RECORD (RESTRICTED)
  ──────────────────────────────────────
  NRIC:         620514-14-5678          → REMOVE (direct identifier)
  Full Name:    Tan Ah Kow              → REMOVE (direct identifier)
  Address:      No. 14, Jalan Ampang    → GENERALISE → "Kuala Lumpur"
  Date of Birth: 14 May 1962           → GENERALISE → "1960-1964 cohort"
  Ethnicity:    Chinese                 → RETAIN (research variable)
  Diagnosis:    Type 2 Diabetes (E11)  → RETAIN (ICD-10 code only)
  HbA1c Result: 8.4%                   → RETAIN
  Medications:  Metformin 1000mg       → RETAIN (generic drug name)
  Physician:    Dr. Rajesh Kumar       → REMOVE (identifies treating doctor)
  Clinic:       Diabetes Centre, HKL   → GENERALISE → "Major public hospital, KL"

  RESEARCH DATASET (ANONYMISED — OUTSIDE PDPA SCOPE)
  ──────────────────────────────────────────────────
  Patient_Ref:  RES-2024-00847         → Pseudonym (internal to HKL only)
  Age_Cohort:   60-64                  → Generalised age
  Region:       Kuala Lumpur           → Generalised location
  Ethnicity:    Chinese
  Diagnosis:    E11 (Type 2 Diabetes)
  HbA1c:        8.4%
  Medication:   Metformin 1000mg

  K-ANONYMITY CHECK:
  The research dataset must satisfy k-anonymity ≥ 5:
  At least 5 patients share each combination of
  Age_Cohort + Region + Ethnicity.
  If any combination has fewer than 5 records → further
  generalise or suppress those records before sharing.
```

**PDPA 2010 Link:** Section 40 and Schedule 1 of PDPA 2010 list sensitive personal data requiring additional protection — health data is explicitly included. The de-identification pipeline transforms PDPA-regulated personal health data into research data outside PDPA scope. The DPO signs off on the adequacy of de-identification before data is released to UM.

**CDMP Link:** This scenario tests de-identification techniques (anonymisation, generalisation, suppression), the distinction between pseudonymisation and anonymisation, PDPA scope, and the data security governance role of the DPO.

---

### Scenario 3: LHDN (Inland Revenue Board) — Breach Response and NACSA Notification

**Business Context:**
LHDN's e-Filing system experiences a data breach. An attacker exploits a SQL injection vulnerability in the income declaration portal and exfiltrates approximately 180,000 taxpayer records containing: NRIC, name, employer name, income figures, and bank account numbers (for tax refunds). LHDN's CISO activates the incident response plan at 02:14 AM when SIEM alerts flag anomalous database query volumes.

**Incident Response Execution:**

```
LHDN BREACH INCIDENT TIMELINE

  02:14  SIEM alert: Anomalous SELECT volume on taxpayer DB
  02:17  SOC analyst confirms: external IP extracting records
         at 12,000 rows/minute via the e-Filing API layer

  02:22  CONTAINMENT:
         → e-Filing portal taken offline (availability vs security)
         → Attacking IP blocked at perimeter firewall
         → API rate limiting tightened to 100 req/min
         → Database session monitoring activated

  02:45  SCOPE ASSESSMENT:
         → Forensic analysis of query logs: 180,247 records
         → Data types: NRIC, name, employer, income, bank acct
         → Attack vector: SQL injection in tax declaration form
         → Duration: 47 minutes of active exfiltration

  03:00  ESCALATION:
         → CISO briefs Director General
         → Legal and DPO notified
         → Incident Response Team assembled

  06:00  REGULATORY NOTIFICATION:
         → NACSA notified (LHDN = critical national infrastructure)
         → MCMC notified (Cybersecurity Act 2018 obligation)
         → MOF (Ministry of Finance) briefed as data controller

  09:00  AFFECTED PARTY NOTIFICATION PLANNING:
         → 180,247 affected taxpayers to be notified
         → Notification template drafted (per PDPA best practice)
         → MyGov portal notice + direct email to affected taxpayers

  D+3   REMEDIATION:
         → SQL injection vulnerability patched (WAF rule + code fix)
         → All taxpayer passwords force-reset
         → Enhanced monitoring deployed on e-Filing DB
         → Bank account field encrypted at rest (was plain text)

  D+14  POST-INCIDENT REVIEW:
         → Root cause: lack of parameterised queries in 2019 legacy code
         → Contributing: no WAF (Web Application Firewall) before e-Filing
         → Control gaps: Bank account numbers not encrypted at rest
         → Recommendations: WAF deployment, code security review,
           encryption-at-rest for all PAN/bank account fields,
           quarterly penetration testing programme
```

**Regulatory Obligations Triggered:**
Under Malaysia's PDPA 2010 (as amended post-2022 with mandatory breach notification provisions), LHDN is obligated to notify affected data subjects without undue delay. NACSA's National Cyber Security Policy designates LHDN as a Critical National Information Infrastructure (CNII) operator — mandatory incident reporting applies. The Cybersecurity Act 2018 (Act 791) requires CNII operators to report cybersecurity incidents to NACSA within 6 hours.

**CDMP Link:** This scenario tests the incident response lifecycle, regulatory breach notification obligations, post-incident remediation, and the governance role of the DPO/CISO in a data security programme.

---

## Section 4: Visual Diagrams + Cheat Sheet

### 4.1 Data Security Control Framework — Layered Defence

```
DEFENCE IN DEPTH — LAYERED SECURITY CONTROLS

  OUTER LAYER: NETWORK SECURITY
  ──────────────────────────────────────────────────────
  Firewalls, IDS/IPS, Anti-DDoS, Network segmentation,
  DMZ (Demilitarised Zone), VPN for remote access

  ▼ Data that passes network controls reaches:

  MIDDLE LAYER: APPLICATION SECURITY
  ──────────────────────────────────────────────────────
  Authentication (MFA), Session management,
  Input validation (prevent SQL injection/XSS),
  Web Application Firewall (WAF),
  API security (OAuth, rate limiting, API keys)

  ▼ Authenticated users reach:

  INNER LAYER: DATA SECURITY
  ──────────────────────────────────────────────────────
  Access control (RBAC/ABAC), Data classification,
  Encryption at rest, Dynamic data masking,
  Row-level security, Column-level permissions,
  Audit logging of every data access event

  ▼ Approved access is monitored by:

  MONITORING LAYER: DETECTION & RESPONSE
  ──────────────────────────────────────────────────────
  SIEM (log aggregation + anomaly detection),
  DLP (data loss prevention),
  User behaviour analytics (UBA),
  24/7 Security Operations Centre (SOC),
  Automated incident response playbooks
```

### 4.2 Need-to-Know vs Need-to-Share

```
TWO COMPETING PRINCIPLES — BALANCING ACT

  NEED-TO-KNOW (Security default)
  ─────────────────────────────────────────────────────
  Grant access only to those who NEED the data to perform
  their job. Deny by default; grant by exception.
  → Risk: Over-restriction limits data utility
  → Applied when: High sensitivity data; regulatory constraint

  NEED-TO-SHARE (Analytics/collaboration default)
  ─────────────────────────────────────────────────────
  Share data broadly to maximise analytical value,
  enable innovation, and improve operational efficiency.
  → Risk: Over-sharing increases breach surface area
  → Applied when: Low-sensitivity aggregated/anonymised data

  RESOLUTION:
  ─────────────────────────────────────────────────────
  Data classification resolves the tension:
  RESTRICTED / CONFIDENTIAL → Need-to-Know
  INTERNAL / PUBLIC → Need-to-Share (within appropriate bounds)

  The data model determines what data exists.
  The classification determines how sensitive it is.
  The access control model determines who can see it.
  The audit log proves who did see it.
```

### 4.3 PDPA 2010 — Security Obligations at a Glance

```
PDPA 2010 (ACT 709) — DATA SECURITY REQUIREMENTS

  Section 9 — Security of Personal Data
  ───────────────────────────────────────────────────────
  "A data user shall take practical steps to protect
  the personal data from any loss, misuse, modification,
  unauthorised or accidental access or disclosure,
  alteration or destruction."

  WHAT THIS REQUIRES IN PRACTICE:
  ✓ Encryption for personal data at rest and in transit
  ✓ Access controls limiting access to authorised staff
  ✓ Staff training on data handling obligations
  ✓ Secure disposal of personal data media
  ✓ Third-party processor contracts with security obligations
  ✓ Incident response plan for data breaches
  ✓ Regular security review of systems handling personal data

  Section 10 — Retention of Personal Data
  ───────────────────────────────────────────────────────
  Personal data shall not be retained longer than necessary.
  → Secure disposal at end of retention period is a
    security AND compliance requirement.

  Sensitive Personal Data (Schedule 1) — Requires heightened protection:
  Physical/mental health | Ethnicity/race | Religion | Politics
  Criminal offences | Sexual offences | Trade union membership
  → RESTRICTED classification minimum
```

### 4.4 Masking vs Tokenisation vs Anonymisation — Decision Guide

```
WHICH TECHNIQUE TO CHOOSE?

  Do you need to REVERSE the transformation?
  │
  ├── NO → Use ANONYMISATION (irreversible)
  │        When: Public datasets, open data, research
  │        PDPA: Anonymous data is outside PDPA scope
  │
  └── YES
       │
       Is the original value needed ONLY in a SECURE VAULT
       (not in the production system)?
       │
       ├── YES → Use TOKENISATION
       │         When: Payment card numbers (PCI DSS);
       │         replace PAN with token in merchant system,
       │         real PAN stays in secure token vault
       │
       └── NO
            │
            Is re-identification needed per PERSON
            (same person → same pseudonym)?
            │
            ├── YES → Use PSEUDONYMISATION
            │         When: Analytics, research where
            │         longitudinal tracking per person matters
            │         PDPA: Still personal data — PDPA applies
            │
            └── NO → Use DATA MASKING
                      STATIC: Non-production environments,
                              test data, development
                      DYNAMIC: Production access for lower-
                               privilege users (e.g., call centre)
```

### 4.5 Cheat Sheet — Chapter 7 Key Terms

| Term | One-Line Definition | Exam Trap |
|---|---|---|
| **CIA Triad** | Confidentiality, Integrity, Availability — the three security properties | Over-controlling Confidentiality can threaten Availability |
| **Data Classification** | Assigning sensitivity levels to data to determine appropriate controls | Classification is a GOVERNANCE decision, not a technical one |
| **DAC** | Data owner controls access permissions | Flexible but hard to audit at scale; owner may over-grant |
| **MAC** | System enforces classification-based policy; individuals cannot override | Rigid; used in government/defence contexts |
| **RBAC** | Permissions assigned to roles; users assigned to roles | Most common in enterprise; watch for "role explosion" |
| **ABAC** | Access decisions based on multiple attributes of user + data + context | Most flexible; most complex; context-aware |
| **Least Privilege** | Grant only the minimum access needed to perform a function | Applies to users AND automated processes/service accounts |
| **Segregation of Duties** | No single person controls an entire sensitive process end-to-end | Classic exam scenario: initiator ≠ approver |
| **Static Masking** | Permanent replacement of sensitive values in non-production data | Irreversible; safe for test environments |
| **Dynamic Masking** | Real-time masking applied at query time for lower-privilege users | Original data unchanged; mask applied in the presentation layer |
| **Tokenisation** | Replace sensitive value with a random token; original stored in vault | Reversible only with access to the vault; PCI DSS standard |
| **Pseudonymisation** | Replace direct identifiers with consistent pseudonyms per person | Still personal data under PDPA — re-identification is possible |
| **Anonymisation** | Irreversible removal/transformation of all identifying information | Truly anonymous data is outside PDPA scope |
| **Encryption at Rest** | Data on disk/storage is encrypted | Key management is as critical as encryption itself |
| **Encryption in Transit** | Data moving across networks is encrypted (TLS 1.2/1.3) | TLS 1.0/1.1 are deprecated — never use SSL |
| **MFA** | Multi-Factor Authentication — ≥ 2 authentication factors required | BNM RMIT mandates MFA for privileged and remote access |
| **DLP** | Data Loss Prevention — detects and blocks unauthorised data exfiltration | Network DLP + Endpoint DLP + Storage DLP = full coverage |
| **SIEM** | Security Information and Event Management — aggregates and analyses security logs | Detection tool; does not prevent breaches, only detects them |
| **Data Breach** | Unauthorised access, disclosure, modification, or destruction of personal data | PDPA breach notification; BNM 24-hour notification; NACSA 6-hour |
| **RPO/RTO** | Recovery Point Objective / Recovery Time Objective (see Chapter 6) | Security and operations share these metrics; availability is CIA |

### 4.6 CDMP Exam Traps — Chapter 7

```
COMMON EXAM TRAPS — DATA SECURITY

  TRAP 1: Pseudonymisation ≠ Anonymisation
  ──────────────────────────────────────────
  "Pseudonymised data is outside the scope of PDPA."
  → FALSE. Pseudonymised data is still personal data because
    re-identification is possible with the mapping key.
    ONLY anonymised data (irreversible, no re-id possible) is
    outside PDPA scope.

  TRAP 2: RBAC scope
  ───────────────────
  "RBAC eliminates the need for data classification."
  → FALSE. Classification defines WHAT controls are needed.
    RBAC is the MECHANISM that enforces those controls.
    You need both — classification first, RBAC second.

  TRAP 3: Encryption = security
  ───────────────────────────────
  "Encrypting customer data at rest satisfies all PDPA
  security obligations."
  → FALSE. Encryption is ONE control. PDPA Section 9 requires
    'practical steps' — which includes access control, staff
    training, secure disposal, and incident response.

  TRAP 4: The CIA tension
  ────────────────────────
  "The primary goal of data security is maximum
  confidentiality."
  → FALSE. DAMA positions security as BALANCING all three:
    Confidentiality, Integrity, AND Availability.
    A system locked down so tightly that authorised users
    cannot access data has failed Availability — a security
    failure, not a security success.

  TRAP 5: Masking in production
  ───────────────────────────────
  "Static data masking is appropriate for protecting
  sensitive fields in a production database."
  → FALSE. Static masking permanently replaces data — it
    should be used in non-production environments (UAT, dev).
    In production, DYNAMIC masking preserves the original data
    while presenting masked values to lower-privilege users.

  TRAP 6: Who owns data classification?
  ───────────────────────────────────────
  "The IT security team is responsible for classifying data."
  → FALSE. Data classification is a BUSINESS decision owned
    by the Data Owner (a business role). IT implements the
    technical controls that enforce the classification.
    Business defines sensitivity; IT enforces it.
```

---

## Section 5: Official DAMA Images

### DAMA Data Security Knowledge Area Context Diagram

*Source: DAMA International, DAMA-DMBOK2 Knowledge Area Context Diagram Series*
*License: Creative Commons CC BY-ND 4.0 | © DAMA International*

![DAMA Data Security KA Context Diagram](https://dama.org/wp-content/uploads/sites/2326/2025/04/x-2.png.webp)

> **Reading the context diagram:** Data Security receives inputs from Data Governance (security policies and classification standards), Data Architecture (data flows and system boundaries), and external regulatory requirements (PDPA, BNM RMIT, PCI DSS). Its outputs include access control implementations, audit logs, incident reports, and security metrics. Note that Data Security controls apply to ALL other Knowledge Areas — every chapter in the DAMA Wheel has a security dimension that Chapter 7 governs.

*Note: If the image above does not render, refer to Day01 Section 5 for the complete DAMA KA gallery.*

---

## Chapter 7 at a Glance — One-Page Summary

```
DATA SECURITY — CDMP EXAM SUMMARY
══════════════════════════════════════════════════════════════

WHAT:   Policies, procedures, and controls protecting data
        from unauthorised access, use, disclosure, or destruction

FOUNDATION: CIA TRIAD
  Confidentiality → Who can see it
  Integrity       → Is it accurate and unaltered
  Availability    → Can authorised users access it when needed

DATA CLASSIFICATION (4 tiers):
  RESTRICTED    → Highest sensitivity; PDPA sensitive data
  CONFIDENTIAL  → Business-sensitive; personal data (combined)
  INTERNAL      → Internal use only; no external sharing
  PUBLIC        → Approved for unrestricted access

ACCESS CONTROL MODELS:
  DAC   → Owner controls access (flexible; hard to audit)
  MAC   → System enforces classification (rigid; government)
  RBAC  → Role-based permissions (most common enterprise)
  ABAC  → Attribute + context-based (granular; cloud-native)

PRINCIPLES:
  Least Privilege      → Minimum access required
  Segregation of Duties → No single end-to-end control

PRIVACY-PRESERVING TECHNIQUES:
  Static Masking   → Non-prod environments; irreversible
  Dynamic Masking  → Production; lower-privilege view
  Tokenisation     → PCI DSS; reversible with vault
  Pseudonymisation → Research; consistent pseudonym; PDPA still applies
  Anonymisation    → Public data; irreversible; outside PDPA

ENCRYPTION:
  At Rest: AES-256 | In Transit: TLS 1.2+ | Key management critical

ACTIVITIES: Classify → Policy → Standards → Implement → Audit → Respond → Train

MALAYSIAN REGULATIONS:
  PDPA 2010 S.9 (Security) | BNM RMIT (access, encryption, audit)
  Cybersecurity Act 2018 (CNII breach: 6-hour notification to NACSA)

EXAM WEIGHT: ~11% — One of the highest-weighted chapters
══════════════════════════════════════════════════════════════
```


