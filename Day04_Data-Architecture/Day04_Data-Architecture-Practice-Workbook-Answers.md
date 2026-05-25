# Day 04 — Data Architecture Practice Workbook: Model Answers

**DAMA-DMBOK2 Chapter 4 | CDMP Exam Aligned**
**Study Plan:** Day 4 of 17 | Knowledge Area Weight: 6%
**Malaysian Context:** PDPA 2010, BNM RMIT 2020, MyDIGITAL Blueprint, GLC frameworks

---

> **How to use this file:**
> Each workbook question is answered at four levels:
> 1. **Model Answer** — exam-ready, concise, DAMA-precise
> 2. **Expanded Analysis** — deeper explanation with frameworks and nuance
> 3. **Malaysian Context** — localised scenario connecting to M'sian regulations and industries
> 4. **CDMP Exam Angle** — what the exam tests, common traps, key terms to remember

---

## Section 1: Business Drivers for Data Architecture

---

### Q1 — List three business goals that data architecture supports

**Model Answer:**

1. **Strategic Alignment** — Ensures that data assets, systems, and flows are structured to directly support the organisation's strategic objectives, enabling data to be used as a competitive differentiator rather than an operational burden.

2. **Operational Efficiency & Reduced Complexity** — A well-designed architecture eliminates data silos, redundant systems, and fragmented integration points, reducing the cost and time associated with data movement, transformation, and maintenance.

3. **Regulatory Compliance & Risk Reduction** — Architecture artefacts (data flows, subject area maps, lineage diagrams) provide the structural evidence needed to demonstrate compliance with data privacy laws, audit requirements, and regulatory mandates.

**Expanded Analysis:**

DAMA-DMBOK2 positions Data Architecture as the *blueprint for managing data assets*. It bridges business strategy and technical execution by translating business requirements into data structures, integration designs, and governance frameworks. The three goals above map directly to the DAMA context diagram inputs: business strategy drives architecture decisions, operational needs define integration requirements, and regulatory obligations constrain the design space.

A fourth commonly cited goal — **scalability and future-readiness** — ensures that the architecture can absorb new data volumes, new source systems, and emerging technology paradigms (cloud, AI, streaming) without requiring a complete redesign.

**Malaysian Context:**

In Malaysia's GLC environment, these three goals manifest as:

| Business Goal | Malaysian Example |
|---|---|
| Strategic Alignment | Maybank's M25+ strategy requires a unified customer data architecture spanning 9 ASEAN markets — architecture defines how customer data flows across borders while respecting each country's data sovereignty rules |
| Operational Efficiency | Telekom Malaysia consolidating 12+ legacy billing systems into a single Customer Data Hub — architecture reduces reconciliation effort from days to hours |
| Regulatory Compliance | BNM RMIT 2020 requires banks to document data lineage and demonstrate data quality at source — only possible with a governed architecture design |

Under PDPA 2010, data architecture decisions (where data is stored, how it moves, who accesses it) are not merely technical choices — they are compliance obligations. Architecture diagrams serve as evidence during PDPA audits.

**CDMP Exam Angle:**

- The exam may ask: *"Which activity is the primary purpose of Data Architecture?"* — The correct framing is **translating business strategy into data requirements** (not building databases or selecting technology).
- Know that Data Architecture is one of the four EA domains (Business / Application / Technology / **Data**) — TOGAF and Zachman are the named frameworks.
- Architecture supports governance by defining ownership, stewardship zones, and authoritative sources — this links Chapter 4 back to Chapter 3 (Data Governance).

---

### Q2 — Describe a situation where poor architecture increases complexity

**Model Answer:**

A retail bank runs separate Customer Relationship Management (CRM), loan origination, credit card, and mobile banking systems — each maintaining its own customer master record with different definitions of "customer ID," "address," and "account status." When regulatory reporting requires a 360° customer view, analysts must manually reconcile four systems with no canonical customer model, no published data lineage, and no single authoritative source. The result: regulatory reports take three weeks to produce, contain errors discovered only at audit, and the remediation effort consumes 40% of the data team's capacity.

**Expanded Analysis:**

This scenario illustrates several architectural failure modes simultaneously:

```
POOR ARCHITECTURE — Failure Cascade

  CRM System          Loan System         Card System        Mobile App
  ─────────────       ─────────────       ─────────────      ─────────────
  Cust_ID (GUID)      CustomerNo (INT)    CardHolder_ID      user_id (hash)
  Address_Line1       MailingAddress      BillingAddr        LastKnownAddr
  Status = "Active"   AcctStatus = "A"   CardStatus = "1"   [no status field]
       │                   │                   │                   │
       └───────────────────┴───────────────────┴───────────────────┘
                                     │
                         No integration layer
                         No canonical model
                         No authoritative source
                                     │
                               ▼ COMPLEXITY ▼
                    Manual reconciliation → errors → rework
                    Regulatory reporting delays → BNM findings
                    Customer duplicates → wrong credit decisions
```

This is precisely what DAMA Chapter 4 defines as the **technical debt accumulation** caused by ungoverned, point-to-point integration without an Enterprise Data Model (EDM). Each new system added to this environment multiplies the integration complexity exponentially (n×(n-1) integration points for n systems).

**Malaysian Context:**

This scenario is common in Malaysian financial institutions subject to BNM RMIT 2020. BNM's RMIT requires banks to demonstrate **data lineage**, **data accuracy at source**, and **end-to-end traceability** for all critical data elements (CDEs). A bank without a governed architecture cannot satisfy these requirements because:

- There is no defined authoritative source for customer data
- Data lineage cannot be traced when manual reconciliation replaces automated integration
- Quality controls cannot be applied consistently across four independent systems

CIMB's multi-market expansion across ASEAN is a real-world example where poor customer data architecture initially created complexity: different subsidiary systems used different customer keys, making group-level reporting difficult until a canonical customer model was established as part of their data transformation programme.

**CDMP Exam Angle:**

