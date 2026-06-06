# Day 09 — Document & Content Management
## DAMA-DMBOK2 Chapter 9 | CDMP Exam Weight: ~6%

**Study Plan:** Day 9 of 17 | Often underestimated — unstructured data is 80%+ of enterprise data
**Malaysian Context:** National Archives Act 2003, Companies Act 2016, Electronic Commerce Act 2006, Digital Signature Act 1997, PDPA 2010 in unstructured content, e-Government MyDIGITAL
**Connections:** Metadata (Chapter 12) governs content descriptors | Data Security (Chapter 7) applies to documents | Data Governance (Chapter 3) sets retention policy

---

## Section 1: Core Summary — What Is Document & Content Management

Document and Content Management (DCM) encompasses the technologies, processes, and governance frameworks used to create, store, organise, retrieve, protect, and dispose of unstructured and semi-structured data — the documents, records, images, emails, contracts, reports, web pages, and digital assets that make up the majority of enterprise information. Structured data in databases is estimated to represent only 20% of enterprise information; the remaining 80% exists as unstructured or semi-structured content, largely ungoverned in most organisations.

### DAMA Definition

DAMA-DMBOK2 defines Document & Content Management as: *"processes, techniques, and technologies for controlling the capture, storage, access, and use of data and information stored outside relational databases."* The distinction from other KAs is the nature of the data — not rows and columns in tables, but files, documents, records, images, audio, video, and web content that carry business meaning but do not conform to a rigid relational schema.

### Why This Chapter Matters for the CDMP Exam

Chapter 9 carries approximately **6% of exam weight**. The exam tests: understanding of content types (structured / unstructured / semi-structured), the vocabulary of content management (DMS, CMS, ECM, DAM, records management), the content lifecycle, taxonomy and controlled vocabulary concepts, records management and legal hold procedures, and the regulatory obligations governing document retention. This chapter also tests the recognition that PDPA 2010 applies to personal data in documents — not just databases.

### Three Core Business Drivers

**Operational efficiency and knowledge access** — Employees spend a significant portion of their working time searching for documents, re-creating content that already exists, or working from outdated versions. Enterprise Content Management (ECM) systems with properly governed taxonomies and search capabilities reduce this friction — the right document is findable by the right person at the right time.

**Regulatory compliance and records management** — The Companies Act 2016, National Archives Act 2003, BNM regulations, and PDPA 2010 impose legal obligations on how long certain records must be kept, in what format, and how they must ultimately be disposed of. Organisations that cannot find or produce records under legal discovery, regulatory examination, or audit face contempt, fines, and reputational damage.

**Risk reduction through governance** — Uncontrolled content is a risk multiplier. Outdated policy documents still in circulation create liability. Sensitive personal data in email attachments not covered by database security controls creates PDPA exposure. Proprietary business information in unmanaged SharePoint folders creates IP leakage risk. DCM governance brings the 80% of unstructured content under the same governance principles applied to structured data.

---

## Section 2: DAMA Framework View — Concepts, Activities, Governance

### 2.1 Content Types — The Spectrum

```
CONTENT TYPE SPECTRUM

  STRUCTURED DATA                SEMI-STRUCTURED            UNSTRUCTURED DATA
  (Covered: Chapters 5-8)       (Bridge)                   (This Chapter)
  ────────────────────           ─────────────────          ─────────────────────
  Rows and columns               Self-describing            No predefined structure
  Relational tables              with schema hints          Free-form content
  Fixed schema                   Variable schema

  Examples:                      Examples:                  Examples:
  • Database records             • XML files                • Word documents
  • Spreadsheet cells            • JSON documents           • PDFs / Contracts
  • CSV exports                  • HTML pages               • Emails / Attachments
  • Transactional logs           • YAML configs             • Presentations
                                 • Email headers            • Images / Photos
                                                            • Audio recordings
                                                            • Video files
                                                            • Instant messages
                                                            • Social media posts

  PDPA NOTE: Personal data is personal data regardless of format.
  A PDF contract containing customer NRIC is subject to PDPA 2010
  — the same as a database record containing that NRIC.
```

### 2.2 Content Management System Types

