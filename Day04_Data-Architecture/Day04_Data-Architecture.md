# Day 04 — Data Architecture
**DAMA-DMBOK2 | Chapter 4 | Exam Weight: 6%**

> *"Data Architecture defines the blueprint for managing data assets by aligning with organisational strategy to establish strategic data requirements and designs to meet those requirements."*
> — DAMA-DMBOK2, Chapter 4

---

## 1. Core Summary & Big Ideas

### What This Chapter Is Really About

Chapter 4 is the **structural blueprint layer** of data management. If Chapter 3 (Governance) answers *who decides*, then Chapter 4 answers *what we are building and how it all fits together*. Data Architecture translates organisational strategy into a coherent, documented blueprint for how data assets will be created, stored, integrated, and used — across systems, processes, and business units.

The central metaphor DAMA uses is an analogy to building architecture: just as an architect designs the layout of a building before construction begins, a Data Architect designs the structure of an organisation's data landscape before systems are built. Without this blueprint, systems grow in an uncoordinated way — producing data silos, integration failures, and technical debt.

Three questions define the scope of Data Architecture:

- **What data exists or needs to exist?** — Identifying and classifying data assets across the enterprise
- **How does data flow?** — Understanding movement of data across systems, processes, and boundaries
- **How does data support strategy?** — Ensuring data structures align with business capabilities and goals

---

### Core Definitions

| Term | DAMA-DMBOK2 Definition / Key Point |
|------|-------------------------------------|
| **Data Architecture** | Identifying the data needs of the enterprise and designing and maintaining the master blueprints to meet those needs. It defines the standard that govern which data is collected and how it is stored, arranged, integrated, and put to use in data systems and in organisations |
| **Enterprise Architecture (EA)** | A discipline that proactively and holistically leads enterprise responses to disruptive forces by identifying and analysing the execution of change. Data Architecture is one of four EA domains |
| **Enterprise Data Model (EDM)** | A high-level, integrated definition of data within an enterprise — a holistic view of enterprise data, showing subject areas, their relationships, and key entities within each subject area |
| **Subject Area** | A logical grouping of related data entities that represents a major area of business concern — e.g., Customer, Product, Finance, Employee |
| **Data Flow** | The movement of data from its origin point through its storage, transformation, and consumption points. Data flows show how data moves across systems and processes |
| **Data Architecture Artefact** | Any document or model produced as part of the Data Architecture practice — includes EDMs, data flow diagrams, data taxonomies, asset inventories, integration specifications |

> **Key distinction the exam tests:** Data Architecture is a **KA within DMBOK2**, but it also lives within **Enterprise Architecture**. The CDMP exam tests your ability to position Data Architecture correctly within both contexts — it is not the same as Data Modeling (which is Chapter 5 and operates at a more detailed level).

---

### Data Architecture vs. Data Modeling — The Critical Distinction

This is one of the most frequently tested distinctions in the CDMP exam for this topic area:

| Dimension | Data Architecture (Ch. 4) | Data Modeling (Ch. 5) |
|-----------|--------------------------|----------------------|
| **Scope** | Enterprise-wide; strategic | Project or domain level; tactical |
| **Level** | High — subject areas, data flows, integration | Detailed — entities, attributes, relationships |
| **Primary Artefact** | Enterprise Data Model (subject area level) | Conceptual / Logical / Physical data models |
| **Audience** | CxO, Enterprise Architects, DGC | Developers, DBAs, analysts |
| **Time horizon** | Long-term (years) | Short-to-medium term (project lifecycle) |
| **Driven by** | Business strategy and capability model | Business requirements and system design |
| **Governed by** | Data Governance Council; Enterprise Architecture Review Board | Data modeling standards; SDLC process |

> Architecture sets the direction. Modeling fills in the detail. You cannot model correctly without an architectural context to model within.

---

## 2. The DAMA Framework View — Architecture in Context

### The Four Enterprise Architecture Domains

Data Architecture does not exist in isolation. DAMA positions it within the broader Enterprise Architecture (EA) landscape as one of four interdependent domains:

