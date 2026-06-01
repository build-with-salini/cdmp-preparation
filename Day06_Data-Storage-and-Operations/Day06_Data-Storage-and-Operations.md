# Day 06 — Data Storage & Operations
## DAMA-DMBOK2 Chapter 6 | CDMP Exam Weight: ~6%

**Study Plan:** Day 6 of 17 | Foundational chapter for physical data management
**Malaysian Context:** BNM BCP/DR guidelines, PDPA 2010 retention obligations, MyDIGITAL cloud-first, MCMC data localisation
**Connections:** Feeds from Chapter 5 (Data Modelling → physical implementation) | Links to Chapter 7 (Data Security) and Chapter 13 (Data Quality)

---

## Section 1: Core Summary — What Is Data Storage & Operations

Data Storage & Operations covers the design, implementation, and support of stored data assets across their operational lifecycle. Where Chapter 5 produces the *model* for data, Chapter 6 governs the *environment* in which that model is physically realised and operated. It is the domain of the Database Administrator (DBA), the storage architect, and the data operations team — the people responsible for keeping data accessible, performant, consistent, and recoverable.

### DAMA Definition

DAMA-DMBOK2 defines the scope of Data Storage & Operations as encompassing: *"the design, implementation, and support activities related to the storage of data assets — databases, data files, and other repositories — across their operational lifecycle."* This includes the technologies used to store data, the processes used to keep stored data accessible and reliable, and the practices used to manage data through retention, archival, and eventual disposal.

### Why This Chapter Matters for the CDMP Exam

Chapter 6 carries approximately **6% of exam weight**. The exam tests conceptual understanding — not deep DBA technical knowledge. You need to know the categories of database types and when each is appropriate, the principles that govern database transactions (ACID) and distributed systems (CAP), the difference between backup strategies and their recovery implications, and how data retention obligations shape storage decisions. This chapter also provides the physical reality context for Chapter 5's modelling and Chapter 7's security controls.

### Three Core Business Drivers

**Ensuring data availability** — Data that cannot be accessed when needed has no business value. Storage & Operations establishes the infrastructure, replication, and redundancy mechanisms that keep data available to authorised users and processes within defined service levels.

**Protecting data integrity and recoverability** — Hardware fails, software has bugs, and human errors occur. The backup, recovery, and disaster recovery practices in this chapter ensure that when something goes wrong, data can be restored to a known correct state within an acceptable time window — defined by the Recovery Point Objective (RPO) and Recovery Time Objective (RTO).

**Managing data across its lifecycle** — Data does not need to be stored the same way forever. Active transactional data belongs in fast, expensive storage. Aged data that must be retained for compliance can move to cheaper archival storage. Data past its retention period must be securely disposed of. Managing this lifecycle efficiently reduces cost without compromising compliance or analytical access.

---

## Section 2: DAMA Framework View — Concepts, Activities, Roles

### 2.1 Database Types — The Technology Landscape

DAMA Chapter 6 recognises that different data storage needs require different database technologies. The exam tests the ability to match a business use case to the appropriate database type.

```
DATABASE TYPE SELECTION MAP

  PRIMARY USE CASE
       │
       ├─ Structured transactional data (CRUD)?
       │        → RELATIONAL DATABASE (RDBMS)
       │          Oracle, SQL Server, PostgreSQL, MySQL
       │          Key: ACID transactions; normalised schemas
       │
       ├─ Analytical / reporting workloads?
       │        → COLUMNAR / ANALYTICAL DATABASE
       │          Snowflake, Redshift, BigQuery, Teradata
       │          Key: Column-oriented storage; fast aggregations
       │
       ├─ Flexible / semi-structured documents?
       │        → DOCUMENT STORE (NoSQL)
       │          MongoDB, Couchbase, Firestore
       │          Key: JSON/BSON documents; schema-on-read
       │
       ├─ Key-value lookup (high throughput, simple reads)?
       │        → KEY-VALUE STORE
       │          Redis, DynamoDB, Memcached
       │          Key: Extreme speed; simple data structures
       │
       ├─ Highly connected data (networks, relationships)?
       │        → GRAPH DATABASE
       │          Neo4j, Amazon Neptune, JanusGraph
       │          Key: Nodes + edges; relationship traversal
       │
       ├─ Time-stamped sensor / IoT / financial data?
       │        → TIME-SERIES DATABASE
       │          InfluxDB, TimescaleDB, kdb+
       │          Key: Optimised for append + time-range queries
       │
       └─ Wide-column / massive distributed scale?
                → WIDE-COLUMN STORE
                  Apache Cassandra, HBase, Bigtable
                  Key: Horizontal scale; eventual consistency
```