| System Type | Purpose | Examples | Key Capability |
|---|---|---|---|
| **Document Management System (DMS)** | Manage the lifecycle of formal documents (version control, check-in/check-out, approval workflows) | SharePoint, OpenText, Alfresco | Version control; workflow; access control |
| **Web Content Management (WCM)** | Manage content published on websites and portals, separating content from presentation | WordPress, Sitecore, Adobe Experience Manager | Non-technical authoring; template-based publishing |
| **Records Management System (RMS)** | Manage official records with defined retention schedules, legal holds, and auditable disposal | HP Records Manager, Laserfiche, M-Files | Retention enforcement; legal hold; disposal audit |
| **Digital Asset Management (DAM)** | Manage rich media files (images, videos, brand assets) with metadata and rights management | Bynder, Canto, Adobe AEM Assets | Rights management; format conversion; metadata |
| **Enterprise Content Management (ECM)** | Unified platform combining DMS, RMS, workflow, and collaboration | OpenText ECM, Microsoft 365, IBM FileNet | Integration of all content management functions |
| **Email Management** | Archive, manage, and govern email as a corporate record | Veritas Enterprise Vault, Microsoft Exchange Archive | Retention; e-discovery; PDPA compliance |
| **Knowledge Management** | Capture, organise, and share institutional knowledge | Confluence, Notion, SharePoint Knowledge Base | Search; tagging; expertise location |

### 2.3 Content Lifecycle — The Six Stages

```
CONTENT LIFECYCLE — DAMA CHAPTER 9

  ┌──────────────────────────────────────────────────────────┐
  │  1. CREATE / CAPTURE                                     │
  │  Content is authored, generated, or captured            │
  │  (document written, email sent, scan digitised,         │
  │   web form submitted, report generated)                 │
  │  Key activity: Apply metadata at point of creation      │
  │  (author, date, content type, classification,           │
  │   retention category) — hardest to retrofit later       │
  └──────────────────────────┬───────────────────────────────┘
                             ▼
  ┌──────────────────────────────────────────────────────────┐
  │  2. STORE / ORGANISE                                     │
  │  Content is stored in an appropriate repository         │
  │  with a taxonomy-based folder structure, tags,          │
  │  and searchable metadata.                               │
  │  Key activity: Enforce naming conventions, folder        │
  │  hierarchy, and access controls at storage              │
  └──────────────────────────┬───────────────────────────────┘
                             ▼
  ┌──────────────────────────────────────────────────────────┐
  │  3. ACCESS / USE                                         │
  │  Authorised users find, retrieve, and use content       │
  │  Key activity: Full-text search; metadata-driven        │
  │  navigation; check-in/check-out for versioning;         │
  │  access logging for PDPA compliance                     │
  └──────────────────────────┬───────────────────────────────┘
                             ▼
  ┌──────────────────────────────────────────────────────────┐
  │  4. MAINTAIN / UPDATE                                    │
  │  Content is revised, approved, and versioned            │
  │  Key activity: Version control (v1.0, v1.1, v2.0);     │
  │  approval workflow; superseded version management;      │
  │  content review schedule (policy docs reviewed          │
  │  annually; contracts reviewed on expiry)                │
  └──────────────────────────┬───────────────────────────────┘
                             ▼
  ┌──────────────────────────────────────────────────────────┐
  │  5. ARCHIVE                                              │
  │  Content past its active use period is moved to         │
  │  lower-cost storage but remains accessible for          │
  │  compliance, audit, or historical reference             │
  │  Key activity: Automated archival trigger (by age,      │
  │  status change, or event); searchable archive index     │
  └──────────────────────────┬───────────────────────────────┘
                             ▼
  ┌──────────────────────────────────────────────────────────┐
  │  6. DISPOSE / DESTROY                                    │
  │  Content past its retention period is permanently       │
  │  deleted with documented authorisation                  │
  │  Key activity: Retention policy check; legal hold       │
  │  check; disposal certificate; secure deletion           │
  │  (shred physical; crypto-erase digital)                 │
  └──────────────────────────────────────────────────────────┘
```

### 2.4 Records Management — Official Records and Their Governance

A **record** is content that serves as evidence of a business activity, decision, or transaction, and which must be managed according to a defined retention schedule. Not all content is a record — an internal draft document is not a record; a signed contract is. The distinction matters for retention, legal hold, and disposal governance.

```
RECORDS MANAGEMENT — KEY CONCEPTS

  OFFICIAL RECORD vs NON-RECORD
  ─────────────────────────────────────────────────────────
  RECORD:                              NON-RECORD:
  • Signed contracts                   • Working drafts
  • Board minutes                      • Personal notes
  • Regulatory submissions             • Duplicate copies
  • Financial statements               • Reference materials
  • Audit reports                      • Convenience copies
  • Customer correspondence (formal)   • Transient emails
  • HR employment agreements           • Blank forms

  RECORDS RETENTION SCHEDULE
  ─────────────────────────────────────────────────────────
  Maps each record type to:
  • Retention trigger (what starts the clock)
  • Retention period (how long to keep)
  • Retention authority (which law/regulation requires it)
  • Disposal method (secure delete, physical shred, archive)

  Malaysian Records Retention Examples:
  ──────────────────────────────────────────────────────────
  Record Type                 Period   Authority
  Audited financial accounts  7 years  Companies Act 2016
  Board resolutions           Permanent Companies Act 2016
  Customer KYC records        7 years  BNM AML/CFT guidelines
  Employee records            7 years  Employment Act 1955
  Tax records                 7 years  Income Tax Act 1967
  Contracts (commercial)      6 years  Limitation Act 1953
  Medical records             7 years  Private Healthcare Act
  National government records Varies   National Archives Act 2003

  RECORDS MANAGEMENT LIFECYCLE:
  Creation → Classification → Filing → Retrieval →
  Retention check → Legal hold check → Disposition
```

