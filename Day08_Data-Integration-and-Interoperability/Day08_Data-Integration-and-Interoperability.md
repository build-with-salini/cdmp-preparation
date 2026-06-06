# Day 08 — Data Integration & Interoperability
## DAMA-DMBOK2 Chapter 8 | CDMP Exam Weight: ~6%

**Study Plan:** Day 8 of 17 | Bridges operational systems and analytical platforms
**Malaysian Context:** MyDIGITAL Blueprint, BNM RMIT data flow documentation, PDPA cross-border transfer, national API standards (MDEC), OpenAPI Malaysia
**Connections:** Builds on Chapter 4 (Architecture) | Depends on Chapter 5 (canonical model) | Feeds Chapter 11 (DW&BI) and Chapter 14 (Big Data)

---

## Section 1: Core Summary — What Is Data Integration & Interoperability

Data Integration is the process of consolidating data from multiple source systems into a unified, consistent, and usable form. Data Interoperability is the capability of different systems and organisations to exchange and make use of information, sharing a common understanding of what that information means. Together, they represent the plumbing and the semantics of an enterprise data landscape — the technical pipes through which data moves, and the agreements that ensure what arrives at the destination means the same thing as what left the source.

### DAMA Definition

DAMA-DMBOK2 defines Data Integration & Interoperability as: *"processes related to the movement and consolidation of data within and between data stores, applications, and organisations."* The emphasis on both movement (technical) and consolidation (semantic) reflects that integration is not complete when data arrives at its destination — it is complete only when that data can be understood and used correctly.

### Why This Chapter Matters for the CDMP Exam

Chapter 8 carries approximately **6% of exam weight**. The exam tests: knowledge of the primary integration approaches (ETL, ELT, CDC, virtualisation, API, event streaming) and when each is appropriate; understanding of integration architecture patterns and their trade-offs; the concept of data latency and how different integration approaches achieve different latency profiles; and the governance requirements for managing integrations (interface catalogues, API governance, data lineage through integration layers). This chapter is highly practical — almost every enterprise data problem involves integration.

### Three Core Business Drivers

**Enabling cross-system analytics** — No organisation's data lives in one system. Customer data is in the CRM. Transactions are in core banking. Products are in the ERP. Regulatory reporting requires a consolidated view across all three. Data integration is what makes cross-system analytics possible — without it, every report requires manual extract-and-reconcile.

**Reducing operational friction** — When systems cannot share data in real time, operational processes require manual re-entry, phone calls, and email chains to synchronise information. A loan application that requires a branch officer to manually key customer data from the CRM into the loan system (because the two are not integrated) wastes time, introduces errors, and creates a poor customer experience.

**Meeting regulatory data requirements** — BNM RMIT 2020 requires Malaysian banks to document data flows and demonstrate data lineage from source to regulatory report. PDPA 2010 requires data controllers to know where personal data flows, including to third-party processors and across borders. Both obligations are fundamentally integration governance requirements — they cannot be met without a managed, documented integration architecture.

---

## Section 2: DAMA Framework View — Approaches, Patterns, Governance

### 2.1 Integration Approaches — The Technology Options

```
INTEGRATION APPROACH SELECTION MAP

  What is the DATA LATENCY requirement?
  │
  ├─ HOURS / DAILY (Batch acceptable)
  │       │
  │       ├─ Transform BEFORE loading?
  │       │      → ETL (Extract → Transform → Load)
  │       │        Traditional; staging area; data warehouse
  │       │
  │       └─ Load raw THEN transform?
  │              → ELT (Extract → Load → Transform)
  │                Cloud-native; data lake first; transform in-place
  │
  ├─ MINUTES (Near real-time / Micro-batch)
  │       → MICRO-BATCH STREAMING
  │         Apache Spark Streaming (configurable batch intervals)
  │         AWS Glue incremental runs
  │
  ├─ SECONDS (Near real-time / Low latency)
  │       → CDC (Change Data Capture)
  │         Capture only CHANGED records from source DB
  │         Tools: Debezium, Oracle GoldenGate, AWS DMS
  │         Method: Database log-based (most efficient) or
  │                 trigger-based / timestamp-based
  │
  ├─ MILLISECONDS (Real-time / Event-driven)
  │       → EVENT STREAMING
  │         Apache Kafka, AWS Kinesis, Azure Event Hubs
  │         Publish-subscribe; consumer groups; event replay
  │         Use for: fraud detection, IoT, real-time dashboards
  │
  └─ ON-DEMAND (No movement / Query-time)
          → DATA VIRTUALISATION / FEDERATION
            Query source systems directly at query time
            No data movement; always fresh
            Trade-off: Source system load; network latency
```

### 2.2 ETL vs ELT — The Fundamental Shift