| Database Type | Strengths | Weaknesses | Malaysian Example |
|---|---|---|---|
| **Relational (RDBMS)** | ACID guarantees; mature ecosystem; SQL standard | Vertical scaling limits; rigid schema | Core banking (Oracle); HR systems (SAP) |
| **Columnar** | Fast analytics on large datasets; compression | Not optimised for row-level CRUD | Maybank analytics (Snowflake); BNM reporting |
| **Document Store** | Flexible schema; natural JSON fit for APIs | No strong joins; eventual consistency | eCommerce product catalogues; mobile app backends |
| **Key-Value** | Sub-millisecond reads; massive throughput | No complex queries; no relationships | Session management; caching; OTP storage |
| **Graph** | Relationship traversal; fraud pattern detection | Complex to query; limited ecosystem | AML fraud network analysis; social graphs |
| **Time-Series** | Optimised for time-stamped append workloads | Limited to temporal use cases | Petronas IoT sensor data; stock price feeds |
| **Wide-Column** | Horizontal scale to petabytes | Eventual consistency; complex operations | Telemetry data; large-scale event logs |

### 2.2 ACID Properties — The Foundation of Transactional Integrity

ACID is the set of properties that guarantee reliable transaction processing in a relational database. It is one of the most frequently tested concepts in Chapter 6.

```
ACID PROPERTIES — TRANSACTION INTEGRITY

  ┌─────────────────────────────────────────────────────────┐
  │  A — ATOMICITY                                          │
  │  "All or nothing"                                       │
  │                                                         │
  │  A transaction is treated as a single unit. Either ALL  │
  │  operations within the transaction succeed and are      │
  │  committed, or ALL are rolled back if any one fails.    │
  │                                                         │
  │  Example: Bank transfer of MYR 1,000 from Account A    │
  │  to Account B. Two operations:                          │
  │  1. Debit A by 1,000                                    │
  │  2. Credit B by 1,000                                   │
  │  If Step 2 fails, Step 1 must be rolled back.          │
  │  Money cannot vanish or be created.                     │
  └─────────────────────────────────────────────────────────┘
  ┌─────────────────────────────────────────────────────────┐
  │  C — CONSISTENCY                                        │
  │  "Only valid data is written"                           │
  │                                                         │
  │  A transaction brings the database from one valid       │
  │  state to another valid state, honouring all defined    │
  │  rules, constraints, and referential integrity.         │
  │                                                         │
  │  Example: An account balance cannot go negative if a    │
  │  CHECK constraint enforces balance >= 0.               │
  │  A transaction that would violate this is rejected.     │
  └─────────────────────────────────────────────────────────┘
  ┌─────────────────────────────────────────────────────────┐
  │  I — ISOLATION                                          │
  │  "Transactions don't interfere with each other"         │
  │                                                         │
  │  Concurrent transactions execute as if they were        │
  │  sequential — intermediate states are not visible       │
  │  to other transactions.                                 │
  │                                                         │
  │  Example: Two tellers simultaneously processing        │
  │  withdrawals from the same account. Isolation ensures  │
  │  neither teller sees the other's in-progress changes   │
  │  until both transactions are committed.                 │
  └─────────────────────────────────────────────────────────┘
  ┌─────────────────────────────────────────────────────────┐
  │  D — DURABILITY                                         │
  │  "Committed data survives failures"                     │
  │                                                         │
  │  Once a transaction is committed, it remains committed  │
  │  even in the event of system failure, power loss,       │
  │  or crash. The committed state is written to durable    │
  │  storage (disk) before the commit acknowledgment is    │
  │  returned to the application.                           │
  │                                                         │
  │  Example: A payment committed at 14:32:05 is still     │
  │  present after the server restarts at 14:32:10.        │
  └─────────────────────────────────────────────────────────┘
```

### 2.3 CAP Theorem — The Distributed Systems Trade-off

CAP Theorem states that a distributed data system can guarantee at most **two of three** properties simultaneously: Consistency, Availability, and Partition Tolerance.