### 2.5 Taxonomy, Controlled Vocabulary, and Ontology

These three concepts form the information architecture of a content management system — the framework that allows content to be systematically organised, consistently described, and efficiently found.

```
VOCABULARY CONTROL CONCEPTS — HIERARCHY

  CONTROLLED VOCABULARY (Simplest)
  ─────────────────────────────────────────────────────────
  A defined, authorised list of terms used to describe
  and tag content. No relationships between terms.
  Purpose: Ensure consistent tagging — all documents about
  "human resources" are tagged "Human Resources" not "HR",
  "Personnel", "People Management", or "Workforce".

  Example: Document Type vocabulary:
  ["Policy", "Procedure", "Contract", "Report",
   "Correspondence", "Minutes", "Form", "Guideline"]
  → Only these values are allowed in the Document_Type field.

  TAXONOMY (Middle — hierarchical)
  ─────────────────────────────────────────────────────────
  A controlled vocabulary organised into a hierarchical
  classification structure (parent-child relationships).
  Purpose: Navigate content by browsing a topic hierarchy.

  Example: Business Function taxonomy:
  Finance
  ├── Accounting
  │   ├── Accounts Payable
  │   └── Accounts Receivable
  ├── Treasury
  │   ├── Cash Management
  │   └── FX Management
  └── Financial Reporting
      ├── Regulatory Reporting
      └── Management Reporting

  THESAURUS (Middle — relational)
  ─────────────────────────────────────────────────────────
  Controlled vocabulary with relationships between terms:
  Preferred terms, synonyms, broader/narrower terms.

  Example: "Personal Data" entry in a thesaurus:
  PREFERRED TERM: Personal Data
  SYNONYM: Personal Information, Private Data
  BROADER TERM: Data
  NARROWER TERM: Sensitive Personal Data, Biometric Data
  RELATED TERM: Data Subject, PDPA, Data Controller

  ONTOLOGY (Most complex — semantic)
  ─────────────────────────────────────────────────────────
  A formal representation of concepts, their properties,
  and the relationships between them — including complex
  semantic relationships beyond simple hierarchy.
  Purpose: Enable machine reasoning; knowledge graphs;
  AI-driven content discovery.

  Example: FIBO (Financial Industry Business Ontology) defines
  relationships between: Contract → Party → Obligation →
  Financial Instrument → Market → Regulator
  — enabling AI to reason about financial documents.

  FOLKSONOMY (User-driven — no control)
  ─────────────────────────────────────────────────────────
  Tags applied by users without a controlled vocabulary.
  Flexible but inconsistent. "HR", "Human Resources",
  "People", "Personnel" all exist simultaneously.
  Used in: social media, internal wikis, informal tagging.
  Problem: Inconsistent; ambiguous; retrieval is unreliable.
```

### 2.6 Metadata for Content — Describing the Document

Content metadata is the structured information that describes a document — enabling search, classification, retention enforcement, and access control. DAMA Chapter 9 distinguishes three metadata types for content:

**Descriptive metadata** — Describes what the content is about, enabling discovery and search. Examples: title, subject, keywords, abstract, author, date, language, content type.

**Structural metadata** — Describes the internal structure and relationships of content. Examples: table of contents, page count, embedded objects, document version, document relationships (this contract supersedes that contract).

**Administrative metadata** — Supports management of the content asset: access rights, retention category, disposal date, legal hold status, format, file size, checksum (for integrity verification).