```
┌──────────────────────────────────────────────────────────┐
│               ENTERPRISE ARCHITECTURE                     │
├─────────────────┬────────────────┬────────────────────────┤
│  BUSINESS       │  APPLICATION   │  TECHNOLOGY            │
│  ARCHITECTURE   │  ARCHITECTURE  │  ARCHITECTURE          │
│                 │                │                        │
│  Strategy,      │  Systems,      │  Infrastructure,       │
│  capabilities,  │  software,     │  platforms,            │
│  processes,     │  integrations, │  networks,             │
│  functions      │  APIs          │  cloud, hardware       │
├─────────────────┴────────────────┴────────────────────────┤
│                 DATA ARCHITECTURE                          │
│  Enterprise Data Model, Data Flows, Data Standards,       │
│  Subject Areas, Integration Architecture, Data Taxonomy   │
│  — the DATA layer that runs ACROSS all three domains —    │
└──────────────────────────────────────────────────────────┘
```

Data Architecture is unique among the four EA domains because it cuts across all three: business processes create data, applications manage and transform data, and technology infrastructure stores and moves it. A Data Architect must understand all three layers to design a coherent data blueprint.

**Common EA Frameworks used in Data Architecture work:**

| Framework | Description | CDMP Relevance |
|-----------|-------------|----------------|
| **TOGAF** (The Open Group Architecture Framework) | Most widely used EA framework; includes Architecture Development Method (ADM) | Know that Data Architecture aligns with TOGAF's Information Architecture layer |
| **Zachman Framework** | 6×6 matrix: rows = stakeholder perspectives, columns = interrogatives (What, How, Where, Who, When, Why) | Data Architecture addresses the "What" column across multiple rows |
| **FEAF** (Federal Enterprise Architecture Framework) | US government EA framework; includes Data Reference Model | Relevant for public sector data architecture |
| **DoDAF** (Department of Defense Architecture Framework) | US military EA; data-centric views | Specialist context |

---

### The Strategic Alignment Model

DAMA references Henderson and Venkatraman's **Strategic Alignment Model** to explain how Data Architecture connects business strategy to IT infrastructure. The model has four domains arranged in a 2×2:

```
                EXTERNAL (Market-facing)
         ┌─────────────────────────────────────┐
BUSINESS │  BUSINESS STRATEGY  │  IT STRATEGY  │
         ├─────────────────────┼───────────────┤
IT       │  ORGANISATIONAL     │  IT           │
         │  INFRASTRUCTURE     │  INFRASTRUCTURE│
         │  & PROCESSES        │  & PROCESSES  │
         └─────────────────────────────────────┘
                INTERNAL (Operations)
```

Data Architecture operates primarily in the lower half — translating strategy into operational infrastructure — while maintaining alignment with the upper half (business and IT strategy). This model explains why Data Architecture decisions cannot be made by IT alone: they must be driven by business strategy.

---

### The Amsterdam Information Model

DAMA also references the **Amsterdam Information Model** as a way of understanding how data architecture relates to information management:

```
     STRATEGIC
     ┌──────────────────────────────────────┐
     │  INFORMATION  ← → COMMUNICATION      │
     │  MANAGEMENT        MANAGEMENT        │
     ├──────────────────────────────────────┤
     │  DATA         ← → TECHNOLOGY         │
     │  MANAGEMENT        MANAGEMENT        │
     └──────────────────────────────────────┘
     OPERATIONAL
```

This model reinforces the DAMA position: data management (including Data Architecture) is distinct from — but interdependent with — technology management. Data Architecture bridges both.

---

### Core Data Architecture Artefacts

These are the primary outputs of the Data Architecture practice. Each is a testable concept:

| Artefact | Description | Exam Relevance |
|----------|-------------|----------------|
| **Enterprise Data Model (EDM)** | A high-level, integrated view of enterprise data — typically showing 10–30 subject areas and their relationships. Not detailed — it orients and coordinates | Governance sponsors and approves the EDM. It is a DGC artefact, not just an IT one |
| **Data Flow Diagrams** | Show how data moves between systems, processes, and organisational boundaries. Include source, transformation, and destination | Required for lineage documentation; tested in Type 4 (Process) questions |
| **Data Value Chain** | Maps data as it moves from raw capture through processing to final consumption as insight or decision support | Connects Data Architecture to business value — Chapter 1 concept applied |
| **Subject Area Model** | Groups related entities into logical domains (Customer, Product, Order, Finance). The topmost level of the data model hierarchy | Tested in Type 6 (Role) questions — Data Architects define subject areas |
| **Data Taxonomy** | A hierarchical classification of data types and categories used across the enterprise | Enables consistent data classification for governance, security, and metadata management |
| **Data Asset Inventory** | A catalogue of all significant data assets — their location, owner, classification, and relationships | Prerequisite for Metadata Management (Ch. 12) and Data Governance (Ch. 3) |
| **Integration Architecture** | Defines the patterns and standards for data movement and consolidation between systems (ETL, API, event streaming, etc.) | Connects to Data Integration & Interoperability (Ch. 8) |