```
ETL vs ELT — DETAILED COMPARISON

  ETL (Traditional — Pre-Cloud Era)
  ────────────────────────────────────────────────────────
  EXTRACT   → Pull data from source systems
  TRANSFORM → Clean, standardise, reshape in a STAGING AREA
              (separate server between source and target)
  LOAD      → Load clean, transformed data into target DW

  Strengths:
  • Data warehouse always contains clean, governed data
  • Transformation logic is explicit and auditable
  • Target system protected from raw data quality issues

  Weaknesses:
  • Staging area is expensive infrastructure
  • Long transformation time = high latency
  • Schema must be defined before loading (schema-on-write)
  • Difficult to reprocess historical data if rules change

  Best for: Traditional on-premise data warehouses
            Governed BI reporting environments
            BNM regulatory reporting (predictable, clean)

  ────────────────────────────────────────────────────────

  ELT (Modern — Cloud-Native Era)
  ────────────────────────────────────────────────────────
  EXTRACT   → Pull data from source systems
  LOAD      → Load RAW data directly into cloud data lake/DW
              (schema-on-read; transform later)
  TRANSFORM → Transform in-place using cloud compute power
              (dbt, Spark, BigQuery SQL, Snowflake SQL)

  Strengths:
  • Raw data preserved — can re-transform with new rules
  • No staging area infrastructure needed
  • Cloud compute scales elastically for transformation
  • Schema flexibility: load now, define schema later

  Weaknesses:
  • Raw data in warehouse may contain quality issues
  • Transformation logic spread across many tools
  • Governance of raw → transformed layers requires discipline

  Best for: Cloud data platforms (Snowflake, BigQuery, Redshift)
            Data lakes and lakehouses
            Data science workloads requiring raw data access
            MyDIGITAL cloud-first data platform initiatives

  ────────────────────────────────────────────────────────
  KEY INSIGHT FOR EXAM:
  ETL = Transform BEFORE loading (staging area)
  ELT = Load raw THEN transform (in the target platform)
```

### 2.3 Change Data Capture (CDC) — Efficient Near-Real-Time Integration

CDC is a pattern for identifying and capturing only the data that has changed since the last extraction, rather than extracting the full dataset every time. This dramatically reduces data movement volume and enables near-real-time integration.

```
CDC METHODS — THREE APPROACHES

  LOG-BASED CDC (Best practice — most efficient)
  ─────────────────────────────────────────────────────
  Reads the database transaction log (write-ahead log / redo log)
  to capture INSERT, UPDATE, and DELETE events as they occur.
  The source database is not queried — no performance impact.
  Tools: Debezium (open source), Oracle GoldenGate, AWS DMS,
         Microsoft SQL Server CDC

  Flow:
  Source DB → Transaction Log → CDC Tool → Message Queue → Target

  TIMESTAMP-BASED CDC (Simple — limited)
  ─────────────────────────────────────────────────────
  Query source table for rows where LAST_UPDATED_AT > last run time.
  Simple to implement; no special tools required.
  Limitation: Cannot detect DELETE operations (deleted rows have no timestamp).
  Only works if tables have reliable updated_at columns.

  TRIGGER-BASED CDC (Legacy — avoid)
  ─────────────────────────────────────────────────────
  Database triggers fire on INSERT/UPDATE/DELETE and write
  change records to an audit table.
  Limitation: Adds overhead to every write operation on source.
  Performance impact on high-throughput OLTP systems.

  CDC CAPTURE — WHAT IT CATCHES:
  ─────────────────────────────────────────────────────
  Log-based:        INSERT ✓   UPDATE ✓   DELETE ✓
  Timestamp-based:  INSERT ✓   UPDATE ✓   DELETE ✗
  Trigger-based:    INSERT ✓   UPDATE ✓   DELETE ✓ (with impact)
```

### 2.4 Integration Architecture Patterns

```
INTEGRATION PATTERNS — COMPARISON

  PATTERN 1: POINT-TO-POINT (Anti-pattern at scale)
  ─────────────────────────────────────────────────────
  System A ←──→ System B
  System A ←──→ System C
  System B ←──→ System C

  For n systems: n×(n-1)/2 integration points
  4 systems = 6 integrations
  10 systems = 45 integrations (unmanageable)

  Problems:
  • Every integration is custom-built
  • No central point for monitoring or governance
  • Adding a new system requires n-1 new integrations
  • Known as "spaghetti integration"

  ─────────────────────────────────────────────────────
  PATTERN 2: HUB-AND-SPOKE (Classic enterprise)
  ─────────────────────────────────────────────────────
  System A ──→ [HUB] ──→ System B
  System C ──→ [HUB] ──→ System D
  System E ──→ [HUB]

  Hub types: ESB (Enterprise Service Bus), middleware,
             MDM hub, canonical data model

  For n systems: n×2 integrations (linear, not quadratic)
  Benefits: Central governance; single point for monitoring;
            canonical transformation in the hub

  Problems: Hub becomes a single point of failure;
            performance bottleneck for high-throughput

  ─────────────────────────────────────────────────────
  PATTERN 3: PUBLISH-SUBSCRIBE / EVENT BUS (Modern)
  ─────────────────────────────────────────────────────
  PRODUCER: System A publishes events to TOPIC: customer.updated
  CONSUMER 1: CRM subscribes → receives customer.updated events
  CONSUMER 2: Analytics subscribes → receives customer.updated events
  CONSUMER 3: Fraud engine subscribes → receives customer.updated events

  Benefits:
  • Producers and consumers are decoupled (don't know each other)
  • New consumers can subscribe without changing the producer
  • Events are replayed — consumers can catch up after downtime
  • Scales horizontally — add more consumers freely

  Tools: Apache Kafka, AWS SNS/SQS, Azure Event Hubs, RabbitMQ

  ─────────────────────────────────────────────────────
  PATTERN 4: API-BASED (Request-Response)
  ─────────────────────────────────────────────────────
  Consumer → [REST API Request] → Producer
  Producer → [JSON Response]    → Consumer

  Synchronous: Consumer waits for response (tight coupling)
  Asynchronous: Consumer gets callback when ready (loose coupling)

  Protocols: REST (most common), SOAP (legacy/enterprise),
             GraphQL (flexible queries), gRPC (high-performance)
  Formats:   JSON (default REST), XML (SOAP/legacy), Protobuf (gRPC)

  Best for: On-demand data retrieval; mobile/web app backends;
            B2B data exchange; government API portals
```

