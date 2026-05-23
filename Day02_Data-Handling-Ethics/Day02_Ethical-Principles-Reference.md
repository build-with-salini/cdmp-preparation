# Day 02 — Ethical Principles Reference
**DAMA-DMBOK2 | Chapter 2 | Supplementary Material**

> *"Always choose actions that promote fairness, accountability, and respect for individuals and their data."*
> — Ethical Principles Summary, DAMA-DMBOK2

---

## Overview

This reference expands the seven core ethical principles from the DAMA-DMBOK2 framework into a detailed study resource. Each principle is mapped to its DMBOK2 source, a working definition, practical examples, Malaysian regulatory context, CDMP exam signals, and common violations — giving you multiple angles to recognise and apply each principle under exam conditions.

---

## The Seven Ethical Principles — Master Reference Table

| # | Principle | Core Definition | What It Requires in Practice | What Violates It |
|---|-----------|----------------|------------------------------|------------------|
| 1 | **Fairness** | Ensure data collection, analysis, and use are free from bias or discrimination | Audit algorithms for disparate impact; use representative datasets; test models across demographic groups | Training a model on historically biased data without testing for discriminatory outcomes |
| 2 | **Transparency** | Be open about how and why data is collected, processed, and shared | Publish privacy notices; document model logic; communicate data use purposes clearly | Deploying an AI model with no explainability; burying data use terms in 4,000-word T&Cs |
| 3 | **Accountability** | Assign responsibility for data use decisions and their consequences | Governance councils review and report on ethical data use; data owners are named; audit trails exist | No named Data Owner for a domain; no record of who approved a data use decision |
| 4 | **Consent** | Collect and use data with informed, voluntary agreement from individuals | Obtain new consent when reusing data for a purpose beyond original scope; consent must be specific, informed, unambiguous | Reusing purchase data for marketing analytics when original consent form only mentioned order processing |
| 5 | **Privacy** | Protect individuals' rights to control their personal data | Mask personal identifiers; minimise access to sensitive data; implement Privacy by Design | Sharing patient records across systems without access controls; retaining personal data beyond its purpose |
| 6 | **Stewardship** | Manage data as a valuable asset with care and integrity | Apply retention, quality, and security policies consistently; document lineage; maintain data accuracy | Collecting data "just in case" with no retention schedule; siloed data with no quality checks |
| 7 | **Lawfulness** | Comply with all applicable data protection regulations and obligations | Follow GDPR, PDPA, HIPAA, BNM RMIT, or other relevant laws; monitor regulatory changes | Processing personal data without a lawful basis; transferring data cross-border without appropriate safeguards |

---

## Principle 1 — Fairness

### Definition
Ensure that data collection, analysis, and use are free from bias or discrimination.

### DMBOK2 Grounding
Maps to the Belmont Principle of **Justice** — fair and equitable treatment of people. DAMA explicitly states that the ethical principle of justice creates a *positive duty* to identify and address bias, not merely to avoid intentional discrimination.

### What It Requires

| Action Area | Detail |
|-------------|--------|
| **Data Collection** | Sampling methodology must be tested for systematic exclusion of demographic groups |
| **Model Training** | Training datasets must be audited for historical bias before use — biased history produces biased outputs |
| **Algorithm Testing** | Disparate impact testing must be performed across gender, race, age, income, and geography segments |
| **Ongoing Monitoring** | Models must be monitored post-deployment — bias can emerge as data distributions shift |
| **Documentation** | Bias testing methodology, results, and remediation must be documented and auditable |

### Practical Examples

| Context | Fairness Failure | Ethical Response |
|---------|-----------------|------------------|
| Hiring | AI screening model trained on historical hires rejects more women than men | Audit training data; apply bias detection; require human review for borderline cases |
| Lending | Credit model disadvantages applicants from certain postcodes | Test model for postcode-based disparate impact; use alternative data sources |
| Customer Segmentation | High-value segment excludes a demographic group, leading to differential service quality | Review segmentation logic; test outcomes across demographic groups |
| Healthcare | Predictive model for disease risk performs worse for minority populations | Ensure training data is representative; test model accuracy by demographic group |