```
CAP THEOREM — DISTRIBUTED SYSTEM TRADE-OFFS

                    CONSISTENCY
                    (All nodes see
                    the same data
                    at the same time)
                         △
                        / \
               CA       /   \      CP
            (RDBMS)    /     \   (HBase,
                      /       \  MongoDB
                     /         \  strong)
                    /           \
                   /_____________\
         AVAILABILITY            PARTITION
         (System stays          TOLERANCE
         operational            (Works despite
         during failures)       network splits)
              AP
          (Cassandra,
           DynamoDB,
          CouchDB)

  CA: Consistency + Availability (sacrifice partition tolerance)
      → Traditional RDBMS in single-node deployment
      → Not suitable for truly distributed systems

  CP: Consistency + Partition Tolerance (sacrifice availability)
      → HBase, Zookeeper, MongoDB (strong consistency mode)
      → System may become unavailable during network partition
      → Correct for: banking, financial transactions

  AP: Availability + Partition Tolerance (sacrifice consistency)
      → Cassandra, DynamoDB, CouchDB
      → Always available; data may be temporarily inconsistent
      → Correct for: shopping carts, social media feeds, DNS
```

**Key exam insight:** Partition tolerance is non-negotiable in any truly distributed system — network partitions happen. The real choice is between **CP** (banking, where wrong data is worse than downtime) and **AP** (e-commerce, where availability matters more than immediate consistency).

### 2.4 Backup Strategies — Types and Trade-offs

```
BACKUP TYPES — COMPARISON

  FULL BACKUP
  ───────────────────────────────────────────────────────
  What:    Complete copy of all data in the database
  When:    Typically weekly (resource-intensive)
  Pros:    Simplest recovery — restore from one backup set
  Cons:    Largest storage requirement; longest backup time
  Recovery: Restore latest full backup → done

  DIFFERENTIAL BACKUP
  ───────────────────────────────────────────────────────
  What:    All data changed since the LAST FULL backup
  When:    Typically daily
  Pros:    Faster than full; simpler recovery than incremental
  Cons:    Grows larger each day until next full backup
  Recovery: Restore latest full + latest differential → done

  INCREMENTAL BACKUP
  ───────────────────────────────────────────────────────
  What:    All data changed since the LAST BACKUP (any type)
  When:    Hourly or more frequently
  Pros:    Smallest backup size; fastest backup operation
  Cons:    Slowest recovery — must apply every incremental
           in sequence from last full backup
  Recovery: Restore full + every incremental in order → done

  TRANSACTION LOG BACKUP
  ───────────────────────────────────────────────────────
  What:    The database transaction log (all committed
           transactions since last log backup)
  When:    Every 15-60 minutes for critical systems
  Pros:    Enables point-in-time recovery (restore to
           specific minute before a data corruption event)
  Cons:    Requires full model recovery mode; complex
  Recovery: Restore full + differentials + all log backups
             → apply logs up to the desired point in time

  ─────────────────────────────────────────────────────────────
  COMPARISON SUMMARY

  Type          Backup Speed   Recovery Speed   Storage Size
  Full          Slowest        Fastest          Largest
  Differential  Medium         Medium           Medium (grows)
  Incremental   Fastest        Slowest          Smallest
  Tran. Log     Fast           Complex          Small per backup
```

### 2.5 RPO and RTO — The Business Recovery Targets

**Recovery Point Objective (RPO)** — The maximum acceptable amount of data loss measured in time. If RPO = 1 hour, the organisation can tolerate losing at most 1 hour of transactions. RPO drives backup frequency: to achieve a 1-hour RPO, backups must run at least every hour.

**Recovery Time Objective (RTO)** — The maximum acceptable time from the moment of failure to the moment normal operations are restored. If RTO = 4 hours, the system must be back online within 4 hours of a failure. RTO drives infrastructure design: high availability clusters, hot standbys, and pre-tested recovery runbooks.

```
RPO vs RTO — VISUAL REPRESENTATION

  FAILURE EVENT
       │
       ▼
  ─────●──────────────────────────────●────────▶ Time
  Last │←──── DATA LOSS WINDOW ──────►│Recovery
  Good │              RPO              │Complete
  Backup                                    │
                                      RTO   │
  ◄────────────────────────────────────────►│
  Failure time ────────────────── Recovery complete

  RPO determines: HOW OFTEN to back up
  RTO determines: HOW FAST to recover (infrastructure cost)

  LOW RPO (minutes) → Frequent backups + log shipping
  LOW RTO (minutes) → Hot standby + automatic failover
  BOTH LOW          → Active-active clustering (expensive)
  BOTH HIGH         → Weekly backup restored manually (cheap)
```

