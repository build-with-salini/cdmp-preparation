# Day 02 — Data Handling Ethics
**DAMA-DMBOK2 | Chapter 2 | Exam Weight: ~11% (within Data Governance)**

> *"Ethics means doing it right when no one is looking."*
> — W. Edwards Deming (cited in DAMA-DMBOK2, Chapter 2)

---

## 1. Core Summary & Big Ideas

### What This Chapter Is Really About

Chapter 2 is the **moral and legal foundation** of the entire DMBOK2. While Chapter 1 establishes *why* data must be managed, Chapter 2 establishes *what principles must govern that management* from an ethical and societal perspective. It is the chapter that answers: "Just because we *can* use data this way — should we?"

This chapter is frequently underestimated by CDMP candidates. It is not a soft or theoretical chapter. It carries real exam weight because data ethics sits at the intersection of Data Governance (the highest-weighted KA at 11%) and every other practice area. The CDMP code of ethics is also a formal certification requirement — you sign it when you become certified.

Three core tensions run through the entire chapter:

- **Legal compliance vs. ethical obligation** — Following the law is the minimum. Ethics demands more.
- **Business value vs. individual rights** — Data has economic value, but it also represents people whose dignity must be respected.
- **Technical capability vs. social responsibility** — Organizations can do far more with data than they ethically should.

---

### Core Definitions

| Term | DAMA-DMBOK2 Definition / Key Point |
|------|-------------------------------------|
| **Ethics** | Principles of behavior based on ideas of right and wrong — specifically fairness, respect, responsibility, integrity, quality, reliability, transparency, and trust |
| **Data Handling Ethics** | How to procure, store, manage, use, and dispose of data in ways aligned with ethical principles |
| **Privacy** | A fundamental human right. The right of individuals to control information about themselves. Ethical imperative even where not legally mandated |
| **Beneficence** | Do not harm — maximize possible benefits and minimize possible harms |
| **Justice (data context)** | Fair and equitable treatment of people; awareness that algorithms and data processes can perpetuate systemic unfairness |
| **Bias** | An inclination of outlook — in statistics, deviation from expected values. Can be introduced at collection, selection, analysis, or presentation |
| **Data Masking** | Practice where only appropriate submitted data unlocks processes — operators cannot see the underlying values |
| **Privacy by Design** | Embedding privacy protections into system architecture from the beginning, not bolted on after deployment |

> **Key distinction the exam tests:** Following the law is not the same as ethical data handling. An organisation that is PDPA-compliant but uses customer data to discriminate algorithmically is legally covered but ethically failing. DAMA's position: **ethics is the higher standard**.

---

### The Three Core Ethical Concerns

These three themes organise everything in Chapter 2. Every scenario, every risk, every principle maps back to at least one of them.

**1. Impact on People**
Data represents characteristics of individuals and is used to make decisions that affect their lives — employment, credit, healthcare, housing. There is therefore an imperative to manage its quality and reliability. Inaccurate data doesn't just affect reports — it affects people's outcomes.

**2. Potential for Misuse**
Data can be used to mislead, discriminate, manipulate, or harm. The misuse is not always intentional — it can emerge from poor process design, lack of lineage documentation, or inadequate bias controls. Ethical imperative: prevent misuse whether or not it is intentional.

**3. Economic Value of Data**
Data has real economic value. Ethics of data ownership determine who can access that value and under what conditions. When data about one party (customers) is monetised by another party (the organisation) without informed consent, there is an ethical — and often legal — violation.

---

### The Belmont Principles Applied to Data

The Belmont Principles (originally for biomedical research) are explicitly cited by DAMA as a framework for data ethics. These are **high-frequency exam targets** in Type 2 (Principle-Based) and Type 10 (Judgment) questions.

| Principle | Biomedical Origin | Data Management Application |
|-----------|-------------------|----------------------------|
| **Respect for Persons** | Treat individuals with dignity and autonomy | Does your data system limit people's freedom of choice? Is consent informed and genuine? Does it protect people with diminished autonomy? |
| **Beneficence** | Do not harm; maximise benefit, minimise harm | Is data processing unnecessarily invasive? Are stakeholder harms systematically identified? Is there a less risky way to meet the business need? |
| **Justice** | Fair and equitable treatment | Does the algorithm produce outcomes that disproportionately harm specific groups? Is machine learning trained on biased datasets that reinforce cultural prejudice? |
| **Respect for Law & Public Interest** | Added by US Menlo Report (2012) | Are data practices transparent and compliant with law? Are societal interests considered beyond the immediate business case? |