```
METADATA SCHEMA EXAMPLE — MAYBANK CONTRACT DOCUMENT

  DESCRIPTIVE METADATA
  ──────────────────────────────────────────────
  Title:          "Customer Loan Agreement — Residential"
  Document_Type:  Contract
  Subject:        Residential Mortgage; Housing Loan
  Keywords:       mortgage, residential, property, loan agreement
  Author:         Retail Banking Division
  Creation_Date:  2024-03-15
  Language:       English / Bahasa Malaysia (bilingual)

  STRUCTURAL METADATA
  ──────────────────────────────────────────────
  Version:        2.1 (supersedes v2.0 dated 2023-01-01)
  Related_Docs:   Customer_KYC_Record_ACC-001234,
                  Property_Valuation_Report_PRO-5678
  Page_Count:     24
  Format:         PDF/A (archival format)
  Checksum:       SHA-256: a1b2c3d4...

  ADMINISTRATIVE METADATA
  ──────────────────────────────────────────────
  Classification:       RESTRICTED
  Retention_Category:   Loan_Agreement
  Retention_Trigger:    Loan_Closure_Date
  Retention_Period:     7 years post closure
  Disposal_Date:        [Auto-calculated on closure]
  Legal_Hold_Status:    None
  Access_Group:         Retail_Banking_Officers, Legal_Team
  Storage_Location:     ECM_Production/Contracts/Mortgage/2024/
  PDPA_Contains_PII:    Yes (customer NRIC, address, income)
  DPO_Review_Required:  Yes (on disposal)
```

### 2.7 Legal Hold / Litigation Hold

A **legal hold** (also called a litigation hold) is a formal instruction to suspend the normal retention and disposal schedule for records that may be relevant to actual or anticipated legal proceedings, regulatory investigations, or internal investigations.

```
LEGAL HOLD PROCESS

  TRIGGER EVENT
  → Litigation threatened or commenced
  → Regulatory investigation opened (BNM, MACC, SC)
  → Internal investigation authorised by Board
       │
       ▼
  HOLD NOTICE ISSUED
  → General Counsel / Legal team issues formal Hold Notice
  → Specifies: scope (what records), custodians (who holds them),
    date range, legal matter reference
       │
       ▼
  HOLD APPLIED IN SYSTEMS
  → Records Management System: Suspension flag set on affected records
  → Normal retention/disposal jobs BYPASS records with active holds
  → Email archive: Custodian mailboxes placed under hold
  → Shared drives: Folders flagged; automated deletion disabled
       │
       ▼
  HOLD MAINTAINED
  → Custodians notified of their preservation obligation
  → Regular reminders issued (hold does not expire automatically)
  → New records created that fall within scope are also held
       │
       ▼
  HOLD RELEASED
  → Legal team confirms matter is resolved
  → General Counsel issues formal Hold Release notice
  → Records management system lifts suspension flag
  → Normal retention schedule resumes
  → Records that are now past their retention period are
    queued for disposal (they were preserved, not extended)
       │
       ▼
  POST-HOLD AUDIT
  → Document what was held, for how long, and under which matter
  → Confirm no records were improperly disposed during hold period
```

### 2.8 E-Discovery

**E-discovery** (electronic discovery) is the process of identifying, preserving, collecting, processing, reviewing, and producing electronically stored information (ESI) in response to legal proceedings or regulatory requests. In Malaysia, e-discovery obligations arise in:

- Civil litigation (the Rules of Court 2012 require disclosure of relevant electronic records)
- Securities Commission investigations
- MACC (Malaysian Anti-Corruption Commission) investigations
- BNM regulatory examinations requiring transaction and communication records

E-discovery capability requires: a searchable archive of all relevant content types (email, documents, instant messages), the ability to search across all custodians by date range, keyword, and metadata, and legal hold capability to preserve materials during proceedings.

---

## Section 3: Real-World Scenarios — Malaysian Context

### Scenario 1: Maybank — ECM Implementation for Loan Documentation Compliance

**Business Context:**
Maybank processes approximately 8,000 residential mortgage applications per month. Each application generates 15–20 documents: application forms, NRIC copies, salary slips, EPF statements, property valuations, legal agreements, and insurance policies. These were stored in a mix of physical files, scanned PDFs on shared drives, and email attachments — with no consistent naming convention, no version control, and no automated retention management.

**The Content Management Challenge:**

A BNM examination found three categories of findings:
1. Loan agreements from 2017 could not be produced within the required 24-hour window — they were on a decommissioned server.
2. Some customer documents (NRIC copies, salary slips) existed in uncontrolled email folders on individual officers' mailboxes — not subject to the bank's PDPA controls.
3. Multiple versions of the standard loan agreement template were in circulation — three branches were using an outdated template that did not include a required BNM disclosure clause.

**ECM Solution Design:**