### 2.6 High Availability and Disaster Recovery

**High Availability (HA)** — Architectural design that minimises planned and unplanned downtime within a single data centre or region. HA eliminates single points of failure through redundancy (clustered servers, RAID storage, redundant network paths) and automatic failover.

**Disaster Recovery (DR)** — The ability to restore operations after a catastrophic event (fire, flood, power grid failure, cyber attack) that affects an entire data centre. DR requires geographically separated infrastructure — a secondary site that can assume operations when the primary site is lost.

```
HA vs DR — SCOPE AND DESIGN

  HIGH AVAILABILITY (same site)       DISASTER RECOVERY (different site)
  ─────────────────────────────       ────────────────────────────────────
  Protects against:                   Protects against:
  • Hardware failure (server, disk)   • Data centre destruction
  • Network component failure         • Regional power outage
  • Software crash                    • Natural disaster
  • Planned maintenance downtime      • Ransomware / cyber attack

  Design:                             Design:
  • Database clustering               • Active-Passive DR site
  • Automatic failover                • Active-Active geo-redundancy
  • Shared storage / replication      • Log shipping to secondary
  • Load balancing                    • Backup tapes off-site

  Target:                             Target:
  • RTO: seconds to minutes           • RTO: hours to days
  • RPO: near zero (synchronous)      • RPO: minutes to hours (async)

  Cost: Medium                        Cost: High (doubles infrastructure)
```

### 2.7 Data Retention, Archiving, and Purging

**Data Retention** — The policy-driven decision about how long specific categories of data must be kept, balancing business need, legal obligation, and cost. Retention periods are defined by regulation (PDPA, financial record-keeping laws), contract, and business policy.

**Data Archiving** — Moving data that is no longer actively used but must be retained to lower-cost, slower-access storage (cold storage). Archived data remains queryable but with higher latency. Archiving reduces the size of production databases, improving operational performance.

**Data Purging / Disposition** — The permanent deletion of data that has exceeded its retention period. Purging must be secure (data cannot be recovered post-purge) and documented (an audit record confirms what was purged, when, by whom, and under which policy authority).

```
DATA LIFECYCLE — STORAGE TIERS

  ACTIVE / HOT DATA                WARM DATA               COLD / ARCHIVE DATA
  ─────────────────                ──────────              ───────────────────
  Frequently accessed              Occasionally accessed    Rarely accessed
  Current transactional            Recent history          Historical / compliance
  Sub-millisecond reads            Second-range reads      Minute-range reads

  Storage: Fast SSD / NVMe         Storage: SAS HDD        Storage: Object storage
  Cost: Highest per GB             Cost: Medium            Cost: Lowest per GB
  Example: Core banking            Example: Last 2 years   Example: 7+ year archive
           transaction table                of transactions          for tax records

            │                           │                           │
            ▼                           ▼                           ▼
       PRODUCTION DB              DATA WAREHOUSE             DATA LAKE / ARCHIVE
       (Oracle, SQL Server)       (Snowflake, Redshift)      (AWS S3 Glacier)

  PURGE: When retention period expires → secure deletion + audit record
```

### 2.8 DBA Roles and Key Activities

| DBA Role | Focus | Key Responsibilities |
|---|---|---|
| **System DBA** | Infrastructure | Installation, patching, server configuration, storage management, HA/DR setup |
| **Database DBA** | Logical design | Schema management, user access, performance tuning, backup/recovery |
| **Application DBA** | Application support | Query optimisation, index design, stored procedure management, application integration |
| **Data Warehouse DBA** | Analytics platform | ETL pipeline management, partition strategy, aggregation management, query performance |
| **Cloud DBA** | Cloud-native databases | Managed service configuration, auto-scaling, cloud cost optimisation |

**Key DBA Activities (DAMA Ch. 6):**
Understanding data storage technology; defining data storage requirements; managing database technology; managing database operations (create, update, delete, backup, restore); supporting business continuity; managing data migration and conversion; monitoring and tuning database performance.

---

## Section 3: Real-World Scenarios — Malaysian Context