- The exam tests understanding of **why** architecture matters — frame your answer in terms of *data quality degradation*, *integration complexity*, and *governance failure*, not technology obsolescence.
- Key term: **spaghetti integration** — point-to-point connections without a canonical model or integration hub.
- Remember: architecture problems appear on the exam as governance problems. When you see "conflicting definitions," "no single source of truth," or "manual reconciliation" — the root cause is architectural.

---

## Section 2: Essential Concepts of Data Architecture

---

### Q3 — Define conceptual, logical, and physical models in your own words

**Model Answer:**

**Conceptual Model** — The highest-level representation of what the business cares about. It identifies the major subject areas (Customer, Product, Transaction, Party) and their relationships in business language, without any technical detail. The audience is business stakeholders and data governance leadership.

**Logical Model** — A technology-neutral, detailed specification of the data entities, attributes, and relationships that will support the business requirements. It includes data types, cardinality, business rules, and key constraints — but makes no reference to a specific database platform, storage format, or physical design. The audience is data architects, business analysts, and data stewards.

**Physical Model** — The implementation-specific design that translates the logical model into a format deployable on a specific technology platform (Oracle, SQL Server, Snowflake, Hadoop, etc.). It includes table names, column names, data types, indexes, partitioning strategies, and performance-oriented denormalization. The audience is database administrators, developers, and data engineers.

**Expanded Analysis:**

The three-level model hierarchy is a cornerstone of DAMA Chapter 4 and appears across multiple CDMP knowledge areas:

```
THREE-LEVEL DATA MODELLING HIERARCHY

  ┌─────────────────────────────────────────────┐
  │  CONCEPTUAL MODEL                           │
  │  "What does the business care about?"       │
  │                                             │
  │   [Customer] ────── [Product]               │
  │       │                 │                   │
  │   [Transaction] ─── [Channel]               │
  │                                             │
  │  Language: Business terms                   │
  │  Audience: Executives, Governance           │
  │  Detail:   Subject areas + relationships    │
  └──────────────────┬──────────────────────────┘
                     │ Refined into
  ┌──────────────────▼──────────────────────────┐
  │  LOGICAL MODEL                              │
  │  "What data entities and rules exist?"      │
  │                                             │
  │   Customer {CustomerID PK, Name, NRIC,      │
  │             DateOfBirth, Nationality}       │
  │   Account {AccountID PK, CustomerID FK,     │
  │            Type, OpenDate, Status}          │
  │                                             │
  │  Language: Business + technical neutral     │
  │  Audience: Architects, Analysts, Stewards   │
  │  Detail:   Entities, attributes, keys, rules│
  └──────────────────┬──────────────────────────┘
                     │ Implemented as
  ┌──────────────────▼──────────────────────────┐
  │  PHYSICAL MODEL                             │
  │  "How is data stored in THIS system?"       │
  │                                             │
  │   TABLE: tbl_cust_master (Oracle 19c)       │
  │   cust_id     NUMBER(10) NOT NULL PK        │
  │   full_name   VARCHAR2(200) NOT NULL        │
  │   ic_number   CHAR(12) UNIQUE               │
  │   INDEX: idx_cust_ic ON ic_number           │
  │   PARTITION: BY RANGE(open_date)            │
  │                                             │
  │  Language: Platform-specific SQL/DDL        │
  │  Audience: DBAs, Engineers                  │
  │  Detail:   Tables, columns, indexes, perf.  │
  └─────────────────────────────────────────────┘
```

The critical distinction for the exam: **logical models are technology-independent**. A logical model created today should remain valid regardless of whether the eventual implementation is a relational database, a document store, a data lake, or a graph database.

**Malaysian Context:**

In Malaysian financial services, these three levels appear in practice as:

- **Conceptual**: BNM requires banks to maintain a *Data Architecture Blueprint* showing major subject areas — this is the enterprise conceptual model, often presented to the Board Risk Committee as evidence of data governance maturity under RMIT.
- **Logical**: PDPA 2010 compliance requires banks to map personal data attributes to data subjects — this is logical modelling work (identifying entities like "Individual," "Consent," "Purpose of Processing").
- **Physical**: When Maybank migrated to a cloud-native data platform, physical models had to be redesigned for columnar storage (Snowflake/BigQuery) even though logical models remained unchanged — demonstrating the independence of the two levels.

**CDMP Exam Angle:**

- **Most common exam trap**: Confusing "logical" with "physical." The exam will describe a scenario with entities and attributes but no table names or database platform — that is a **logical** model, not physical.
- Remember the audience rule: if the document is for a business stakeholder → conceptual; for a data analyst or steward → logical; for a DBA or developer → physical.
- DAMA links these three levels to the **Data Modelling & Design** Knowledge Area (Chapter 5) — architecture defines the need, modelling executes the design.

---

### Q4 — Provide one example of a canonical structure

**Model Answer:**

A **Canonical Customer Model** in a financial institution defines a single, enterprise-wide standard representation of a "Customer" entity — including all attributes, their definitions, data types, valid values, and rules — that every system must conform to when sending or receiving customer data through the integration layer.

**Example — Canonical Customer Record:**

```
CANONICAL CUSTOMER MODEL (Enterprise Standard v2.1)
────────────────────────────────────────────────────
Entity: Customer

Attribute           Type        Rule / Source of Truth
────────────────────────────────────────────────────
customer_id         UUID        System-generated; unique globally
ic_number           CHAR(12)    Malaysian NRIC format: YYMMDD-SS-GGGG
full_name           VARCHAR(200) As per MyKad; no abbreviation permitted
date_of_birth       DATE        ISO 8601 (YYYY-MM-DD); derived from IC
nationality         CHAR(3)     ISO 3166-1 alpha-3 (MYS, SGP, GBR…)
resident_status     ENUM        RESIDENT / NON_RESIDENT / PR
primary_address     JSON        Structured per Pos Malaysia postcode standard
mobile_number       VARCHAR(15) E.164 format (+601X-XXXXXXX)
pdpa_consent_status ENUM        CONSENTED / WITHDRAWN / PENDING
consent_date        DATETIME    UTC timestamp of last consent event
────────────────────────────────────────────────────
Authoritative Source: Core Banking System (CBS)
Owner: Chief Data Officer
Governed by: Data Architecture Review Board
```