```
MAYBANK LOAN DOCUMENTATION ECM ARCHITECTURE

  CONTENT TAXONOMY (Loan Processing Domain)
  ──────────────────────────────────────────────────────
  Mortgage Loans
  ├── Application Documents
  │   ├── Application Form (latest version only)
  │   ├── Income Verification
  │   │   ├── Salary Slip (3 months)
  │   │   └── EPF Statement
  │   └── Identity Documents
  │       ├── NRIC (front + back)
  │       └── Passport (non-citizens)
  ├── Property Documents
  │   ├── SPA (Sale & Purchase Agreement)
  │   ├── Property Valuation Report
  │   └── Land Title (certified copy)
  ├── Legal Agreements
  │   ├── Loan Agreement (governed template: v3.2 CURRENT)
  │   ├── Letter of Offer
  │   └── Deed of Assignment
  └── Insurance
      ├── MRTA / MLTT Policy
      └── Fire Insurance Certificate

  METADATA ENFORCEMENT AT CAPTURE:
  ──────────────────────────────────────────────────────
  Mandatory metadata on all documents:
  • Account_Number (links to core banking)
  • Document_Type (from controlled vocabulary)
  • Customer_IC (triggers PDPA controls)
  • Capture_Date (auto-populated)
  • Captured_By (authenticated user ID)
  • Branch_Code
  → Documents without complete metadata rejected at upload

  TEMPLATE GOVERNANCE:
  ──────────────────────────────────────────────────────
  • Loan Agreement template v3.2 is the SINGLE MASTER copy
  • All branches access template from ECM (not local drive)
  • Superseded versions are archived (visible but not editable)
  • Legal team controls the template — only they can publish new versions
  • Version publication triggers automatic notification to all branch managers

  RETENTION AUTOMATION:
  ──────────────────────────────────────────────────────
  On LOAN_CLOSURE event in core banking:
  → Core banking API triggers ECM retention workflow
  → All loan documents tagged: Disposal_Date = Closure_Date + 7 years
  → DPO notification scheduled at T-30 days before disposal
  → On disposal date: Legal hold check → DPO approval → Secure delete
  → Disposal certificate generated and archived permanently
```

**BNM RMIT + PDPA Link:** The ECM system creates a complete, searchable, governed record of every loan document. BNM examination requests can be fulfilled within hours (not days). PDPA Data Subject Access Requests are serviced from the ECM — all personal data related to a customer can be located across the entire loan file in minutes, not weeks.

---

### Scenario 2: LHDN — Records Management for National Tax Records

**Business Context:**
LHDN (Inland Revenue Board) holds the tax records of every Malaysian individual and company. Under the Income Tax Act 1967, tax records must be retained for 7 years. Under the National Archives Act 2003, government records with permanent historical or administrative value must be transferred to Arkib Negara Malaysia (National Archives) rather than disposed of. LHDN's Records Management programme must balance these dual obligations.

**Records Classification Framework:**

```
LHDN RECORDS CLASSIFICATION AND RETENTION

  RECORD CATEGORY         RETENTION   AUTHORITY        FINAL DISPOSITION
  ──────────────────────────────────────────────────────────────────────
  Individual tax returns  7 years     Income Tax Act   Dispose (secure)
  Corporate tax returns   7 years     Income Tax Act   Dispose (secure)
  Tax audit reports       10 years    LHDN Policy      Dispose (secure)
  Court judgements        Permanent   National         Transfer to
  (tax disputes)                      Archives Act     Arkib Negara
  Landmark tax rulings    Permanent   National         Transfer to
  (policy precedent)                  Archives Act     Arkib Negara
  Board minutes           Permanent   National         Transfer to
  (Director General)                  Archives Act     Arkib Negara
  Staff HR records        7 years     Employment Act   Dispose (secure)
  after separation
  IT audit logs           3 years     LHDN Policy      Dispose (secure)
  e-Filing transaction    7 years     Income Tax Act   Dispose (secure)
  logs

  LEGAL HOLD TRIGGERS:
  • Active tax audit (record held for audit duration + 3 years)
  • Active court proceeding (record held until final judgment)
  • MACC investigation referral (record held until cleared)

  NATIONAL ARCHIVES ACT 2003:
  Government bodies must:
  1. Maintain a File Plan (classification scheme for all records)
  2. Notify Arkib Negara before disposing of any records
  3. Transfer records of permanent value to Arkib Negara
  4. Obtain approval before destroying any government records
```

**Digital Preservation Challenge:**
LHDN's e-Filing system has been operational since 2004. Tax returns from 2004 were submitted in XLS format. By 2024, Microsoft Excel has changed significantly and some legacy formats are not guaranteed to open correctly. Digital preservation requires migrating records from obsolete formats to archival standards:
- **PDF/A** (ISO 19005) — archival PDF format designed to remain readable indefinitely, with embedded fonts and no external dependencies
- **XML** — structured text format readable by any future system without proprietary software
- **TIFF** — archival image format for scanned physical documents

**CDMP Link:** This scenario tests records management principles, the distinction between retention-driven disposal and permanent archival transfer, legal hold application, and digital preservation standards.

---

### Scenario 3: Sime Darby — Managing Unstructured Content Across a Diversified Conglomerate