### Scenario 1: CIMB Digital Bank — Database Selection for a Multi-Product Platform

**Business Context:**
CIMB is building a new digital banking platform (CIMB Clicks 2.0) that must simultaneously support high-volume retail transactions, real-time fraud scoring, personalised product recommendations, and BNM regulatory reporting. The platform architect must select the right database technology for each workload — not a single database for everything.

**The Design Challenge:**
Legacy thinking: "Use Oracle for everything." Modern reality: different workloads have fundamentally different access patterns, consistency requirements, and scale needs. Using a single RDBMS for all workloads means the system is over-engineered for some and under-powered for others.

**Polyglot Persistence Architecture:**

The architect recommends a **polyglot persistence** approach — using the right database type for each specific workload:

```
CIMB DIGITAL PLATFORM — POLYGLOT PERSISTENCE

  WORKLOAD                DB TYPE         PRODUCT         REASON
  ─────────────────────────────────────────────────────────────────
  Core account ledger     Relational      Oracle 19c      ACID; regulatory
  Customer master data    Relational      PostgreSQL      ACID; referential integrity
  Session management      Key-Value       Redis           Sub-ms; simple lookup
  User profiles / prefs   Document        MongoDB         Flexible schema; API-native
  Fraud detection features Graph          Neo4j           Relationship traversal
  Real-time analytics     Columnar        ClickHouse      Fast aggregations
  BNM regulatory reports  Data Warehouse  Snowflake       Historical; governed
  Audit / event logs      Time-Series     TimescaleDB     Append; time-range queries
  Long-term archive       Object Storage  AWS S3          Low cost; compliance
```

**Regulatory Implication:**
BNM's Business Continuity Management (BCM) policy requires banks to define RPO and RTO for all critical systems. For the core account ledger (Oracle), CIMB sets RPO = 15 minutes and RTO = 2 hours — driving a synchronous replication setup with a hot standby in a secondary data centre. For the recommendation engine (MongoDB), the tolerances are more relaxed: RPO = 4 hours, RTO = 8 hours — a cost-effective asynchronous backup is sufficient.

**CDMP Link:** This scenario tests database type selection, polyglot persistence concept, and the relationship between RPO/RTO requirements and infrastructure design choices.

---

### Scenario 2: Maybank — Data Retention and PDPA Disposal Programme

**Business Context:**
Following a PDPA 2010 audit finding, Maybank's Data Governance team is required to implement a formal Data Retention and Disposal programme. The auditor found that personal data from closed accounts (closed more than 7 years ago) was still sitting in production databases — far beyond any legally justifiable retention period.

**The Retention Framework:**

Maybank establishes a Data Retention Schedule that maps each data category to its retention trigger, retention period, and disposal method:

```
MAYBANK DATA RETENTION SCHEDULE (Excerpt)

  Data Category           Retention Trigger   Period   Disposal Method
  ─────────────────────────────────────────────────────────────────────
  Customer KYC records    Account closure     7 years  Secure purge + audit log
  Transaction records     Transaction date    7 years  Archive → purge
  Consent records         Consent withdrawal  3 years  Secure purge
  Loan agreements         Loan closure        10 years Archive → purge (legal hold)
  Regulatory reports      Report date         10 years Archive (BNM requirement)
  Marketing preferences   Account closure     1 year   Purge immediately
  ATM CCTV metadata       Recording date      90 days  Overwrite (cyclic)
  System access logs      Log creation        3 years  Archive → purge
  Failed login attempts   Event date          1 year   Purge

  LEGAL HOLDS: Data subject to active litigation or regulatory
  investigation is frozen — normal retention schedules suspended
  until legal hold is lifted by General Counsel.
```

**The Technical Implementation:**

The data operations team implements a three-tier lifecycle automation:

1. **Tier 1 (0–2 years)**: Data in production Oracle databases — full ACID, fastest access, replicated for HA.
2. **Tier 2 (2–7 years)**: Migrated to archive Snowflake tables — queryable for regulatory requests but not in production. Cost: ~15% of Tier 1 per GB.
3. **Tier 3 (7+ years)**: Moved to AWS S3 Glacier — cold archive, retrieval time 3–5 hours, lowest cost. Triggered by automated retention policy scheduler.