---

### The Three Data Architecture Levels

Data Architecture spans three levels of abstraction, each serving a different audience and purpose:

```
LEVEL 1 — CONCEPTUAL (Enterprise / Strategic)
  What: Enterprise Data Model — subject areas and high-level relationships
  Who: CDO, DGC, Enterprise Architects, senior business leaders
  Example: "Customer" is a subject area with relationships to "Order" and "Product"

LEVEL 2 — LOGICAL (Domain / Design)
  What: Detailed data models — entities, attributes, relationships, business rules
  Who: Data Modelers, Business Analysts, project teams
  Example: Customer entity has attributes: CustomerID, Name, Segment, Status

LEVEL 3 — PHYSICAL (System / Implementation)
  What: Database schemas, table structures, indexes, partitioning, platform specifics
  Who: DBAs, developers, infrastructure architects
  Example: CUSTOMER table in Oracle DB with specific column types and constraints
```

> **Exam rule:** Data Architecture primarily operates at Level 1 (Conceptual). Data Modeling (Ch. 5) operates at Levels 2 and 3. The exam will test whether you can correctly assign artefacts and activities to the right level.

---

### Data Architecture Activities — The Four Core Tasks

DMBOK2 defines four primary activities for the Data Architecture practice:

**Activity 1 — Establish the Data Architecture Practice**
Before producing artefacts, the organisation must establish the governance structure, tools, and processes for Data Architecture to function:
- Define the Data Architecture team's roles, reporting structure, and mandate
- Select EA frameworks and data modeling tools
- Establish an Architecture Review Board (ARB) or Architecture Review process
- Define standards for artefact production and maintenance

**Activity 2 — Integrate with Enterprise Architecture**
Data Architecture must not operate in isolation:
- Align Data Architecture with Business, Application, and Technology Architecture domains
- Participate in EA governance processes — project reviews, change control, technology decisions
- Ensure the EDM reflects current business capabilities and strategy
- Coordinate with the DGC on governance of architectural standards

**Activity 3 — Define the Data Architecture**
This is the core production activity:
- Develop the Enterprise Data Model (subject areas and relationships)
- Document data flows across systems and processes
- Identify critical data elements and their sources of record
- Define data integration patterns and standards
- Develop the data taxonomy and classification scheme
- Create and maintain the data asset inventory

**Activity 4 — Review and Maintain Data Architecture**
Architecture is not a one-time deliverable:
- Review architecture artefacts on a defined schedule (typically annual)
- Assess impact of new projects, system changes, and business strategy shifts
- Update the EDM and data flows as the landscape evolves
- Participate in project SDLC gates to ensure architectural compliance
- Track technical debt in data architecture and recommend remediation

---

### Must-Know CDMP Exam Concepts & Traps for Chapter 4

**Concept 1 — Data Architecture is a Business Function, Not Just IT (Trap: IT ownership)**
The EDM must be sponsored by the DGC and aligned to business strategy. If an exam scenario presents Data Architecture as a purely technical function managed by IT, that is an anti-pattern. Business strategy drives architectural decisions.

**Concept 2 — EDM ≠ Data Dictionary (Trap: conflating artefacts)**
The Enterprise Data Model shows subject areas and their relationships at a high level. A data dictionary documents detailed attributes and definitions. They are different artefacts at different levels of abstraction.

**Concept 3 — Architecture Precedes Modeling (Trap: wrong sequence)**
Architecture is established before detailed modeling begins. If an exam scenario shows detailed data models being built before an Enterprise Data Model exists, that is a sequencing failure — and a common cause of data silos.

**Concept 4 — Subject Areas Are Business-Driven (Trap: system-driven)**
Subject areas should reflect business domains and capabilities — not system boundaries or database schemas. A "Customer" subject area exists because the business cares about customers — not because there is a Customer database. Systems come and go; business domains persist.

**Concept 5 — Data Architecture Enables Data Governance (Trap: treating them as separate)**
The EDM provides governance with the map it needs to assign ownership, define stewardship domains, and manage data quality at an enterprise level. Governance without Architecture is like governing a country without a map. Architecture without Governance is a blueprint no one enforces.

