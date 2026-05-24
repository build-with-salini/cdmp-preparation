# Day 03 — Data Governance
**DAMA-DMBOK2 | Chapter 3 | Exam Weight: 11% (Highest-weighted KA)**

> *"Data governance is to data what auditing and accounting are to finance. Auditors and controllers set the rules for managing financial assets. Data governance professionals set rules for managing data assets."*
> — DAMA-DMBOK2, Chapter 3

---

## 1. Core Summary & Big Ideas

### What This Chapter Is Really About

Chapter 3 is **the most important chapter in the DMBOK2 for the CDMP exam** — it carries the highest individual KA weight at 11%. More than any other chapter, it defines *how* organisations make decisions about data: who has the right to decide, who is accountable for execution, and how compliance with those decisions is enforced and measured.

Data Governance is also the structural centre of the DAMA Wheel. Every other Knowledge Area — Modeling, Security, Quality, Metadata — requires governance to function with accountability and consistency. Without it, each KA operates as a silo. With it, they form a coherent, enterprise-wide system.

Three central questions run through the entire chapter:

- **Who decides?** — Decision rights, authority, and accountability structures
- **How is it enforced?** — Policies, standards, issue management, and compliance monitoring
- **How is it sustained?** — Cultural change management, metrics, and programme evolution

---

### Core Definitions

| Term | DAMA-DMBOK2 Definition / Key Point |
|------|-------------------------------------|
| **Data Governance (DG)** | *"The exercise of authority and control (planning, monitoring, and enforcement) over the management of data assets."* |
| **Data Stewardship** | The most common label to describe accountability and responsibility for data and processes that ensure effective control and use of data assets |
| **Data Owner** | A business Data Steward who has **approval authority** for decisions about data within their domain |
| **Data Policy** | Directives that codify principles and management intent into fundamental rules governing the creation, acquisition, integrity, security, quality, and use of data |
| **Business Glossary** | A tool housing agreed-upon definitions of business terms and relating these to data — necessary because people use words differently |
| **Data Asset Valuation** | The process of understanding and calculating the economic value of data to an organisation |
| **DGC** | Data Governance Council — the senior governance body that reviews, approves, and adopts governance policies, standards, and architecture |

> **Key distinction the exam loves to test:** Data Governance is NOT the same as IT Governance. IT Governance makes decisions about IT investments, application portfolios, and technical architecture. Data Governance focuses exclusively on the management of data assets and of data *as* an asset. COBIT is an IT governance framework — it covers only a small portion of data management.

---

### The Three Essential DG Programme Characteristics

These three attributes define what a good DG programme looks like. Any DG programme that lacks any of these will eventually fail — and exam questions will present failure scenarios corresponding to these gaps.

**1. Sustainable**
DG is not a project with a defined end. It is an ongoing process requiring organisational commitment beyond initial implementation. Sustainability depends on business leadership, sponsorship, and ownership — not on IT.

**2. Embedded**
DG is not an add-on process bolted alongside existing workflows. DG activities must be incorporated into software development methods, analytics use of data, Master Data Management, and risk management. An embedded DG programme changes how work gets done — not just how it gets reported.

**3. Measured**
DG done well has positive financial impact, but demonstrating that impact requires understanding the starting point and planning for measurable improvement. Ungoverned DG programmes cannot prove their value — and therefore cannot sustain executive sponsorship.

---

### The Six Data Governance Principles

These six principles are the **foundation of all DG policy and activities**. They are directly tested in Type 2 (Principle-Based) and Type 10 (Judgment) exam questions.

| # | Principle | Meaning in Practice |
|---|-----------|---------------------|
| 1 | **Leadership and Strategy** | Successful DG starts with visionary and committed leadership. Data management activities are guided by a data strategy driven by enterprise business strategy |
| 2 | **Business-driven** | DG is a *business programme*, not an IT programme. It must govern IT decisions about data as much as it governs business interaction with data |
| 3 | **Shared Responsibility** | Across all KAs, DG is a shared responsibility between business data stewards and technical data management professionals — neither can own it alone |
| 4 | **Multi-layered** | DG occurs at both enterprise and local levels and often at levels in between. Enterprise DG coordinates; local DG executes |
| 5 | **Framework-based** | Because DG activities require coordination across functional areas, the programme must establish an operating framework that defines accountabilities and interactions |
| 6 | **Principle-based** | Guiding principles are the foundation of DG activities, especially DG policy. Principles should be articulated *before* policy is written |