**Disposal Process:**
When data reaches end of retention period, a disposal workflow is triggered: automated job identifies records for purge → Data Steward reviews and approves → secure deletion executed (three-pass overwrite for sensitive fields) → disposal certificate generated with: record count, data category, retention period, disposal method, authoriser name, timestamp.

**PDPA 2010 Link:** Section 10 (Retention of Personal Data) requires that personal data shall not be retained longer than necessary for its stated purpose. The disposal certificate is the evidence of compliance. Without it, Maybank cannot demonstrate PDPA compliance during an audit.

**CDMP Link:** This scenario tests data retention policy, storage tier management, data lifecycle management (DLM), and the governance link between retention decisions and regulatory compliance.

---

### Scenario 3: Petronas — Disaster Recovery for a Critical Operations Database

**Business Context:**
Petronas operates an upstream operations database that tracks real-time production data from offshore oil platforms — flow rates, pressure readings, equipment status, and safety sensor data. An outage of this system threatens operational continuity and worker safety. The system must meet stringent BCP (Business Continuity Planning) requirements mandated by DOSH (Department of Occupational Safety and Health) and Petronas's own operational risk framework.

**DR Design:**

The DR design team defines the requirements first — business requirements drive the technical solution:

```
PETRONAS OPERATIONS DB — DR REQUIREMENTS

  System Classification:    Mission Critical (Tier 1)
  Criticality Reason:       Worker safety; production continuity
  RPO:                      5 minutes (maximum data loss acceptable)
  RTO:                      15 minutes (maximum downtime acceptable)
  Availability Target:      99.99% (< 53 minutes downtime per year)

  DR ARCHITECTURE DESIGN:

  PRIMARY SITE (Kuala Lumpur DC)
  ┌────────────────────────────────────────┐
  │  Active Oracle RAC Cluster (3 nodes)   │
  │  Synchronous replication → Standby     │
  │  Automated failover within 30 seconds  │
  │  SSD storage; 10Gbps interconnect      │
  └───────────────────┬────────────────────┘
                      │ Synchronous log shipping
                      │ (RPO < 5 minutes)
  SECONDARY SITE (Cyberjaya DC)
  ┌────────────────────────────────────────┐
  │  Oracle Data Guard Hot Standby         │
  │  Pre-warmed; ready to accept traffic   │
  │  Switchover time: < 15 minutes (RTO)   │
  │  Tested quarterly via DR drill         │
  └───────────────────┬────────────────────┘
                      │ Asynchronous backup
  TERTIARY SITE (AWS Asia Pacific)
  ┌────────────────────────────────────────┐
  │  Cloud backup (daily full + hourly log)│
  │  Used only if both DCs are lost        │
  │  RTO: 4 hours for cloud recovery       │
  └────────────────────────────────────────┘

  DR TESTING SCHEDULE:
  Monthly:     Backup restoration test (verify backup integrity)
  Quarterly:   Planned switchover to secondary site (test RTO)
  Annually:    Full DR simulation (both sites offline scenario)
```

**The Critical Operational Rule:** DR capability that has not been tested is not DR capability — it is an untested hypothesis. BNM's BCM guidelines (and Petronas's internal policy) require DR drills at defined frequencies. The quarterly switchover test is the only way to confirm that the 15-minute RTO is achievable in practice, not just in theory.

**CDMP Link:** This scenario tests RPO/RTO definition, HA vs DR distinction, backup strategy selection, and the governance requirement for regular DR testing.

---

## Section 4: Visual Diagrams + Cheat Sheet

### 4.1 OLTP vs OLAP — The Fundamental Design Split

```
OLTP vs OLAP — COMPARISON

  OLTP (Online Transaction Processing)  OLAP (Online Analytical Processing)
  ──────────────────────────────────    ──────────────────────────────────
  PURPOSE: Run the business             PURPOSE: Understand the business
  QUERIES: Short, targeted (PK lookup)  QUERIES: Long, aggregating (millions of rows)
  OPERATIONS: INSERT/UPDATE/DELETE      OPERATIONS: Mostly SELECT (read-heavy)
  SCHEMA: Highly normalised (3NF)       SCHEMA: Denormalised (star/snowflake)
  CONCURRENCY: Many concurrent users    CONCURRENCY: Few concurrent users, large queries
  DATA VOLUME: Current data (GBs)       DATA VOLUME: Historical data (TBs-PBs)
  RESPONSE TIME: Milliseconds           RESPONSE TIME: Seconds to minutes acceptable
  ACID: Required (financial integrity)  ACID: Not critical (reads only)
  EXAMPLES: Core banking, ERP, CRM      EXAMPLES: Data warehouse, BI reporting

  ────────────────────────────────────────────────────────────────
  KEY DESIGN PRINCIPLE: DO NOT run analytics on the OLTP database.
  Heavy analytical queries lock tables and degrade transactional
  performance. The data warehouse exists to separate these workloads.
```