**Concept 6 — TOGAF and Zachman Are Referenced, Not Prescribed (Trap: assuming DAMA mandates a framework)**
DAMA references TOGAF, Zachman, and other EA frameworks as options. DAMA does not mandate a specific EA framework. The exam may test recognition of these frameworks but will not require deep knowledge of their internal mechanics.

---

## 3. Real-World Business Context & Applications

### Scenario 1 — Financial Services: Core Banking Transformation

**The Failure (Without Chapter 4 Principles)**

A large Malaysian bank embarks on a core banking system replacement — migrating from a 20-year-old legacy system to a modern platform. The project is led by IT with a focus on system migration. No Data Architecture work is commissioned before implementation begins.

Eighteen months in:
- The new system uses a completely different data structure for "Account" — the legacy system had one account type, the new system has six. No mapping was designed before migration began.
- The data warehouse, built to feed off the legacy system, cannot be updated to reflect the new structure because no one documented what changed and why.
- A "Customer" in the new core banking system does not match a "Customer" in the CRM system — 40% of records cannot be automatically linked.
- Regulatory reports fail because three source systems now define "balance" differently and no reconciliation rule was designed.

**Root Cause (DMBOK2 lens):** No Enterprise Data Model was created before the project began — so there was no architectural blueprint to define how "Customer," "Account," and "Balance" should be consistently represented across systems. Data Architecture was not integrated with the project's EA approach. No architectural review gate existed in the SDLC.

---

**The Success (With Chapter 4 Principles)**

The same bank, with a CDO-led approach, commissions Data Architecture work as the *first* workstream of the transformation:

- A subject area Enterprise Data Model is produced covering: Party (Customer/Counterparty), Account, Product, Transaction, Collateral, and Relationship.
- Data flows from the new core banking system to the data warehouse, CRM, regulatory reporting layer, and mobile banking app are documented before any system build begins.
- Critical data elements — "Customer ID," "Account Balance," "Transaction Date" — are defined in the Business Glossary with system-of-record designations.
- An Architecture Review Gate is built into the SDLC: no system goes to build without a Data Architecture sign-off confirming it aligns with the EDM.

The migration completes with full data lineage documentation, reconciled customer records, and regulatory reports that pass BNM examination on first submission.

---

### Scenario 2 — Government/Public Sector: MyDigital Data Architecture

**The Failure (Without Chapter 4 Principles)**

A Malaysian government ministry launches a citizen services digitalisation initiative — creating separate digital portals for tax, health, identity verification, and social assistance. Each portal is built by a different vendor, on a different technology stack, with no shared data architecture.

Three years later:
- A citizen's identity number (MyKad IC) is stored in four different formats across the four systems — three of them incompatible with direct matching.
- Eligibility for social assistance cannot be verified automatically because the health, tax, and identity systems cannot exchange data reliably.
- A single citizen who has moved address must update their information in four separate government systems — none of which talk to each other.
- A national analytics initiative to model social assistance effectiveness cannot be built because there is no integrated view of citizen data.

**Root Cause (DMBOK2 lens):** No enterprise-level Data Architecture defined the standard for citizen identity, shared data elements, or system integration patterns before procurement began. Each system was designed within its own boundary — not as part of a coherent national data landscape.

---

**The Success (With Chapter 4 Principles)**

The Ministry commissions a National Data Architecture — led by MAMPU (Malaysian Administrative Modernisation and Management Planning Unit) in collaboration with MDEC — before any new system procurement:

- A National Enterprise Data Model is developed covering: Citizen, Organisation, Location, Transaction, Entitlement, and Event.
- MyKad IC number is standardised as the universal citizen identifier across all government systems — with a master citizen index maintained by the National Registration Department as the single system of record.
- Data integration standards are defined: all government systems must expose and consume citizen data via a standardised Government API Gateway.
- New system procurements require architectural compliance as a mandatory evaluation criterion.

The result: citizen data updated in one system propagates to all connected systems within 24 hours. Eligibility verification becomes automated. The national analytics platform has a coherent, integrated view of citizen data for policy modelling.

---

### Scenario 3 — Retail / E-Commerce: Data Architecture for Omnichannel

**The Failure (Without Chapter 4 Principles)**

A Malaysian retail conglomerate operates physical stores, an e-commerce platform, a mobile app, and a loyalty programme — each built at different times by different teams. No shared Data Architecture exists.