### Malaysian Regulatory Link
- **PDPA 2010 — Data Integrity Principle**: Data must be accurate and not misleading — biased data produces inaccurate representations of individuals
- **BNM RMIT**: Financial institutions must ensure models used in credit decisions are explainable and do not produce discriminatory outcomes
- **MyDIGITAL / MDEC**: AI governance guidelines emphasise fairness in algorithmic decision-making

### CDMP Exam Signal
Questions involving algorithmic bias, biased training data, or discriminatory outcomes → **Fairness** is the primary principle. Secondary: **Accountability** (who is responsible for detecting it), **Transparency** (can the decision be explained).

---

## Principle 2 — Transparency

### Definition
Be open about how and why data is collected, processed, and shared.

### DMBOK2 Grounding
Maps to the OECD **Openness Principle** and the GDPR requirement for **lawfulness, fairness, and transparency**. DAMA ties transparency to the concept of truthfulness — not using data to mislead, and being clear about sources, uses, and intent.

### What It Requires

| Action Area | Detail |
|-------------|--------|
| **Privacy Notices** | Clear, plain-language notices stating what data is collected, why, how long it will be kept, and with whom it is shared |
| **AI/Model Explainability** | Individuals affected by automated decisions must be able to understand the basis of those decisions |
| **Data Lineage** | Organisations must be able to show where data came from and how it was transformed |
| **Purpose Disclosure** | Specific purpose of data collection must be stated at the point of collection — not buried or vague |
| **Change Communication** | If data use changes materially, stakeholders must be informed |

### Practical Examples

| Context | Transparency Failure | Ethical Response |
|---------|---------------------|------------------|
| AI Loan Decisions | Customers denied loans with no explanation | Publish model decision criteria; provide written reasons; offer human review |
| Marketing Analytics | Customer data reused for marketing without disclosure | Update privacy notice; re-obtain consent for new purpose |
| Data Sharing | Customer data shared with third parties not mentioned in original notice | Amend privacy notice; disclose third-party recipients |
| BI Reporting | Chart uses manipulated scale to make performance look better | Use honest visualisation; include context and methodology notes |

### Malaysian Regulatory Link
- **PDPA 2010 — Notice & Choice Principle**: Data subjects must be informed of the purpose of collection and their choices regarding use
- **BNM RMIT**: Financial institutions must be able to explain model-driven decisions to regulators and customers
- **MCMC guidelines**: Digital communications must be transparent about data collection practices

### CDMP Exam Signal
Questions involving unexplained automated decisions, misleading visualisations, hidden data uses, or privacy notice failures → **Transparency** is the primary principle.

---

## Principle 3 — Accountability

### Definition
Assign responsibility for data use decisions and their consequences.

### DMBOK2 Grounding
Maps to the OECD **Accountability Principle** and GDPR's explicit **Accountability Principle** (organisations must demonstrate compliance, not merely claim it). In DMBOK2, accountability is operationalised through Data Governance — specifically through the roles of Data Owners, Data Stewards, and the Data Governance Council.

### What It Requires

| Action Area | Detail |
|-------------|--------|
| **Named Data Owners** | Every data domain must have a named business manager with approval authority over decisions about that data |
| **Governance Council Oversight** | The DGC reviews and reports on ethical data use — not just compliance checklists |
| **Audit Trails** | All data access, modification, and sharing decisions must be logged and auditable |
| **Escalation Paths** | Clear issue escalation paths so that ethical concerns can be raised and resolved |
| **Consequences** | Accountability is meaningless without consequences for violations — codes of conduct must be enforced |

### Practical Examples

| Context | Accountability Failure | Ethical Response |
|---------|----------------------|------------------|
| Data Breach | No named owner for the breached data — responsibility is unclear | Establish Data Owner for all sensitive domains before incidents occur |
| Regulatory Finding | Organisation cannot demonstrate who approved a data processing decision | Implement decision logging in governance workflow tools |
| Model Failure | AI model produces biased outputs; no one is responsible for monitoring | Assign Model Owner; establish model governance review schedule |
| Policy Non-Compliance | Employees violate data retention policy; no mechanism to detect or enforce | Automated compliance monitoring; annual ethics sign-off tied to performance review |