### 2.5 Data Interoperability — Three Dimensions

Interoperability is the ability of systems to exchange and make use of information. DAMA distinguishes three dimensions that must all be achieved for true interoperability:

```
THREE DIMENSIONS OF INTEROPERABILITY

  TECHNICAL INTEROPERABILITY
  ─────────────────────────────────────────────────────────
  Can the systems physically exchange data?
  → Compatible network protocols (TCP/IP, HTTPS)
  → Compatible messaging formats (JSON, XML, CSV, Parquet)
  → Compatible API standards (REST, SOAP, GraphQL)
  → Compatible authentication (OAuth 2.0, SAML, API keys)

  Without technical interoperability: Systems cannot connect.
  Example: A government portal using SOAP XML cannot accept
  data from a mobile app sending JSON REST without a
  translation layer.

  SYNTACTIC INTEROPERABILITY
  ─────────────────────────────────────────────────────────
  Do the systems agree on the FORMAT and STRUCTURE of data?
  → Date formats: DD/MM/YYYY vs YYYY-MM-DD (ISO 8601)
  → Number formats: 1,234.56 (EN) vs 1.234,56 (EU)
  → Code lists: Status = "A" vs Status = "Active" vs Status = 1
  → Character encoding: UTF-8 vs UTF-16 vs ASCII

  Without syntactic interoperability: Data arrives but is
  misinterpreted. "01/02/2024" means 1 February in Malaysia
  but 2 January in the United States.

  SEMANTIC INTEROPERABILITY
  ─────────────────────────────────────────────────────────
  Do the systems MEAN THE SAME THING by the same terms?
  → "Customer" in System A = individual retail buyer
  → "Customer" in System B = any party with a contract
     (includes suppliers, agents, counterparties)
  → These are NOT the same concept despite the same name.

  Without semantic interoperability: Data arrives in the right
  format but with the wrong meaning. A "Customer Count" report
  that merges both definitions will overcount.

  SOLUTION: Canonical data model + business glossary + data
  dictionary (links Chapters 5, 8, and 12)
```

### 2.6 Data Latency — Matching Integration to Business Need

```
DATA LATENCY SPECTRUM

  BATCH                  MICRO-BATCH         NEAR REAL-TIME    REAL-TIME
  (Hours / Daily)        (Minutes)           (Seconds)         (Milliseconds)
  ───────────────        ───────────         ──────────────    ─────────────
  ETL / ELT              Spark Streaming     CDC (log-based)   Event streaming
  Scheduled jobs         Short-interval      Message queues    (Kafka / Kinesis)
                         batch runs

  Use cases:             Use cases:          Use cases:        Use cases:
  Nightly DW loads       Hourly reports      Inventory sync    Fraud detection
  Monthly regulatory     Dashboard refresh   Price updates     Real-time bidding
  submissions            Order processing    Account balance   IoT sensor alerts
  Historical analytics

  Cost:   Lowest         Low-medium          Medium-high       Highest
  Complex: Simplest      Simple              Moderate          Most complex

  BNM RMIT reporting → Batch (daily/monthly) acceptable
  BNM fraud monitoring → Real-time required
  PDPA consent sync → Near real-time (hours SLA)
```

### 2.7 Data Virtualisation

Data virtualisation creates a virtual, unified view of data from multiple source systems without physically moving or copying the data. Queries against the virtual layer are translated by the virtualisation engine into queries against the actual source systems at runtime.

```
DATA VIRTUALISATION — HOW IT WORKS

  CONSUMER (analyst / application / report)
       │
       │ Queries a VIRTUAL TABLE as if it were a single DB
       ▼
  ┌──────────────────────────────────────────────┐
  │  DATA VIRTUALISATION LAYER                   │
  │  (Denodo, TIBCO Data Virtualization,         │
  │   Starburst, Dremio)                         │
  │                                              │
  │  Virtual Table: customer_360_view            │
  │  → Translates query into sub-queries         │
  │    against each source system                │
  └─────┬─────────────┬────────────┬─────────────┘
        │             │            │
        ▼             ▼            ▼
   Oracle CRM    Core Banking   Cloud CRM
   (on-premise)  (SQL Server)   (Salesforce API)

  BENEFITS:                       LIMITATIONS:
  • No data movement / copies     • Source system load at query time
  • Always fresh (no staleness)   • Network latency for each query
  • Fast to implement (no ETL)    • Performance limited by slowest source
  • Good for PoC / exploration    • Not suitable for complex analytics
  • PDPA-friendly: data stays     • No transformation/enrichment capability
    in place (less data movement)   at virtualisation layer
```