Every downstream system (CRM, mobile app, analytics, reporting) receives customer data in this canonical structure. Source systems that store data differently must translate to this canonical form at the integration layer — they do not force the canonical model to adapt to them.

**Expanded Analysis:**

The canonical data model is the architectural answer to the problem of semantic heterogeneity — where different systems use different terms, formats, or rules for the same real-world concept. Rather than building n×(n-1) point-to-point translations between systems, a canonical model creates a **hub** that all systems translate to and from. This pattern is fundamental to Enterprise Application Integration (EAI) and Service-Oriented Architecture (SOA).

```
WITHOUT CANONICAL MODEL          WITH CANONICAL MODEL
(n×(n-1) translations)           (n×2 translations)

CRM ←──→ Loan                    CRM ──→ Canonical
 ↕    ×   ↕                      Loan ──→ Canonical
Card ←──→ Mobile                 Card ──→ Canonical
                                 Mobile → Canonical
 6 translation mappings          4 translation mappings
 (grows quadratically)           (grows linearly)
```

**Malaysian Context:**

Under BNM RMIT 2020, Malaysian banks must designate **Critical Data Elements (CDEs)** and ensure their quality can be measured end-to-end. The canonical customer model is the mechanism by which CDEs are defined and enforced. For example, BNM's requirement that banks accurately identify a customer across all products (for single-borrower exposure limits under Basel II) is only enforceable if a canonical customer identifier exists and is consistently used.

MyDIGITAL's national data sharing framework similarly requires a canonical model for citizen data so that government agencies can exchange information on a common semantic basis — the same principle at the national level.

**CDMP Exam Angle:**

- Canonical model = **enterprise standard representation** used in integration — do not confuse with a physical database design.
- The exam may describe a scenario with multiple systems exchanging data in incompatible formats and ask what architectural artefact resolves this — the answer is a **canonical data model** (or **Enterprise Data Model at the integration layer**).
- Key relationship: canonical model → integration architecture → data quality → governance. All four are tested across different CDMP chapters.

---

## Section 3: Architecture Patterns & Styles

---

### Q5 — Compare a data warehouse vs. data lake

**Model Answer:**

| Dimension | Data Warehouse | Data Lake |
|---|---|---|
| **Data Structure** | Structured only; schema-on-write | Structured, semi-structured, and unstructured; schema-on-read |
| **Processing Model** | ETL (Extract → Transform → Load) | ELT (Extract → Load → Transform later) |
| **Schema Definition** | Defined before loading (schema-on-write) | Defined at query time (schema-on-read) |
| **Primary Users** | Business analysts, report consumers | Data scientists, ML engineers, exploratory analysts |
| **Query Pattern** | Predefined, repeating BI queries | Ad hoc, exploratory, machine learning |
| **Data Quality** | High; enforced at ingestion | Variable; raw data preserved as-is |
| **Latency** | Batch (hourly, daily) | Near real-time to batch depending on ingestion pipeline |
| **Cost Model** | High storage cost; optimised for query performance | Low storage cost; compute cost at query time |
| **Governance Maturity** | High; catalogued, lineaged, access-controlled | Often lower; risk of becoming a "data swamp" |
| **Examples** | Teradata, Oracle DW, Snowflake, Amazon Redshift | AWS S3 + Glue, Azure Data Lake Storage, Databricks Delta Lake |
| **DAMA Positioning** | Authoritative, governed reporting platform | Flexible, exploratory data environment |

**Expanded Analysis:**

DAMA-DMBOK2 recognises both patterns as valid architectural choices, appropriate for different use cases. The key architectural principle is **fitness for purpose**: a data warehouse is optimised for consistent, governed reporting; a data lake is optimised for flexibility, volume, and exploration.

The **data lakehouse** (popularised by Databricks and Delta Lake) is an emerging hybrid pattern that combines the low-cost storage and schema flexibility of a data lake with the ACID transactions, data quality enforcement, and governance capabilities of a data warehouse. This hybrid is increasingly relevant for organisations that need both governed BI reporting and data science capabilities from the same platform.

```
ARCHITECTURE PATTERN SPECTRUM

  Data Warehouse          Data Lakehouse           Data Lake
  ──────────────          ──────────────           ──────────
  High governance         Medium governance        Low governance
  Schema-on-write         ACID + flexible schema   Schema-on-read
  BI/Reporting            BI + Data Science        Data Science/ML
  Low flexibility         Medium flexibility       High flexibility
  High data quality       Enforced quality         Variable quality
  ETL                     ELT + quality layer      ELT (raw)
```

**Malaysian Context:**

In Malaysia's banking sector, a typical architecture separates the two:

- **Data Warehouse**: CIMB uses an enterprise data warehouse for regulatory reporting (BNM monthly submissions, BCBS 239 risk reports). All data is validated, reconciled, and lineaged before entering the warehouse. Auditability is paramount.

- **Data Lake**: Petronas operates a data lake to ingest IoT sensor data from oilfield equipment (unstructured telemetry, logs, maintenance records). Data scientists explore raw signals to build predictive maintenance models before any schema is imposed.

- **Malaysian Regulatory Implication**: BNM RMIT 2020 implicitly favours a data warehouse model for regulatory CDEs because it requires demonstrated data quality and lineage — characteristics of a governed warehouse. Data lakes used for regulatory reporting without quality controls risk BNM findings.

**CDMP Exam Angle:**

- The exam will present a scenario and ask which pattern is appropriate — focus on the **use case**: governed reporting → warehouse; exploratory/ML → lake; both → lakehouse.
- Key trap: a data lake is **not automatically better** because it stores more data. An ungoverned data lake becomes a "data swamp" — a common exam distractor.
- DAMA describes the data warehouse in the context of **Data Warehousing & Business Intelligence** (Chapter 11) and data lakes in the context of **Big Data & Data Science** (Chapter 14) — architecture spans both.

---

### Q6 — Identify when a company should choose data mesh

**Model Answer:**