### Malaysian Regulatory Link
- **PDPA 2010 — General Principle**: The data processor/controller is accountable for compliance with all PDPA principles
- **BNM RMIT**: Boards and senior management of financial institutions are accountable for technology and data risk
- **Companies Act 2016**: Directors of Malaysian companies have fiduciary duties that extend to data governance failures with financial implications

### CDMP Exam Signal
Questions involving who is responsible for a data decision, what body should review a data ethics issue, or how compliance is demonstrated → **Accountability** is the primary principle.

---

## Principle 4 — Consent

### Definition
Collect and use data with informed, voluntary agreement from individuals.

### DMBOK2 Grounding
Maps to the PDPA **General Principle** and GDPR's requirement that consent be freely given, specific, informed, and unambiguous. DAMA's Chapter 2 links this to the Belmont Principle of **Respect for Persons** — individuals have the right to autonomy and self-determination over their data.

### What It Requires

| Action Area | Detail |
|-------------|--------|
| **Specificity** | Consent must be obtained for each specific purpose — blanket consent for "any future use" is not valid |
| **Informed** | Individuals must understand what they are consenting to in plain language — not legal jargon |
| **Voluntary** | Consent must not be a condition of service where data use is unrelated to that service |
| **Withdrawable** | Individuals must be able to withdraw consent, and withdrawal must be as easy as giving it |
| **Re-Consent** | When data is reused for a purpose beyond the original scope, new consent is required |

### Practical Examples

| Context | Consent Failure | Ethical Response |
|---------|----------------|------------------|
| E-Commerce | Purchase history reused for marketing analytics — original consent only covered order processing | Obtain new explicit consent for marketing analytics use |
| Healthcare | Patient records used for drug research — patients consented only to treatment | Obtain separate research consent; anonymise where possible |
| Employment | Employee wellness data used for performance assessment — employees consented only to wellness programme | Separate wellness and performance data; obtain explicit consent for any crossover |
| Mobile App | App collects location data continuously — consent form mentioned "occasional location access" | Re-present consent form with accurate description; allow granular permission settings |

### Malaysian Regulatory Link
- **PDPA 2010 — General Principle**: Personal data may only be processed with consent, unless an exception applies
- **PDPA 2010 — Notice & Choice Principle**: Must inform and give choice at point of collection
- **MyHEALTH data governance guidelines**: Patient consent frameworks for health data sharing

### CDMP Exam Signal
Questions involving data reuse, purpose creep, or data sharing beyond original scope → **Consent** is the primary principle. Often paired with **Transparency** (was the original notice clear?) and **Lawfulness** (is there a legal basis other than consent?).

---

## Principle 5 — Privacy

### Definition
Protect individuals' rights to control their personal data.

### DMBOK2 Grounding
DAMA explicitly states privacy is a fundamental human right. Connects to the EDPS position (2015) that "privacy is a fundamental human right" and that "dignity, privacy, and autonomy" are the platform on which a sustainable digital environment is built. Privacy by Design — embedding privacy controls from the beginning rather than retrofitting — is the operationalisation of this principle.

### What It Requires

| Action Area | Detail |
|-------------|--------|
| **Data Minimisation** | Only collect data that is necessary for the stated purpose |
| **Access Controls** | Minimise who can access sensitive data; implement role-based access |
| **Masking & Anonymisation** | Mask personal identifiers in non-production environments; test anonymisation for re-identification risk |
| **Retention Limitation** | Personal data must not be kept longer than necessary for its purpose |
| **Privacy by Design** | Privacy controls are built into system architecture from the start |
| **Subject Rights** | Individuals must be able to access, correct, and request deletion of their data |

### Practical Examples

