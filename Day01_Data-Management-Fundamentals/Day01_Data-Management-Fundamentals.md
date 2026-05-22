# Day 01 — Data Management
**DAMA-DMBOK2 | Chapter 1 | Exam Weight: 2%**

> *"Failure to manage data is similar to failure to manage capital. It results in waste and lost opportunity."*
> — DAMA-DMBOK2, Chapter 1

---

## 1. Core Summary & Big Ideas

### What This Chapter Is Really About

Chapter 1 is the **philosophical and architectural foundation** of the entire DMBOK2. It does not teach you *how* to execute any single data management function. Instead, it answers three foundational questions:

- **Why** does data management matter as a business discipline?
- **What** does managing data actually mean — and what does it *not* mean?
- **How** do all 11 Knowledge Areas relate to each other within a single coherent framework?

Every subsequent chapter derives its authority from what is established here. If you skip or skim Chapter 1, every other chapter will feel like a collection of disconnected techniques rather than a unified system of practice.

---

### Core Definitions

These are high-frequency CDMP exam targets. Know them precisely — not approximately.

| Term | DAMA-DMBOK2 Definition |
|------|------------------------|
| **Data** | Facts represented in a structured or unstructured form. Data is a *means of representation* — it stands for things other than itself (Chisholm, 2010). It is both an interpretation of objects *and* an object that must itself be interpreted. |
| **Information** | Data in context. Data becomes information when it is given structure, definition, and meaning relevant to a specific question or decision. |
| **Knowledge** | Information synthesized and applied. The patterns, insights, and understanding that emerge from information and enable purposeful decisions. |
| **Data Management** | *"The development, execution, and supervision of plans, policies, programs, and practices that deliver, control, protect, and enhance the value of data and information assets throughout their lifecycles."* |

> **Key distinction the exam loves to test:** Data is *not* the same as information. Organizations often have enormous volumes of data but very little actionable information — because they have not managed context (Metadata). Data management is the discipline that bridges this gap.

---

### Breaking Down the DAMA Definition

The definition of Data Management is deceptively dense. Each word carries weight:

| Component | What It Means in Practice |
|-----------|--------------------------|
| **Development** | Frameworks, policies, and strategies must be *designed deliberately* — they do not emerge naturally from operations |
| **Execution** | A governance policy sitting in a document is not data management. It must be operationalised |
| **Supervision** | Data management is ongoing — it requires monitoring, measurement, and continuous improvement |
| **Plans, Policies, Programs, Practices** | Four instruments that work together: plans set direction, policies set rules, programs deliver change, practices embed behaviour |
| **Deliver, Control, Protect, Enhance** | The full stewardship spectrum — from provisioning data to users through to defending it from misuse |
| **Throughout their lifecycles** | No lifecycle stage is optional. Management begins at data creation and ends at disposal |

---

### The DAMA Data Management Principles

These 10 principles are the **philosophical backbone** of the DMBOK2. Every Knowledge Area, every activity, every governance decision is grounded in one or more of these. They are the most tested concepts in Type 2 (Principle-Based) and Type 10 (Judgment) CDMP exam questions.

| # | Principle | What It Means |
|---|-----------|---------------|
| 1 | **Data is an asset with unique properties** | Unlike physical assets, data is not consumed when used, can be infinitely replicated, and loses value if poorly maintained — it needs its own management discipline |
| 2 | **The value of data can and should be expressed in economic terms** | Data decisions must be justified by business value — replacement cost, risk cost, market value, identified opportunities |
| 3 | **Managing data means managing the quality of data** | Quality is not a separate initiative bolted on top. It is intrinsic to data management — you cannot separate the two |
| 4 | **It takes Metadata to manage data** | You cannot govern, secure, or integrate data you cannot describe. Metadata is the prerequisite for almost every other data management activity |
| 5 | **It takes planning to manage data** | Data quality and data value do not emerge naturally. They require deliberate design, defined processes, and proactive management decisions |
| 6 | **Data management is cross-functional** | Neither IT nor the business can manage data alone. It requires shared accountability and collaboration across technical and business roles |
| 7 | **Data management requires an enterprise perspective** | Silo-based data management creates contradictions and redundancy. Enterprise-wide thinking is the prerequisite for consistent, trusted data |
| 8 | **Data management must account for a range of perspectives** | Regulators, customers, executives, engineers — all have different data needs. All are valid. Data management must serve them all |
| 9 | **Data management is lifecycle management** | From creation through disposal, every stage of a data asset's life requires active management decisions |
| 10 | **Different types of data have different lifecycle characteristics** | Master data, transactional data, reference data, and unstructured content each behave differently and cannot be managed identically |

