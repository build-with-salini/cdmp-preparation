# Day 05 — Data Modelling & Design
## DAMA-DMBOK2 Chapter 5 | CDMP Exam Weight: ~11%

**Study Plan:** Day 5 of 17 | One of the highest-weighted chapters on the CDMP exam
**Malaysian Context:** PDPA 2010, BNM RMIT 2020, MyDIGITAL Blueprint, GLC data platforms
**Connections:** Feeds directly into Chapter 4 (Architecture), Chapter 6 (Storage), Chapter 10 (Metadata), Chapter 13 (Quality)

---

## Section 1: Core Summary — What Is Data Modelling & Why It Matters

Data modelling is the process of discovering, analysing, and representing data requirements in a precise, visual form called a **data model**. DAMA-DMBOK2 positions the data model as the most important artefact in data management after the data itself — it is the shared language through which business requirements are translated into structured data designs, and through which those designs are governed over time.

### DAMA Definition

DAMA defines Data Modelling & Design as: *"the process of discovering, analysing, representing, and communicating data requirements in a precise form called the data model."* A data model documents what an organisation knows about its data — the entities, attributes, relationships, constraints, and rules that define how data reflects the real world.

The central tension in data modelling is balancing **precision** (technical correctness, implementability) with **comprehensibility** (business stakeholders must be able to validate the model reflects their needs). A technically perfect model that business stakeholders cannot read will embed the wrong business rules into the data structure — a form of technical debt that compounds over years.

### Why Data Modelling Matters for the CDMP Exam

Chapter 5 carries approximately **11% of exam weight** — tied for the highest-weighted single chapter alongside Data Governance and Data Quality. The exam tests conceptual understanding of model levels and types, the ability to identify the right model for a given scenario, normalisation principles, dimensional modelling patterns, and model governance. Every scenario question that describes a database design, a reporting structure, or a data integration problem draws on Chapter 5.

### The Three Core Contributions of Data Modelling

**Formalising business rules** — A data model captures business rules in structured form. The rule "a customer must have exactly one primary address" becomes a cardinality constraint. The rule "a product can belong to multiple categories" becomes a many-to-many relationship. Without this formalisation, rules exist only in people's heads and are inconsistently implemented across systems.

**Creating a shared vocabulary** — The entity names, attribute names, and relationship names in a data model become the organisation's agreed terminology for its data. When the model is maintained as a living artefact connected to a business glossary, it bridges the semantic gap between business and technical teams.

**Enabling data quality management** — A data model defines what is valid: the data types, value ranges, referential integrity constraints, and business rules that separate correct data from incorrect data. Without a model, there is no objective basis for measuring or enforcing data quality.

---

## Section 2: DAMA Framework View — Activities, Inputs, Outputs, Roles

### 2.1 Data Modelling Activities (DAMA Chapter 5)

DAMA defines five primary activities for Data Modelling & Design:

**Activity 1 — Plan Data Modelling**
Define the scope, audience, notation standard, tooling, and governance process for the modelling effort. Determine which model level is required (conceptual, logical, physical) and who will review and approve the model. Without planning, modelling efforts produce artefacts that no one maintains.

**Activity 2 — Build the Data Model**
Execute the modelling work: discover data requirements through interviews and document analysis; represent entities, attributes, relationships, and constraints using the chosen notation; validate with business stakeholders; and iterate. This is the core creative and analytical work of the data modeller.

**Activity 3 — Review the Data Model**
Conduct formal quality reviews against defined criteria: completeness (all required entities and attributes present), correctness (accurate reflection of business rules), consistency (no contradictions within the model or with other models), comprehensibility (diagrams are readable and definitions are clear), and precision (appropriate level of detail for the model level).

**Activity 4 — Maintain the Data Model**
Keep the model current as business requirements, regulatory obligations, and systems change. An unmaintained model becomes misleading — it describes a system that no longer exists and omits systems that do. Model maintenance requires governance processes: change requests, version control, review cycles, and model owner accountability.

**Activity 5 — Integrate with Data Governance**
Link data model artefacts to the business glossary, data dictionary, data lineage documentation, and data quality rules. A data model is not a standalone document — it is a hub in the broader data governance ecosystem.