### 2.8 Integration Governance — Interface Catalogue and API Management

**Interface Catalogue** — A governed registry of all data interfaces (integrations) in the enterprise. For each interface, the catalogue records: source system, target system, data elements exchanged, integration method (ETL/CDC/API), frequency/latency, data owner, interface owner, data classification, and lineage impact.

The interface catalogue serves as the foundation for BNM RMIT data flow documentation — regulators expect banks to demonstrate knowledge of all data flows, particularly those involving personal data or critical regulatory data.

**API Governance** — As organisations shift from ETL to API-based integration, governance of APIs becomes critical:

```
API GOVERNANCE FRAMEWORK

  API DESIGN STANDARDS
  → REST conventions (versioning: /v1/, /v2/)
  → Consistent error codes and response formats
  → Pagination standards for large datasets
  → Rate limiting policies (prevent abuse)

  API CATALOGUE / PORTAL
  → Self-service discovery for developers
  → Published documentation (OpenAPI/Swagger spec)
  → Test environment (sandbox) for integration development
  → Usage metrics and dependency tracking

  API SECURITY
  → Authentication: OAuth 2.0 / API keys / mutual TLS
  → Authorisation: Scopes limiting what each consumer can access
  → Input validation: Prevent injection attacks
  → Rate limiting + DDoS protection

  API LIFECYCLE MANAGEMENT
  → Versioning: Maintain v1 while migrating consumers to v2
  → Deprecation: Announce → grace period → retire
  → Breaking changes: Never without version bump
  → Consumer notification: Registry of all API consumers

  MALAYSIAN CONTEXT:
  MDEC's OpenAPI Malaysia initiative promotes standardised
  government API design for MyDIGITAL data sharing.
  BNM's Open API Framework (for open banking) requires
  licensed banks to expose standardised customer account
  APIs to licensed third-party providers (with customer consent).
```

---

## Section 3: Real-World Scenarios — Malaysian Context

### Scenario 1: CIMB Open Banking — API-Based Integration Under BNM's Open Finance Framework

**Business Context:**
BNM's Open Finance Framework (announced 2022) requires Malaysian banks to provide licensed third-party providers (TPPs) — fintechs and non-bank financial services companies — with API access to customer account information and payment initiation, subject to customer consent. CIMB must design a governed API integration layer that exposes customer data to TPPs while satisfying PDPA consent requirements and BNM's technical security standards.

**Integration Design:**

```
CIMB OPEN BANKING API ARCHITECTURE

  CUSTOMER
  ─────────────────────────────────────────────────────────
  Grants consent via CIMB mobile app:
  "Allow Grab Financial to view my account balance and
   last 3 months of transactions for credit scoring"
  Consent stored: ConsentRecord {scope, TPP_ID, expiry_date}
       │
       ▼
  THIRD-PARTY PROVIDER (e.g., Grab Financial)
  ─────────────────────────────────────────────────────────
  Calls CIMB Open Banking API:
  GET /v2/accounts/{accountId}/transactions
  Authorization: Bearer {OAuth_token}
       │
       ▼
  CIMB API GATEWAY (Kong / Apigee)
  ─────────────────────────────────────────────────────────
  Checks:
  ✓ OAuth token valid (not expired)
  ✓ Token scope includes "read:transactions"
  ✓ Consent record active and not withdrawn
  ✓ Rate limit: max 100 calls/minute per TPP
  ✓ Request logged for audit trail
       │
       ▼
  CIMB CORE BANKING API
  ─────────────────────────────────────────────────────────
  Returns: {
    account_id: "ACC-001234",
    balance: 12540.80,
    currency: "MYR",
    transactions: [...last 90 days...],
    data_as_of: "2024-10-15T14:30:00+08:00"
  }

  PDPA CONTROLS:
  → Consent must be explicit and specific (per transaction type)
  → Customer can withdraw consent via CIMB app at any time
  → Consent withdrawal propagates to API gateway within 60 seconds
  → All API calls logged: TPP ID, endpoint, timestamp, data returned
  → Data returned to TPP is the minimum required (data minimisation)
```

**BNM Open Finance + PDPA Link:**
The consent linkage between the PDPA consent record and the API gateway authorisation is the critical design element. When a customer withdraws consent, the OAuth token must be revoked and all future API calls from that TPP must be blocked — in real time. This is an integration and security design requirement, not just a policy statement.

**CDMP Link:** This scenario tests API governance, consent-driven data access control, API security (OAuth), data minimisation in integration, and the governance of third-party data sharing relationships.