---

### Privacy Law Principles — Global to Malaysian Context

DAMA traces the lineage of privacy law from OECD (1980) → EU GDPR (2016) → national implementations. Understanding this lineage helps you understand *why* PDPA is structured the way it is.

**OECD Fair Information Processing Standards (8 Principles — 1980):**
These remain the foundation of virtually every national privacy law. Know them:
1. Collection Limitation — data collection should be limited and lawful
2. Data Quality — data should be accurate and relevant
3. Purpose Specification — the purpose of collection must be stated at collection
4. Use Limitation — data must not be used for purposes beyond what was stated
5. Security Safeguards — reasonable protection against loss, destruction, or misuse
6. Openness — transparency about data practices
7. Individual Participation — the right to access and correct one's own data
8. Accountability — organisations must be accountable for compliance

**GDPR (2016) — The Gold Standard:**
The GDPR is the most comprehensive codification of data ethics in law. Its seven principles (Lawfulness, Fairness & Transparency / Purpose Limitation / Data Minimisation / Accuracy / Storage Limitation / Integrity & Confidentiality / Accountability) are direct expressions of the OECD standards. GDPR also mandates **Privacy by Design** and grants individuals rights to access, rectification, portability, and erasure.

**Malaysian PDPA 2010 (Act 709) — The Local Framework:**

Malaysia's Personal Data Protection Act follows the same lineage. It applies to any commercial entity processing personal data and is structured around seven data protection principles:

| PDPA Principle | Meaning | Exam/Practice Relevance |
|----------------|---------|------------------------|
| **General Principle** | Must have consent for processing; or must fall under a prescribed exception | All data collection requires a lawful basis — consent is the default |
| **Notice & Choice** | Data subjects must be informed of the purpose and their choices | Privacy notices, consent forms, opt-out mechanisms |
| **Disclosure** | Personal data may not be disclosed without consent, except to authorised parties | Data sharing agreements, third-party access controls |
| **Security** | Practical steps to protect against loss, misuse, modification, and unauthorised access | Encryption, access controls, incident response |
| **Retention** | Personal data must not be kept longer than necessary | Retention schedules, disposal procedures |
| **Data Integrity** | Data must be accurate, complete, not misleading | Data quality controls, regular data cleansing |
| **Access** | Data subjects have the right to access and correct their personal data | Subject access request procedures |

> **Malaysian exam context:** PDPA does not currently have a mandatory data breach notification requirement (I believe this is correct as of the DMBOK2 context, though amendments may update this — verify with current PDPC guidance). GDPR mandates 72-hour breach notification. This is a deliberate difference and may appear as a comparison question.

---

## 2. The DAMA Framework View — Ethics as Governance

### Where Ethics Lives in the DAMA Wheel

Data Handling Ethics does not have its own slot on the DAMA Wheel — it is the **ethical backbone that runs through all 11 Knowledge Areas**. However, its closest structural home is **Data Governance**, because:

- Governance sets the policies that define acceptable data use
- Governance owns the code of ethics and compliance oversight
- Governance manages the relationship between data rights and data use

Every KA has ethical implications, but the table below maps the most direct connections:

| Knowledge Area | Key Ethical Risk | Ethics Principle at Stake |
|----------------|-----------------|--------------------------|
| Data Governance | Weak policies allow misuse | Accountability, oversight |
| Data Modeling & Design | Systems designed to extract data beyond consent | Respect for Persons, Purpose Limitation |
| Data Security | Inadequate protection → breach → harm | Beneficence (do no harm), Security Safeguards |
| Metadata Management | Unreliable Metadata → data misunderstood and misused | Data Quality, Openness |
| Data Quality | Inaccurate data → wrong decisions affecting people | Data Integrity, Accuracy |
| Data Warehousing & BI | Misleading visualisations, biased reports | Justice, Truthfulness |
| Data Integration | Lineage gaps → cannot prove data represents what it claims | Accountability, Openness |
| Reference & Master Data | Inconsistent identity data → discriminatory outcomes | Justice, Data Quality |
| Big Data & Data Science | Algorithmic bias, re-identification of anonymous data | Justice, Beneficence, Privacy |
| Document & Content Management | Retention of personal data beyond legal period | Retention Limitation, PDPA |
| Data Architecture | Systems that do not embed privacy controls | Privacy by Design |