### 2.2 Model Levels — The Three-Level Hierarchy

```
DATA MODEL LEVELS — DAMA FRAMEWORK

  ┌─────────────────────────────────────────────────────────┐
  │  CONCEPTUAL DATA MODEL (CDM)                            │
  │                                                         │
  │  Purpose:  Represent the business view of data          │
  │  Audience: Business leaders, governance, executives     │
  │  Content:  Subject areas + high-level relationships     │
  │  Detail:   No attributes; no technical constraints      │
  │  Format:   Entity-Relationship diagram (high-level)     │
  │                                                         │
  │  Example:  CUSTOMER ──places──► ORDER                   │
  │            ORDER ──contains──► PRODUCT                  │
  └──────────────────────┬──────────────────────────────────┘
                         │ Decomposed into
  ┌──────────────────────▼──────────────────────────────────┐
  │  LOGICAL DATA MODEL (LDM)                               │
  │                                                         │
  │  Purpose:  Define data requirements in detail           │
  │  Audience: Data architects, analysts, stewards          │
  │  Content:  Entities, all attributes, PK/FK, rules       │
  │  Detail:   Data types (logical); business rules;        │
  │            cardinality; normalisation                   │
  │  Format:   ERD with full attribute list                 │
  │                                                         │
  │  Example:  Customer {CustID PK, ICNumber UNIQUE,        │
  │            Name NOT NULL, DOB, Nationality}             │
  │            Order {OrderID PK, CustID FK, OrderDate,     │
  │            TotalAmount, Status}                         │
  └──────────────────────┬──────────────────────────────────┘
                         │ Implemented as
  ┌──────────────────────▼──────────────────────────────────┐
  │  PHYSICAL DATA MODEL (PDM)                              │
  │                                                         │
  │  Purpose:  Define actual database implementation        │
  │  Audience: DBAs, developers, data engineers             │
  │  Content:  Tables, columns, indexes, partitions,        │
  │            storage parameters, denormalisation          │
  │  Detail:   Platform-specific; performance-optimised     │
  │  Format:   DDL-ready schema diagram                     │
  │                                                         │
  │  Example:  TABLE tbl_customer (Oracle 19c)              │
  │            cust_id     NUMBER(10) PK,                   │
  │            ic_number   CHAR(12) UNIQUE NOT NULL,        │
  │            INDEX idx_cust_ic ON ic_number               │
  │            PARTITION BY RANGE (registration_date)       │
  └─────────────────────────────────────────────────────────┘
```

### 2.3 Data Model Types

DAMA recognises six primary data model types, each suited to different data structures and use cases:

| Model Type | Best For | Key Characteristic | CDMP Signal |
|---|---|---|---|
| **Relational** | Transactional systems, OLTP | Entities, attributes, normalised tables | Most common type; highest exam frequency |
| **Dimensional** | Reporting, analytics, OLAP | Facts + dimensions; star/snowflake schema | Chapter 11 (DW&BI) link |
| **Object-Oriented** | OOP systems, complex inheritance | Classes, methods, inheritance hierarchies | Less common on exam |
| **Fact-Based (FBM)** | Knowledge representation | Facts as first-class citizens; no nulls | Niche; know the name |
| **Time-Based** | Temporal data, audit trails | Bitemporal modelling; valid time vs transaction time | Increasingly tested |
| **NoSQL / Document** | Unstructured, semi-structured | JSON, graph, columnar, key-value schemas | Chapter 6 Storage link |

### 2.4 Normalisation — The Relational Model Foundation

Normalisation is the process of structuring a relational data model to reduce redundancy and improve data integrity. DAMA and the CDMP exam test understanding of the first four normal forms:

```
NORMALISATION LEVELS — EXAM REFERENCE

  UNNORMALISED (0NF)
  ──────────────────
  Repeating groups exist; data can be duplicated
  e.g., Customer row contains: Phone1, Phone2, Phone3

  ↓ Remove repeating groups

  FIRST NORMAL FORM (1NF)
  ───────────────────────
  All attributes are atomic (no repeating groups)
  Each row is uniquely identifiable by a primary key
  e.g., Separate PhoneNumber table, linked by CustID

  ↓ Remove partial dependencies

  SECOND NORMAL FORM (2NF)
  ────────────────────────
  In 1NF + every non-key attribute fully depends on
  the ENTIRE primary key (no partial dependencies)
  Applies only when PK is composite
  e.g., OrderItem table: OrderID + ProductID = PK
        ProductName depends only on ProductID → move to Product table

  ↓ Remove transitive dependencies

  THIRD NORMAL FORM (3NF)
  ───────────────────────
  In 2NF + no non-key attribute depends on another
  non-key attribute (no transitive dependencies)
  e.g., Customer(CustID, PostCode, City, State)
        City and State depend on PostCode, not CustID
        → Move to PostCode reference table

  ↓ Remove all remaining functional dependencies

  BOYCE-CODD NORMAL FORM (BCNF)
  ──────────────────────────────
  Every determinant is a candidate key
  Stricter than 3NF; handles anomalies 3NF misses
  e.g., If multiple overlapping candidate keys exist
```

**Denormalisation**: The deliberate reversal of normalisation for performance reasons. Physical models for reporting systems often denormalise (pre-join tables, add redundant columns) to reduce query execution time. Denormalisation is a physical model decision — logical models should be normalised to 3NF or BCNF.

### 2.5 Dimensional Modelling

Dimensional modelling is the dominant design pattern for data warehouses and analytical systems. It was developed by Ralph Kimball and is structured around **fact tables** and **dimension tables**.

```
DIMENSIONAL MODEL — STAR SCHEMA EXAMPLE
(Retail Sales Analytics)

         ┌──────────────┐
         │  DIM_DATE    │
         │  DateKey PK  │
         │  Year        │
         │  Quarter     │
         │  Month       │
         │  Day         │
         └──────┬───────┘
                │
┌───────────┐   │   ┌────────────────────────┐
│ DIM_STORE │   │   │     FACT_SALES          │
│ StoreKey  │   │   │  (Grain: 1 row per      │
│ StoreName │───┼───│   transaction line)     │
│ Region    │   │   │                         │
│ State     │   │   │  DateKey FK             │
└───────────┘   │   │  StoreKey FK            │
                │   │  ProductKey FK          │
         ┌──────┘   │  CustomerKey FK         │
         │          │  SalesAmount MEASURE    │
┌────────┴──────┐   │  Quantity MEASURE       │
│  DIM_PRODUCT  │   │  DiscountAmount MEASURE │
│  ProductKey   │───┘                         │
│  ProductName  │   └────────────────────────┘
│  Category     │
│  Brand        │
└───────────────┘

STAR SCHEMA: Fact table directly joined to dimension tables
SNOWFLAKE:   Dimension tables further normalised (sub-dimensions)
             e.g., DIM_PRODUCT → DIM_CATEGORY (separate table)
```

**Key Dimensional Concepts for the CDMP Exam:**

- **Grain**: The lowest level of detail captured in a fact table — must be declared explicitly ("one row per daily store transaction" vs "one row per product sold per transaction"). Wrong grain causes double-counting and incorrect aggregations.
- **Additive measures**: Sum correctly across all dimensions (e.g., Sales Amount). Can be summed by date, by store, by product simultaneously.
- **Semi-additive measures**: Sum correctly across some dimensions (e.g., Account Balance can be summed by account but not by time — you cannot add Monday's balance to Tuesday's balance).
- **Non-additive measures**: Cannot be summed (e.g., Ratio, Percentage, Margin %). Must be recalculated.
- **Slowly Changing Dimensions (SCD)**: How to handle changes to dimension attributes over time.

### 2.6 Slowly Changing Dimensions (SCD) — A Critical Exam Topic