| Context | Privacy Failure | Ethical Response |
|---------|----------------|------------------|
| Social Media Mining | Marketing team mines usernames and personal comments without consent | Aggregate sentiment data only; anonymise before analysis; comply with platform ToS |
| Data Lakes | Personal data loaded into analytics environment without masking | Classify and mask sensitive fields at ingestion; apply data access governance |
| Third-Party Sharing | Customer data shared with vendor without data processing agreement | Establish DPA with all vendors; limit data shared to minimum necessary |
| Legacy Systems | Old customer records retained 10 years beyond last transaction | Define and enforce retention schedules; automated purge after policy threshold |

### Malaysian Regulatory Link
- **PDPA 2010 — Security Principle**: Practical steps to protect against loss, misuse, modification, and unauthorised disclosure
- **PDPA 2010 — Retention Principle**: Data must not be kept longer than necessary
- **PDPA 2010 — Access Principle**: Individuals may access and correct their personal data

### CDMP Exam Signal
Questions involving social media data, anonymisation, data retention, access controls, or re-identification risk → **Privacy** is the primary principle. Often linked to **Lawfulness** (PDPA compliance) and **Stewardship** (retention policies).

---

## Principle 6 — Stewardship

### Definition
Manage data as a valuable asset with care and integrity.

### DMBOK2 Grounding
Directly maps to DMBOK2's foundational premise from Chapter 1: *"Failure to manage data is similar to failure to manage capital."* Stewardship is the operationalisation of treating data as an asset — applying consistent policies for quality, retention, security, and lineage across the entire data lifecycle.

### What It Requires

| Action Area | Detail |
|-------------|--------|
| **Data Quality** | Maintain accuracy, completeness, timeliness, and consistency of data |
| **Retention Policies** | Define and enforce how long each data category is kept — and when it must be deleted |
| **Security Policies** | Apply access controls, encryption, and audit logging consistently |
| **Lineage Documentation** | Know where data came from, how it was transformed, and who used it |
| **Data Minimisation** | Collect only what is needed — "just in case" collection is a stewardship failure |
| **Lifecycle Management** | Actively manage data from creation through to disposal |

### Practical Examples

| Context | Stewardship Failure | Ethical Response |
|---------|---------------------|------------------|
| Data Collection | Analytics team collects 50 attributes "just in case" — only 8 are ever used | Apply purpose specification before collection; review and delete unnecessary fields |
| Data Quality | Customer address data is 40% incomplete — decisions based on it are unreliable | Define quality rules; implement automated quality checks; assign Data Steward |
| Lineage | Organisation cannot trace how a regulatory report figure was calculated | Document data lineage from source to report; maintain transformation rules |
| Disposal | Personal data retained 7 years past customer relationship end — no retention schedule exists | Define category-level retention schedules; implement automated expiry flagging |

### Malaysian Regulatory Link
- **PDPA 2010 — Data Integrity Principle**: Data must be accurate, complete, and not misleading
- **PDPA 2010 — Retention Principle**: Active lifecycle management from collection to disposal
- **BNM RMIT**: Financial institutions must maintain complete and accurate data for risk reporting purposes

### CDMP Exam Signal
Questions involving data quality, retention, lifecycle management, or "over-collection" → **Stewardship** is the primary principle. Often paired with **Accountability** (who is the Data Steward?) and **Privacy** (retention limits).

---

## Principle 7 — Lawfulness

### Definition
Comply with all applicable data protection regulations and obligations.

### DMBOK2 Grounding
Maps to the OECD principle of accountability and the GDPR's first principle of **lawfulness, fairness, and transparency**. DAMA's position: law is the *floor*, not the ceiling. Lawfulness is the minimum. Ethics demands more. But lawfulness is still a hard, non-negotiable requirement.

### What It Requires

| Action Area | Detail |
|-------------|--------|
| **Legal Basis** | Every data processing activity must have a defined legal basis (consent, contract, legal obligation, vital interests, public task, or legitimate interests) |
| **Regulatory Compliance** | Ongoing compliance with PDPA, BNM RMIT, BCBS 239, GDPR (if applicable), HIPAA (if applicable) |
| **Cross-Border Transfers** | Data transfers across jurisdictions require appropriate safeguards (SCCs, adequacy decisions, binding corporate rules) |
| **Regulatory Monitoring** | Governance function must monitor evolving regulatory requirements — laws change |
| **Non-Compliance Consequences** | Understanding penalties for non-compliance and building compliance into risk management |