---

### The Six Risks of Unethical Data Handling

These six unethical practices are explicitly named in DMBOK2 Chapter 2. They are tested directly in Type 3 (Scenario) and Type 4 (Process) exam questions.

**Risk 1 — Timing Manipulation**
Using selective time periods to misrepresent a trend or metric. Classic example: selecting a starting date for a chart that makes a declining metric appear stable, or "end of day" equity trades that artificially inflate closing prices. This is not just unethical — in financial markets, it is illegal (market timing / market manipulation).

*The data professional's duty:* BI staff are often the first to identify timing anomalies. The ethical obligation is to alert governance or management, not to silently produce the misleading report.

**Risk 2 — Misleading Visualisations**
Charts and graphs constructed to mislead: manipulated scales, truncated axes, pie charts that do not sum to 100%, omitted data points, or visual comparisons that imply a relationship that does not exist. Edward Tufte's *The Visual Display of Quantitative Information* (1983) is the canonical reference on ethical visualisation design.

**Risk 3 — Unclear Definitions / Invalid Comparisons**
Presenting data without sufficient context so that the audience draws the wrong conclusion — even without any intention to deceive. Example from DMBOK2: comparing "people on welfare" (defined as anyone in a household receiving benefits) with "people with full-time jobs" (defined as individuals who personally work full time) and presenting them as equivalent metrics. The ethical duty: always define the population being measured and the metric being applied.

**Risk 4 — Bias**
Bias can enter at any point in the data lifecycle — collection, selection, analysis, interpretation, or presentation. DAMA identifies five specific bias types:

- *Data collection for pre-defined result* — analyst is pressured to reach a predetermined conclusion
- *Biased use of collected data* — data is selectively used or discarded to confirm a predetermined approach
- *Hunch and search* — analyst uses only data that confirms their hunch
- *Biased sampling methodology* — the selection method introduces systematic skew
- *Context and culture* — culturally embedded assumptions that are invisible without external perspective

> **High-risk scenario:** Predictive algorithms determining "criminal risk" of individuals — if trained on historically biased crime data, these models will perpetuate and amplify systemic injustice while presenting results as objective. This is a named example in DMBOK2.

**Risk 5 — Transforming and Integrating Data**
When data moves between systems, it changes. Without documented lineage and quality standards, an organisation cannot prove that data represents what it claims. DMBOK2 identifies four specific ethical risks in integration:
- Limited knowledge of data origin and lineage
- Poor data quality (no measurable standards, no measurement)
- Unreliable Metadata (no definitions, no lineage documentation)
- No auditable data remediation history (changes made without formal change control)

**Risk 6 — Obfuscation / Redaction Failures**
Anonymisation is not always sufficient. In large datasets, individuals can be re-identified by combining multiple partially-anonymised fields (the "Netflix problem" and similar research findings). Data masking, aggregation, and data marking each carry specific limitations that must be understood and documented in governance policies.

---

### Establishing an Ethical Data Culture — The Four-Step Process

DAMA's prescribed approach for building ethics into an organisation's data practice:

```
Step 1: REVIEW CURRENT STATE
         └─ Map existing data handling practices
         └─ Identify gaps between current practice and ethical/legal requirements
         └─ Deliverable: documentation of ethical principles underlying current collection, use, oversight

Step 2: IDENTIFY PRINCIPLES, PRACTICES, RISK FACTORS
         └─ Define guiding principles (e.g., "people have a right to health data privacy")
         └─ Map principles → risks → practices → controls
         └─ Align with regulatory requirements (PDPA, BNM RMIT, GDPR if applicable)

Step 3: CREATE STRATEGY & ROADMAP
         └─ Values statements
         └─ Code of ethics + ethics policy
         └─ Compliance framework
         └─ Risk assessments (likelihood + implication)
         └─ Training and communications plan (annual sign-off)
         └─ Monitoring and auditing approach
         └─ Roadmap with management-approved timeline

Step 4: ADOPT SOCIALLY RESPONSIBLE ETHICAL RISK MODEL
         └─ For analytics/BI/Data Science projects:
              └─ Population selection (who is studied and who is excluded?)
              └─ Data capture (how is consent obtained?)
              └─ Analytics focus (what decisions will be made?)
              └─ Results accessibility (who can act on outputs and how?)
```