```
SCD TYPES — EXAM REFERENCE

  Scenario: Customer Sarah moves from KL to Penang.
  How does the dimension table handle this?

  SCD TYPE 1 — Overwrite (No History)
  ─────────────────────────────────────
  Simply update the record. Previous value lost.
  CustomerKey | Name  | City
  1001        | Sarah | Penang  ← KL history gone

  Use when: History is irrelevant or wrong data is corrected

  SCD TYPE 2 — Add New Row (Full History)
  ─────────────────────────────────────────
  Insert a new row; mark previous row as expired.
  CustomerKey | Name  | City    | StartDate  | EndDate    | Current
  1001        | Sarah | KL      | 2020-01-01 | 2024-06-30 | N
  1002        | Sarah | Penang  | 2024-07-01 | 9999-12-31 | Y

  Use when: Historical analysis requires knowing the
  attribute value at the time of the transaction

  SCD TYPE 3 — Add New Column (Limited History)
  ───────────────────────────────────────────────
  Add a "Previous" column alongside "Current."
  CustomerKey | Name  | CurrentCity | PreviousCity
  1001        | Sarah | Penang      | KL

  Use when: Only one prior value matters;
  not more than one historical state needed
```

### 2.7 Forward and Reverse Engineering

**Forward Engineering** (Model → Database): Generating DDL (Data Definition Language) SQL from a physical data model. The model is the source of truth; the database is derived from it. This is the correct direction in a governed environment.

**Reverse Engineering** (Database → Model): Extracting a data model from an existing database by reading its schema, constraints, and relationships. Used to document legacy systems where no model artefact exists. The resulting model is an AS-IS description, not a validated design.

### 2.8 Inputs, Outputs, Roles

| Element | Detail |
|---|---|
| **Inputs** | Business requirements, existing models, metadata, data quality rules, regulatory requirements |
| **Outputs** | Conceptual model, logical model, physical model, data dictionary, model metadata |
| **Roles** | Data Architect (designs), Data Modeller (executes), Business Analyst (requirements), Data Steward (validates), DBA (physical implementation) |
| **Tools** | ER/Studio, erwin Data Modeler, PowerDesigner, Lucidchart, draw.io, dbdiagram.io |
| **Governance** | Model Review Board, version control (e.g., Git for DDL), change management process |

---

## Section 3: Real-World Scenarios — Malaysian Context

### Scenario 1: Maybank Customer Onboarding — Logical Model for PDPA Compliance

**Business Context:**
Maybank's digital onboarding team is building a new e-KYC (electronic Know Your Customer) platform for retail banking. The platform must capture personal data, link it to PDPA 2010 consent records, and satisfy BNM's CDD (Customer Due Diligence) requirements under AMLA.

**The Modelling Challenge:**
The team's first attempt was a single "Customer" table with 60+ columns, including fields for consent status, address, occupation, and source of funds — all crammed into one flat structure with no referential integrity. Analysts were finding records with consent_status = "Y" but no corresponding consent_date. The model violated 3NF because PostalCity and PostalState depended on PostalCode, not on CustomerID.

**Data Modeller's Response:**

Step 1 — Normalise to 3NF: Decompose the flat Customer table into Customer (identity), CustomerAddress (separately keyed), CustomerContact (phone + email), and PostalArea (PostCode → City, State lookup).

Step 2 — Model the consent relationship separately: Create a ConsentRecord entity linked to Customer with a foreign key, capturing consent_type (Marketing/DataSharing/CreditCheck), consent_status, consent_timestamp, consent_channel (branch/online/mobile), and withdrawal_timestamp. This models the PDPA 2010 requirement that consent must be specific, informed, and withdrawable — and that withdrawal must be recorded.

Step 3 — Declare authoritative source: The e-KYC platform is designated the System of Record for consent data. All downstream systems query consent status from this source — they do not maintain their own consent fields.

**CDMP Link:** This scenario tests normalisation (3NF), entity decomposition, and the modelling of regulatory requirements. It also demonstrates that data modelling is a governance activity — the model encodes the rules.

---

### Scenario 2: Petronas Retail — Dimensional Model for Sales Analytics

**Business Context:**
Petronas Dagangan (the retail fuel arm) operates over 900 petrol stations across Malaysia. The analytics team needs a data warehouse to analyse daily sales by station, product type (RON95, RON97, diesel, lubricants), time period, and region for both performance reporting and pricing strategy.