### 4.2 Storage Hierarchy — Speed vs Cost

```
STORAGE HIERARCHY

  SPEED (fastest → slowest)          COST (most → least expensive per GB)

  CPU Cache (L1/L2/L3)               CPU Cache        ← Most expensive
  ─────────────────────
  In-memory (RAM)                    In-memory (RAM)
  ─────────────────────
  NVMe SSD (local)                   NVMe SSD (local)
  ─────────────────────
  SSD Array (SAN)                    SSD Array
  ─────────────────────
  HDD (SAS/SATA)                     HDD (SAS)
  ─────────────────────
  Object Storage (warm)              Object Storage
  ─────────────────────
  Cold Archive (S3 Glacier,          Cold Archive     ← Least expensive
  Azure Archive, tape)
  ─────────────────────────────────────────────────────────
  Design principle: Match data temperature to storage tier.
  Hot data → fast/expensive storage.
  Cold data → slow/cheap storage.
  Never pay NVMe prices for 7-year-old audit logs.
```

### 4.3 Database Transaction Isolation Levels

```
TRANSACTION ISOLATION LEVELS (SQL Standard)

  Problem phenomena:
  ─────────────────
  Dirty Read:        Reading uncommitted data from another transaction
  Non-Repeatable:    Reading same row twice gets different values
  Phantom Read:      A query run twice returns different rows

  Isolation Level      Dirty  Non-Rep  Phantom   Performance
  ─────────────────────────────────────────────────────────
  READ UNCOMMITTED     Yes    Yes      Yes       Fastest (unsafe)
  READ COMMITTED       No     Yes      Yes       Default (most RDBMS)
  REPEATABLE READ      No     No       Yes       Slower
  SERIALIZABLE         No     No       No        Slowest (safest)

  Malaysian Banking Standard:
  SERIALIZABLE or REPEATABLE READ for financial transactions
  (Consistency over raw performance)
```

### 4.4 Data Retention Decision Framework

```
DATA RETENTION DECISION TREE

  Does a law or regulation mandate a minimum retention period?
  │
  ├── YES → Retain for at least the legally mandated period.
  │         (PDPA 2010 S.10, BNM regulations, Companies Act)
  │
  └── NO
       │
       Does the organisation have a contractual obligation
       to retain this data?
       │
       ├── YES → Retain for the contract term + defined buffer.
       │
       └── NO
            │
            Is there an ongoing business need (operational,
            analytical, or audit) for this data?
            │
            ├── YES → Define retention period based on business
            │         need. Document justification.
            │
            └── NO → DATA SHOULD BE PURGED.
                     Retaining data without justification
                     increases PDPA liability and storage cost.

  AFTER RETENTION PERIOD EXPIRES:
  ──────────────────────────────────────────────────────
  Check for Legal Hold → If yes: suspend disposal, flag record
  Check for ongoing audit → If yes: suspend disposal
  No holds? → Execute secure disposal → Document in audit log
```

### 4.5 Cheat Sheet — Chapter 6 Key Terms