**Business Context:**
Sime Darby operates across five divisions (Motors, Plantation, Industrial, Logistics, Healthcare) in 18 countries. The Group faces a common GLC challenge: each division independently manages its own documents using different systems (SharePoint, Google Drive, local file servers, email), with no enterprise taxonomy, no consistent naming conventions, and no group-level search. Legal discovers during due diligence for an acquisition that a critical joint venture agreement cannot be located — it exists somewhere in three different divisional systems.

**Information Architecture Design:**

```
SIME DARBY ENTERPRISE CONTENT TAXONOMY (Top Level)

  Sime Darby Group
  ├── Corporate Governance
  │   ├── Board & Board Committees (permanent records)
  │   ├── Shareholder Meetings (permanent records)
  │   ├── Regulatory Filings (Bursa, Securities Commission)
  │   └── Group Policies & Procedures
  ├── Finance & Treasury
  │   ├── Audited Financial Statements
  │   ├── Treasury Instruments
  │   └── Tax Records
  ├── Legal & Contracts
  │   ├── Corporate Contracts (JVA, MOA, SHA)
  │   ├── Property & Leases
  │   ├── IP & Trademarks
  │   └── Litigation Files
  ├── Operations (sub-divided by division)
  │   ├── Sime Darby Motors
  │   ├── Sime Darby Plantation
  │   ├── Sime Darby Industrial
  │   ├── Sime Darby Logistics
  │   └── Sime Darby Healthcare
  └── Human Resources
      ├── Employment Contracts (classified: CONFIDENTIAL)
      ├── Group HR Policies
      └── Training Records

  FEDERATED SEARCH:
  Enterprise search engine indexes content across all divisional
  ECM systems. A legal team search for "Sarawak Joint Venture" returns
  results from ALL divisional systems, ranked by relevance, with
  metadata showing system, owner, date, and classification.

  PDPA CONTROLS ON UNSTRUCTURED CONTENT:
  Documents tagged as containing personal data (employee contracts,
  customer correspondence, medical records in Healthcare division)
  trigger additional access controls:
  → Only authorised roles can download (not just view)
  → Downloads logged with user, timestamp, and justification
  → Bulk export of personal data documents requires DPO approval
```

**Companies Act 2016 Link:** Under Section 245 of the Companies Act 2016, every company must keep its accounting records, minute books, and registers at its registered office and retain them for 7 years. Sime Darby's ECM governance ensures Board minutes (permanent), financial records (7 years), and contracts (contract period + 6 years under Limitation Act) are systematically managed.

---

## Section 4: Visual Diagrams + Cheat Sheet

### 4.1 Content Governance Framework

```
CONTENT GOVERNANCE FRAMEWORK

  POLICY LAYER (Data Governance)
  ──────────────────────────────────────────────────────────
  • Records Retention Schedule (what, how long, disposal method)
  • Content Classification Policy (what classification each type gets)
  • Access Control Policy (who can access which content categories)
  • Naming Convention Standards (folder structure, file naming)
  • Template Governance (who owns master templates; how published)

  PROCESS LAYER
  ──────────────────────────────────────────────────────────
  Create → Apply metadata → File to taxonomy → Access control
  → Review/update → Retain → Legal hold check → Dispose

  TECHNOLOGY LAYER
  ──────────────────────────────────────────────────────────
  ECM Platform (SharePoint / OpenText / Laserfiche)
  + Records Management Module (retention enforcement)
  + E-discovery / Legal Hold Module
  + Enterprise Search (full-text + metadata)
  + Email Archive (Outlook / Exchange compliance archive)

  STEWARDSHIP LAYER
  ──────────────────────────────────────────────────────────
  Content Owner: Accountable for accuracy of content
  Records Manager: Manages retention schedules and disposal
  Information Architect: Owns taxonomy and metadata standards
  DPO: Reviews disposal of PDPA-regulated content
  Legal Counsel: Manages legal holds and e-discovery requests
```

### 4.2 Taxonomy vs Folksonomy — The Governance Trade-off

```
TAXONOMY vs FOLKSONOMY

  TAXONOMY (Governed)              FOLKSONOMY (User-driven)
  ─────────────────────────        ──────────────────────────
  Defined by Information Architect  Defined by users as they tag
  Controlled vocabulary            Free text; no control
  Hierarchical structure           Flat tag list
  Consistent: "Policy" always      Inconsistent: "Policy",
  means Policy                     "Policies", "POL", "SOP"
  Findable: browse the hierarchy   Variable: depends on tagger
  Maintainable: central ownership  Unmanageable at scale
  Slow to build                    Fast to start
  Required for: regulatory records Fine for: internal wikis,
  compliance, legal hold, PDPA     knowledge sharing, innovation

  BEST PRACTICE: Use both.
  Taxonomy for GOVERNED content (records, contracts, policies)
  Folksonomy for COLLABORATIVE content (team wikis, brainstorming)
  The ECM system enforces taxonomy for records; allows folksonomy
  for informal knowledge content.
```