**The Modelling Challenge:**
The source OLTP system has 47 normalised tables with complex joins. Analysts spend hours writing queries with 15-table joins. Reports run for 45 minutes and frequently time out. The team needs a dimensional model optimised for analytics.

**Data Modeller's Response:**

Star Schema Design:
- **FACT_STATION_SALES** — Grain: one row per product sold per transaction per day. Measures: SalesVolumeLiters (additive), SalesAmountMYR (additive), DiscountAmount (additive), BasePrice (non-additive — recalculate). Foreign keys to all dimension tables.
- **DIM_STATION** — StationKey, StationCode, StationName, Region, State, StationClass (Full/Self-service), Operator.
- **DIM_PRODUCT** — ProductKey, ProductCode, ProductName, FuelType, RonRating, ProductCategory.
- **DIM_DATE** — DateKey, FullDate, Year, Quarter, Month, WeekOfYear, DayName, IsWeekend, IsPublicHoliday.
- **DIM_CUSTOMER** — For loyalty members (Mesra card): CustomerKey, MemberTier, RegistrationDate. Non-members use a default "Anonymous" row.

**SCD Decision:** DIM_STATION uses SCD Type 2 to capture station class changes (when a station upgrades from self-service to full-service, historical sales should reflect the old classification for accurate like-for-like analysis).

**Result:** Average report query time drops from 45 minutes to under 2 seconds. Pricing analysts can slice fuel volume by region × product × day in real-time, informing RON95 pricing strategy submissions to the government.

**CDMP Link:** This scenario tests star schema design, grain declaration, additive vs non-additive measures, and SCD selection. A common exam question: "Which SCD type preserves full historical analysis capability?" — Type 2.

---

### Scenario 3: LHDN (Inland Revenue Board) — Enterprise Data Model for Tax Administration

**Business Context:**
LHDN administers income tax, corporate tax, and GST/SST for the Malaysian federal government. Data flows across 14 source systems (e-Filing, MyInvois, employer returns, customs integration, bank reporting). The MyDIGITAL initiative requires LHDN to establish a unified taxpayer data model that supports cross-agency data sharing with JPJ (road transport), JPN (national registration), and SSM (companies commission).

**The Modelling Challenge:**
Each of LHDN's 14 systems defines "Taxpayer" differently. Individual taxpayer in e-Filing is keyed by NRIC; in employer submissions, by Employment Registration Number; in the property tax system, by land title. A taxpayer can appear under three different identifiers with no cross-reference. Cross-system analytics are impossible. MyDIGITAL data sharing requires a common semantic model that government agencies can exchange.

**Data Modeller's Response:**

Step 1 — Subject Area Model (Conceptual): Define five subject areas: Taxpayer (Individual + Corporate), Tax Assessment, Payment, Audit & Enforcement, Cross-Agency Reference. These subject areas are validated with LHDN's Chief Data Officer and presented to the MyDIGITAL interoperability working group.

Step 2 — Enterprise Logical Model: Within the Taxpayer subject area, define: Taxpayer (root entity with TaxpayerID as enterprise golden key), Individual (subtype with NRIC, MyKad name, DOB), LegalEntity (subtype with SSM registration number, company type), TaxpayerIdentifier (cross-reference table linking enterprise TaxpayerID to all source system IDs).

Step 3 — Canonical Exchange Model: Define a canonical Taxpayer message structure for cross-agency data sharing — the format LHDN uses when responding to queries from JPJ or JPN. This canonical model is published as an API contract.

**PDPA 2010 / MyDIGITAL Link:** Cross-agency data sharing of personal tax data requires explicit legal basis under PDPA 2010 Section 6 (data processing conditions). The logical model captures the legal basis attribute on every data sharing transaction — ensuring compliance is modelled, not assumed.

**CDMP Link:** This scenario tests enterprise data modelling, subject area decomposition, subtype/supertype relationships, canonical modelling, and the governance role of a data model in cross-organisation data sharing.

---

## Section 4: Visual Diagrams + Cheat Sheet

### 4.1 Relational Model — Entity Notation Reference