> **Key exam point:** The ethical culture process requires formal **Organisational Change Management (OCM)**. DAMA explicitly links Chapter 2 to Chapter 17 (Data Management Maturity and OCM). Ethics is not a policy exercise — it is a culture transformation.

---

### Must-Know CDMP Exam Concepts & Traps for Chapter 2

**Concept 1 — Law is the Floor, Ethics is the Ceiling**
The most fundamental principle of Chapter 2: compliance with law is the *minimum* requirement, not the definition of ethical behaviour. An exam question that presents "we follow all applicable laws" as a complete data ethics strategy is presenting an incorrect answer.

**Concept 2 — The CDMP Code of Ethics is a Real Requirement**
DAMA explicitly states in Chapter 2 that CDMP certification requires subscribing to a formal code of ethics — including an obligation to handle data ethically for the sake of *society beyond the organisation that employs them*. This means a data professional's ethical obligation extends beyond their employer's interests.

**Concept 3 — Privacy by Design, Not Privacy by Retrofit**
Systems built without privacy controls must be retrofitted — at far greater cost and risk than building privacy in from the start. The GDPR mandates Privacy by Design. Malaysian PDPA's security principle implies it. Any exam scenario where privacy controls are "added later" is describing an anti-pattern.

**Concept 4 — Anonymisation Is Not Guaranteed Protection**
A common exam trap: organisations assume that removing direct identifiers (name, IC number) makes data fully anonymous. DMBOK2 explicitly warns that in large datasets, combinations of quasi-identifiers (age, postcode, employer) can enable re-identification. Anonymisation must be tested and documented, not assumed.

**Concept 5 — Bias Has a Positive Duty to Address**
The ethical principle of justice creates a *positive* duty — not just to avoid discriminating, but to *actively identify and correct* bias in data collection, analysis, and algorithm design. Passive non-discrimination is not sufficient.

**Concept 6 — Data Governance Owns Ethics Oversight**
Ethics oversight is explicitly assigned to Data Governance and legal counsel in DMBOK2. It is *not* owned by IT, compliance, or HR alone. Data Governance must set standards, provide oversight, and review plans proposed by BI, analytics, and Data Science teams.

---

## 3. Real-World Business Context & Applications

### Scenario 1 — Financial Services: Credit Scoring Algorithm

**The Failure (Without Chapter 2 Principles)**

A Malaysian commercial bank deploys an automated credit scoring model to accelerate personal loan approvals. The model is trained on five years of historical loan data and produces a score used to approve or reject applications without human review.

Within 12 months:
- An internal audit finds that applicants from certain postcodes (which correlate with specific ethnic communities) are rejected at 3x the rate of applicants from other postcodes with equivalent income levels.
- The model was trained on historical approval data — but historical approvals were themselves made by loan officers whose decisions reflected longstanding structural biases. The algorithm learned and amplified those biases.
- When a rejected customer requests an explanation, the bank cannot provide one — the model's decision logic is not documented.
- BNM's RMIT guidelines require that models used in credit decisions be explainable and auditable. The bank cannot demonstrate either.

**Root Cause (DMBOK2 lens):** Biased sampling methodology (Risk 4 — training data encoded historical bias), no documentation of data lineage through the model (Risk 5), no explainability = lack of transparency (Belmont: Justice), and governance did not review the Data Science project's ethical risk model (Step 4 failure).

---

**The Success (With Chapter 2 Principles)**

The same bank, before deployment, runs the scoring model through a formal ethical risk model review:
- Population selection: Who is excluded from the training data? (Only historical applicants — not rejected applicants who were never assessed. The bank augments with alternative data.)
- Data capture: Is the source data quality-validated? (A Data Quality audit finds and remediates postcode encoding errors.)
- Analytics focus: The model is tested for disparate impact across demographic segments before deployment.
- Results accessibility: Human review is required for all rejections below a threshold score. Decision logic is documented in a model card stored in the Metadata repository.