---

### DG Business Drivers — The Two Categories

Understanding why an organisation invests in DG is critical for answering Type 4 (Process/Framework) questions. All DG business drivers fall into two categories:

**Reducing Risk:**
- *General risk management* — Oversight of risks data poses to finances or reputation (including legal discovery / e-discovery requirements)
- *Data security* — Controls for availability, usability, integrity, consistency, auditability, and security
- *Privacy* — Control of Personal Identifying Information (PII) through policy and compliance monitoring

**Improving Processes:**
- *Regulatory compliance* — Efficient, consistent responses to regulatory requirements (BNM RMIT, PDPA, Basel II/BCBS 239)
- *Data quality improvement* — Reliable data that supports better business performance
- *Metadata management* — Business glossary; making data findable and understandable
- *Efficiency in development projects* — SDLC improvements, reduction of data-related technical debt
- *Vendor management* — Control of contracts for cloud storage, external data purchase, data product sales, outsourced operations

> **Exam context:** The most common initial driver for DG is regulatory compliance — particularly for financial services and healthcare. Many organisations "back into" DG through MDM (Master Data Management) projects or major data problems, rather than implementing it proactively.

---

## 2. The DAMA Framework View — Governance Architecture

### DG vs. Data Management — The Separation of Duty

This is one of the most tested structural concepts in Chapter 3:

```
Data Governance                        Data Management
(Oversight)                            (Execution)
───────────────────                    ─────────────────────
• Sets policies                        • Follows policies
• Defines standards                    • Implements standards
• Monitors compliance                  • Delivers outcomes
• Resolves issues                      • Reports issues
• Approves architecture                • Builds systems
• Sponsors initiatives                 • Executes initiatives
• Values data assets                   • Creates data assets

Analogy: Auditor / Controller          Analogy: Finance Operations Team
```

> Just as an auditor controls financial processes but does not execute financial management — Data Governance ensures data is properly managed without directly executing data management. This **separation of duty** is a core DMBOK2 concept.

---

### The Three DG Operating Model Types

| Model | Description | Best For | Malaysian Example |
|-------|-------------|----------|-------------------|
| **Centralized** | One DG organisation oversees all activities in all subject areas | Highly regulated, integrated organisations | BNM-regulated financial institutions with group-wide data standards |
| **Replicated** | Same DG operating model and standards adopted by each business unit independently | Conglomerates with similar business units | Sime Darby's plantation, motors, and industrial divisions each running the same DG playbook |
| **Federated** | One DG organisation coordinates with multiple Business Units to maintain consistent definitions and standards while allowing local flexibility | Large diversified organisations with different regulatory environments | Petronas — upstream, downstream, and retail each with domain-specific governance, coordinated centrally |

---

### The Data Governance Organisation — Three Functions

DAMA describes the DG organisation in terms analogous to political governance — with three types of function:

```
┌──────────────────────────────────────────────────────────────────┐
│                   DATA GOVERNANCE ORGANISATION                    │
├──────────────────┬──────────────────────┬────────────────────────┤
│  LEGISLATIVE     │    JUDICIAL          │    EXECUTIVE           │
│  FUNCTIONS       │    FUNCTIONS         │    FUNCTIONS           │
├──────────────────┼──────────────────────┼────────────────────────┤
│ • Define         │ • Issue management   │ • Protect and serve    │
│   policies       │   and escalation     │   data assets          │
│ • Set standards  │ • Conflict           │ • Administrative       │
│ • Define         │   resolution         │   responsibilities     │
│   Enterprise     │ • Compliance         │ • Sponsoring data      │
│   Data           │   rulings            │   management projects  │
│   Architecture   │                      │                        │
├──────────────────┴──────────────────────┴────────────────────────┤
│  TYPICAL BODIES: DGC (Council) → Data Stewardship Steering Cmte  │
│                  → Working Groups → Business Stewards            │
└──────────────────────────────────────────────────────────────────┘
```