```
ERD NOTATION — CROW'S FOOT (most common in practice and on exam)

  Cardinality Notation:
  ─────────────────────
  ─|   One (exactly one)
  ─|<  One or many
  ─○   Zero (optional)
  ─○<  Zero or many
  ─||  One and only one (mandatory)

  Example: Customer to Order relationship

  CUSTOMER                    ORDER
  ──────────────              ──────────────
  CustomerID PK ──||────○<── CustomerID FK
  Name                        OrderID PK
  Email                       OrderDate
  PhoneNo                     TotalAmount

  Reading: "One Customer places zero or many Orders"
           "Each Order belongs to one and only one Customer"

  PRODUCT                     ORDER_LINE
  ──────────────              ───────────────────
  ProductID PK  ──||────○<── ProductID FK (PK)
  ProductName                 OrderID FK (PK)
  UnitPrice                   Quantity
                              UnitPrice (at time of sale)

  ORDER_LINE is a JUNCTION TABLE resolving the
  many-to-many between Order and Product.
  The composite PK (ProductID + OrderID) ensures
  a product appears at most once per order.
```

### 4.2 Subtype / Supertype Pattern

```
SUPERTYPE / SUBTYPE — GENERALISATION HIERARCHY

  Used when: Multiple entity types share common attributes
  but have type-specific attributes

              ┌──────────────────┐
              │    TAXPAYER      │  ← Supertype
              │  TaxpayerID PK   │    (common attributes)
              │  TaxRefNumber    │
              │  RegistrationDate│
              │  Status          │
              └────────┬─────────┘
                       │ IS-A relationship
              ┌────────┴─────────┐
              │                  │
  ┌───────────▼──────┐  ┌────────▼──────────┐
  │   INDIVIDUAL     │  │   LEGAL_ENTITY     │  ← Subtypes
  │  TaxpayerID FK   │  │  TaxpayerID FK     │    (type-specific)
  │  ICNumber        │  │  SSMRegNumber      │
  │  FullLegalName   │  │  CompanyName       │
  │  DateOfBirth     │  │  IncorporationDate │
  │  Nationality     │  │  CompanyType       │
  └──────────────────┘  └────────────────────┘

  Key rules:
  - Every subtype instance IS ALSO a Supertype instance
  - Subtypes can be EXCLUSIVE (instance belongs to one subtype)
    or INCLUSIVE (instance can belong to multiple subtypes)
  - Supertype holds all common attributes; subtypes hold only
    type-specific attributes
```

### 4.3 Data Model Quality Dimensions

```
DATA MODEL QUALITY — FIVE DIMENSIONS (DAMA Ch. 5)

  ┌────────────────────────────────────────────────────────┐
  │  COMPLETENESS                                          │
  │  All required entities, attributes, and relationships  │
  │  are present. No business concept is unrepresented.   │
  │  Test: Can every business question be answered from   │
  │        the model without adding new entities?          │
  └────────────────────────────────────────────────────────┘
  ┌────────────────────────────────────────────────────────┐
  │  CORRECTNESS                                           │
  │  Business rules are accurately encoded. Cardinality   │
  │  constraints match real business rules. Attribute     │
  │  definitions match actual meanings.                   │
  │  Test: Would a subject matter expert validate every   │
  │        relationship and constraint as accurate?        │
  └────────────────────────────────────────────────────────┘
  ┌────────────────────────────────────────────────────────┐
  │  CONSISTENCY                                           │
  │  No contradictions within the model or between        │
  │  this model and other enterprise models.              │
  │  Same entity named and defined the same way           │
  │  across all models in the enterprise.                 │
  └────────────────────────────────────────────────────────┘
  ┌────────────────────────────────────────────────────────┐
  │  COMPREHENSIBILITY                                     │
  │  Diagrams are readable. Definitions are clear.        │
  │  Naming conventions are applied consistently.         │
  │  The target audience can understand the model         │
  │  without a data modeller present to explain it.       │
  └────────────────────────────────────────────────────────┘
  ┌────────────────────────────────────────────────────────┐
  │  PRECISION                                             │
  │  The model is at the right level of detail for its   │
  │  purpose. Conceptual models are not cluttered with    │
  │  physical detail. Physical models include all         │
  │  implementation specifics needed by the DBA.          │
  └────────────────────────────────────────────────────────┘
```