### Practical Examples

| Context | Lawfulness Failure | Ethical Response |
|---------|-------------------|------------------|
| Cross-Border Transfer | Customer data transferred EU→US without reviewing data transfer agreements | Apply Standard Contractual Clauses (SCCs); inform data subjects; obtain DPO sign-off |
| PDPA Breach | Customer data processed for a purpose not covered by consent or another lawful basis | Review lawful basis for all processing activities; update as necessary |
| Retention Violation | Personal data kept indefinitely — no retention schedule reviewed against PDPA | Define retention schedules aligned to PDPA Retention Principle; implement deletion workflows |
| Regulatory Reporting | Risk data submitted to BNM without documented lineage — fails RMIT data governance requirements | Implement data lineage for all regulatory reporting; document methodology |

### Malaysian Regulatory Link
- **PDPA 2010 (Act 709)**: The primary data protection law — applies to all commercial entities processing personal data
- **BNM RMIT 2020**: Risk Management in Technology — data governance requirements for financial institutions
- **MCMC Guidelines**: For digital communications and online data practices
- **BCBS 239**: International standard for risk data aggregation — relevant for Malaysian banks

### CDMP Exam Signal
Questions involving regulatory non-compliance, cross-border data transfers, processing without lawful basis, or regulatory reporting → **Lawfulness** is the primary principle. Remember: **ethics > governance > compliance**, but compliance is always required.

---

## Principles Interaction Map

Some situations involve multiple principles simultaneously. Understanding which principles are *primary* vs *secondary* in a scenario is the key CDMP exam skill.

| Scenario Type | Primary Principle | Secondary Principles |
|--------------|-------------------|----------------------|
| Biased AI/algorithm | Fairness | Accountability, Transparency |
| Data reused without re-consent | Consent | Transparency, Lawfulness |
| Unexplained automated decision | Transparency | Accountability, Fairness |
| Social media personal data mining | Privacy | Consent, Lawfulness |
| Cross-border data transfer without safeguards | Lawfulness | Accountability, Privacy |
| Over-collection of data attributes | Stewardship | Privacy, Lawfulness (Data Minimisation) |
| No named Data Owner | Accountability | Stewardship |
| Misleading visualisation | Transparency | Fairness (if it misrepresents a group) |
| Data breach due to weak access controls | Privacy | Stewardship, Accountability |
| Retaining data past its purpose | Stewardship | Privacy, Lawfulness |

---

## CDMP Exam Quick-Reference: The Seven Principles

| Principle | One-Line Test | Exam Trigger Words |
|-----------|--------------|-------------------|
| **Fairness** | Is anyone being disadvantaged by this data process? | bias, discrimination, disparate impact, algorithm, segmentation |
| **Transparency** | Can people understand what is happening with their data? | explainability, privacy notice, disclosure, hidden, unclear |
| **Accountability** | Is someone responsible and can they prove it? | data owner, governance council, audit trail, escalation |
| **Consent** | Did the individual genuinely agree to this specific use? | reuse, marketing, purpose creep, opt-in, original consent |
| **Privacy** | Are individuals in control of their personal information? | personal data, access controls, anonymisation, social media |
| **Stewardship** | Is data being treated as a well-managed asset? | quality, retention, lineage, over-collection, lifecycle |
| **Lawfulness** | Is there a legal basis for this data activity? | GDPR, PDPA, regulation, cross-border, compliance |

---

*References: DAMA-DMBOK2 Revised Edition, Chapter 2 | PDPA 2010 (Act 709) | GDPR 2016 | OECD Fair Information Processing Standards 1980 | BNM RMIT 2020 | Belmont Report 1979 | Ethical Principles Summary (DAMA-DMBOK2)*