> **Exam Trap:** When a question asks *"what is the primary goal of data management?"*, the correct DAMA answer is always framed as **enabling business value** — not improving IT systems, reducing storage costs, or solving a technical problem. The business value framing is non-negotiable in DAMA's worldview.

---

### The Data Lifecycle

```
  ┌─────────┐    ┌─────────┐    ┌─────────┐    ┌─────────┐    ┌─────────┐
  │ CAPTURE │───▶│  STORE  │───▶│   USE   │───▶│ ARCHIVE │───▶│ DISPOSE │
  └─────────┘    └─────────┘    └─────────┘    └─────────┘    └─────────┘
       │               │               │               │              │
  Data Modelling   Data Storage    Data Quality    Document &    PDPA / Legal
  Architecture     & Operations    Metadata        Content Mgmt  Compliance
                                   DW & BI         Security
```

Every data management Knowledge Area maps to one or more lifecycle stages. **Data only creates value when it is used** — data stored but never accessed is a cost, not an asset.

---

## 2. The DAMA Wheel & Environmental Elements

> 📌 **Official DAMA diagrams in this section are licensed under [CC BY-ND 4.0](https://creativecommons.org/licenses/by-nd/4.0/) by DAMA International.** They may be shared with attribution but not modified.

### The DAMA Wheel — Structure & Architecture

The **DAMA Wheel** is the primary structural framework of DMBOK2. It organises all data management work into 11 Knowledge Areas arranged as a wheel, with **Data Governance at the hub**.

```
                         ┌───────────────────┐
                         │   DATA QUALITY    │
              ┌──────────┤       11%         ├──────────┐
              │          └───────────────────┘          │
   ┌──────────┴──────┐                        ┌─────────┴───────┐
   │    METADATA     │                        │   DATA GOVERNANCE│
   │      11%        │   ╔═══════════════╗   │       11%       │
   └──────────┬──────┘   ║               ║   └─────────┬───────┘
              │          ║     DATA      ║             │
   ┌──────────┴──────┐   ║  GOVERNANCE  ║   ┌─────────┴───────┐
   │  DATA W/H & BI  │   ║   (Centre)   ║   │  DATA MODELING  │
   │      10%        │   ║               ║   │      11%       │
   └──────────┬──────┘   ╚═══════════════╝   └─────────┬───────┘
              │                                         │
   ┌──────────┴──────┐                        ┌─────────┴───────┐
   │  MASTER & REF   │                        │  DATA STORAGE   │
   │  DATA    10%    │                        │  & OPS    6%    │
   └──────────┬──────┘                        └─────────┬───────┘
              │          ┌───────────────────┐          │
              └──────────┤   DOCUMENT &      ├──────────┘
                         │ CONTENT MGT  6%   │
                         └───────────────────┘
```

> **Why is Governance at the centre?** Because every other Knowledge Area requires direction, policy, and oversight — which is exactly what Data Governance provides. Without governance, each KA operates independently with no accountability or coordination. Governance does not *replace* the other KAs; it *enables* them.

**Official DAMA Wheel (Figure 5 — DMBOK2 Revised):**

![DAMA Wheel — The DAMA Framework showing Data Governance at the centre surrounded by 10 Knowledge Areas](https://growthzonecmsprodeastus.azureedge.net/sites/2326/2025/06/Figure-5-The-DAMA-Wheel-Dark-Option.png)

*© DAMA International. Licensed under [CC BY-ND 4.0](https://creativecommons.org/licenses/by-nd/4.0/). Source: [dama.org/dmbok2r-infographics](https://dama.org/dmbok2r-infographics/)*

---

### The 11 Knowledge Areas — At a Glance

| # | Knowledge Area | Chapter | Exam Weight | Core Purpose |
|---|----------------|---------|-------------|--------------|
| 1 | Data Governance | 3 | **11%** | Decision rights, accountability, policy oversight |
| 2 | Data Architecture | 4 | 6% | Blueprint for managing data assets enterprise-wide |
| 3 | Data Modeling & Design | 5 | **11%** | Discovering, representing, and communicating data requirements |
| 4 | Data Storage & Operations | 6 | 6% | Design, implementation, and support of stored data |
| 5 | Data Security | 7 | 6% | Privacy, confidentiality, access control |
| 6 | Data Integration & Interoperability | 8 | 6% | Moving and consolidating data within and between systems |
| 7 | Document & Content Management | 9 | 6% | Lifecycle management of unstructured media |
| 8 | Reference & Master Data | 10 | **10%** | Core shared data reconciled across the enterprise |
| 9 | Data Warehousing & BI | 11 | **10%** | Decision support data, analytics, and reporting |
| 10 | Metadata Management | 12 | **11%** | Context, definitions, lineage — making data understandable |
| 11 | Data Quality | 13 | **11%** | Measuring and improving fitness of data for use |

> **Study priority rule:** Data Governance + Modeling + Metadata + Data Quality + Master Data + DW/BI = **66% of the CDMP exam**. These six areas deserve proportionally deeper study time.

**Data Governance — KA Context Diagram:**

![Data Governance and Stewardship — DMBOK2 Knowledge Area Context Diagram](https://growthzonecmsprodeastus.azureedge.net/sites/2326/2025/04/x-3.png)

*© DAMA International. Licensed under [CC BY-ND 4.0](https://creativecommons.org/licenses/by-nd/4.0/). Source: [dama.org/dmbok2r-infographics](https://dama.org/dmbok2r-infographics/)*

---

### The Environmental Elements (The DAMA Hexagon)

Every Knowledge Area in DMBOK2 is described through **six environmental elements** — a consistent structural lens applied across all 11 chapters. Understanding this hexagon makes every chapter predictable and navigable.

```
              ┌─────────────────────┐
              │  GOALS & PRINCIPLES │
              │  (Why we do it)     │
              └──────────┬──────────┘
                         │
    ┌────────────┐        │        ┌────────────────────┐
    │ TECHNIQUES │        │        │ ROLES &            │
    │ (How we    │◀───────┼───────▶│ RESPONSIBILITIES   │
    │  do it)    │        │        │ (Who does it)      │
    └────────────┘        │        └────────────────────┘
                         │
              ┌──────────┴──────────┐
              │     ACTIVITIES      │
              │  (What we do)       │
              └──────────┬──────────┘
                         │
         ┌───────────────┴───────────────┐
         │                               │
┌────────┴───────┐             ┌─────────┴──────┐
│  DELIVERABLES  │             │ ORGANIZATION & │
│  (What we      │             │ CULTURE        │
│  produce)      │             │ (Context)      │
└────────────────┘             └────────────────┘
```

| Element | CDMP Exam Relevance |
|---------|---------------------|
| **Goals & Principles** | Tested in Type 2 (Principle-Based) questions — "why is X important?" |
| **Activities** | Tested in Type 3 (Scenario) and Type 4 (Process/Framework) — "what should you do first?" |
| **Deliverables** | Tested in Type 6 (Role/Responsibility) — "what does a Data Steward produce?" |
| **Roles & Responsibilities** | Tested heavily in Type 6 — "who is accountable for X?" |
| **Techniques** | Tested in Type 7 (Tool/Technology) — "which tool/method supports X?" |
| **Organization & Culture** | Tested in Type 10 (Judgment) — "what is the biggest barrier to implementation?" |

---

### Must-Know CDMP Exam Concepts & Traps for Chapter 1

**Concept 1 — Shared Responsibility (Trap: it's not IT's job alone)**
The DMBOK2 is unambiguous: data management requires *shared responsibility between business and IT*. If an exam question implies that the CIO or IT department alone should own data governance or data quality, that answer is wrong. Business ownership is non-negotiable.

**Concept 2 — Data as Asset ≠ Just Storing Data (Trap: storage is not management)**
Storing data is not the same as managing it. Data only becomes an asset when it is actively governed, described with Metadata, kept at a defined quality level, and made available for use. A question that frames "we have lots of data stored" as equivalent to "we manage data well" is setting a trap.

**Concept 3 — Metadata is the Prerequisite, Not an Optional Add-On (Trap: Metadata as afterthought)**
Principle 4 — *"It takes Metadata to manage data"* — means that any data initiative that does not begin with defining what the data means will eventually fail. Metadata is not a nice-to-have. It is the foundation.

**Concept 4 — Enterprise Perspective vs. Departmental (Trap: local optimization)**
A data quality improvement project that works in one department but creates inconsistency with the rest of the enterprise is *not* a success from a DAMA perspective. Principle 7 requires enterprise-wide thinking. Local optimization that creates enterprise-level problems is explicitly what DMBOK2 cautions against.

**Concept 5 — The Lifecycle Includes Disposal (Trap: ignoring the end)**
Many practitioners think of data management as creation, storage, and use. DMBOK2 includes **archive and dispose** as explicit lifecycle stages requiring active management decisions. PDPA-style regulations in particular mandate this. An organization that never disposes of data is not managing its lifecycle.

**Concept 6 — Data Management is Not a Project (Trap: treating it as one-time)**
Data management requires *ongoing supervision*, not just a one-time setup. Exam questions that describe a governance programme being "completed" and then handed over to IT to maintain are describing what DAMA would consider a governance failure.

---

## 3. Real-World Business Context & Applications

### Scenario 1 — Fintech: Digital Lending Platform

**The Failure (Without Chapter 1 Principles)**

A Malaysian digital lending startup, growing fast, builds separate systems for loan origination, credit scoring, collections, and customer service — each maintained by a different team. Within 18 months:

- "Customer" is defined differently in each system. The loan origination system counts a "customer" as anyone who submitted an application. The collections system counts anyone with an active overdue account. The CRM counts anyone who created a profile.
- When regulators ask for a report on total unique borrowers, the three systems produce three different numbers. None can be reconciled.
- The credit risk team cannot build reliable models because the same individual appears under five different customer IDs across systems, with conflicting income and employment data.
- A PDPA audit finds that some customer data is retained indefinitely — violating the Retention Principle — because no one owns the data disposal decision.

**Root Cause (DMBOK2 lens):** No enterprise perspective (Principle 7), no Metadata defining what "customer" means (Principle 4), no lifecycle management covering disposal (Principle 9), and data management treated as IT's problem alone (Principle 6).

---

**The Success (With Chapter 1 Principles)**

The same fintech, before scaling, invests three months in foundational data management:

- An enterprise-wide definition of "customer" is agreed between product, risk, compliance, and technology — documented in a Business Glossary (Metadata).
- A single Customer ID framework is designed before any new system is built — the Architecture is set before the code.
- A data retention policy is written aligned to BNM RMIT and PDPA requirements — data older than the defined retention period is flagged for review quarterly.
- Business analysts and IT engineers co-own data quality rules — not one team alone.

**Result:** When the same regulatory request arrives, the fintech produces a single, auditable number within hours, with a documented data lineage trail. Credit risk models are built on a unified, consistent customer dataset. The PDPA audit finds documented retention schedules for every data category.

---

### Scenario 2 — Healthcare: Hospital Network

**The Failure (Without Chapter 1 Principles)**

A private hospital group in Malaysia operates five hospitals, each running a different Electronic Medical Record (EMR) system acquired over 15 years. Leadership wants a group-wide patient safety dashboard to monitor adverse events.

- Patient records exist in five systems. A patient who visits three different hospitals in the group has three unlinked records with potentially contradictory medication histories.
- There is no enterprise definition of "adverse event" — each hospital codes and reports incidents differently.
- The IT department builds the dashboard without business input. Clinicians refuse to use it because the data does not match what they see on the ward.
- When a patient suffers a drug interaction because a prescribing doctor could not see the patient's full medication history (split across two hospital systems), the group cannot produce a complete audit trail for the inquiry.

**Root Cause (DMBOK2 lens):** No enterprise perspective on patient identity (Principle 7), no shared Metadata definitions for clinical concepts (Principle 4), and data management treated as a technology project rather than a clinical governance obligation (Principle 6).

---

**The Success (With Chapter 1 Principles)**

A hospital group with mature data management practices:

- Establishes a Group Patient Index — a Master Data Management programme that links patient records across all five hospitals using a unique Group Patient ID.
- Defines clinical terminology centrally — "adverse event", "readmission", "length of stay" — in a clinical data dictionary agreed by Medical Affairs, not IT.
- The patient safety dashboard is co-designed by clinical leads and data analysts. It is built on trusted, defined, reconciled data.
- When an adverse event occurs, a complete medication history across all five hospitals is retrievable within minutes.

---

### Scenario 3 — E-Commerce: Multi-Category Retailer

**The Failure (Without Chapter 1 Principles)**

A large Malaysian e-commerce platform grows by acquisition, adding fashion, electronics, and grocery verticals through three separate acquisitions. Each vertical manages its own data:

- Product data is stored in three separate catalogs with no common product taxonomy. The same Samsung phone appears as "Samsung Galaxy S24" in one system, "Galaxy S24 5G 256GB" in another, and "Smartphone Samsung" in a third.
- When the CEO asks for total revenue by brand, the analytics team spends three weeks manually reconciling product records. The number they produce has a known 15% error margin that nobody admits in the board presentation.
- A recommendation engine is built on this fragmented product data. It recommends products the customer already owns and fails to cross-sell across verticals — destroying the core business case for the acquisitions.

**Root Cause (DMBOK2 lens):** No enterprise product data architecture, no reference data standards for product taxonomy (Principle 7), no Metadata framework, and no recognition that managing data quality (Principle 3) is a prerequisite for any analytics capability.

---

**The Success (With Chapter 1 Principles)**

The same platform, before building the recommendation engine:

- Creates a unified Product Taxonomy as Reference Data — agreed by merchandising, technology, and analytics — with a single canonical product identifier across all three verticals.
- Implements a data quality programme for product data — completeness, accuracy, and naming consistency measured weekly, owned jointly by merchandising and data engineering.
- The recommendation engine is built on this unified, quality-controlled product catalog.
- Revenue by brand is a standard report generated in minutes, trusted by the board.

> **The pattern across all three scenarios is the same:** data management problems are always presented as technical problems, but they are fundamentally *business management problems*. DAMA's Chapter 1 makes this explicit — and the CDMP exam tests whether you understand this distinction.

---

## 4. Visual Layout Suggestion

### Diagram 1 — The Data-to-Value Chain

The most important conceptual diagram for Chapter 1 is the relationship between raw data, management discipline, and business value.

```
┌─────────────────────────────────────────────────────────────────────┐
│                      DATA-TO-VALUE CHAIN                            │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│   RAW DATA        MANAGED DATA        INFORMATION       VALUE       │
│                                                                     │
│  ┌───────┐   +   ┌─────────────┐  =  ┌──────────┐  →  ┌───────┐   │
│  │ Facts │       │  Metadata   │     │ Context  │     │Insight│   │
│  │ Logs  │       │  Quality    │     │ Meaning  │     │Decision│  │
│  │ Events│       │  Governance │     │ Trust    │     │Revenue│   │
│  │ Docs  │       │  Lifecycle  │     │ Lineage  │     │Control│   │
│  └───────┘       └─────────────┘     └──────────┘     └───────┘   │
│                                                                     │
│   ← Without data management, this chain breaks here →              │
│            Between RAW DATA and MANAGED DATA                        │
└─────────────────────────────────────────────────────────────────────┘
```

---

### Diagram 2 — Data Management as Shared Accountability

A common misconception is that data management sits purely in the IT domain. DMBOK2 explicitly positions it as a **shared discipline**:

```
┌─────────────────────────────────────────────────────┐
│              DATA MANAGEMENT ACCOUNTABILITY          │
├──────────────────────────┬──────────────────────────┤
│     BUSINESS SIDE        │       TECHNOLOGY SIDE     │
├──────────────────────────┼──────────────────────────┤
│ • Define what data means │ • Build systems to store  │
│ • Own data quality rules │   and process data        │
│ • Set retention policies │ • Implement Metadata      │
│ • Validate fitness for   │   repositories            │
│   use                    │ • Enforce data security   │
│ • Fund data initiatives  │ • Manage infrastructure   │
│ • Appoint Data Stewards  │ • Monitor data pipelines  │
│ • Approve data standards │ • Execute data lifecycle  │
├──────────────────────────┴──────────────────────────┤
│                SHARED ZONE                          │
│  ┌─────────────────────────────────────────────┐   │
│  │  Data Governance Council / Data Stewardship │   │
│  │  Business Glossary | Data Quality Rules     │   │
│  │  Data Strategy | Cross-functional Standards │   │
│  └─────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────┘
```

---

### Diagram 3 — The 10 Principles Grouped by Theme

```
┌─────────────────────────────────────────────────────────────────────┐
│              DATA MANAGEMENT PRINCIPLES — THEMATIC VIEW              │
├─────────────────────────┬───────────────────────────────────────────┤
│  ASSET THINKING         │  #1 Data is an asset with unique          │
│                         │     properties                            │
│                         │  #2 Value can be expressed economically   │
├─────────────────────────┼───────────────────────────────────────────┤
│  QUALITY THINKING       │  #3 Managing data = managing quality      │
│                         │  #4 It takes Metadata to manage data      │
├─────────────────────────┼───────────────────────────────────────────┤
│  STRATEGIC THINKING     │  #5 It takes planning to manage data      │
│                         │  #7 Enterprise perspective is required    │
├─────────────────────────┼───────────────────────────────────────────┤
│  PEOPLE THINKING        │  #6 Data management is cross-functional   │
│                         │  #8 Must account for a range of           │
│                         │     perspectives                          │
├─────────────────────────┼───────────────────────────────────────────┤
│  LIFECYCLE THINKING     │  #9 Data management is lifecycle mgmt     │
│                         │  #10 Different data types, different      │
│                         │      lifecycle characteristics            │
└─────────────────────────┴───────────────────────────────────────────┘
```

---

### Diagram 4 — CDMP Question Type Map for Chapter 1

```
┌────────────────────────┬──────────────────────────────────────────┐
│    QUESTION TYPE       │   WHAT CHAPTER 1 CONCEPT IT TESTS        │
├────────────────────────┼──────────────────────────────────────────┤
│ Type 1 — Definition    │ DMBOK2 definition of Data Management;    │
│                        │ Data vs. Information distinction          │
├────────────────────────┼──────────────────────────────────────────┤
│ Type 2 — Principle     │ The 10 Data Management Principles;       │
│                        │ Why Metadata is foundational              │
├────────────────────────┼──────────────────────────────────────────┤
│ Type 4 — Process       │ Data Lifecycle sequence                   │
│                        │ (Capture→Store→Use→Archive→Dispose)       │
├────────────────────────┼──────────────────────────────────────────┤
│ Type 5 — Comparison    │ Data vs. Information vs. Knowledge;      │
│                        │ Data as asset vs. physical assets         │
├────────────────────────┼──────────────────────────────────────────┤
│ Type 6 — Role          │ Shared responsibility (Business + IT);   │
│                        │ Who sits at the centre of the DAMA Wheel  │
├────────────────────────┼──────────────────────────────────────────┤
│ Type 9 — Integration   │ How the DAMA Wheel KAs depend on each    │
│                        │ other; why Governance is at the centre    │
├────────────────────────┼──────────────────────────────────────────┤
│ Type 10 — Judgment     │ First step when starting a data programme;│
│                        │ Biggest barrier to data management success │
└────────────────────────┴──────────────────────────────────────────┘
```

---

## Quick-Reference Cheat Sheet

| Concept | One-Line Answer |
|---------|----------------|
| DMBOK2 definition | Development, execution, and supervision of plans, policies, programs, and practices... throughout their lifecycles |
| What sits at the DAMA Wheel centre | Data Governance |
| How many Knowledge Areas | 11 (Chapters 3–13) |
| Data Lifecycle order | Capture → Store → Use → Archive → Dispose |
| Who is responsible for data management | Business AND IT — shared responsibility |
| Why Metadata matters | You cannot manage data you cannot describe (Principle 4) |
| Highest exam-weight KAs | Data Governance, Modeling, Metadata, Data Quality (11% each) |
| What makes data a unique asset | Not consumed when used; infinite replication; loses value if poorly maintained |
| Primary business driver | Enable organizations to get value from data assets |
| Biggest cultural barrier | Treating data management as IT's problem alone |

---

## Works Cited

- DAMA International. *DAMA-DMBOK: Data Management Body of Knowledge, 2nd Edition*. Technics Publications, 2017.
- Chisholm, M. (2010). *Definitions in Data Management*. Design Media Publishing.
- Evans, N. and Price, J. (2012). *Barriers to the Effective Deployment of Information Assets: An Executive Management Perspective.*
- Personal Data Protection Act 2010 (Act 709), Malaysia — pdp.gov.my
- Bank Negara Malaysia. *Risk Management in Technology (RMIT) Policy Document*, 2020 — bnm.gov.my