---

### Data Stewardship — Types and Roles

Data Stewardship is the core execution mechanism of DG. Understanding the hierarchy of stewardship roles is a high-frequency exam topic.

| Steward Type | Role | Authority Level |
|-------------|------|-----------------|
| **Chief Data Steward** | Chairs DG bodies; may act as CDO in virtual DG organisations; Executive Sponsor | Highest |
| **Executive Data Steward** | Senior managers serving on the Data Governance Council | Enterprise |
| **Enterprise Data Steward** | Oversight of a data domain across business functions | Cross-functional |
| **Business Data Steward** | Business professionals; subject matter experts; accountable for a subset of data; work with stakeholders to define and control data | Domain |
| **Data Owner** | A Business Data Steward with **approval authority** for decisions about data within their domain | Decision-making |
| **Technical Data Steward** | IT professionals operating within a KA — DBAs, BI Specialists, Data Quality Analysts, Metadata Administrators | Technical |
| **Coordinating Data Steward** | Leads and represents teams of business and technical stewards; critical in large organisations | Coordination |

> **Exam trap:** "The best Data Stewards are often *found*, not *made*." — This means organisations should identify people already stewarding data informally and formalise their roles. But DAMA also affirms that stewards *can* be developed through training. The "found vs. made" quote is a frequent distractor in exam questions.

---

### The 17 DG Activities — Organised by Programme Phase

Chapter 3 describes 17 data governance activities. These are tested in Type 4 (Process/Framework) questions — often as "what should be done first?" or "what is the correct sequence?"