### 4.3 Version Control for Documents

```
DOCUMENT VERSION CONTROL — STANDARDS

  VERSION NUMBERING CONVENTION:
  Major.Minor.Draft → e.g., v2.1.3

  2   = Major version (significant content change; re-approval required)
  .1  = Minor version (editorial corrections; no re-approval)
  .3  = Draft iteration (not yet approved; internal use only)

  STATUS STATES:
  DRAFT     → Work in progress; version = 0.x.y or x.y.z
  PENDING   → Submitted for approval; locked from editing
  APPROVED  → Current official version; all others superseded
  SUPERSEDED → Older official version (retained for reference/audit)
  OBSOLETE  → No longer valid; must not be used; retained per retention

  EXAMPLE — Loan Agreement Template Version History:
  v1.0 APPROVED  2019-01-15  Initial BNM disclosure template
  v1.1 SUPERSEDED 2020-03-01  Minor corrections
  v2.0 SUPERSEDED 2022-07-01  PDPA 2022 amendment clauses added
  v2.1 SUPERSEDED 2023-06-15  Interest rate disclosure update
  v3.0 SUPERSEDED 2024-01-01  New BNM Open Finance clauses
  v3.1 APPROVED  2024-08-01  Current version ← ALL BRANCHES USE THIS
  v3.2 DRAFT     2024-10-10  Pending for 2025 regulatory update

  POLICY: Only APPROVED versions are distributed.
  SUPERSEDED versions are archived (read-only) for audit.
  OBSOLETE versions are clearly marked and not searchable by default.
```

### 4.4 Cheat Sheet — Chapter 9 Key Terms

| Term | One-Line Definition | Exam Trap |
|---|---|---|
| **Unstructured Data** | Data with no predefined schema (documents, emails, images) | ~80% of enterprise data is unstructured — not the minority |
| **Semi-structured data** | Has some structure but not rigid schema (XML, JSON, HTML) | Between structured DB data and fully unstructured documents |
| **ECM** | Enterprise Content Management — unified platform for all content types | ECM includes DMS + RMS + workflow + collaboration |
| **DMS** | Document Management System — version control, workflow, access for documents | Focused on documents specifically, not all content types |
| **RMS** | Records Management System — enforces retention schedules and disposal | Records have legal weight; not all documents are records |
| **DAM** | Digital Asset Management — rich media files with rights management | Rights management is DAM-specific (not in DMS) |
| **Controlled Vocabulary** | Authorised list of terms for consistent content tagging | No hierarchy; flat list only — compare to taxonomy |
| **Taxonomy** | Hierarchical classification structure for content | Has parent-child relationships; not just a flat list |
| **Folksonomy** | User-generated free-form tags without control | Fast to start; inconsistent at scale; not for governed records |
| **Ontology** | Formal semantic model of concepts and their complex relationships | Most complex; enables machine reasoning and AI discovery |
| **Record** | Content serving as evidence of a business activity requiring managed retention | Not all documents are records; records have defined retention |
| **Retention Schedule** | Policy mapping record types to retention periods and disposal methods | Driven by law, regulation, contract, and business need |
| **Legal Hold** | Suspension of normal retention/disposal due to legal proceedings | Holds suspend disposal — they do not extend retention periods |
| **E-discovery** | Process of identifying and producing ESI for legal proceedings | Requires searchable archive + legal hold capability |
| **Metadata (content)** | Descriptive + Structural + Administrative metadata for content | Metadata enables search, retention enforcement, and access control |
| **PDF/A** | ISO 19005 archival PDF format — self-contained, long-term readable | Preferred format for digital preservation of official records |
| **National Archives Act 2003** | Malaysian law governing retention and transfer of government records | Government records of permanent value must go to Arkib Negara |
| **Companies Act 2016** | Requires companies to retain accounting records and minutes for 7 years | Section 245 applies to all Sdn Bhd and Berhad companies |

### 4.5 CDMP Exam Traps — Chapter 9