| Term | One-Line Definition | Exam Trap |
|---|---|---|
| **ACID** | Atomicity, Consistency, Isolation, Durability — transactional integrity properties | ACID applies to relational databases; not guaranteed in NoSQL/AP systems |
| **CAP Theorem** | Distributed systems can guarantee only 2 of: Consistency, Availability, Partition Tolerance | Partition tolerance is non-negotiable → the real choice is CP vs AP |
| **RPO** | Max acceptable data loss (in time) — drives backup frequency | RPO is about data loss, not downtime — do not confuse with RTO |
| **RTO** | Max acceptable downtime — drives recovery infrastructure investment | RTO is about recovery speed, not data loss |
| **Full Backup** | Complete copy of all data | Slowest to create; fastest to restore |
| **Differential Backup** | Changes since last FULL backup | Faster backup than full; simpler recovery than incremental |
| **Incremental Backup** | Changes since last backup OF ANY TYPE | Fastest to create; slowest to restore |
| **Transaction Log Backup** | Log of all committed transactions since last log backup | Enables point-in-time recovery |
| **HA (High Availability)** | Redundancy within a single site to minimise downtime | HA protects against hardware/software failure; not disasters |
| **DR (Disaster Recovery)** | Ability to restore from a geographically separate site | DR protects against site-level events (fire, flood, cyber) |
| **Data Archiving** | Moving aged but retained data to cheaper, slower storage | Archived data is still queryable; purged data is not |
| **Data Purging** | Permanent, documented deletion of data past retention period | Must be secure + auditable — not just DELETE FROM table |
| **Data Retention** | Policy defining how long data must be kept | Driven by regulation, contract, and business need |
| **OLTP** | Transactional workload; INSERT/UPDATE/DELETE; normalised | Do not run analytics on OLTP — degrades transactional performance |
| **OLAP** | Analytical workload; SELECT; denormalised for fast aggregation | Designed for read-heavy, aggregate queries across large datasets |
| **Polyglot Persistence** | Using multiple database types for different workloads in one system | Not a problem — it is a design pattern matching tool to workload |
| **Sharding** | Horizontal partitioning — distributing data across multiple servers | Sharding is a physical scalability technique; not a data modelling concept |
| **Replication** | Copying data to one or more replica servers for HA or read scaling | Synchronous replication → strong consistency; Async → eventual consistency |
| **Data Disposition** | The formal, governed process of destroying data at end of retention | Requires policy authority, secure method, and audit documentation |

### 4.6 CDMP Exam Traps — Chapter 6

```
COMMON EXAM TRAPS — DATA STORAGE & OPERATIONS

  TRAP 1: RPO vs RTO confusion
  ─────────────────────────────
  "A system with RPO = 0 means no data can ever be lost."
  → TRUE — but this requires synchronous replication (expensive).
    Do not confuse with RTO = 0 (instant recovery — essentially impossible).

  TRAP 2: ACID ≠ all databases
  ──────────────────────────────
  "NoSQL databases do not provide ACID guarantees."
  → Generally TRUE for AP NoSQL systems. Some NoSQL databases
    (MongoDB 4+ with multi-document transactions, CockroachDB)
    DO provide ACID at the document level. Know the nuance.

  TRAP 3: Archiving ≠ Purging
  ─────────────────────────────
  "Data that has been archived has been disposed of."
  → FALSE — archived data still exists in cheaper storage.
    Purged data is permanently deleted.

  TRAP 4: Recovery speed by backup type
  ───────────────────────────────────────
  "Incremental backup provides the fastest recovery time."
  → FALSE — incremental provides fastest BACKUP time; slowest
    RECOVERY time (must apply every incremental in sequence).
    Full backup provides fastest recovery.

  TRAP 5: CAP — Partition Tolerance is not optional
  ───────────────────────────────────────────────────
  "A CA system (Consistency + Availability, no PT) is viable
  for distributed banking."
  → FALSE — in any distributed system, network partitions WILL
    occur. PT cannot be sacrificed. The real choice is CP vs AP.

  TRAP 6: HA vs DR scope
  ───────────────────────
  "High Availability protects against data centre disasters."
  → FALSE — HA protects within a single site (hardware/software
    failure). DR protects against site-level failures.
    Both are needed for comprehensive continuity coverage.
```

---

## Section 5: Official DAMA Images

### DAMA Data Storage & Operations Knowledge Area Context Diagram

*Source: DAMA International, DAMA-DMBOK2 Knowledge Area Context Diagram Series*
*License: Creative Commons CC BY-ND 4.0 | © DAMA International*

![DAMA Data Storage & Operations KA Context Diagram](https://dama.org/wp-content/uploads/sites/2326/2025/04/x-11.png.webp)

> **Reading the context diagram:** Data Storage & Operations receives the physical data model from Data Modelling & Design (Chapter 5) as its primary input — the model defines the structure; Storage & Operations implements and manages it. Its outputs include operational data stores, backup sets, archived data, and performance metrics. It is governed by Data Governance (Chapter 3) through policies, and feeds data quality monitoring back to Data Quality management (Chapter 13).

*Note: If the image above does not render, refer to Day01 Section 5 for the complete DAMA KA gallery.*

---