---

### Scenario 2: MyDIGITAL — Government Agency Data Sharing and Semantic Interoperability

**Business Context:**
Malaysia's MyDIGITAL initiative requires government agencies to share data to improve citizen services. The Ministry of Health (MOH) needs to share patient vaccination status with the Ministry of Education (MOE) for school enrolment verification. Two agencies — each with separate legacy systems — must achieve interoperability without replacing either system.

**The Interoperability Challenge:**

```
MOH SYSTEM                      MOE SYSTEM
──────────────────────          ──────────────────────
Patient_IC: CHAR(14)            StudentIC: VARCHAR(20)
             (with dashes)                  (no dashes)
VaccStatus:  INT (1=Full,       VaccinationStatus: VARCHAR
             2=Partial,                    ("Complete"/"Incomplete"
             3=Unvaccinated)                /"Unknown")
VaccDate:    DATETIME           LastVaccinatedDate: DATE
             (UTC timestamp)               (DD/MM/YYYY local)
Vaccine_Nm:  CHAR(10) code      VaccineType: Full name string
             (e.g., "COV-P")               (e.g., "Pfizer-BioNTech")

TECHNICAL: Both REST APIs (✓ Technical interoperability achieved)
SYNTACTIC: Date formats differ; code vs text for vaccine name (✗)
SEMANTIC:  "VaccStatus = 2 (Partial)" — what does Partial mean?
           Does MOE define "Complete" as 2 doses or 3 doses? (✗)
```

**Interoperability Solution:**

Step 1 — **Semantic agreement**: Joint working group (MOH data steward + MOE data steward + MyDIGITAL) defines agreed definitions: "Full vaccination = completion of primary vaccination schedule as defined by MOH at time of enrolment, regardless of number of doses." This is a governance decision, documented in a shared business glossary.

Step 2 — **Canonical message design**: Define a canonical VaccinationStatus exchange message in JSON using ISO standards for dates (ISO 8601) and agreed vocabulary:
```json
{
  "ic_number": "620514145678",        ← No dashes; CHAR(12)
  "vaccination_status": "COMPLETE",   ← Enum: COMPLETE/PARTIAL/NOT_VACCINATED
  "last_vaccination_date": "2023-09-14", ← ISO 8601 date
  "vaccines_received": ["Pfizer-BioNTech", "Sinovac"],
  "data_as_of": "2024-10-15",
  "source_system": "MySejahtera",
  "data_classification": "CONFIDENTIAL"
}
```

Step 3 — **Translation layer**: MOH's integration layer translates from its internal format (CHAR dashes, INT codes, UTC datetime) to the canonical message before sending to MOE. MOE's integration layer translates from canonical to its internal format upon receipt. Neither system's internal schema changes.

**PDPA Cross-Border Angle:**
This scenario involves only domestic sharing between Malaysian government agencies — straightforward. Had MOH needed to share vaccination data with Singapore's MOH (ASEAN health corridor), PDPA Section 129 would apply: data cannot be transferred to a country without adequate data protection unless one of the listed exceptions applies (e.g., data subject consent, contractual necessity, or ministerial order approving the transfer).

**CDMP Link:** This scenario tests all three interoperability dimensions, canonical message design, translation layers, and PDPA cross-border transfer restrictions.

---

### Scenario 3: Petronas — CDC-Based Integration for Real-Time Operations Monitoring

**Business Context:**
Petronas's upstream operations database (Oracle) records production data from 47 offshore platforms. The analytics team needs a real-time operations dashboard showing current production volumes, equipment status, and alerts. The current approach — nightly ETL — means the dashboard is always 24 hours behind. A safety incident at Platform 3A was flagged in the operations system at 14:22 but did not appear in the monitoring dashboard until the next morning's ETL run.

**CDC Integration Design:**

```
PETRONAS CDC PIPELINE — REAL-TIME OPERATIONS INTEGRATION

  SOURCE: Oracle Upstream Operations DB
  ─────────────────────────────────────────────────────────
  Tables: PLATFORM_STATUS, PRODUCTION_READING, SAFETY_ALERT
  Change rate: ~50,000 row changes per hour across all tables

  STEP 1: CDC CAPTURE (Log-based — Oracle LogMiner / GoldenGate)
  ─────────────────────────────────────────────────────────
  Oracle redo log read → only changed rows captured
  No impact to source DB query performance
  Captures: INSERT / UPDATE / DELETE with before/after values
  Latency from source change to capture: < 1 second

  STEP 2: CDC STREAM (Apache Kafka)
  ─────────────────────────────────────────────────────────
  Topics:
  petronas.ops.platform_status   → consumed by: dashboard, alerts
  petronas.ops.production_reading → consumed by: dashboard, analytics
  petronas.ops.safety_alert       → consumed by: SAFETY ALERT CONSUMER
                                    (highest priority; pages on-call)

  Kafka retention: 7 days (replay capability)
  Partitioned by: platform_id (ordering guaranteed per platform)

  STEP 3: STREAM CONSUMERS
  ─────────────────────────────────────────────────────────
  Consumer 1: Real-time dashboard (ClickHouse)
              Ingests CDC events → updates materialised view
              Dashboard latency from source change: < 5 seconds

  Consumer 2: Safety Alert System
              Subscribes to safety_alert topic
              Any new safety alert → immediate push notification
              to platform supervisor + KL operations centre

  Consumer 3: Data Warehouse (Snowflake)
              Micro-batch: accumulates CDC events → loads every
              15 minutes into DW for historical analytics
              (Different consumers can have different latency needs)

  BEFORE CDC:  24-hour latency (nightly ETL)
  AFTER CDC:   < 5-second latency (real-time streaming)
  Safety improvement: Safety alerts visible in 5 seconds vs 24 hours
```