A company should choose a **data mesh** architecture when all four of the following conditions are present:

1. **Scale of data domains**: The organisation has multiple distinct business domains (e.g., Finance, HR, Operations, Customer, Product) each producing significant volumes of data with domain-specific semantics.
2. **Centralisation bottleneck**: A centralised data team has become a bottleneck — domain teams are waiting months for data pipelines, transformations, or reports to be built by a central data engineering function.
3. **Domain ownership capability**: Domain teams have (or can develop) the technical capability to own, govern, and serve their own data as products.
4. **Federated governance readiness**: The organisation can implement federated governance — common standards and policies enforced consistently across autonomous domain teams — rather than requiring central control of all data.

**Expanded Analysis:**

Data mesh (popularised by Zhamak Dehghani, 2019) is a **socio-technical** architecture paradigm built on four principles:

```
DATA MESH — FOUR PRINCIPLES

  1. DOMAIN OWNERSHIP
     Each business domain owns its data end-to-end
     (ingestion → transformation → serving)
     ↓
  2. DATA AS A PRODUCT
     Domain data is served as a product with an SLA,
     schema contract, quality guarantees, and discoverability
     ↓
  3. SELF-SERVE DATA INFRASTRUCTURE
     A shared platform layer enables domain teams to
     build and serve data products without central engineering
     ↓
  4. FEDERATED COMPUTATIONAL GOVERNANCE
     Common standards (naming, classification, privacy, quality)
     are enforced programmatically across all domain products
```

Data mesh is **not** a replacement for all other patterns — it is appropriate specifically for large, complex, distributed organisations where centralised models create organisational rather than purely technical constraints.

**When NOT to choose data mesh:**

- Small organisations with a single data domain
- Early-stage data maturity (no domain data ownership culture)
- Regulatory environments requiring strict centralised data control (e.g., certain BNM reporting requirements)
- When the bottleneck is technical (bad tooling) rather than organisational (central team too small)

**Malaysian Context:**

Sime Darby, as a diversified conglomerate operating across plantations, motors, industrials, and healthcare, is a strong candidate for data mesh:

- Each division (e.g., Sime Darby Motors, Sime Darby Plantation) has distinct data domains with domain-specific semantics
- A centralised data team serving all divisions creates delays in analytics delivery for business-critical decisions
- Each division has operational data systems and analytics needs that differ fundamentally

The data mesh model would allow Sime Darby Motors to own and serve vehicle sales, service, and inventory data as domain products — while Sime Darby Plantation independently owns palm oil yield, weather, and plantation data products. Federated governance ensures that customer data definitions, PDPA compliance standards, and data quality thresholds are consistent across all domains.

**CDMP Exam Angle:**

- Data mesh is a DAMA-adjacent concept (it post-dates DMBOK2 first edition) — the exam may test it as an emerging architecture pattern under Chapter 4 or Chapter 14.
- The key differentiator: data mesh addresses **organisational bottlenecks**, not purely technical ones. If the exam scenario describes a central data team that cannot keep up with demand from multiple business units — that points to data mesh.
- Know the four principles by name — they are frequently tested in scenario-based questions.

---

## Section 4: Architecture Lifecycle (AS-IS → TO-BE → Gaps)

---

### Q7 — Document an AS-IS state for a system you know

**Model Answer — AS-IS: Malaysian Regional Bank Customer Data Environment**

**Organisation**: Mid-sized Malaysian bank (Tier-2, approximately RM 50B in assets)
**Scope**: Customer data management across retail banking operations

```
AS-IS STATE DOCUMENTATION
══════════════════════════════════════════════════════════════

SYSTEM LANDSCAPE (Current State)

  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐
  │  Core Banking│  │   CRM        │  │  Card Mgmt   │
  │  System (CBS)│  │  (Salesforce)│  │  System      │
  │  Oracle Fin. │  │  Cloud-based │  │  Legacy AS400 │
  └──────┬───────┘  └──────┬───────┘  └──────┬───────┘
         │                 │                  │
         │    Point-to-point integrations      │
         │    (batch files, manual uploads)    │
         └─────────────────┴──────────────────┘
                           │
                     No canonical model
                     No master data management
                     No data lineage tracking

DATA QUALITY ISSUES (Measured)
  - Customer duplicate rate: ~8% across CBS and CRM
  - Address match rate (CBS vs CRM): 63%
  - NRIC format standardisation: 41% compliant
  - Missing mobile number: 22% of records

INTEGRATION ARCHITECTURE
  - CBS → CRM: Nightly batch file (CSV), manual upload by IT
  - CRM → Card: No integration; card team re-keys customer data
  - Reporting: Analysts pull from 3 systems, reconcile in Excel

GOVERNANCE STATE
  - No designated data owner for Customer subject area
  - No data dictionary for customer attributes
  - No documented data lineage
  - PDPA consent records stored in a separate Access database

REGULATORY RISK
  - BNM RMIT assessment: Non-compliant (data lineage, CDE quality)
  - PDPA 2010: Unable to produce consent audit trail within 24 hours
  - BCBS 239: Single-borrower exposure calculation requires manual effort

══════════════════════════════════════════════════════════════
AS-IS Assessment: POOR — High operational risk, compliance exposure
```

**Expanded Analysis:**

DAMA Chapter 4 specifies that an AS-IS architecture assessment must document: current systems, integration patterns, data flows, data quality levels, governance maturity, and the regulatory/compliance posture. This holistic view is what distinguishes an architecture assessment from a simple system inventory — the AS-IS must capture not just *what exists* but *how well it works* and *what risks it creates*.

**Malaysian Context:**

This AS-IS scenario is representative of Malaysian Tier-2 banks that grew through acquisition or organic expansion without a data architecture strategy. BNM's RMIT 2020 enforcement has forced many such institutions into formal architecture programmes — making the AS-IS documentation exercise a regulatory necessity, not merely a good practice. Banks that cannot produce a documented AS-IS within 90 days of a BNM RMIT assessment typically receive a compliance finding with remediation timelines.

**CDMP Exam Angle:**