### 4.4 Model Type Selection Guide

```
CHOOSING THE RIGHT DATA MODEL TYPE

  Is the data primarily TRANSACTIONAL?
  (CRUD: Create, Read, Update, Delete)
         │
         ├── YES → RELATIONAL MODEL (3NF)
         │         Entities, attributes, normalised tables
         │         Tools: Oracle, SQL Server, PostgreSQL
         │
         └── NO
              │
              Is the primary use ANALYTICAL / REPORTING?
              │
              ├── YES → DIMENSIONAL MODEL (Star/Snowflake)
              │         Facts + Dimensions; denormalised
              │         Tools: Snowflake, Redshift, BigQuery
              │
              └── NO
                   │
                   Is the data TEMPORAL / AUDIT-HEAVY?
                   │
                   ├── YES → TIME-BASED MODEL
                   │         Bitemporal; valid time + transaction time
                   │         Used for: financial records, regulatory audit
                   │
                   └── NO
                        │
                        Is the data DOCUMENT / GRAPH / KEY-VALUE?
                        │
                        └── YES → NoSQL SCHEMA DESIGN
                                  JSON, graph, columnar based on
                                  access pattern, not normalisation
```

### 4.5 Cheat Sheet — Chapter 5 Key Terms

| Term | One-Line Definition | Exam Trap |
|---|---|---|
| **Conceptual Model** | Business-level view; subject areas; no attributes | Not a high-level logical model — no attributes at all |
| **Logical Model** | Technology-neutral; full entities + attributes + rules | Must be independent of any physical platform |
| **Physical Model** | Platform-specific implementation; tables, indexes, DDL | Denormalisation here is valid; not in logical |
| **Entity** | A category of things about which data is collected | Must be uniquely identifiable (has a PK) |
| **Attribute** | A property of an entity | Must be atomic (1NF) |
| **Primary Key (PK)** | Unique identifier for each entity instance | Candidate key chosen as the primary identifier |
| **Foreign Key (FK)** | Attribute referencing a PK in another entity | Enforces referential integrity |
| **Cardinality** | The numeric relationship between entity instances | One-to-one, one-to-many, many-to-many |
| **1NF** | Atomic attributes; no repeating groups | First and most fundamental normalisation step |
| **2NF** | No partial dependencies (composite PK only) | Only relevant when PK is composite |
| **3NF** | No transitive dependencies | Most common target for OLTP design |
| **BCNF** | Every determinant is a candidate key | Stricter than 3NF; not always required |
| **Fact Table** | Central table in dimensional model; stores measures | Contains FK to all dimensions + numeric measures |
| **Dimension Table** | Descriptive context for facts | Denormalised for query performance |
| **Grain** | Lowest level of detail in a fact table | Must be declared explicitly; wrong grain → wrong answers |
| **SCD Type 1** | Overwrite; no history | Use for corrections, not for business history |
| **SCD Type 2** | New row; full history | Default for dimensions that change over time |
| **SCD Type 3** | New column; limited history | Use when only one prior state matters |
| **Forward Engineering** | Model → Database (DDL generation) | Correct direction in governed environments |
| **Reverse Engineering** | Database → Model (from existing schema) | Documents AS-IS; not a design activity |
| **Canonical Model** | Enterprise-standard representation used in integration | Resolves semantic heterogeneity; not a physical design |
| **Subtype/Supertype** | Generalisation hierarchy for entity types | Supertype holds common attributes; subtypes hold type-specific |

### 4.6 CDMP Exam Traps — Chapter 5