```
COMMON EXAM TRAPS — DOCUMENT & CONTENT MANAGEMENT

  TRAP 1: PDPA applies only to databases
  ───────────────────────────────────────
  "Documents and emails are not subject to PDPA because
   they are not stored in a database."
  → FALSE. PDPA 2010 applies to ALL personal data regardless
    of format. A PDF containing a customer's NRIC is subject
    to the same PDPA obligations as a database record.

  TRAP 2: Legal hold = extended retention period
  ──────────────────────────────────────────────
  "A legal hold extends the retention period for affected
   records."
  → FALSE. A legal hold SUSPENDS disposal during the hold.
    When the hold is lifted, the normal retention schedule
    resumes. Records past their retention period at hold
    release are queued for disposal — the hold did not extend
    their retention period.

  TRAP 3: All documents are records
  ───────────────────────────────────
  "Every document in the organisation is a record and
   must be managed under the records retention schedule."
  → FALSE. Only documents serving as evidence of business
    activities, decisions, or transactions are records.
    Working drafts, personal notes, and duplicate copies
    are non-records and can be disposed of freely.

  TRAP 4: Taxonomy vs ontology
  ──────────────────────────────
  "An ontology is simply a more detailed taxonomy."
  → FALSE. A taxonomy is a hierarchical classification.
    An ontology is a formal semantic model with complex
    relationships (not just parent-child) that enables
    machine reasoning. They are fundamentally different
    in purpose and complexity.

  TRAP 5: Folksonomy is sufficient for governance
  ─────────────────────────────────────────────────
  "User-generated tags (folksonomy) provide adequate
   content organisation for compliance purposes."
  → FALSE. Folksonomy is inconsistent and ungoverned.
    Regulated records (financial, legal, HR) require a
    controlled vocabulary or taxonomy to ensure consistent
    classification and reliable retention enforcement.

  TRAP 6: Digital format = permanent preservation
  ─────────────────────────────────────────────────
  "Scanning physical documents to PDF ensures their
   permanent preservation."
  → FALSE. Standard PDFs may become unreadable if fonts,
    plugins, or software dependencies become unavailable.
    Long-term digital preservation requires archival formats
    (PDF/A, TIFF, XML) that are self-contained and
    standards-based.
```

---

## Section 5: Official DAMA Images

### DAMA Document & Content Management Knowledge Area Context Diagram

*Source: DAMA International, DAMA-DMBOK2 Knowledge Area Context Diagram Series*
*License: Creative Commons CC BY-ND 4.0 | © DAMA International*

![DAMA Document & Content Management KA Context Diagram](https://dama.org/wp-content/uploads/sites/2326/2025/04/x-5.png.webp)

> **Reading the context diagram:** Document & Content Management receives inputs from Data Governance (retention policies, classification standards) and Data Security (access controls for content). Its outputs include governed repositories, searchable content archives, and compliance records for legal and regulatory purposes. Note that Metadata Management (Chapter 12) is deeply interconnected — content metadata is both a product of DCM governance and a consumer of the enterprise metadata framework.

*Note: If the image above does not render, refer to Day01 Section 5 for the complete DAMA KA gallery.*

---

## Chapter 9 at a Glance — One-Page Summary

```
DOCUMENT & CONTENT MANAGEMENT — CDMP EXAM SUMMARY
══════════════════════════════════════════════════════════════

WHAT:   Technologies, processes, and governance for content
        stored outside relational databases (~80% of enterprise data)

CONTENT TYPES:
  Structured   → DB rows/columns (Chapters 5-8)
  Semi-struct  → XML, JSON, HTML (bridge)
  Unstructured → Documents, emails, images, video, audio

SYSTEM TYPES:
  DMS  → Document lifecycle: version control, workflow, access
  RMS  → Records: retention schedules, legal hold, disposal
  ECM  → Unified: DMS + RMS + workflow + collaboration
  DAM  → Rich media: images/video with rights management
  WCM  → Web content: non-technical authoring + publishing

CONTENT LIFECYCLE:
  Create → Store/Organise → Access/Use → Maintain →
  Archive → Dispose (with retention + legal hold checks)

VOCABULARY CONTROL:
  Controlled Vocabulary → Flat authorised term list
  Taxonomy             → Hierarchical classification
  Thesaurus            → Preferred terms + relationships
  Ontology             → Semantic model; machine reasoning
  Folksonomy           → User tags; inconsistent; not for records

RECORDS MANAGEMENT:
  Record = evidence of business activity → managed retention
  Non-record = draft, personal note, duplicate → dispose freely
  Retention Schedule: type → trigger → period → disposal method
  Legal Hold: SUSPENDS disposal (does not extend retention)

KEY MALAYSIAN REGULATIONS:
  National Archives Act 2003 → Government records → Arkib Negara
  Companies Act 2016 S.245   → 7-year retention for accounts/minutes
  Income Tax Act 1967        → 7-year retention for tax records
  PDPA 2010                  → Applies to personal data in ALL formats

METADATA FOR CONTENT: Descriptive + Structural + Administrative
DIGITAL PRESERVATION: PDF/A, TIFF, XML (archival formats)
E-DISCOVERY: Identify + preserve + collect + produce ESI for legal

EXAM WEIGHT: ~6%
══════════════════════════════════════════════════════════════
```

---