BNM's RMIT audit finds a model governance framework with explainability documentation, a bias testing report, and a quarterly model performance review schedule. The bank passes without findings.

---

### Scenario 2 — Healthcare: Patient Data Sharing

**The Failure (Without Chapter 2 Principles)**

A private hospital group in Malaysia shares de-identified patient data with a pharmaceutical company for drug research purposes. The data dictionary includes: age band, district, gender, diagnosis code, medication, outcome. The hospital's legal team confirms there is no PDPA breach — no direct identifiers are included.

Six months later, a researcher at the pharmaceutical company publishes a finding that was derived by combining the hospital dataset with a publicly available health ministry dataset. By joining on age band + district + diagnosis code + medication, 12% of the records can be uniquely identified. Three patients with stigmatised conditions (HIV, mental health diagnoses) are effectively re-identified in the research literature.

The hospital faces reputational damage, a regulatory inquiry from the PDPC, and loss of patient trust. The pharmaceutical company's publication is retracted.

**Root Cause (DMBOK2 lens):** Anonymisation was assumed sufficient without testing (Risk 6 — obfuscation failure). No data sharing agreement defined acceptable downstream uses. The ethical risk model was not applied before data transfer. Legal compliance was treated as equivalent to ethical responsibility (Concept 1 exam trap).

---

**The Success (With Chapter 2 Principles)**

The same hospital group establishes an **ethical data sharing protocol** before entering any data sharing arrangement:
- A Data Governance committee reviews all proposed data sharing arrangements, applying the ethical risk model
- Before sharing, re-identification risk is tested using the K-anonymity method — any dataset where 12% of records can be uniquely identified fails the test and must be further aggregated
- The data sharing agreement explicitly prohibits joining with external datasets without prior approval
- Data is tagged with provenance Metadata: origin, owner, allowable uses, and expiry date
- The pharmaceutical company's research team signs a code of ethics that mirrors the hospital's data handling principles

The resulting dataset passes re-identification testing (K-anonymity ≥ 10), the research is published with full ethical review documentation, and the hospital's data sharing framework becomes a model cited by MCMC in a data governance guidance paper.

---

### Scenario 3 — E-Commerce / Retail: Behavioural Data Monetisation

**The Failure (Without Chapter 2 Principles)**

A major Malaysian e-commerce platform collects extensive behavioural data — clicks, searches, purchase history, browsing patterns, time of day, device type — and sells aggregated audience segments to third-party advertisers. The platform's privacy notice states (in a 4,000-word document) that data "may be used to improve services and for marketing purposes."

Problems emerge:
- A third-party advertiser uses the audience segments to target advertisements for high-interest loans specifically at users whose browsing patterns suggest financial stress (late-night searches for "pinjaman segera", frequent discount filtering, delayed cart checkouts). This is predatory targeting — exploiting vulnerable individuals.
- The platform's Data Science team builds a "customer lifetime value" model that systematically de-prioritises customer service responsiveness for accounts below a revenue threshold. Customers with low predicted CLV wait an average of 4x longer for resolution. This discriminatory service quality is not disclosed.
- A PDPA subject access request reveals that some customers' data has been retained for 7 years with no documented retention policy — violating the Retention Principle.

**Root Cause (DMBOK2 lens):** Consent was obtained through deliberately obscure notice (violation of Notice & Choice Principle, PDPA). The ethical risk model was not applied to the CLV model's discriminatory service implications (Justice, Beneficence). Data was retained without a documented retention schedule (PDPA Retention Principle). Third-party use was not governed by a data sharing agreement with ethical use restrictions.

---

**The Success (With Chapter 2 Principles)**

The platform's CDO commissions a full ethical data culture review:
- All consent notices are rewritten to plain Bahasa Malaysia and English — tested for comprehension with a sample of actual users
- The data monetisation programme is reviewed against the ethical risk model: predatory targeting use cases are explicitly prohibited in the third-party data use policy, with contractual penalties
- The CLV model undergoes a Justice review — the disparate service quality finding is escalated to the COO, who mandates a baseline service level regardless of predicted CLV
- Retention schedules are defined for every data category and implemented in the data lake governance layer — automated flagging for review at expiry
- An annual ethics affirmation is introduced for all employees who handle customer data