**Phase 1 — Define & Design**
1. Define Data Governance for the Organisation
2. Perform Readiness Assessment *(4 types: maturity, capacity to change, collaborative readiness, business alignment)*
3. Perform Discovery and Business Alignment
4. Develop Organisational Touch Points *(CDO's connections to procurement, budget, regulatory compliance, SDLC)*
5. Develop Data Governance Strategy *(Charter + Operating Framework + Roadmap + Operational Success Plan)*
6. Define the DG Operating Framework

**Phase 2 — Build & Govern**
7. Develop Goals, Principles, and Policies *(Drafted → Steward review → DGC adoption)*
8. Underwrite Data Management Projects *(DGC business case + oversight)*
9. Engage Change Management *(ADKAR model; formal OCM programme)*
10. Engage in Issue Management *(8 categories; escalation path to DGC)*
11. Assess Regulatory Compliance Requirements

**Phase 3 — Sustain & Improve**
12. Implement Data Governance *(Incremental rollout; MDM or business unit first)*
13. Sponsor Data Standards and Procedures
14. Develop a Business Glossary
15. Coordinate with Architecture Groups *(DGC sponsors/approves data architecture artefacts)*
16. Sponsor Data Asset Valuation
17. Embed Data Governance *(Community of Interest; sustainability planning)*

---

### The Readiness Assessment — Four Dimensions

Before implementing DG, DAMA prescribes four specific assessments. These are frequently tested as a set:

```
┌────────────────────────┬────────────────────────────────────────────────┐
│ Assessment             │ What It Measures                               │
├────────────────────────┼────────────────────────────────────────────────┤
│ Data Management        │ Current capabilities and capacity; how well    │
│ Maturity               │ the organisation manages data today (see Ch 15)│
├────────────────────────┼────────────────────────────────────────────────┤
│ Capacity to Change     │ Organisational readiness to change behaviours  │
│                        │ required for DG; identifies resistance points  │
├────────────────────────┼────────────────────────────────────────────────┤
│ Collaborative          │ Ability to collaborate across functions —       │
│ Readiness              │ stewardship is cross-functional by definition  │
├────────────────────────┼────────────────────────────────────────────────┤
│ Business Alignment     │ How well data use aligns with business         │
│                        │ strategy; often reveals ad hoc data practices  │
└────────────────────────┴────────────────────────────────────────────────┘
```

---

### Issue Management — The Eight Categories

DG must manage issues arising from data governance activities. DMBOK2 names eight specific issue categories — a direct exam target:

1. **Authority** — Questions regarding decision rights and procedures
2. **Change Management Escalations** — Issues arising from the change management process
3. **Compliance** — Issues with meeting compliance requirements
4. **Conflicts** — Conflicting policies, procedures, business rules, names, definitions, standards, architecture, data ownership, or stakeholder interests
5. **Conformance** — Issues related to conformance to policies, standards, architecture, and procedures
6. **Contracts** — Negotiation and review of data sharing agreements, buying/selling data, cloud storage
7. **Data Security and Identity** — Privacy, confidentiality, breach investigations
8. **Data Quality** — Detection and resolution of data quality issues

*Issue escalation path: Local Stewardship Teams → Data Stewardship Steering Committee → Data Governance Council → Corporate Governance / Management*

---

### Data Asset Valuation — The Four Methods

Data has economic value — but calculating it requires specific approaches. DMBOK2 defines four:

| Method | Description | When to Use |
|--------|-------------|-------------|
| **Replacement Cost** | Cost to recover/recreate data lost in disaster or breach | Risk quantification; insurance; disaster recovery planning |
| **Market Value** | Value as a business asset at time of merger or acquisition | M&A due diligence; data product pricing |
| **Identified Opportunities** | Value of income from opportunities identified in data (BI), by using data for transactions, or by selling data | Business case for analytics investment |
| **Risk Cost** | Potential penalties, remediation costs, and litigation from legal/regulatory risk — from absent, present-but-shouldn't-be, or incorrect data | Compliance investment justification; PDPA breach risk |

---

### Must-Know CDMP Exam Concepts & Traps for Chapter 3

**Concept 1 — DG is a Business Programme, Not an IT Programme (Trap: IT ownership)**
This is the most consistently tested concept in Chapter 3. Any exam answer that places ownership of DG with IT, the CIO, or the IT department alone is wrong. DG is business-driven and requires C-suite business sponsorship (CDO, CFO, CRO).

**Concept 2 — Data Governance ≠ IT Governance (Trap: conflating the two)**
IT governance (COBIT) manages IT assets — hardware, software, technical architecture. Data governance manages data assets. They are separate disciplines with different scope, tools, and accountabilities.

**Concept 3 — DG is Not a One-Time Project (Trap: project framing)**
Chapter 3 explicitly states DG requires an ongoing programme. Any scenario that describes a DG programme being "completed" and handed over is describing a governance failure. DG never ends — it evolves.

**Concept 4 — Federated vs. Centralized vs. Replicated (Trap: confusing the models)**
Centralized = one body governs everything. Replicated = each unit uses the same model independently. Federated = central coordination with local flexibility. Many organisations incorrectly believe they need centralised DG for consistency — federated models can achieve consistency with greater organisational buy-in.

**Concept 5 — The Business Glossary is a Governance Tool (Trap: seeing it as a documentation exercise)**
A Business Glossary is not just a list of terms. Each term is associated with Metadata: synonyms, metrics, lineage, business rules, the responsible steward, etc. It is the primary mechanism by which DG manages shared understanding across the enterprise.

**Concept 6 — OCM is Required for DG Success (Trap: underestimating cultural change)**
Chapter 3 explicitly links DG to Organisational Change Management (Chapter 17). DG requires people to change their behaviours. Without a formal OCM programme with executive sponsorship, DG programmes consistently fail. Cultural resistance is named as the most common DG implementation failure mode.

**Concept 7 — Data Owner Has Approval Authority (Trap: confusing roles)**
A Data Owner is specifically defined as a Business Data Steward with *approval authority* for decisions about data within their domain. This is a precise definition. Not all stewards have approval authority — only the Data Owner does.

---

## 3. Real-World Business Context & Applications

### Scenario 1 — Financial Services: GLC Bank Data Governance Programme

**The Failure (Without Chapter 3 Principles)**

A large Malaysian government-linked bank decides to implement a Data Governance programme after a BNM examination finding cites "inadequate data lineage documentation" for regulatory capital reporting (relevant to BCBS 239 principles on risk data aggregation). The bank assigns the programme to the IT department and tasks the Head of Enterprise Architecture with leading it.

Within 12 months:
- The IT team produces extensive technical documentation — data dictionaries, system maps, data flow diagrams. But business terms are still undefined: "credit exposure" means different things in Risk, Finance, and the Front Office.
- Business stakeholders do not engage with the DG programme because they see it as an IT initiative producing IT documentation.
- Policies are drafted but not adopted — the DGC has no business representation, and the CFO (who would be the natural sponsor) has never been briefed on the programme.
- BNM's next examination finds that regulatory reporting still lacks a single, authoritative definition of "exposure at default" — the programme has improved technical documentation but not business alignment.

**Root Cause (DMBOK2 lens):** DG placed in IT rather than as a business programme (Principle 2 violation). No business sponsorship at C-level. No Business Glossary defining terms across Risk, Finance, and Front Office. DG was a project with deliverables, not a sustainable programme (Characteristic 1 violation).

---

**The Success (With Chapter 3 Principles)**

The same bank restarts the programme with the Group CFO as Executive Sponsor and appoints a Chief Data Officer reporting to the CEO. A Data Governance Council is established with representation from Risk, Finance, Operations, Technology, and Compliance. A federated operating model is chosen — Group DG coordinates definitions and standards; each business division executes stewardship activities.

- The first deliverable is a Business Glossary for the 40 data terms used in regulatory capital reporting. Each term is approved by the relevant Data Owner (a senior business manager) and signed off by the DGC.
- Business Data Stewards are identified in each division — people who were already informally managing data quality issues. Their roles are formalised with 20% of their time dedicated to stewardship.
- BNM's follow-up examination finds consistent definitions, documented data lineage, and auditable change control for all regulatory data elements. The finding is closed.

---

### Scenario 2 — Healthcare: Private Hospital Group MDM-Driven DG

**The Failure (Without Chapter 3 Principles)**

A private hospital group operates six facilities and decides to implement a Patient Master Data Management system to create a unified patient record across all sites. The MDM project team — entirely from IT — defines "patient" as any record in the system. The MDM goes live, but:
- Clinical staff in different hospitals still use different local definitions of "active patient," "discharged patient," and "deceased patient" — so the unified count is never trusted.
- There is no process for escalating data quality issues in the patient record — clinical staff raise issues verbally, they are logged nowhere, and nothing is resolved systematically.
- The Medical Director and Chief Nursing Officer were never consulted during design. They refuse to endorse the system.

**Root Cause (DMBOK2 lens):** MDM without DG — no Business Glossary defining clinical terms, no issue management process, no business sponsorship for data definitions. This is the "backing into DG through MDM" pattern DAMA describes — but done incorrectly by treating MDM as a technology project rather than a data governance exercise.

---

**The Success (With Chapter 3 Principles)**

The hospital group's COO sponsors a Data Governance programme explicitly as a precondition for MDM success. The programme begins with a readiness assessment — the collaborative readiness assessment reveals that clinical staff have strong informal networks but no formal data coordination mechanisms. The capacity-to-change assessment reveals resistance from senior clinicians who see "data governance" as administration.

DG communication is reframed: "You told us patient record inconsistencies cost your team 15 minutes per transfer. This programme fixes that." Clinical staff become the visible beneficiaries, not just compliance recipients. A clinical Data Stewardship team is formed with a senior nurse and physician in each facility. Within 90 days: a glossary of 25 core clinical terms is agreed, approved by the DGC (which includes the Medical Director), and built into the MDM system as validated reference data. Issue escalation is now tracked in a workflow tool with SLA.

---

### Scenario 3 — Energy/GLC: Petronas-Style Data Governance at Scale

**The Failure (Without Chapter 3 Principles)**

A large Malaysian energy conglomerate has five business divisions (upstream, downstream, LNG, gas processing, retail). Each division has built its own data practices independently over 20 years. A corporate initiative to implement an integrated analytics platform reveals the problem: "production volume" is calculated differently in three divisions, and the group-level dashboard cannot reconcile them.

- There is no enterprise data definition for "production volume."
- Each division's IT team independently manages its data — there is no cross-divisional data ownership.
- When the analytics team asks "who owns this data?" — the answer differs depending on who you ask in each division.
- The board is presented three different production figures in the same board pack.

**Root Cause (DMBOK2 lens):** No enterprise data governance operating model — purely local data management. No Data Owner identified at enterprise level. No Business Glossary with enterprise-approved definitions. Data governance has never been separated from IT governance (conflation trap).

---

**The Success (With Chapter 3 Principles)**

The conglomerate adopts a **federated DG model** — appropriate given its scale and division diversity. A Group Data Office is established under the Group CFO. An enterprise Business Glossary begins with 15 critical business terms — starting with "production volume," "revenue," and "customer." Each term is worked through a cross-divisional Data Stewardship Working Group, producing an approved definition signed off by the DGC.

Division-level DG programmes use the centrally approved definitions as a baseline but are permitted to add division-specific extensions. A Group Data Governance Scorecard tracks conformance across divisions. Within six months, the board receives a single, reconciled production figure — with documented lineage showing exactly how it was calculated from each division's source systems.

---

## 4. Visual Diagrams, Cheat Sheet & Quick Reference

### The DG Programme Architecture

```
         ENTERPRISE LEVEL
         ┌─────────────────────────────────────────────────┐
         │          DATA GOVERNANCE COUNCIL (DGC)          │
         │   (Executive Sponsors + Business Leaders)        │
         │   Approves: Policies / Standards / Architecture  │
         └─────────────────────────┬───────────────────────┘
                                   │ Delegates
         ┌─────────────────────────▼───────────────────────┐
         │      DATA STEWARDSHIP STEERING COMMITTEE         │
         │   (Enterprise & Coordinating Data Stewards)      │
         │   Manages: Issue escalation / Policy rollout     │
         └─────────────────────────┬───────────────────────┘
                                   │ Coordinates
         DOMAIN / FUNCTIONAL LEVEL │
         ┌─────────────────────────▼───────────────────────┐
         │   BUSINESS UNIT DATA STEWARDSHIP TEAMS           │
         │   (Business Data Stewards + Data Owners)         │
         │   Execute: Day-to-day governance activities      │
         │   Maintain: Business Glossary terms in domain    │
         └─────────────────────────┬───────────────────────┘
                                   │ Supported by
         TECHNICAL LEVEL           │
         ┌─────────────────────────▼───────────────────────┐
         │     TECHNICAL DATA STEWARDS                      │
         │   (DBAs, BI Specialists, DQ Analysts,            │
         │    Metadata Administrators, Integration Team)     │
         │   Implement: Standards / Quality Rules / Access  │
         └─────────────────────────────────────────────────┘
```

---

### DG Strategy Deliverables — The Four Components

```
┌─────────────────────────────────────────────────────────────────┐
│                    DG STRATEGY DOCUMENT                          │
├──────────────────┬──────────────────┬──────────────────┬────────┤
│   CHARTER        │  OPERATING       │ IMPLEMENTATION   │ PLAN   │
│                  │  FRAMEWORK       │ ROADMAP          │ FOR    │
│                  │                  │                  │ OPS    │
│ • Vision         │ • Structure      │ • Policy         │SUCCESS │
│ • Mission        │ • Roles &        │   timeline       │        │
│ • Principles     │   accountability │ • Business       │ Target │
│ • Business       │ • Decision       │   Glossary       │ state  │
│   drivers        │   rights         │   launch         │ of     │
│ • Readiness      │ • Interaction    │ • Architecture   │ sustain│
│   assessment     │   model          │   artefacts      │ -able  │
│ • Success        │ • Issue          │ • Standards      │ DG     │
│   criteria       │   escalation     │ • Compliance     │ ops    │
└──────────────────┴──────────────────┴──────────────────┴────────┘
```

---

### OCM in DG — The ADKAR Model Applied

DAMA cites the ADKAR change management model (Prosci/Hiatt & Creasey) as the framework for managing DG cultural change:

```
A ─ AWARENESS       "People understand WHY data governance is needed"
    (Communications: promote value of data assets)

D ─ DESIRE          "People choose to participate and support DG"
    (Communications: incentives aligned with DG behaviours)

K ─ KNOWLEDGE       "People know HOW to change their behaviour"
    (Training: data stewardship, policy, glossary usage)

A ─ ABILITY         "People can implement new skills and behaviours"
    (Coaching, tools, workflow support, stewardship communities)

R ─ REINFORCEMENT   "People sustain the new behaviours over time"
    (Metrics, KPIs, performance reviews tied to DG compliance)
```

---

### DG Metrics Framework

DAMA organises DG metrics into three categories:

```
┌───────────────────────────────────────────────────────────────┐
│                    DG METRICS FRAMEWORK                        │
├──────────────────┬──────────────────┬─────────────────────────┤
│     VALUE        │   EFFECTIVENESS  │    SUSTAINABILITY        │
├──────────────────┼──────────────────┼─────────────────────────┤
│ • Contributions  │ • Achievement of │ • Are policies and      │
│   to business    │   goals and      │   processes working?    │
│   objectives     │   objectives     │                         │
│ • Reduction of   │ • Stewards using │ • Are staff following   │
│   risk           │   relevant tools │   guidance and changing │
│ • Improved       │ • Communication  │   behaviour as needed?  │
│   operational    │   effectiveness  │                         │
│   efficiency     │ • Education /    │ • Conformance to        │
│                  │   training       │   standards             │
│                  │   effectiveness  │                         │
│                  │ • Speed of       │                         │
│                  │   change         │                         │
│                  │   adoption       │                         │
└──────────────────┴──────────────────┴─────────────────────────┘
```

---

### Chapter 3 Quick-Reference Cheat Sheet

| Concept | Key Fact to Remember |
|---------|---------------------|
| DG definition | Exercise of authority and control (planning, monitoring, enforcement) over data assets |
| 3 essential DG characteristics | Sustainable / Embedded / Measured |
| 6 DG principles | Leadership & Strategy / Business-driven / Shared Responsibility / Multi-layered / Framework-based / Principle-based |
| DG vs IT Governance | IT governance = IT assets (COBIT). Data governance = data assets. Separate disciplines |
| 3 operating model types | Centralized / Replicated / Federated |
| DG three functions | Legislative (policies/standards), Judicial (issue mgmt), Executive (protect/serve/admin) |
| Data Owner definition | Business Data Steward with **approval authority** in their data domain |
| "Found not made" quote | Best stewards are identified from informal practice — but stewards can also be trained |
| 4 readiness assessment types | Maturity / Capacity to change / Collaborative readiness / Business alignment |
| 8 issue management categories | Authority / Change mgmt escalations / Compliance / Conflicts / Conformance / Contracts / Security & Identity / Data Quality |
| 4 data asset valuation methods | Replacement cost / Market value / Identified opportunities / Risk cost |
| Business Glossary purpose | Shared definitions + Metadata (synonyms, lineage, rules, steward) — not just a term list |
| DG success failure mode | Cultural resistance — requires formal OCM programme (ADKAR) with executive sponsorship |
| DGC role | Reviews, approves, adopts: policies, standards, architecture; oversees data management project sponsorship |
| Implementation approach | Incremental — MDM project first, or by region/division — never enterprise-wide as first effort |
| DG metrics categories | Value / Effectiveness / Sustainability |

---

## 5. Official DAMA Knowledge Area Visual Reference

> © DAMA International. Licensed under [CC BY-ND 4.0](https://creativecommons.org/licenses/by-nd/4.0/). Source: [dama.org/dmbok2r-infographics](https://dama.org/dmbok2r-infographics/).

### Data Governance & Stewardship — KA Context Diagram

![Data Governance and Stewardship — DMBOK2 Knowledge Area Context Diagram](https://growthzonecmsprodeastus.azureedge.net/sites/2326/2025/04/x-3.png)

---

*References: DAMA-DMBOK2 Revised Edition, Chapter 3 | BNM Risk Management in Technology (RMIT) 2020 | BCBS 239 Principles for Effective Risk Data Aggregation | PDPA 2010 (Act 709) | Prosci ADKAR Change Management Model*