- AS-IS documentation is the foundation of the architecture lifecycle — the exam may ask what should be captured. Remember: **systems, integrations, data quality, governance, and compliance posture**.
- AS-IS is not a critique — it is an objective description. The gaps between AS-IS and TO-BE reveal the remediation roadmap.
- DAMA links AS-IS documentation to **Enterprise Architecture** practice — specifically Zachman's descriptive framework (What exists now, who owns it, how it works, when it runs, where it lives, why it exists).

---

### Q8 — List three gaps preventing achievement of a TO-BE state

**Model Answer — Three Gaps: Current Bank → Target State (Unified Customer Data Architecture)**

**TO-BE Vision**: A unified, governed customer master data environment with real-time integration, documented lineage, and BNM RMIT compliance.

**Gap 1 — No Canonical Customer Model (Semantic Gap)**

The AS-IS has four systems with different customer identifiers, attribute names, and format rules. The TO-BE requires a single canonical customer model with an enterprise customer ID as the golden record key. This gap cannot be closed by technology alone — it requires governance decisions about which system is the authoritative source, what the canonical attribute definitions are, and who owns the customer subject area.

**Gap 2 — Batch Integration Instead of Real-Time (Technical Gap)**

The AS-IS relies on nightly batch file transfers with manual steps. The TO-BE requires near-real-time customer data synchronisation across all systems via an API-based integration layer (Event-Driven Architecture or Enterprise Service Bus). This gap requires new integration infrastructure investment, API design, and change management across system owners.

**Gap 3 — No Data Lineage or Governance Artefacts (Governance Gap)**

The AS-IS has no data dictionary, no lineage documentation, and no designated data owners. The TO-BE requires full lineage traceability from source system to regulatory report — a BNM RMIT requirement. This gap requires establishing Data Architecture governance processes: a Data Architecture Review Board, a Data Dictionary as a managed artefact, and stewardship roles for the Customer subject area.

**Expanded Analysis — Gap Analysis Framework:**

```
GAP ANALYSIS STRUCTURE

  AS-IS State              GAP TYPE          TO-BE State
  ─────────────────────────────────────────────────────
  No canonical model    → Semantic Gap  → Enterprise canonical
                                          customer model (v1.0)

  Nightly batch only    → Technical Gap → Real-time API
                                          integration layer

  No lineage/governance → Governance Gap→ Data Dictionary +
                                          lineage + stewards

  ─────────────────────────────────────────────────────
  Gap Priority: Governance Gap > Semantic Gap > Technical Gap
  (Cannot build technology on an unresolved semantic gap)
```

The sequencing is critical: governance gaps must be addressed before semantic gaps, and semantic gaps (canonical model) must be resolved before technical gaps (integration layer). Building a real-time integration layer before the canonical model is agreed creates a fast-moving, well-integrated system that shares bad data efficiently — making the problem worse.

**Malaysian Context:**

For Malaysian banks under BNM RMIT 2020, these three gap types translate to specific RMIT risk management outcomes:

- **Semantic Gap** → RMIT Principle 3 (Data Architecture): Banks must document data flows and subject area definitions for all CDEs.
- **Technical Gap** → RMIT Principle 4 (Data Quality): Real-time data synchronisation is a prerequisite for measuring CDE quality at point of use.
- **Governance Gap** → RMIT Principle 2 (Data Governance): Data lineage and ownership documentation is explicitly required.

BNM typically sequences remediation in the same order — governance structure first, semantic standards second, technical implementation third.

**CDMP Exam Angle:**

- Know the three gap types: **semantic, technical, governance** — the exam may use different labels but tests the same concept.
- The exam tests sequencing: governance gaps must be resolved before technical implementation. A scenario that describes a bank building new integration infrastructure without resolving ownership disputes is demonstrating the wrong sequence.
- Gap analysis feeds directly into the **Architecture Roadmap** — the output of the lifecycle that prioritises initiatives by impact and dependency.

---

## Section 5: Organisational Enablement & Cultural Change

---

### Q9 — Explain how training supports architecture adoption

**Model Answer:**

Training builds the shared vocabulary, conceptual understanding, and skills that allow stakeholders across the organisation to participate meaningfully in architecture decisions, comply with architecture standards, and maintain architecture artefacts over time.