The consequences emerge when the group attempts to implement a single customer view:
- "Customer" is defined differently in each channel — the loyalty system uses member number, e-commerce uses email, the store POS uses phone number, and the app uses device ID. No universal customer identifier exists.
- Product data is maintained in four separate product catalogues with different category structures, attribute schemas, and pricing logic. A "product" in the store system may correspond to three different records in the e-commerce system.
- The Group CDO cannot produce a consolidated revenue-by-product report — the product hierarchies are incompatible.

**Root Cause (DMBOK2 lens):** Each channel's system was designed without reference to an enterprise subject area model. No universal identifiers were defined for Customer or Product. No integration architecture specified how customer and product data should flow between channels.

---

**The Success (With Chapter 4 Principles)**

A Data Architecture programme is established with four deliverables before any new system integration work begins:

1. **Enterprise Subject Area Model** — six subject areas: Customer, Product, Order, Store/Channel, Inventory, Finance. Approved by the DGC.
2. **Universal Identifier Framework** — a Group Customer ID is generated for every unique individual. A Group Product ID links all channel-specific product codes to a single enterprise product record. The National Registration Department's IC number is used as the citizen identity anchor where customers are Malaysian residents.
3. **Data Flow Map** — documents how customer and product data flows from each channel system to the enterprise data platform, with transformation rules and system-of-record designations.
4. **Integration Standards** — all new system integrations must use the standardised API and messaging formats defined in the Integration Architecture document.

Within 12 months: a single customer view is operational. The Group CDO produces the first-ever enterprise revenue-by-product report. Omnichannel loyalty integration — previously blocked — goes live.

---

## 4. Visual Diagrams, Cheat Sheet & Quick Reference

### Enterprise Architecture — Data Architecture Position

```
      BUSINESS STRATEGY
           │
           ▼
┌──────────────────────────────────────────────────────────────┐
│              ENTERPRISE ARCHITECTURE (EA)                     │
│                                                               │
│  ┌───────────────┐  ┌───────────────┐  ┌──────────────────┐  │
│  │   BUSINESS    │  │  APPLICATION  │  │   TECHNOLOGY     │  │
│  │ ARCHITECTURE  │  │ ARCHITECTURE  │  │ ARCHITECTURE     │  │
│  │               │  │               │  │                  │  │
│  │ Capabilities  │  │ Systems       │  │ Infrastructure   │  │
│  │ Processes     │  │ APIs          │  │ Cloud/On-prem    │  │
│  │ Functions     │  │ Integrations  │  │ Networks         │  │
│  └───────┬───────┘  └───────┬───────┘  └────────┬─────────┘  │
│          │                  │                   │            │
│          └──────────────────▼───────────────────┘            │
│                    ┌────────────────┐                         │
│                    │     DATA       │                         │
│                    │ ARCHITECTURE   │                         │
│                    │                │                         │
│                    │ EDM, Data      │                         │
│                    │ Flows, Subject │                         │
│                    │ Areas, Taxonomy│                         │
│                    └────────────────┘                         │
└──────────────────────────────────────────────────────────────┘
           │
           ▼
    SYSTEM IMPLEMENTATION
```

---

### Enterprise Data Model — Subject Area Structure

```
┌─────────────────────────────────────────────────────────────┐
│               ENTERPRISE DATA MODEL (EDM)                    │
│                   [Subject Area Level]                        │
├─────────────┬──────────────┬──────────────┬─────────────────┤
│   PARTY     │   PRODUCT    │    ORDER /   │   FINANCE       │
│             │              │  TRANSACTION │                 │
│  Customer   │  Item        │  Sale        │  Invoice        │
│  Employee   │  Service     │  Purchase    │  Payment        │
│  Vendor     │  Bundle      │  Transfer    │  Account        │
│  Partner    │  SKU         │  Event       │  GL Entry       │
├─────────────┴──────────────┴──────────────┴─────────────────┤
│   LOCATION  │  REFERENCE   │    RISK /    │   EMPLOYEE /    │
│             │   DATA       │  COMPLIANCE  │    HR           │
│  Geography  │  Code sets   │  Exposure    │  Role           │
│  Address    │  Taxonomies  │  Limit       │  Contract       │
│  Region     │  Standards   │  Incident    │  Payroll        │
└─────────────┴──────────────┴──────────────┴─────────────────┘

  Subject areas are BUSINESS-driven — not system-driven
  Each subject area has a named Data Steward/Owner
  Relationships between subject areas show integration points
```