```
COMMON EXAM TRAPS — DATA MODELLING & DESIGN

  TRAP 1: Confusing model levels
  ────────────────────────────────
  The exam describes a diagram with entities, attributes,
  and cardinality but no table names or database platform.
  → This is a LOGICAL model (not physical)

  TRAP 2: Normalisation scope
  ────────────────────────────
  "Which normal form removes transitive dependencies?"
  → 3NF (not 2NF, which removes partial dependencies)
  Remember: 2NF = partial; 3NF = transitive

  TRAP 3: Additive vs Non-additive
  ─────────────────────────────────
  "A measure representing average transaction value
  should be summed to produce totals."
  → FALSE — averages are non-additive; must be recalculated

  TRAP 4: SCD Type purpose
  ──────────────────────────
  "To preserve full history of dimension changes, use:"
  → SCD Type 2 (not Type 3, which only keeps one prior value)

  TRAP 5: Data model vs Data dictionary
  ───────────────────────────────────────
  A data model shows relationships between entities.
  A data dictionary defines what each attribute means.
  The exam may ask which artefact answers "What does
  this field mean?" → Data dictionary (or business glossary)

  TRAP 6: Grain and double-counting
  ───────────────────────────────────
  A fact table with grain "one row per day per store" will
  produce WRONG results if you try to calculate individual
  transaction counts from it — the grain is too coarse.
  Always match the grain to the analytical question.
```

---

## Section 5: Official DAMA Images

### DAMA Data Modelling & Design Knowledge Area Context Diagram

*Source: DAMA International, DAMA-DMBOK2 Knowledge Area Context Diagram Series*
*License: Creative Commons CC BY-ND 4.0 | © DAMA International*

![DAMA Data Modelling & Design KA Context Diagram](https://dama.org/wp-content/uploads/sites/2326/2025/04/x-10.png.webp)

> **Reading the context diagram:** The Data Modelling & Design KA sits within the DAMA Wheel as one of the 10 surrounding Knowledge Areas. Its inputs include business requirements and existing models; its outputs feed into Data Storage & Operations (physical implementation), Metadata Management (data dictionary), and Data Governance (model governance). Note how Data Architecture (Chapter 4) is an upstream KA — architecture defines the blueprint that modelling elaborates.

*Note: If the image above does not render, refer to Day01 Section 5 which contains the full DAMA KA gallery including the Data Modelling & Design context diagram.*

---

## Chapter 5 at a Glance — One-Page Summary

```
DATA MODELLING & DESIGN — CDMP EXAM SUMMARY
══════════════════════════════════════════════════════════════

WHAT:   The process of discovering, analysing, representing,
        and communicating data requirements in precise form

WHY:    Formalises business rules; creates shared vocabulary;
        enables data quality measurement and enforcement

LEVELS:
  Conceptual → Subject areas; business language; no attributes
  Logical    → Entities, attributes, keys, rules; tech-neutral
  Physical   → Tables, columns, indexes; platform-specific

TYPES:
  Relational    → OLTP; normalised; 3NF target
  Dimensional   → OLAP; star/snowflake; facts + dimensions
  Time-Based    → Bitemporal; audit + historical analysis
  NoSQL         → Document/graph/columnar; access-pattern driven

NORMALISATION:
  1NF → Atomic attributes; no repeating groups
  2NF → No partial dependencies (composite PK)
  3NF → No transitive dependencies (OLTP target)
  BCNF → Every determinant is a candidate key

DIMENSIONAL KEY CONCEPTS:
  Grain → Lowest level of detail (must declare explicitly)
  Facts → Numeric measures (additive/semi/non-additive)
  Dims  → Descriptive context (SCD Type 1/2/3)
  Star  → Fact + denormalised dimensions (fast queries)
  Snow  → Fact + normalised dimensions (space efficient)

QUALITY DIMENSIONS:
  Completeness | Correctness | Consistency
  Comprehensibility | Precision

ACTIVITIES: Plan → Build → Review → Maintain → Govern

EXAM WEIGHT: ~11% — One of the highest-weighted chapters
══════════════════════════════════════════════════════════════
```

---

*Day 05 | DAMA-DMBOK2 Chapter 5 — Data Modelling & Design*
*CDMP Exam Preparation | 17-Day Study Programme*
*Malaysian Context: PDPA 2010 | BNM RMIT 2020 | MyDIGITAL Blueprint*
*Next: Day 06 — Data Storage & Operations (Chapter 6)*