Without training:
- Business stakeholders cannot engage with architecture artefacts (they don't know what a subject area or canonical model is)
- Technical teams implement systems without reference to the enterprise architecture (they don't know it exists or why it matters)
- Data stewards cannot fulfil their role in maintaining the data dictionary (they don't know what a steward does or how to update an artefact)

With targeted training, architecture becomes a shared organisational capability rather than the exclusive knowledge of a small architecture team.

**Expanded Analysis — Training by Audience:**

```
TRAINING PROGRAMME DESIGN FOR ARCHITECTURE ADOPTION

  Audience              Content                      Outcome
  ─────────────────────────────────────────────────────────────
  Executive/Board       Why architecture matters;    Sponsorship &
                        risk of poor architecture;   budget approval
                        BNM RMIT compliance link

  Business Leaders      What subject areas are;      Demand for
                        how to read a conceptual     architecture
                        model; governance roles      participation

  Data Stewards         How to maintain the Data     Artefact quality
                        Dictionary; what a           and currency
                        canonical attribute is;
                        how to log issues

  Developers/           Canonical model standards;   Compliance with
  Engineers             integration layer usage;     architecture
                        physical model conventions   standards

  Data Analysts         How to use lineage docs;     Trusted data
                        what authoritative sources   consumption
                        are; how to request changes
```

DAMA-DMBOK2 connects training to **Organisational Change Management (OCM)** — specifically the ADKAR model (Awareness → Desire → Knowledge → Ability → Reinforcement). Training addresses the "Knowledge" and "Ability" phases of ADKAR, but must be preceded by Awareness (why change is needed) and Desire (personal motivation to participate). Training without Awareness is ineffective because learners don't know why the content matters.

**Malaysian Context:**

In Malaysian GLCs, architecture adoption training faces a specific cultural challenge: **hierarchical deference**. Staff may understand and even agree with architectural standards privately, but will not challenge a senior leader's decision to bypass the canonical model for a pet project. Training must therefore include not just technical content but also governance escalation pathways — how to raise an architectural concern through the Data Governance Council without career risk.

Petronas' Group Data Management programme explicitly includes "Data Leadership" training for senior managers — recognising that architecture adoption requires leadership behaviour change, not just technical skill-building.

**CDMP Exam Angle:**

- Training is part of the **OCM** component of Data Architecture implementation — DAMA positions it alongside communication, sponsorship, and feedback mechanisms.
- The exam may ask what the primary barrier to architecture adoption is — common answers include lack of executive sponsorship, unclear data ownership, or competing priorities. Training alone does not resolve these.
- Connect training to the **ADKAR model** (from Chapter 3, Data Governance OCM) — it applies equally to architecture adoption.

---

### Q10 — Describe communication methods that reduce resistance

**Model Answer:**

Effective communication methods that reduce resistance to architecture adoption include:

1. **Use-case storytelling** — Frame architecture in terms of business pain points it resolves (e.g., "This canonical model will reduce your month-end reconciliation from 3 days to 3 hours"). Business stakeholders respond to outcomes, not technical abstractions.

2. **Executive briefings with regulatory framing** — Presenting architecture decisions to senior leadership in the context of BNM RMIT or PDPA compliance converts a "nice to have" into a "must do." Regulatory risk creates urgency that technical arguments do not.

3. **Visible quick wins** — Identify one high-impact, fast-deliverable architecture improvement and publicise the business result (e.g., first canonical customer model deployed → duplicate rate drops from 8% to 1.2% → announce this result in a cross-departmental newsletter). Demonstrated value reduces scepticism.

4. **Architecture Review Board as a collaborative forum** — When architecture decisions are made transparently in a forum where business and technical stakeholders participate, resistance decreases because stakeholders feel heard. Contrast with architecture mandates imposed without consultation, which generate compliance resistance.

5. **Two-way feedback channels** — Provide mechanisms for technical teams to flag where architecture standards create impractical constraints, with a defined process for standard exceptions. Resistance often comes from standards that do not accommodate legitimate edge cases.

**Expanded Analysis:**

DAMA-DMBOK2 identifies resistance as a natural response to change — not a sign of bad faith. The root causes of architecture resistance typically fall into four categories:

```
RESISTANCE ROOT CAUSES & COMMUNICATION RESPONSES

  Root Cause               Communication Response
  ──────────────────────────────────────────────────────────
  "I don't understand      Plain-language executive summary;
  why we need this"        one-page business case; visual
                           diagrams not technical specs

  "This adds work          Show total cost of non-compliance
  without benefit"         vs. total cost of architecture work;
                           calculate hours saved post-adoption

  "My team wasn't          Architecture Review Board; stakeholder
  consulted"               consultation phase before standards
                           are finalised; retrospective feedback

  "We've tried this        Reference a successful prior
  before and it failed"    architecture initiative (internal or
                           peer institution); show what's
                           different this time

  "I'll lose control       Clarify the governance model: domain
  of my data"              teams retain ownership; architecture
                           sets standards, not control
```

**Malaysian Context:**

In Malaysian corporate culture, resistance to architecture change often manifests as **passive non-compliance** — teams formally agree to architecture standards in governance forums but continue building systems that bypass them. This is particularly common in organisations with strong siloed divisional cultures (GLCs with legacy business unit autonomy).

Effective communication in this context requires:
- Visible C-suite endorsement (CDO or CIO actively sponsoring the architecture programme in town halls)
- Linking architecture compliance to performance review metrics (which requires HR partnership)
- Creating champions within each business unit who act as internal advocates for the architecture

Maybank's data transformation programme successfully reduced resistance by embedding data architects within each business unit for the first 12 months — enabling face-to-face trust-building rather than top-down mandate communication.

**CDMP Exam Angle:**

- Communication is part of the **OCM toolkit** — the exam may ask what should happen *before* technical implementation begins. Answer: stakeholder communication and change management.
- Know the ADKAR sequence: **Awareness → Desire → Knowledge → Ability → Reinforcement**. Communication addresses Awareness and Desire; training addresses Knowledge and Ability; performance management addresses Reinforcement.
- A common exam scenario: "An architecture programme has strong technical design but stakeholders are not adopting the standards. What is the primary missing element?" Answer: **communication and change management** (not better technology, not more training).

---

## Section 6: Case Study Practice

---

### Case 1 — Five customer systems with mismatched fields. What model should you define?

**Scenario:** A firm has five customer systems: a CRM (Salesforce), a loan origination system (LOS), a card management system (CMS), a mobile banking app, and a digital onboarding portal. Each system stores customer data with different field names, formats, and identifier schemes. Analysts cannot produce a unified customer view without manual reconciliation.

---

**Model Answer:**

Define an **Enterprise Canonical Customer Model** — a governed, enterprise-wide standard specification for the "Customer" subject area that all five systems must conform to when exchanging customer data.

This canonical model must be implemented as the semantic contract at the **integration layer** — each source system translates its internal customer representation to the canonical form before sending data, and translates from canonical form when receiving. No source system is required to change its internal data structure; transformation happens at the boundary.

---

**Expanded Answer — What to Define:**

**Step 1 — Establish the Customer Subject Area**

Define "Customer" as a formal subject area within the Enterprise Data Model (EDM). A subject area groups all entities, attributes, and relationships related to a single business concept. For this firm, the Customer subject area includes: Individual Customer, Organisation Customer, Customer Account Relationship, Customer Contact, Customer Consent.

**Step 2 — Define the Canonical Customer Model**

```
ENTERPRISE CANONICAL CUSTOMER MODEL v1.0
══════════════════════════════════════════════════════════════

Entity: CUSTOMER (root entity — all systems)

  Attribute                 Type      Format               Rule
  ──────────────────────────────────────────────────────────────
  enterprise_customer_id    UUID      System-generated     PK; unique globally
  ic_number                 CHAR(12)  YYMMDD-SS-GGGG       Malaysian NRIC; validated
  passport_number           VARCHAR   ISO                  If non-citizen; exclusive with IC
  full_legal_name           VARCHAR   As per MyKad         No abbreviation
  date_of_birth             DATE      YYYY-MM-DD           Derived from IC where possible
  nationality               CHAR(3)   ISO 3166-1 alpha-3
  resident_status           ENUM      RESIDENT/PR/FOREIGN
  primary_mobile            VARCHAR   E.164 format         +60XX-XXXXXXX
  primary_email             VARCHAR   RFC 5322
  pdpa_consent_status       ENUM      CONSENTED/WITHDRAWN
  consent_timestamp         DATETIME  UTC ISO 8601
  authoritative_source_id   VARCHAR   System code (CBS/CRM/LOS)
  golden_record_flag        BOOLEAN   TRUE = master record

Entity: CUSTOMER_SYSTEM_XREF (cross-reference)

  enterprise_customer_id  →  FK to CUSTOMER
  source_system_code      →  'CRM', 'LOS', 'CMS', 'MOBILE', 'ONBOARD'
  source_customer_id      →  system-native identifier
  source_last_updated     →  DATETIME UTC

══════════════════════════════════════════════════════════════
```

**Step 3 — Designate the Authoritative Source**

Declare the Core Banking System (or closest equivalent) as the **System of Record** for the enterprise_customer_id and IC number. All other systems defer to this source for identity resolution. This is a governance decision, not a technical one — it requires sign-off from the Data Governance Council and documented in the Data Architecture artefacts.

**Step 4 — Implement the Integration Hub**

```
INTEGRATION ARCHITECTURE (Hub-and-Spoke with Canonical Model)

  ┌──────────────┐                      ┌──────────────┐
  │   Salesforce │ ──transform──→        │  Enterprise  │
  │   CRM        │               │       │  Integration │
  └──────────────┘               ├──────►│  Hub         │
  ┌──────────────┐               │       │  (Canonical  │
  │ Loan Orig.   │ ──transform──→┤       │   Customer   │
  │ System       │               │       │   Model)     │
  └──────────────┘               ├──────►│              │
  ┌──────────────┐               │       └──────┬───────┘
  │ Card Mgmt    │ ──transform──→┤              │
  │ System       │               │       ┌──────▼───────┐
  └──────────────┘               ├──────►│  Customer    │
  ┌──────────────┐               │       │  Golden      │
  │ Mobile App   │ ──transform──→┤       │  Record      │
  └──────────────┘               │       │  (MDM Hub)   │
  ┌──────────────┐               │       └──────────────┘
  │ Digital      │ ──transform──→┘
  │ Onboarding   │
  └──────────────┘
```

**Malaysian Context:**

Under PDPA 2010, this firm must be able to respond to a Data Subject Access Request (DSAR) within a reasonable time — which requires producing all personal data held about a customer across all five systems. Without a canonical customer model and cross-reference table, this is impossible to do reliably. The canonical model is therefore not only an architectural best practice but a PDPA compliance mechanism.

Under BNM RMIT, the enterprise_customer_id enables single-borrower exposure calculation across the loan and card systems — a critical risk management requirement that cannot be met with five mismatched identifier schemes.

**CDMP Exam Angle:**

- The question tests knowledge of **canonical data model** and **Enterprise Data Model (EDM)** — both are Chapter 4 concepts.
- The exam may present this as a multiple-choice: "What is the FIRST step when five systems have conflicting customer definitions?" The answer is **establish a canonical data model** — not build a new database, not implement MDM software (the tool follows the model, not the reverse).
- Know the relationship: Subject Area (conceptual) → Canonical Model (logical) → MDM Hub (physical implementation).

---

### Case 2 — A bank needs real-time fraud detection. What architecture pattern applies?

**Scenario:** A Malaysian bank processes 2 million card transactions daily. The fraud operations team currently reviews flagged transactions using end-of-day batch reports — by which time fraudulent transactions have already been settled. The bank needs to detect and block fraud within milliseconds of transaction initiation.

---

**Model Answer:**

The appropriate architecture pattern is **Event-Driven Architecture (EDA)** with a **Lambda Architecture** or **Kappa Architecture** variant, implementing a **real-time streaming pipeline** using technologies such as Apache Kafka (event streaming), Apache Flink or Spark Streaming (real-time processing), and a feature store (fraud model feature serving).

The core pattern: every transaction event is published to a streaming platform the moment it occurs → real-time fraud scoring rules and ML models are applied within the streaming layer → a decision (approve / flag / block) is returned to the payment system before transaction settlement.

---

**Expanded Answer — Architecture Pattern Design:**

```
REAL-TIME FRAUD DETECTION ARCHITECTURE
══════════════════════════════════════════════════════════════

LAYER 1: EVENT GENERATION
  ┌────────────────────────────────────────────────────────┐
  │  Transaction Sources                                   │
  │  POS Terminal │ ATM │ Online Banking │ Mobile App      │
  └─────────────────────────┬──────────────────────────────┘
                            │ Transaction event (JSON)
                            │ {txn_id, card_id, amount,
                            │  merchant, timestamp, location}
                            ▼

LAYER 2: EVENT STREAMING (Apache Kafka / AWS Kinesis)
  ┌────────────────────────────────────────────────────────┐
  │  Event Stream: transactions_raw                        │
  │  Partitioned by card_id for ordering guarantees        │
  │  Retention: 7 days for replay capability               │
  └─────────────────────────┬──────────────────────────────┘
                            │
              ┌─────────────┴──────────────┐
              │                            │
              ▼                            ▼
LAYER 3a: SPEED LAYER             LAYER 3b: BATCH LAYER
(Real-time, <100ms)               (Historical, daily)
  Apache Flink / Spark              Spark on HDFS / S3
  Streaming                         Scheduled batch jobs
  ├─ Rule-based scoring             ├─ ML model training
  │  (velocity, geo-anomaly,        ├─ Feature engineering
  │   merchant blacklist)           └─ Performance reporting
  └─ ML model inference
     (pre-trained, low-latency)
              │
              ▼
LAYER 4: FRAUD DECISION SERVICE
  ┌────────────────────────────────────────────────────────┐
  │  Decision Engine                                       │
  │  APPROVE (score < 0.3) → pass to payment gateway      │
  │  REVIEW  (0.3–0.7)     → soft block + alert analyst   │
  │  BLOCK   (score > 0.7) → decline + alert customer     │
  └─────────────────────────┬──────────────────────────────┘
                            │ Decision returned in <200ms
                            ▼
LAYER 5: PAYMENT GATEWAY (existing)
  Transaction approved or declined in real time

══════════════════════════════════════════════════════════════
PATTERN TYPE: Lambda Architecture
  - Speed Layer: real-time streaming decisions
  - Batch Layer: model retraining and performance analytics
  - Serving Layer: unified fraud case management dashboard

ALTERNATIVELY — KAPPA ARCHITECTURE (simpler):
  Eliminate the batch layer; use the streaming layer for all
  processing including historical reprocessing (via Kafka replay)
  Preferred when: lower operational complexity is prioritised
  over maximum analytical flexibility
```

**Architecture Pattern Summary:**

| Dimension | Lambda Architecture | Kappa Architecture |
|---|---|---|
| Layers | Speed + Batch + Serving | Streaming only |
| Complexity | Higher (two processing stacks) | Lower (one stack) |
| Historical reprocessing | Batch layer handles | Kafka replay |
| Use when | Need separate batch and real-time | Can unify all processing |
| For fraud detection | Suitable if model training is batch | Suitable if streaming covers all |

**Malaysian Context:**

BNM's requirements for financial institutions include transaction monitoring and suspicious transaction reporting (STR) to Bank Negara under the Anti-Money Laundering Act (AMLA). Real-time fraud detection architecture directly supports AMLA compliance — suspicious transactions can be flagged and escalated to compliance officers within seconds rather than the next business day.

Maybank's MAE (Maybank Anytime Everywhere) digital platform handles millions of transactions daily. The fraud detection architecture deployed must handle the latency constraints of mobile payment UX (a blocked transaction must receive a response within 2 seconds for acceptable user experience) while meeting BNM's STR requirements.

The event-driven pattern also supports PDPA 2010 data minimisation principles — transaction events carry only the fields needed for fraud scoring, not full personal profiles, reducing personal data exposure within the streaming pipeline.

**CDMP Exam Angle:**

- The exam tests **architecture pattern selection by use case** — real-time processing → Event-Driven Architecture / Streaming.
- Know the contrast: **batch architecture** is unsuitable for millisecond-latency decisions. The exam may present a scenario where a batch approach is described as solving a real-time problem — that is a wrong answer.
- Key terms: **Lambda Architecture** (speed + batch + serving layers), **Kappa Architecture** (streaming only), **Event-Driven Architecture** (EDA), **streaming platform** (Kafka/Kinesis).
- The fraud detection case also connects to **Data Security** (Chapter 7) and **Data Quality** (Chapter 13) — architecture does not exist in isolation from other DAMA KAs.

---

## Summary Table — All Workbook Questions

| Section | Question | Key Answer Concept | DAMA Chapter Link |
|---|---|---|---|
| Business Drivers | 3 business goals | Strategic alignment, Efficiency, Compliance | Ch.4 Architecture Purpose |
| Business Drivers | Poor architecture complexity | Spaghetti integration, no canonical model | Ch.4 Architecture Value |
| Essential Concepts | 3 model levels | Conceptual / Logical / Physical hierarchy | Ch.4 + Ch.5 Data Modelling |
| Essential Concepts | Canonical structure | Enterprise Canonical Customer Model | Ch.4 Integration Architecture |
| Patterns & Styles | Warehouse vs Lake | Schema-on-write vs Schema-on-read; ETL vs ELT | Ch.4 + Ch.11 + Ch.14 |
| Patterns & Styles | Data mesh conditions | Domain scale + Centralisation bottleneck + Domain capability + Federated governance | Ch.4 Emerging Patterns |
| Lifecycle | AS-IS documentation | Systems + integrations + DQ + governance + compliance | Ch.4 Architecture Lifecycle |
| Lifecycle | 3 gaps to TO-BE | Semantic gap, Technical gap, Governance gap | Ch.4 Gap Analysis |
| Org. Enablement | Training adoption | ADKAR K + A phases; audience-specific content | Ch.4 OCM + Ch.3 ADKAR |
| Org. Enablement | Communication methods | Storytelling, quick wins, ARB forum, 2-way feedback | Ch.4 OCM Communication |
| Case Study 1 | 5 mismatched systems | Enterprise Canonical Customer Model + MDM hub | Ch.4 EDM + Integration |
| Case Study 2 | Real-time fraud | Event-Driven + Lambda/Kappa Architecture | Ch.4 + Ch.14 Streaming |

---

## CDMP Quick-Reference — Chapter 4 Exam Signals

| If the exam scenario says… | The answer involves… |
|---|---|
| "Different systems use different definitions" | Canonical data model / Enterprise Data Model |
| "Business strategy → data requirements" | Data Architecture as translation function |
| "No single source of truth" | Authoritative source designation + MDM |
| "Governed reporting, predefined queries" | Data Warehouse |
| "Exploratory analysis, ML, raw data" | Data Lake |
| "Multiple domains, central team bottleneck" | Data Mesh |
| "What is documented first in the lifecycle?" | AS-IS state |
| "Real-time processing, millisecond latency" | Event-Driven / Streaming Architecture |
| "Architecture artefact for business audience" | Conceptual model / Subject area map |
| "Platform-specific design with indexes" | Physical data model |
| "Resistance to new architecture standards" | OCM + Communication + ADKAR |

---

*Day 04 Supplementary File | DAMA-DMBOK2 Chapter 4 | CDMP Exam Preparation*
*Malaysian Context: PDPA 2010 (Act 709) | BNM RMIT 2020 | MyDIGITAL Blueprint*
*Prepared as part of 17-Day CDMP Study Programme*