**Data Lineage Through Integration:**
The CDC pipeline must maintain lineage: every record in the real-time dashboard and data warehouse can be traced back to its source platform, source table, source record, and the timestamp of the original change. This traceability supports BNM RMIT data lineage requirements (for any financial data in scope) and Petronas's own operational audit requirements.

**CDMP Link:** This scenario tests CDC approach selection (log-based), Kafka publish-subscribe pattern, multiple consumers with different latency needs, and data lineage through the integration layer.

---

## Section 4: Visual Diagrams + Cheat Sheet

### 4.1 Data Flow Diagram — Conceptual Layers

```
ENTERPRISE DATA FLOW — CONCEPTUAL LAYERS

  ┌──────────────────────────────────────────────────────────┐
  │  SOURCE LAYER                                            │
  │  ERP | CRM | Core Banking | Mobile App | IoT | Ext. APIs│
  │  (Operational systems — produce data)                   │
  └─────────────────────────┬────────────────────────────────┘
                            │ Integration layer
                ┌───────────┴───────────┐
                │                       │
          Batch/ELT               CDC/Streaming
          (ETL tools,             (Kafka, Debezium,
           dbt, Airflow)           GoldenGate)
                │                       │
                └───────────┬───────────┘
                            │
  ┌─────────────────────────▼────────────────────────────────┐
  │  INTEGRATION / STORAGE LAYER                             │
  │  Data Lake (raw) | Data Warehouse (governed) |           │
  │  MDM Hub | Canonical Model | API Gateway                 │
  └─────────────────────────┬────────────────────────────────┘
                            │ Serving layer
  ┌─────────────────────────▼────────────────────────────────┐
  │  CONSUMPTION LAYER                                       │
  │  BI / Dashboards | Regulatory Reports | ML Models |      │
  │  External APIs (Open Banking, B2B) | Applications        │
  └──────────────────────────────────────────────────────────┘

  DATA LINEAGE runs vertically through all layers:
  Source record → Integration transformation → Storage → Report
  Every transformation step must be documented for BNM RMIT compliance.
```

### 4.2 Integration Pattern Trade-offs

```
PATTERN COMPARISON — DECISION GUIDE

  POINT-TO-POINT
  Complexity: O(n²) — grows quadratically   Use when: < 3 systems, temporary
  Governance: None                           Avoid when: > 3 systems, long-term

  HUB-AND-SPOKE (ESB)
  Complexity: O(n) — grows linearly         Use when: Centralised governance needed
  Governance: Central                        Avoid when: High-throughput real-time needed
  Single point of failure: YES

  PUBLISH-SUBSCRIBE (Event Bus)
  Complexity: O(n) — grows linearly         Use when: Real-time; multiple consumers
  Governance: Distributed (topic-based)      per event; decoupled producers/consumers
  Single point of failure: NO (Kafka is distributed)

  API (Request-Response)
  Complexity: Per-pair                       Use when: On-demand; consumer controls timing
  Governance: API catalogue + gateway        Avoid when: High-frequency push needed
  Synchronous (blocking) by default

  DATA VIRTUALISATION
  Complexity: Metadata only                  Use when: PoC; source data must stay in place;
  Governance: Virtual layer catalogue                  PDPA data minimisation; low-frequency
  Source load: YES — query time                       queries
```

### 4.3 PDPA Cross-Border Data Transfer Rules

```
PDPA 2010 — CROSS-BORDER DATA TRANSFER (Section 129)

  RULE: Personal data shall not be transferred to any place
        outside Malaysia unless the receiving country provides
        a level of protection equivalent to PDPA.

  EXCEPTIONS (transfer is permitted if):
  ─────────────────────────────────────────────────────────
  1. The place is listed in a Ministerial Order as adequate
     (similar to GDPR adequacy decisions)

  2. Data subject has CONSENTED to the transfer

  3. Transfer is necessary for a CONTRACT between data
     subject and data user (e.g., international payment)

  4. Transfer is for legal proceedings

  5. Data subject's vital interests require it

  6. Data has been made public by the data subject

  ─────────────────────────────────────────────────────────
  INTEGRATION IMPLICATIONS:
  ─────────────────────────────────────────────────────────
  Any integration that sends Malaysian personal data to
  a cloud provider's servers outside Malaysia triggers
  Section 129 considerations.

  Common scenarios:
  → Sending customer data to US-based SaaS CRM (Salesforce)
    → Requires contractual data processing agreement (DPA)
    → Data Processing Agreement must include PDPA-equivalent protections

  → Using AWS Singapore region
    → Singapore has PDPA 2012 — generally considered adequate
    → Contractual DPA still recommended

  → ML model training on EU servers
    → Requires explicit consent or contractual basis
    → GDPR and PDPA both apply if EU citizens' data is included
```