---

### Data Flow — Simple Template

```
SOURCE SYSTEM          INTEGRATION LAYER         CONSUMPTION
┌──────────────┐       ┌─────────────────┐       ┌──────────────┐
│  CRM System  │──────▶│  ETL / API /    │──────▶│  Data        │
│  (Customer   │       │  Event Stream   │       │  Warehouse   │
│   records)   │       │                 │       │  (Analytics) │
└──────────────┘       │  Transformation │       └──────────────┘
                       │  rules applied  │
┌──────────────┐       │  Data quality   │       ┌──────────────┐
│  Core Banking│──────▶│  checks applied │──────▶│  Regulatory  │
│  (Account,   │       │                 │       │  Reporting   │
│   Balance)   │       │  Lineage        │       │  (BNM/SC)    │
└──────────────┘       │  documented     │       └──────────────┘
                       └─────────────────┘
                              │
                              ▼
                    DATA ARCHITECTURE GOVERNS:
                    • What data moves (subject areas)
                    • How it moves (integration standards)
                    • What transforms (business rules)
                    • Who owns each flow (system of record)
```

---

### Architecture Artefacts — Governed by Whom

```
┌────────────────────────────┬──────────────────┬───────────────────┐
│ Artefact                   │ Who Produces      │ Who Approves      │
├────────────────────────────┼──────────────────┼───────────────────┤
│ Enterprise Data Model      │ Data Architects   │ DGC + EA Board    │
│ Data Flow Diagrams         │ Data Architects   │ Data Owner + DGC  │
│ Subject Area Model         │ Data Architects   │ DGC               │
│ Data Taxonomy              │ Data Architects   │ DGC               │
│ Data Asset Inventory       │ Data Stewards     │ Data Owners       │
│ Integration Architecture   │ Integration Arch  │ EA Board + DGC    │
│ Data Standards (naming etc)│ Data Architects   │ DGC               │
└────────────────────────────┴──────────────────┴───────────────────┘
```

---

### Chapter 4 Quick-Reference Cheat Sheet

| Concept | Key Fact to Remember |
|---------|---------------------|
| Data Architecture definition | Blueprint for managing data assets; aligns organisational strategy with data design |
| Exam weight | 6% — lower weight but foundational to all other KAs |
| 4 EA domains | Business / Application / Technology / **Data** (Data Architecture is the data domain) |
| EA Frameworks | TOGAF (most common), Zachman (6×6 matrix), FEAF, DoDAF — DAMA references but does not mandate any |
| EDM purpose | High-level integrated view of enterprise data — subject areas and relationships, NOT detailed attributes |
| Subject area | Logical grouping of related data driven by business domains — not system boundaries |
| 3 architecture levels | Conceptual (EDM/subject areas) → Logical (entities/attributes) → Physical (tables/schemas) |
| Architecture vs Modeling | Architecture = strategic, enterprise, long-term. Modeling = tactical, project, detailed |
| 4 Data Architecture activities | Establish practice / Integrate with EA / Define architecture / Review and maintain |
| Key artefacts | EDM, Data Flow Diagrams, Data Taxonomy, Data Asset Inventory, Integration Architecture |
| Who approves the EDM | Data Governance Council (DGC) — it is a governance artefact, not just a technical one |
| Data flows document | How data moves from source → transformation → consumption, with lineage and system-of-record |
| Architecture precedes modeling | Enterprise Data Model must exist before detailed data models are built — sequencing rule |
| Malaysian context | BNM RMIT requires documented data/technology architecture for financial institutions; MyDIGITAL requires national data architecture standards |

---

## 5. Official DAMA Knowledge Area Visual Reference

> © DAMA International. Licensed under [CC BY-ND 4.0](https://creativecommons.org/licenses/by-nd/4.0/). Source: [dama.org/dmbok2r-infographics](https://dama.org/dmbok2r-infographics/).

### Data Architecture — KA Context Diagram

![Data Architecture — DMBOK2 Knowledge Area Context Diagram](https://growthzonecmsprodeastus.azureedge.net/sites/2326/2025/04/x-13.png)

---

*References: DAMA-DMBOK2 Revised Edition, Chapter 4 | BNM Risk Management in Technology (RMIT) 2020 | MDEC MyDIGITAL Framework | TOGAF — The Open Group Architecture Framework | Zachman Framework for Enterprise Architecture*