The platform's new privacy framework receives recognition from the PDPC as an example of Privacy by Design implementation in the Malaysian e-commerce sector.

---

## 4. Visual Diagrams, Cheat Sheet & Quick Reference

### The Ethics-Governance-Compliance Triangle

```
                    ┌─────────────────────────┐
                    │        ETHICS           │
                    │  (Principles of right   │
                    │   and wrong — highest   │
                    │   standard)             │
                    └───────────┬─────────────┘
                                │
                                │ informs
                                ▼
                    ┌─────────────────────────┐
                    │       GOVERNANCE        │
                    │  (Policies, oversight,  │
                    │   codes of conduct,     │
                    │   decision rights)      │
                    └───────────┬─────────────┘
                                │
                                │ operationalises
                                ▼
                    ┌─────────────────────────┐
                    │      COMPLIANCE         │
                    │  (Legal minimum —       │
                    │   PDPA, RMIT, GDPR      │
                    │   — the floor,          │
                    │   not the ceiling)      │
                    └─────────────────────────┘

     EXAM RULE: Ethics > Governance > Compliance in terms of
     aspiration. Legal compliance alone is NEVER a complete
     answer to an ethics question.
```

---

### Belmont Principles → Data Ethics → Malaysian Context

```
┌──────────────────┬────────────────────────────┬───────────────────────────┐
│ Belmont          │ Data Ethics Application    │ Malaysian Regulatory Link  │
│ Principle        │                            │                           │
├──────────────────┼────────────────────────────┼───────────────────────────┤
│ Respect for      │ Informed consent; don't     │ PDPA General Principle    │
│ Persons          │ limit autonomy; protect     │ (consent required);       │
│                  │ vulnerable groups           │ Notice & Choice Principle │
├──────────────────┼────────────────────────────┼───────────────────────────┤
│ Beneficence      │ Do not harm; maximise       │ BNM RMIT: Technology Risk │
│                  │ benefit; minimise           │ Management — harm to      │
│                  │ processing risk             │ financial system          │
├──────────────────┼────────────────────────────┼───────────────────────────┤
│ Justice          │ No discriminatory           │ PDPA Data Integrity;      │
│                  │ algorithms; fair treatment  │ Malaysia Anti-Discrimination│
│                  │ across demographics         │ principles                │
├──────────────────┼────────────────────────────┼───────────────────────────┤
│ Respect for      │ Follow PDPA, RMIT, GDPR    │ PDPC enforcement; BNM     │
│ Law & Public     │ (if applicable); consider   │ supervisory review;       │
│ Interest         │ societal impact             │ MCMC content guidelines   │
└──────────────────┴────────────────────────────┴───────────────────────────┘
```

---

### Six Unethical Practices — Quick Identification Guide

```
┌──────────────────────────┬──────────────────────────────────────────────┐
│ Unethical Practice       │ How to Spot It in an Exam Scenario            │
├──────────────────────────┼──────────────────────────────────────────────┤
│ 1. Timing Manipulation   │ "We report Q4 numbers using Oct–Nov data"     │
│                          │ "End of day trade volumes look higher"        │
├──────────────────────────┼──────────────────────────────────────────────┤
│ 2. Misleading Visuals    │ Y-axis starts at 80 to exaggerate small       │
│                          │ changes; pie chart does not add to 100%       │
├──────────────────────────┼──────────────────────────────────────────────┤
│ 3. Unclear Definitions   │ Two metrics presented side-by-side with       │
│                          │ different underlying definitions              │
├──────────────────────────┼──────────────────────────────────────────────┤
│ 4. Bias                  │ Model trained on historical data that was     │
│                          │ itself biased; sample excludes certain groups │
├──────────────────────────┼──────────────────────────────────────────────┤
│ 5. Integration Failure   │ "We don't know exactly how the data was       │
│                          │ transformed between the source and the DW"    │
├──────────────────────────┼──────────────────────────────────────────────┤
│ 6. Obfuscation Failure   │ "Names removed so it's anonymous" without     │
│                          │ testing quasi-identifier re-identification     │
└──────────────────────────┴──────────────────────────────────────────────┘
```

---

### Ethics Culture Roadmap — ASCII