### 4.4 Data Exchange Formats — Quick Reference

```
DATA EXCHANGE FORMATS — COMPARISON

  Format    Type          Use Case              Strengths         Weaknesses
  ──────────────────────────────────────────────────────────────────────────
  JSON      Text/human    REST APIs; web apps   Readable; widely  Verbose; no schema
            readable      mobile backends       supported         enforcement by default

  XML       Text/human    SOAP APIs; legacy     Self-describing;  Very verbose;
            readable      enterprise; EDI       schema (XSD)      slow parsing

  CSV       Text/flat     Simple data export;   Universal support No schema; no types;
                          spreadsheet import    lightweight       poor for nested data

  Parquet   Binary/       Data lakes; Spark;    Column-oriented;  Not human-readable;
            columnar      analytical            highly compressed needs tooling
                          workloads             fast analytics

  Avro      Binary/       Kafka streaming;      Schema evolution; Not human-readable;
            row           real-time pipelines   compact binary    schema management
                                                                  overhead

  Protobuf  Binary        gRPC; high-           Smallest size;    Steep learning curve;
                          performance APIs      fastest parsing   schema required

  EDI       Structured    B2B trade             Industry standard Legacy; complex;
            text          (retail, logistics)   (EDIFACT, X12)    specialist tooling

  PARQUET AND AVRO are the preferred formats for modern data engineering
  pipelines — used extensively in Malaysian cloud data platform projects.
```

### 4.5 Cheat Sheet — Chapter 8 Key Terms

| Term | One-Line Definition | Exam Trap |
|---|---|---|
| **ETL** | Extract → Transform (staging) → Load | Transform happens BEFORE loading; staging area required |
| **ELT** | Extract → Load raw → Transform in-place | Transform happens AFTER loading; cloud-native approach |
| **CDC** | Captures only data that has changed since last extraction | Log-based CDC is best practice; timestamp-based misses DELETEs |
| **Data Virtualisation** | Query-time unified view without moving data | Always fresh; but loads source systems at query time |
| **Canonical Model** | Enterprise-standard data structure used in integration | Resolves semantic heterogeneity; defined in Chapter 4/5 |
| **Technical Interoperability** | Systems can physically connect (protocols, formats) | Necessary but not sufficient — semantic alignment also needed |
| **Syntactic Interoperability** | Systems agree on data format and structure | Date formats, code lists, character encoding |
| **Semantic Interoperability** | Systems agree on the MEANING of data | Hardest to achieve; requires governance (business glossary) |
| **Hub-and-Spoke** | Central hub mediates all integrations (linear complexity) | Hub is a single point of failure; ESB is the classic tool |
| **Publish-Subscribe** | Producers publish events; consumers subscribe to topics | Decoupled; scalable; Kafka is the dominant tool |
| **Point-to-Point** | Direct integration between each pair of systems | Anti-pattern at scale: O(n²) complexity |
| **API Governance** | Catalogue, standards, security, lifecycle management for APIs | APIs without governance become the new spaghetti integration |
| **Interface Catalogue** | Registry of all data interfaces in the enterprise | Required for BNM RMIT data flow documentation |
| **Data Lineage** | Traceable path of data from source through transformation to target | Must be maintained through integration layers for RMIT compliance |
| **Data Latency** | Time delay between source data change and availability in target | Match latency to business need — real-time is most expensive |
| **PDPA S.129** | Personal data cannot be transferred outside Malaysia without adequate protection | Triggered by any cloud integration storing Malaysian personal data overseas |

### 4.6 CDMP Exam Traps — Chapter 8

```
COMMON EXAM TRAPS — DATA INTEGRATION & INTEROPERABILITY

  TRAP 1: ETL vs ELT staging
  ────────────────────────────
  "In ELT, data is transformed in a staging area before
   being loaded into the target."
  → FALSE. ELT loads data RAW into the target first,
    then transforms it IN PLACE within the target.
    The staging area belongs to ETL, not ELT.

  TRAP 2: CDC and DELETE capture
  ────────────────────────────────
  "Timestamp-based CDC captures all changes including deletions."
  → FALSE. Timestamp-based CDC relies on an updated_at column —
    deleted rows cannot update their own timestamp.
    Log-based CDC is required to capture DELETE operations.

  TRAP 3: Virtualisation = always fresh
  ───────────────────────────────────────
  "Data virtualisation eliminates the need for ETL pipelines
   because it always provides real-time data."
  → PARTIALLY TRUE but misleading. Virtualisation provides
    fresh data, but it loads source systems at query time.
    For high-frequency analytics, it is LESS efficient than ETL.
    Virtualisation is best for low-frequency, exploratory queries.

  TRAP 4: Interoperability vs integration
  ─────────────────────────────────────────
  "Integration and interoperability are the same thing."
  → FALSE. Integration is the TECHNICAL process of connecting systems.
    Interoperability is the CAPABILITY to exchange and USE data
    meaningfully (including semantic alignment). You can have
    integration without interoperability (data flows but is
    misunderstood at the destination).

  TRAP 5: Hub-and-spoke eliminates failure risk
  ───────────────────────────────────────────────
  "Hub-and-spoke integration is more resilient than
   point-to-point because it centralises control."
  → FALSE. The hub is a SINGLE POINT OF FAILURE.
    If the ESB goes down, ALL integrations fail.
    Publish-subscribe (event streaming) is more resilient
    because the broker is distributed.

  TRAP 6: PDPA and cloud storage
  ────────────────────────────────
  "Using a cloud provider's Malaysia region eliminates
   all PDPA cross-border transfer concerns."
  → PARTIALLY TRUE. Data stored in Malaysia-region servers
    avoids Section 129 transfer issues — but if the cloud
    provider's parent company (e.g., US-based) can access
    Malaysian customer data, contractual protections are
    still required.
```

---

## Section 5: Official DAMA Images

### DAMA Data Integration & Interoperability Knowledge Area Context Diagram

*Source: DAMA International, DAMA-DMBOK2 Knowledge Area Context Diagram Series*
*License: Creative Commons CC BY-ND 4.0 | © DAMA International*

![DAMA Data Integration & Interoperability KA Context Diagram](https://growthzonecmsprodeastus.azureedge.net/sites/2326/2025/04/x-17.png)

> **Reading the context diagram:** Data Integration & Interoperability receives inputs from Data Architecture (integration design blueprints), Data Modelling (canonical models used in integration), and Data Security (security controls on data in transit). Its outputs feed Data Warehousing & Business Intelligence (Chapter 11), Reference & Master Data (Chapter 10), and Big Data & Data Science (Chapter 14). The integration layer is the connective tissue of the entire DAMA Wheel — every KA depends on data moving reliably and with preserved meaning.

*Note: If the image above does not render, refer to Day01 Section 5 for the complete DAMA KA gallery.*

---

### DAMA Wheel — Positioning of Data Integration & Interoperability

*Source: DAMA International | CC BY-ND 4.0*

![DAMA Wheel — Data Management Knowledge Areas](https://dama.org/wp-content/uploads/sites/2326/2025/04/x.png.webp)

**Data Integration & Interoperability** in the DAMA Wheel: This KA spans all others — data must flow from where it is created (operational systems) to where it is used (analytics, reporting, AI/ML). Chapter 8 is the implementation of the integration architecture designed in Chapter 4. It connects Data Storage & Operations (Chapter 6, where data sits) to Data Warehousing & Business Intelligence (Chapter 11, where data is analysed) and Reference & Master Data (Chapter 10, which depends on integration to synchronise golden records).

---

## Chapter 8 at a Glance — One-Page Summary

```
DATA INTEGRATION & INTEROPERABILITY — CDMP EXAM SUMMARY
══════════════════════════════════════════════════════════════

WHAT:   Moving and consolidating data within and between
        systems, with shared understanding of its meaning

INTEGRATION APPROACHES:
  ETL   → Transform BEFORE load (staging area; batch)
  ELT   → Load raw THEN transform (cloud-native; flexible)
  CDC   → Capture only changes (log-based best; near real-time)
  Virtual → Query-time view; no data movement; always fresh
  API   → Request-response; on-demand; synchronous/async
  Events → Publish-subscribe; Kafka; real-time; decoupled

ARCHITECTURE PATTERNS:
  Point-to-Point → Anti-pattern at scale (O(n²) complexity)
  Hub-and-Spoke  → Linear complexity; central governance; SPOF
  Pub-Sub        → Linear; decoupled; resilient; real-time
  API Gateway    → Governed API exposure; security; catalogue

INTEROPERABILITY (3 dimensions):
  Technical  → Can systems connect? (protocols, formats)
  Syntactic  → Do they agree on structure? (dates, codes)
  Semantic   → Do they mean the same thing? (business glossary)

DATA LATENCY SPECTRUM:
  Batch → Micro-batch → Near real-time → Real-time
  Match latency to business need (cost increases with speed)

DATA FORMATS:
  JSON/XML → APIs | CSV → Simple export | Parquet/Avro → Big data

GOVERNANCE:
  Interface Catalogue → Registry of all integrations
  API Governance → Catalogue + security + lifecycle
  Data Lineage → Traced through every transformation
  PDPA S.129 → Cross-border transfer restrictions

EXAM WEIGHT: ~6%
══════════════════════════════════════════════════════════════
```

---

*Day 08 | DAMA-DMBOK2 Chapter 8 — Data Integration & Interoperability*
*CDMP Exam Preparation | 17-Day Study Programme*
*Malaysian Context: BNM Open Finance | PDPA 2010 S.129 | MyDIGITAL Blueprint | MDEC OpenAPI*
*Next: Day 09 — Document & Content Management (Chapter 9)*