```
 CURRENT STATE          PRINCIPLES              STRATEGY               ETHICAL CULTURE
 REVIEW                 & RISKS                 & ROADMAP
 ┌─────────────┐        ┌─────────────┐        ┌─────────────┐        ┌─────────────┐
 │ Map current │        │ Define      │        │ Values      │        │ Ongoing     │
 │ practices   │───────▶│ guiding     │───────▶│ statements  │───────▶│ training &  │
 │             │        │ principles  │        │ Code of     │        │ monitoring  │
 │ Identify    │        │             │        │ Ethics      │        │             │
 │ gaps vs.    │        │ Map:        │        │ Policy      │        │ Annual      │
 │ legal &     │        │ Principle   │        │ Compliance  │        │ ethics      │
 │ ethical     │        │ → Risk      │        │ framework   │        │ sign-off    │
 │ obligations │        │ → Practice  │        │ Risk assess.│        │             │
 │             │        │ → Control   │        │ Roadmap     │        │ Whistle-    │
 │ Deliverable:│        │             │        │             │        │ blower      │
 │ Ethics gap  │        │ Industry-   │        │ Training    │        │ protection  │
 │ register    │        │ specific    │        │ plan        │        │             │
 └─────────────┘        │ risks incl. │        └─────────────┘        └─────────────┘
                        │ PDPA/RMIT   │
                        └─────────────┘

  OCM (Organisational Change Management) runs across ALL four stages — see Chapter 17
```

---

### Chapter 2 Quick-Reference Cheat Sheet

| Concept | Key Fact to Remember |
|---------|---------------------|
| Ethics definition | Principles based on right/wrong — fairness, respect, responsibility, integrity, transparency, trust |
| Three core concerns | Impact on people / Potential for misuse / Economic value of data |
| Belmont Principles (3+1) | Respect for Persons, Beneficence, Justice + Respect for Law & Public Interest (Menlo) |
| OECD 8 principles (1980) | Foundation of all modern privacy law including PDPA |
| GDPR (2016) | Gold standard; 7 principles + Privacy by Design + individual rights |
| PDPA 2010 (Malaysia) | 7 principles — General, Notice & Choice, Disclosure, Security, Retention, Data Integrity, Access |
| Six unethical practices | Timing, Misleading Visuals, Unclear Definitions, Bias, Integration Failure, Obfuscation Failure |
| Bias types (5) | Pre-defined result, Biased data use, Hunch & search, Biased sampling, Context & culture |
| Ethical culture steps | Review → Principles/Risks → Strategy/Roadmap → Socially Responsible Risk Model |
| Ethics owner in DMBOK2 | Data Governance + Legal Counsel (jointly) |
| CDMP ethical obligation | Extends to society beyond the employing organisation |
| Privacy by Design | Embed privacy in architecture from the start — not retrofitted |
| Anonymisation warning | Re-identification risk in large datasets — must test, not assume |
| Law vs Ethics | Law = floor (minimum). Ethics = ceiling (aspiration). Compliance alone is insufficient |
| OCM requirement | Ethical culture change requires formal Organisational Change Management |

---

## 5. Official DAMA Knowledge Area Visual Reference

> © DAMA International. Licensed under [CC BY-ND 4.0](https://creativecommons.org/licenses/by-nd/4.0/). Source: [dama.org/dmbok2r-infographics](https://dama.org/dmbok2r-infographics/).
>
> *Citation: DAMA International. The DAMA Guide to the Data Management Body of Knowledge (DAMA-DMBOK2R). 2nd ed, revised. Sedona, AZ: Technics Publications, LLC, 2024.*

### Data Handling Ethics — KA Context Diagram

This diagram shows the inputs, activities, outputs, and relationships for Chapter 2. Note that Ethics connects as an input into virtually every other Knowledge Area through the Governance hub.

![Data Handling Ethics — DMBOK2 Knowledge Area Context Diagram](https://growthzonecmsprodeastus.azureedge.net/sites/2326/2025/04/x-8.png)

---

*References: DAMA-DMBOK2 Revised Edition, Chapter 2 | PDPA 2010 (Act 709) | BNM Risk Management in Technology (RMIT) 2020 | GDPR 2016 | OECD Fair Information Processing Standards 1980 | Belmont Report 1979*

