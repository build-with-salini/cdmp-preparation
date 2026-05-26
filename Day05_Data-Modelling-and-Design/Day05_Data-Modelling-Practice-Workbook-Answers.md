# Day 05 — Data Modelling & Design Practice Workbook: Model Answers

**DAMA-DMBOK2 Chapter 5 | CDMP Exam Aligned**
**Study Plan:** Day 5 of 17 | Knowledge Area Weight: ~11%
**Malaysian Context:** PDPA 2010, BNM RMIT 2020, MyDIGITAL Blueprint, GLC data platforms

---

> **How to use this file:**
> Each workbook question is answered at four levels:
> 1. **Model Answer** — exam-ready, concise, DAMA-precise
> 2. **Expanded Analysis** — deeper explanation with frameworks and nuance
> 3. **Malaysian Context** — localised scenario connecting to M'sian regulations and industries
> 4. **CDMP Exam Angle** — what the exam tests, common traps, key terms to remember

---

## Section 1: Business Drivers for Data Modeling

---

### Q1 — List three business goals that depend on strong data models

**Model Answer:**

1. **Regulatory Compliance and Auditability** — Data models define what personal and financial data is held, where it lives, how it is structured, and what rules govern it. This structural clarity is a prerequisite for demonstrating compliance with regulations such as PDPA 2010, BNM RMIT 2020, and BCBS 239. Regulators cannot audit what cannot be described — and data models are the most precise description of an organisation's data.

2. **Data Quality Measurement and Enforcement** — A data model defines what constitutes valid data: required attributes, data types, allowed values, referential integrity rules, and business constraints. Without a model, there is no objective standard against which to measure quality — and no mechanism to enforce it at the database layer. Strong models embed quality rules as structural constraints, preventing bad data from entering at the source.

3. **Cross-System Reporting and Analytics** — Every report that aggregates data from multiple systems depends on common data definitions. If "Revenue" means different things in the finance system and the CRM, reports will always contradict each other. A strong enterprise data model — with consistent entity definitions, attribute names, and business rule encoding — is the foundation on which trustworthy cross-system analytics are built.

**Expanded Analysis:**

DAMA-DMBOK2 makes a strong claim: *the data model is the most important data management artefact after the data itself.* This is because the model is simultaneously a communication tool (shared vocabulary between business and technology), a governance document (formalised business rules), and a quality enforcement mechanism (structural constraints). Without a model, data management activities — governance, quality, security, lineage — lack a common reference point.

A fourth business driver worth noting is **system integration**: when systems exchange data, they need an agreed contract for what each field means, its format, and its valid values. The canonical data model (Chapter 4) is the output of data modelling applied to the integration domain.

**Malaysian Context:**

In Malaysia's financial sector, BNM RMIT 2020 requires banks to identify and document Critical Data Elements (CDEs) — the specific data fields that underpin regulatory reporting and risk management. Identifying CDEs is fundamentally a data modelling activity: it requires knowing what entities exist, what attributes they carry, and which attributes drive regulatory decisions. A bank without a governed data model cannot reliably identify its CDEs, and therefore cannot meet RMIT's documentation requirements.

Under PDPA 2010, Section 6 requires organisations to process personal data only for the purpose for which it was collected. Data modelling supports this by explicitly identifying which entities contain personal data, what purpose each attribute serves, and whether any attribute is surplus to requirements (data minimisation). The model becomes the evidence base for PDPA compliance.

**CDMP Exam Angle:**

- The exam often asks: *"What is the primary purpose of data modelling?"* — The correct answer is **formalising business requirements** and **creating a shared vocabulary**, not database design or performance optimisation.
- Know the connection: data model → data quality rules → data quality measurement. These three form a dependency chain tested across Chapters 5 and 13.
- Business goals are always the *why* behind modelling. The exam tests whether candidates understand that modelling serves the business, not the technology team.

---

### Q2 — Describe one example where poor modeling creates confusion

**Model Answer:**

A Malaysian retail bank has three separate systems — a core banking system, a CRM, and a mobile banking app — each with its own "Customer" entity. The core banking system records customer status as a numeric code (1 = Active, 2 = Dormant, 3 = Closed). The CRM uses text strings ("Active," "Inactive," "Churned"). The mobile app uses a boolean field (is_active: true/false). When the risk team runs a monthly active customer count for BNM regulatory reporting, they get three different numbers depending on which system they query. No one can agree which number is correct because no one has modelled what "active customer" means at the enterprise level — there is no shared entity definition, no canonical attribute, and no authoritative source.

**Expanded Analysis:**

This is an example of **semantic heterogeneity** — the same real-world concept represented with different structures, values, and meanings across systems. It is one of the most destructive consequences of poor or absent data modelling. The cost is not just analytical confusion; it creates compliance risk (which number goes to BNM?), operational risk (are dormant accounts included in marketing campaigns?), and trust erosion (leadership stops believing in the data).

```
POOR MODELLING IMPACT CHAIN

  Poor model             →  Inconsistent definitions
  (or no model)          →  Multiple "truths" per concept
                         →  Manual reconciliation by analysts
                         →  Report discrepancies in governance forums
                         →  Leadership loses trust in data
                         →  Decisions made on gut feel
                         →  Regulatory risk (wrong reporting numbers)
```

The root cause is the absence of an Enterprise Logical Data Model that defines "Customer" once, authoritatively, with a declared System of Record. Every downstream system derives its customer concept from this canonical definition — it does not reinvent it.

**Malaysian Context:**

This scenario plays out regularly in Malaysian banks that grew through acquisition. When CIMB acquired Southern Bank and Bumiputra-Commerce Bank, the merged entity had multiple customer master tables with incompatible status codes, identifier schemes, and name formats. Resolving this required a formal data modelling programme — defining the enterprise customer entity, mapping each source system's attributes to the canonical model, and designating a single authoritative source.

For GLCs with subsidiaries (e.g., Sime Darby's divisional structure or Petronas's upstream/downstream split), the same problem emerges at group level: each subsidiary models its customers, products, or assets independently, making group-level analytics structurally impossible without a unifying enterprise model.

**CDMP Exam Angle:**

- This scenario is a classic exam setup. When you see "analysts spend weeks reconciling" or "reports give different numbers" — the root cause is **poor or absent data modelling** (specifically: no enterprise entity definition, no canonical model, no authoritative source).
- The solution is always: enterprise data model → canonical definitions → authoritative source designation → governance of the model.
- Know the term **semantic heterogeneity** — it may appear as an exam option.

---

## Section 2: Data Modelling Principles

---

### Q3 — Explain the principle of 'clarity' in your own words

**Model Answer:**

Clarity in data modelling means that every element of the model — every entity name, attribute name, relationship label, and business rule — is unambiguous to its intended audience. A model with clarity can be read and understood by both business stakeholders (who validate that it reflects their reality) and technical implementers (who build from it) without needing the modeller present to explain it. Clarity is achieved through precise naming, explicit definitions attached to every element, consistent notation, and an appropriate level of detail for the model's purpose.

**Expanded Analysis:**

Clarity operates at three levels simultaneously:

**Naming clarity** — Entity and attribute names should be self-explanatory. "Customer" is clear; "Party" may require explanation. "IC_Number" is clearer than "field_47" or "cust_ref_code." Abbreviations and codes that are internal to the modelling team destroy clarity for business stakeholders. A naming standard that prioritises business language over technical shorthand improves clarity.

**Definition clarity** — Every entity and attribute should carry a written definition that states what it represents, what it does not include, and any governing rule. The definition for "Active Customer" in a bank might be: "A customer who has conducted at least one financial transaction within the preceding 90 days and whose account is not flagged as Dormant or Closed per the Account Status reference table." This definition eliminates the ambiguity in the poor modelling example above.

**Visual clarity** — The diagram layout should communicate structure intuitively. Related entities should be spatially grouped. Crossing lines should be minimised. The legend should be visible. A model diagram that requires 30 minutes of explanation before the audience can read it lacks visual clarity.

```
CLARITY — THREE LAYERS

  ┌─────────────────────────────────────────┐
  │  NAMING CLARITY                         │
  │  Business language; no cryptic codes;   │
  │  no unexplained abbreviations           │
  └─────────────────────────────────────────┘
  ┌─────────────────────────────────────────┐
  │  DEFINITION CLARITY                     │
  │  Every entity and attribute has a       │
  │  written definition with scope,         │
  │  exclusions, and governing rules        │
  └─────────────────────────────────────────┘
  ┌─────────────────────────────────────────┐
  │  VISUAL CLARITY                         │
  │  Layout communicates structure;         │
  │  minimal crossing lines; visible legend;│
  │  appropriate level of detail            │
  └─────────────────────────────────────────┘
```

**Malaysian Context:**

In Malaysian organisations, clarity has an additional dimension: **multilingual clarity**. Many GLCs operate in both Bahasa Malaysia and English, and technical entities defined only in English may be misunderstood by business stakeholders who think in BM. A data model for a government agency (e.g., JPN, LHDN) may need entity definitions in both languages. The principle of clarity requires the model to be understandable by its actual audience — not just by the modeller's preferred language.

Maybank's data governance programme includes a requirement that all data model elements in the enterprise data dictionary carry both an English and a simplified Malay description — ensuring that branch-level business users can validate the model against their operational reality.

**CDMP Exam Angle:**

- Clarity is one of DAMA's five data model quality dimensions alongside completeness, correctness, consistency, and precision.
- The exam may describe a scenario where "the model exists but business stakeholders cannot validate it" — this is a **clarity failure** (comprehensibility), not a correctness problem.
- Know the difference: **completeness** = all elements present; **clarity/comprehensibility** = all elements understandable. A complete model can still be unclear.

---

### Q4 — Provide one example of how consistency improves a model

**Model Answer:**

A bank adopts an enterprise naming standard: all primary key attributes must follow the pattern `[EntityName]_ID` (e.g., `Customer_ID`, `Account_ID`, `Product_ID`), and all date attributes must follow the pattern `[EventName]_Date` (e.g., `Open_Date`, `Close_Date`, `Birth_Date`). Before this standard, the five development teams had used `CustNum`, `cust_id`, `customerIdentifier`, `CUST_NO`, and `Customer_Key` interchangeably. After adopting the standard, every data modeller, every developer, and every analyst immediately recognises the primary key of any entity without reading the documentation — reducing errors in join logic and integration code.

**Expanded Analysis:**

Consistency in data modelling operates across three dimensions:

**Intra-model consistency** — Within a single model, the same concept should be represented the same way every time. If "Status" is modelled as an ENUM in the Customer entity, it should be an ENUM everywhere, not a VARCHAR in the Account entity and a BIT in the Product entity.

**Inter-model consistency** — Across all models in the enterprise, shared entities should be defined identically. "Customer" in the CRM model and "Customer" in the loan model should have the same primary key, the same attribute definitions, and the same cardinality rules. Inconsistency across models is the root cause of integration complexity.

**Temporal consistency** — The model should remain consistent with itself as it evolves. When an entity is renamed or an attribute is deprecated, the change must be propagated through all models that reference it. Model governance processes (change control, version management) enforce temporal consistency.

**Malaysian Context:**

Bank Negara Malaysia's RMIT framework requires banks to maintain a documented inventory of Critical Data Elements (CDEs) with consistent definitions across all systems. Consistency in the data model directly enables CDE compliance: if "Account Balance" is defined consistently as "the net ledger balance in MYR at end-of-business on the reporting date" across all models, the CDE definition can be enforced at every point of measurement. Inconsistent models make CDE enforcement impossible — each system would interpret "balance" differently.

**CDMP Exam Angle:**

- Consistency is often tested in the context of **enterprise data models** — the exam may ask what quality dimension is violated when the same entity is defined differently in two related models. Answer: **consistency**.
- Know the distinction: consistency is about sameness across model elements; correctness is about accuracy of individual elements. A model can be internally consistent but still incorrect (e.g., consistently wrong cardinality).
- The exam may also link consistency to **metadata management** (Chapter 10) — the data dictionary is the tool that enforces consistency by providing a single authoritative definition for each model element.

---

## Section 3: Planning a Modelling Effort

---

### Q5 — Define the scope for a modelling effort you know

**Model Answer — Scope: Maybank e-KYC Customer Onboarding Model**

**Project Name:** Enterprise Customer Identity Logical Data Model — e-KYC Programme
**Trigger:** Regulatory requirement (BNM CDD guidelines) + PDPA 2010 compliance gap
**Scope Statement:**

```
MODELLING SCOPE DEFINITION

  IN SCOPE
  ────────────────────────────────────────────────────────
  ✓ Customer Identity subject area (Individual + Corporate)
  ✓ All attributes required for BNM CDD compliance
  ✓ PDPA consent tracking (consent type, timestamp, channel,
    withdrawal record)
  ✓ Customer-to-Account relationship (logical model only)
  ✓ Source-of-Funds and Risk Rating attributes
  ✓ Cross-reference to existing Core Banking System customer IDs
  ✓ Canonical customer exchange model for API integration

  OUT OF SCOPE
  ────────────────────────────────────────────────────────
  ✗ Physical database design (separate DBA deliverable)
  ✗ Product and Account subject areas (separate modelling track)
  ✗ Customer behavioural / transaction history
  ✗ Credit scoring model (separate analytics track)
  ✗ Integration with third-party eKYC vendor (covered by
    architecture design, not data modelling)

  MODEL LEVELS TO PRODUCE
  ────────────────────────────────────────────────────────
  → Conceptual: Subject area map (for governance sign-off)
  → Logical:    Full entity-attribute model (primary deliverable)
  → Physical:   Excluded from this phase

  NOTATION STANDARD
  ────────────────────────────────────────────────────────
  → Crow's Foot ERD notation
  → Tooling: erwin Data Modeler (enterprise standard)
  → Version control: Stored in enterprise model repository

  SUCCESS CRITERIA
  ────────────────────────────────────────────────────────
  → Validated by: BNM compliance team + Chief Data Steward
  → Completeness: All CDD-required attributes represented
  → Correctness: Zero outstanding disputes from business walkthrough
  → Timeline: 6-week delivery; business review in Week 4
```

**Expanded Analysis:**

A well-defined scope prevents two common modelling failures: **scope creep** (the model grows to cover everything, becomes unmanageable, and is never finished) and **scope gap** (critical requirements are missed because they were not explicitly included). DAMA recommends defining scope along four dimensions: subject areas covered, model levels to be produced, systems in scope, and regulatory/business requirements to be satisfied.

The scope definition is also a governance document — it records what was deliberately excluded and why, so that future requests to expand the model can be assessed against the original rationale rather than reopening settled decisions.

**Malaysian Context:**

In Malaysian bank regulatory programmes, scoping a modelling effort requires alignment with BNM's examination cycle. If BNM has notified a bank of a RMIT thematic review in six months, the modelling scope must prioritise the CDEs that BNM will examine — not the CDEs that the data team finds intellectually interesting. Regulatory timelines externally impose scope prioritisation.

**CDMP Exam Angle:**

- Scope definition is part of DAMA's first modelling activity: **Plan Data Modelling**. The exam may test the sequence: Plan → Build → Review → Maintain.
- The exam tests understanding that scope must be agreed with stakeholders *before* modelling begins — not discovered mid-project.
- A common exam scenario: "The modelling project is taking twice as long as planned." Root cause: **inadequate scope definition** leading to scope creep. Solution: revisit and formalise scope boundaries.

---

### Q6 — List stakeholders required for a successful modelling project

**Model Answer:**

| Stakeholder | Role in Modelling Project | Why Their Participation Is Critical |
|---|---|---|
| **Executive Sponsor** (CDO or CIO) | Provides authority, budget, and organisational mandate | Without executive backing, business teams are not compelled to participate; conflicts cannot be resolved |
| **Business Subject Matter Experts (SMEs)** | Validate that entity definitions and business rules reflect operational reality | The modeller captures requirements; the SME verifies them. Without SME validation, the model encodes the modeller's assumptions, not business truth |
| **Data Architect** | Ensures the model fits within the enterprise architecture; defines integration constraints | Model cannot be built in isolation from the systems it will connect to |
| **Data Modeller / Data Analyst** | Executes the modelling work; facilitates requirements sessions; produces and maintains artefacts | Primary delivery role |
| **Data Steward** | Provides governance perspective; enforces naming standards; links model to data dictionary | Without steward involvement, model artefacts are not connected to governance processes and become orphaned |
| **DBA / Data Engineer** | Reviews logical model for implementability; owns physical model derivation | Technical implementers must validate that the logical model can be realised within platform constraints |
| **Compliance / Legal** | Validates that regulatory requirements (PDPA, BNM RMIT) are correctly represented in the model | Compliance rules that are not modelled are not enforced — the model is the compliance contract |
| **End Users / Analysts** | Validate that the model supports the analytical use cases they need | A model that cannot answer the questions analysts actually ask has failed its purpose |

**Expanded Analysis:**

The most common modelling project failure is not technical — it is a **stakeholder participation failure**. Business SMEs are not allocated time to participate (too busy with BAU). The executive sponsor does not resolve disputes about entity definitions between departments. The compliance team is not consulted until after the model is built and then requires rework. DAMA explicitly positions data modelling as a collaborative, multi-stakeholder activity — not a technical exercise conducted in isolation by the data team.

The stakeholder matrix above maps to the DAMA Data Governance role hierarchy (Data Governance Council → Business Stewards → Technical Stewards) and to the RACI concept — each stakeholder has a defined Responsible, Accountable, Consulted, or Informed role in the modelling process.

**Malaysian Context:**

In Malaysian GLC environments, a common gap is the absence of empowered **Business Data Stewards** — individuals within each business unit who can authoritatively validate data definitions. Without this role, modelling sessions devolve into the data team guessing at business rules, presenting them to a committee, and receiving contradictory feedback from different business representatives. The solution is pre-appointing a single Business SME per subject area with decision authority — a governance design decision that must be made before the modelling project begins.

**CDMP Exam Angle:**

- Know that DAMA positions data modelling as a **cross-functional activity** requiring business, technical, and governance stakeholders.
- The exam may ask: "Which role is responsible for validating that the model accurately reflects business requirements?" Answer: **Business Subject Matter Expert (SME)** or **Data Steward**.
- The exam distinguishes between the role that *creates* the model (Data Modeller) and the role that *validates* it (Business SME / Steward) — these are different roles and the confusion between them is a common exam trap.

---

## Section 4: Data Model Patterns

---

### Q7 — Describe a use case for the Party Model

**Model Answer:**

The **Party Model** is a design pattern that uses a single supertype entity — "Party" — to represent any actor that can participate in a business relationship. Subtypes include Individual (a natural person) and Organisation (a legal entity such as a company, government body, or trust). The Party pattern is used when an organisation needs to model relationships between entities that can be *either* an individual or an organisation — such as customers, suppliers, counterparties, agents, or guarantors — without creating separate, duplicated entity structures for each role.

**Use Case — Malaysian Bank Counterparty Model:**

A bank needs to model the counterparty in financial transactions. A counterparty might be:
- An individual retail customer (natural person)
- A sole proprietor (legally an individual but acting commercially)
- An SME company (registered legal entity)
- A foreign corporate group (overseas legal entity)
- A government-linked company (a special category in Malaysian context)

Without the Party pattern, the bank would need separate tables for Individual Customers, Corporate Customers, Individual Suppliers, Corporate Suppliers, and Individual Guarantors — with 80% attribute duplication across all of them (name, address, contact, identifier). Every query spanning multiple counterparty types requires UNION operations. Every new role (e.g., "Business Partner") requires a new table.

With the Party pattern:

```
PARTY MODEL — SUPERTYPE/SUBTYPE DESIGN

        ┌──────────────────────────────────┐
        │  PARTY                           │
        │  Party_ID      PK (UUID)         │
        │  Party_Type    ENUM (IND/ORG)    │
        │  Registered_Name  VARCHAR        │
        │  Registration_Date  DATE         │
        │  Country_Code  CHAR(3)           │
        │  Status        ENUM              │
        └──────────────┬───────────────────┘
                       │ IS-A
            ┌──────────┴──────────┐
            │                     │
  ┌─────────▼─────────┐  ┌────────▼──────────────┐
  │  INDIVIDUAL       │  │  ORGANISATION          │
  │  Party_ID FK      │  │  Party_ID FK           │
  │  IC_Number        │  │  SSM_Reg_Number        │
  │  Full_Legal_Name  │  │  Company_Name          │
  │  Date_Of_Birth    │  │  Incorporation_Date    │
  │  Nationality      │  │  Company_Type          │
  │  Gender           │  │  Authorised_Capital    │
  └───────────────────┘  └────────────────────────┘
            │                           │
            └──────────┬────────────────┘
                       │
        ┌──────────────▼───────────────────┐
        │  PARTY_ROLE                      │
        │  Party_ID        FK              │
        │  Role_Type       ENUM            │
        │  (CUSTOMER / SUPPLIER / AGENT /  │
        │   GUARANTOR / COUNTERPARTY)      │
        │  Effective_Date  DATE            │
        │  Expiry_Date     DATE            │
        └──────────────────────────────────┘

A single Party can have MULTIPLE ROLES over time:
  → Sime Darby is both a CUSTOMER (of Maybank credit) and
    a COUNTERPARTY (in treasury FX transactions)
  → An individual can be both a retail CUSTOMER and a
    GUARANTOR on a business loan
```

**Expanded Analysis:**

The Party model elegantly solves a problem that causes enormous modelling debt in large organisations: the **role-entity conflation** — where different business roles (customer, supplier, partner) are modelled as separate entities even though they represent the same real-world person or organisation. The Party pattern separates *identity* (who someone is — Party) from *role* (how they interact with the organisation — Party Role). This separation enables a party to hold multiple simultaneous roles and to change roles over time without data duplication.

**Malaysian Context:**

In Malaysia's GLC ecosystem, the Party model is critical for group-level data management. Petronas interacts with the same companies as customers (fuel buyers), suppliers (equipment providers), joint venture partners, and regulatory counterparties. Without the Party pattern, Petronas would need four separate entity types to represent what is, in some cases, literally the same company — creating reconciliation complexity across all four.

Under PDPA 2010, the Party model also supports data subject identification: when an individual appears in multiple roles (retail customer, employee, director of a corporate customer), PDPA consent and data subject rights must be managed at the individual level — the Party entity is the hook for PDPA compliance regardless of role.

**CDMP Exam Angle:**

- The Party model is a **reusable design pattern** — the exam may describe a scenario with redundant customer/supplier/partner tables and ask what pattern eliminates the duplication. Answer: **Party Model** (supertype/subtype with Party Role).
- Know the key insight: the Party model separates **identity** (Party) from **role** (Party Role). This is the architectural principle behind the pattern.
- The Party model is used in **Chapter 8: Reference & Master Data** as a canonical pattern for Master Data Management (MDM) — the same concept appears across two chapters.

---

### Q8 — Provide an example where reference data patterns reduce complexity

**Model Answer:**

A Malaysian insurance company operates across life insurance, general insurance, and takaful products. Each business line has independently coded "occupation" for policyholders — Life uses a 3-digit code (e.g., "101 = Professional"), General uses a text field (e.g., "Doctor"), and Takaful uses a 5-digit MOH code (e.g., "10101 = Medical Practitioner"). When the actuarial team needs to calculate risk by occupation across all three product lines, they must manually map three incompatible coding schemes before any analysis is possible.

**Solution — Reference Data Pattern (Occupation Reference Table):**

Define a single enterprise-wide **Occupation Reference Table** with a canonical code, a canonical description, and mapping columns for each source system's legacy code:

```
ENTERPRISE REFERENCE DATA — OCCUPATION TABLE

  Canonical_Code  Canonical_Description     Life_Code  General_Text   Takaful_Code
  ──────────────────────────────────────────────────────────────────────────────
  OCC-001         Medical Practitioner       101        Doctor         10101
  OCC-001         Medical Practitioner       101        Physician      10101
  OCC-002         Legal Professional         102        Lawyer         10201
  OCC-003         Educator - Primary/Sec     103        Teacher        10301
  OCC-004         Educator - Tertiary        104        Lecturer       10401
  OCC-005         Engineer - Civil           201        Civil Eng.     20101
  ...
  REFERENCE OWNER: Chief Actuary + Product Data Steward
  GOVERNANCE: Quarterly review cycle; change requests via DGC
  SOURCE OF TRUTH: This table; all systems map TO it
```

**Result:** The actuarial team queries one table. All three source systems map to canonical codes at the integration layer. Occupation-based risk analysis runs in minutes instead of days. Any change to occupation classification is made once in the reference table and propagated to all systems automatically.

**Expanded Analysis:**

Reference data patterns eliminate a category of complexity called **value heterogeneity** — where the same real-world concept is expressed with different codes, labels, or formats across systems. Unlike the semantic heterogeneity addressed by the canonical data model (which deals with entity and attribute definition), value heterogeneity deals with the *values* stored in those attributes.

Reference data patterns work by designating a single authoritative list for each reference domain (Country, Currency, Occupation, Status, Product Category, etc.) and requiring all systems to either use that list directly or maintain a mapping to it. This connects Chapter 5 (Data Modelling) directly to Chapter 8 (Reference & Master Data), which is dedicated to the management of these reference datasets.

**Malaysian Context:**

Malaysia has several national reference data standards that serve as canonical lists:

- **Country codes**: ISO 3166-1 (enforced in BNM reporting)
- **Currency codes**: ISO 4217 (enforced in bank regulatory submissions)
- **Race/Ethnicity codes**: Department of Statistics Malaysia (DOSm) classification — used in government data collection
- **Postal codes**: Pos Malaysia standard — critical for address validation and delivery routing
- **SSM company type codes**: Companies Commission of Malaysia (SSM) — used in corporate identity verification

Malaysian organisations that map their internal codes to these national standards gain interoperability with government systems, regulatory reporting platforms, and cross-agency data sharing initiatives — all core to the MyDIGITAL national data architecture vision.

**CDMP Exam Angle:**

- Reference data patterns are tested at the intersection of **Chapter 5 (Modelling)** and **Chapter 8 (Reference & Master Data)**. Know that reference data is a *modelling concern* (how it is designed) and a *management concern* (how it is maintained).
- The exam may ask: "What type of data requires an enterprise-wide authoritative list and governance process?" Answer: **Reference data** (country codes, currency codes, status codes, classification codes).
- Know the governance requirement: reference data must have a designated **owner**, a **change management process**, and a **versioning mechanism** — changes to reference values propagate to all consuming systems.

---

## Section 5: Review & Validation

---

### Q9 — List two checks done during a model walkthrough

**Model Answer:**

**Check 1 — Business Rule Accuracy (Correctness)**

The walkthrough facilitator presents each entity relationship and asks the business SME to confirm whether the cardinality constraint reflects how the business actually operates. For example: "This model shows that one Customer can have zero or many Accounts. Is it possible for a Customer to exist with no Account?" If the business rule is that every Customer must have at least one Account, the model must show a minimum cardinality of one — not zero. This check catches modeller assumptions that do not match business reality and must be resolved before the model is used to build anything.

**Check 2 — Completeness Against Requirements (Completeness)**

The facilitator maps every documented business requirement and use case to a specific entity or attribute in the model. For each requirement, the question is: "Can this be answered from the model as drawn?" If a regulatory requirement (e.g., "report customer occupation at time of policy inception") has no corresponding attribute in the model, that is a completeness gap. The walkthrough produces a traceability matrix: requirement → model element → status (covered / gap / out of scope).

**Expanded Analysis — Full Walkthrough Agenda:**

```
MODEL WALKTHROUGH — STRUCTURED AGENDA

  Step 1: Context Setting (15 min)
  ─────────────────────────────────
  Present the scope, purpose, and notation being used.
  Ensure all participants can read the diagram.
  Establish ground rules: validate content, not aesthetics.

  Step 2: Entity-by-Entity Review (45-60 min)
  ─────────────────────────────────────────────
  For each entity:
  ✓ Is the name correct and unambiguous?
  ✓ Is the definition accurate?
  ✓ Are all required attributes present?
  ✓ Are attribute data types appropriate?
  ✓ Are mandatory/optional designations correct?

  Step 3: Relationship Review (30 min)
  ──────────────────────────────────────
  For each relationship:
  ✓ Is the cardinality correct? (Test both directions)
  ✓ Is the relationship label meaningful?
  ✓ Are there missing relationships?
  ✓ Are there relationships that don't belong?

  Step 4: Business Rule Verification (30 min)
  ─────────────────────────────────────────────
  For each business rule encoded in the model:
  ✓ Does the constraint match the business rule exactly?
  ✓ Are any business rules missing from the model?

  Step 5: Issue Log Review (15 min)
  ───────────────────────────────────
  Categorise all issues raised: Critical / Major / Minor
  Assign owners and resolution dates.
  Schedule follow-up review if critical issues found.
```

**Malaysian Context:**

In Malaysian organisations, model walkthroughs often face a cultural challenge: business stakeholders default to agreeing with what the modeller presents to avoid conflict — especially when there is a seniority gap between the presenter and the audience. A skilled Malaysian facilitator must explicitly invite challenge: "Please tell me where this is wrong" rather than "Does this look correct?" The framing matters. Some organisations use anonymous pre-walkthrough surveys to surface disagreements before the meeting, giving quieter stakeholders a voice without requiring public confrontation.

**CDMP Exam Angle:**

- Model walkthroughs are part of DAMA's **Review** activity — the third of five Data Modelling activities.
- Know the five model quality dimensions that walkthroughs check against: **Completeness, Correctness, Consistency, Comprehensibility, Precision**.
- The exam may ask what the output of a model walkthrough is — the answer is an **issue log** with categorised findings and assigned resolution owners.

---

### Q10 — Explain one way to confirm the model aligns with business meaning

**Model Answer:**

Conduct a **business scenario walkthrough** — present a concrete, real-world business event or question to the business SME and ask them to trace how the model would represent it. If the model cannot represent the scenario, or if the path through the model is convoluted and requires workarounds, the model does not reflect business reality.

**Example:** Ask the business SME: "Walk me through what happens when a customer calls to change their primary mobile number, and we need to keep the old number on record for audit purposes." If the model has only one mobile_number attribute per Customer record with no history, it cannot represent this scenario — the old number would be overwritten. The SME's walkthrough reveals a modelling gap: either a separate Contact_History entity is needed, or the mobile number needs an effective date and expiry date structure.

**Expanded Analysis:**

This technique is sometimes called **scenario testing** or **instance-level validation**. Where a walkthrough reviews the model structure, scenario testing validates the model's *content capacity* — can it hold real data representing real business events?

A complementary technique is **data population review** — populating the model with a small sample of real data (or realistic synthetic data) and asking business SMEs to review the populated records. If a populated Customer record with five Address rows, three Phone numbers, and two Consent records "looks right" to a business SME, the model structure has been validated by example. If the populated record looks wrong or incomplete, the model has a gap.

```
BUSINESS MEANING VALIDATION — TWO TECHNIQUES

  SCENARIO WALKTHROUGH          DATA POPULATION REVIEW
  ─────────────────────         ──────────────────────
  Input: A business event        Input: Sample real data
  Process: Trace through         Process: Populate model
           the model             with sample instances
  Output: Can the model          Output: Does a populated
           represent this?               record look correct?
  Best for: Revealing            Best for: Validating
            structural gaps              attribute completeness
```

**Malaysian Context:**

For Malaysian banks preparing for BNM RMIT assessments, scenario testing against regulatory scenarios is standard practice. The data team presents specific BNM data requests ("Provide all customer accounts with balance above MYR 10 million as at 30 June, with KYC status and last transaction date") and traces whether the model can answer them. Any scenario that requires data the model does not contain is a documented gap that must be prioritised in the remediation roadmap.

**CDMP Exam Angle:**

- Model validation is a distinct activity from model review. **Review** checks the model structure against quality criteria. **Validation** confirms the model against business meaning (does it reflect reality?).
- The exam may present a scenario where a technically correct model produces wrong analytical results — this is a **business meaning validation failure**, not a correctness failure in the technical sense.
- Know that validation requires **business SME involvement** — data modellers cannot validate business meaning by themselves.

---

## Section 6: Case Study Practice

---

### Case 1 — Multiple Regions with Different Definitions for "Product," "Category," and "Item"

**Scenario:** A company sells products in multiple regions. Each region uses different definitions for "product," "category," and "item." Analysts spend weeks reconciling meaning before reporting. What modelling activities or structures would help unify these definitions?

---

**Model Answer:**

The core problem is **semantic heterogeneity at the concept level** — the same business entity is defined differently across regions. The solution requires three modelling actions:

1. **Build an Enterprise Conceptual Data Model (CDM)** that defines "Product," "Category," and "Item" as enterprise-wide subject areas with authoritative definitions, independent of any region's interpretation.

2. **Define a Canonical Product Logical Model** — a technology-neutral specification of the Product entity with attributes, rules, and hierarchies (Category → Sub-Category → Item → SKU) that all regions must conform to when reporting.

3. **Create Regional Mapping Tables** — explicit cross-reference tables that map each region's local terminology to the canonical enterprise definition, enabling automated translation at the integration layer.

---

**Expanded Answer:**

**Step 1 — Establish Enterprise Definitions Through Facilitated Modelling**

Convene a multi-region Data Modelling Working Group with one Business SME from each region plus the Chief Data Steward. The goal is consensus on three definitions: What is a "Product"? What is a "Category"? What is an "Item"? These are governance decisions, not technical decisions — the data modeller facilitates, but business SMEs decide.

Document the agreed definitions in the enterprise business glossary, linked to the data model. Example agreed definitions:

- **Product** = A marketable offering sold to customers; may exist in multiple regional variants but shares a common Product Code. Defined at enterprise level.
- **Category** = A classification grouping of Products for commercial and reporting purposes. A Product belongs to exactly one Category at any point in time.
- **Item / SKU** = A specific variant of a Product, distinguished by attributes such as size, colour, or packaging. One Product can have many Items/SKUs.

**Step 2 — Build the Canonical Product Hierarchy Model**

```
CANONICAL PRODUCT HIERARCHY — ENTERPRISE LOGICAL MODEL

  ┌──────────────────────────────┐
  │  PRODUCT_CATEGORY            │
  │  Category_ID    PK           │
  │  Category_Code  UNIQUE       │
  │  Category_Name  VARCHAR      │
  │  Category_Desc  TEXT         │
  │  Parent_Cat_ID  FK (self)    │  ← Enables hierarchy
  │  Effective_Date DATE         │
  └──────────┬───────────────────┘
             │ 1 to many
  ┌──────────▼───────────────────┐
  │  PRODUCT                     │
  │  Product_ID     PK           │
  │  Product_Code   UNIQUE       │  ← Enterprise standard code
  │  Product_Name   VARCHAR      │
  │  Category_ID    FK           │
  │  Launch_Date    DATE         │
  │  Status         ENUM         │
  └──────────┬───────────────────┘
             │ 1 to many
  ┌──────────▼───────────────────┐
  │  PRODUCT_ITEM (SKU)          │
  │  Item_ID        PK           │
  │  SKU_Code       UNIQUE       │
  │  Product_ID     FK           │
  │  Item_Variant   VARCHAR      │  ← Size, Colour, Packaging
  │  Unit_Weight    DECIMAL      │
  │  Unit_Price_MYR DECIMAL      │
  └──────────────────────────────┘
             │
  ┌──────────▼───────────────────┐
  │  REGIONAL_PRODUCT_XREF       │
  │  Item_ID        FK           │  ← Links to canonical Item
  │  Region_Code    CHAR(3)      │  ← MYS, SGP, IDN, THA...
  │  Local_Code     VARCHAR      │  ← Region's internal code
  │  Local_Name     VARCHAR      │  ← Region's local label
  │  Local_Category VARCHAR      │  ← Region's category name
  └──────────────────────────────┘
```

**Step 3 — Governance the Model**

Designate a **Product Data Steward** at enterprise level whose mandate includes maintaining the canonical product definitions, approving additions to the product hierarchy, and resolving conflicts when regional definitions diverge from the canonical standard. Without this role, the model will drift back to regional fragmentation within 12 months.

**Malaysian Context:**

This scenario is directly applicable to Malaysian retailers and distributors expanding across ASEAN (e.g., Aeon, Caring Pharmacy, 7-Eleven Malaysia). Each ASEAN market may classify the same product differently for regulatory (customs, labelling) or commercial (shelf category) reasons. The canonical product model allows group-level consolidated reporting while preserving regional classification flexibility via the REGIONAL_PRODUCT_XREF table.

Under Malaysia's e-Invoicing mandate (enforced by LHDN from August 2024 for large companies), product and service classification must conform to the MSIC (Malaysian Standard Industrial Classification) code — a national reference standard. The canonical product model can incorporate MSIC codes as an attribute, ensuring e-Invoicing compliance is built into the data structure rather than bolted on.

**CDMP Exam Angle:**

- This case tests: **enterprise conceptual modelling**, **canonical data model design**, **reference data patterns**, and **data governance** (stewardship). It spans Chapters 4, 5, and 8.
- The exam may ask: "What is the FIRST step when business units use different definitions for the same concept?" Answer: **establish enterprise definitions through facilitated modelling** — not build a new database, not implement MDM software.
- Key principle: governance decisions (what does "Product" mean?) must precede technical solutions (how do we store it?).

---

### Case 2 — Financial Institution Merging Two Systems with Overlapping Customer IDs

**Scenario:** A financial institution is merging two systems and discovers that customer IDs overlap but represent different people. What type of model or practice would reduce identity ambiguity?

---

**Model Answer:**

The institution should implement a **Customer Identity Resolution Model** using three complementary modelling and MDM practices:

1. **Enterprise Customer Identifier (Golden Key)** — Introduce a new system-generated UUID as the enterprise-wide customer identifier, replacing all source system IDs. The new key is not derived from either legacy system, eliminating the collision problem at its root.

2. **Cross-Reference (XREF) Table** — Model a Customer System Cross-Reference entity that maps every source system customer ID to the new enterprise golden key, preserving the ability to trace back to each source system.

3. **Identity Matching Attributes** — Define the set of non-ID attributes that uniquely identify a real person (NRIC/passport number, full legal name, date of birth) as the **match keys** used to detect duplicates and assign golden keys during the merge.

---

**Expanded Answer:**

**The Identity Ambiguity Problem:**

```
THE COLLISION PROBLEM — BEFORE RESOLUTION

  System A                   System B
  ─────────                  ─────────
  CustID: 10001              CustID: 10001
  Name: Ahmad bin Razak      Name: Lee Chong Wei
  IC:  620514-14-5678        IC:  720910-10-1234

  CustID: 10002              CustID: 10002
  Name: Siti Nurhaliza       Name: Ng Siew Ling
  IC:  781203-02-9876        IC:  850622-08-4321

  PROBLEM: ID 10001 in System A ≠ ID 10001 in System B.
  Any query joining these systems by customer ID returns
  wrong data — Ahmad's records merged with Lee Chong Wei's.
  This is a CRITICAL DATA QUALITY FAILURE with financial,
  legal, and regulatory consequences.
```

**Step 1 — Design the Enterprise Customer Identity Model:**

```
ENTERPRISE CUSTOMER IDENTITY MODEL

  ┌──────────────────────────────────────────┐
  │  CUSTOMER (Enterprise Golden Record)     │
  │                                          │
  │  Enterprise_Cust_ID   UUID  PK           │  ← New; system-generated
  │  IC_Number            CHAR(12) UNIQUE    │  ← Match key 1 (primary)
  │  Passport_Number      VARCHAR  UNIQUE    │  ← Match key 2 (non-citizens)
  │  Full_Legal_Name      VARCHAR NOT NULL   │  ← Match key 3 (secondary)
  │  Date_Of_Birth        DATE    NOT NULL   │  ← Match key 4
  │  Golden_Record_Date   DATETIME           │  ← When golden key assigned
  │  MDM_Confidence_Score DECIMAL            │  ← Match confidence (0-1)
  └──────────────────┬───────────────────────┘
                     │ one-to-many
  ┌──────────────────▼───────────────────────┐
  │  CUSTOMER_SYSTEM_XREF                    │
  │                                          │
  │  XREF_ID              PK                 │
  │  Enterprise_Cust_ID   FK → CUSTOMER      │
  │  Source_System_Code   ENUM (SYS_A/SYS_B) │
  │  Source_Customer_ID   VARCHAR NOT NULL   │  ← Original system ID
  │  Source_Cust_Name     VARCHAR            │  ← As stored in source
  │  Source_IC            VARCHAR            │  ← As stored in source
  │  Match_Method         ENUM               │  ← AUTO/MANUAL/RULE
  │  Match_Confidence     DECIMAL            │
  │  Linked_By            VARCHAR            │  ← Analyst who confirmed
  │  Linked_Date          DATETIME           │
  └──────────────────────────────────────────┘

  MERGE SCENARIOS:
  ─────────────────────────────────────────────────────
  SCENARIO A — Same person in both systems (Merge)
  Ahmad (SysA:10001) + Ahmad (SysB:20456) → UUID: a1b2c3...
  Two XREF rows pointing to one golden record

  SCENARIO B — Different people with same source ID (Split)
  Ahmad (SysA:10001) → UUID: a1b2c3...
  Lee   (SysB:10001) → UUID: d4e5f6...
  Two distinct golden records; same source ID in XREF

  SCENARIO C — Person in only one system (Preserve)
  Siti (SysA:10002 only) → UUID: g7h8i9...
  One XREF row; no counterpart in SysB
```

**Step 2 — Identity Matching Process:**

The match keys (IC number, passport, name + DOB combination) are used to run **deterministic and probabilistic matching** across both source system extracts:

- **Deterministic match**: Identical IC numbers → same person → merge to one golden record (high confidence)
- **Probabilistic match**: Same name + same DOB but slightly different IC format → likely same person → flag for manual review
- **No match**: Different IC, different name → different people → separate golden records

All matches are recorded in the XREF table with match method and confidence score, creating a complete audit trail of the identity resolution process.

**Step 3 — Governance the Model:**

The identity resolution process is not a one-time migration activity — it is an ongoing governance process. New customers must be checked against the golden record database before a new Customer_ID is issued. The **Customer Data Steward** owns the XREF table and is responsible for resolving ambiguous matches escalated by the automated matching process.

**Malaysian Context:**

This scenario is precisely what occurred when several Malaysian financial institutions underwent mergers in the early 2000s (e.g., the 10-bank consolidation to 10 anchor banks mandated by BNM post-1997 Asian Financial Crisis). Each merged bank brought its own customer numbering scheme. The identity resolution exercise — matching customers across legacy systems — was one of the most expensive and risk-laden phases of each merger.

Under BNM RMIT 2020 and AMLA (Anti-Money Laundering Act), banks must be able to identify a customer uniquely across all products and accounts. A customer who has a loan in System A and a savings account in System B must be linked to the same identity — both for single-borrower exposure limits and for AML/CFT suspicious transaction aggregation. The Customer Identity Resolution Model is the technical architecture that enables both compliance requirements.

NRIC (MyKad number) is Malaysia's strongest identity anchor — it is unique, government-issued, and present in almost all customer records. Using IC_Number as the primary match key dramatically simplifies identity resolution compared to markets without a universal national ID.

**CDMP Exam Angle:**

- This case tests **Master Data Management (MDM)** concepts applied through data modelling. Know that identity resolution is a **Chapter 8 (Reference & Master Data)** concern, but the modelling design (golden key, XREF table, match attributes) is a **Chapter 5** deliverable.
- The exam may ask: "A merger results in duplicate customer IDs across two systems. What is the PRIMARY data management concern?" Answer: **identity resolution** (not data migration, not system decommissioning).
- Key exam term: **Golden Record** — the single, authoritative, deduplicated record for a master data entity (Customer, Product, Location). The golden record is produced by the MDM process; the data model provides the structure that holds it.
- A second exam term: **Survivorship Rule** — the business rule that determines which source system's attribute value "wins" when two records are merged. E.g., "Use System A's name if it matches the IC; use System B's address if it is more recent." Survivorship rules are modelling and governance decisions.

---

## Summary Table — All Workbook Questions

| Section | Question | Key Answer Concept | DAMA Chapter Link |
|---|---|---|---|
| Business Drivers | 3 business goals | Compliance, Data Quality, Cross-system Reporting | Ch.5 Modelling Purpose |
| Business Drivers | Poor modelling confusion | Semantic heterogeneity; no canonical definition; multiple "truths" | Ch.5 + Ch.4 Architecture |
| Principles | Clarity | Unambiguous naming, written definitions, visual readability | Ch.5 Model Quality |
| Principles | Consistency example | Enterprise naming standard → all PKs follow `[Entity]_ID` pattern | Ch.5 Model Quality |
| Planning | Scope definition | In/out scope; model levels; notation; success criteria; timeline | Ch.5 Activity 1: Plan |
| Planning | Stakeholders | Sponsor, SME, Architect, Modeller, Steward, DBA, Compliance, Analyst | Ch.5 Roles |
| Patterns | Party Model use case | Financial institution counterparty; one supertype, multiple roles | Ch.5 + Ch.8 MDM |
| Patterns | Reference data example | Enterprise Occupation Reference Table → eliminates value heterogeneity | Ch.5 + Ch.8 Ref Data |
| Review & Validation | 2 walkthrough checks | Business rule accuracy (Correctness); completeness against requirements | Ch.5 Activity 3: Review |
| Review & Validation | Confirming business meaning | Business scenario walkthrough + data population review | Ch.5 Validation |
| Case Study 1 | Multi-region product definitions | Enterprise CDM + Canonical Product Model + Regional XREF + Steward | Ch.5 + Ch.4 + Ch.8 |
| Case Study 2 | Overlapping customer IDs | Enterprise Golden Key (UUID) + XREF Table + Identity Matching + Survivorship | Ch.5 + Ch.8 MDM |

---

## CDMP Quick-Reference — Chapter 5 Exam Signals

| If the exam scenario says… | The answer involves… |
|---|---|
| "Analysts spend weeks reconciling definitions" | Enterprise conceptual model + canonical definitions |
| "Model cannot be understood without explanation" | Clarity / Comprehensibility failure |
| "Same entity defined differently across two models" | Consistency failure; inter-model consistency |
| "Requirement not represented in the model" | Completeness gap; found in model walkthrough |
| "Cardinality constraint doesn't match business rule" | Correctness failure; found in walkthrough Check 1 |
| "Which modelling pattern handles Customers AND Suppliers?" | Party Model (supertype/subtype) |
| "Status codes differ across regions/systems" | Reference data pattern; enterprise reference table |
| "Customer IDs overlap between merged systems" | Identity resolution; Golden Record; XREF table |
| "What is the FIRST data modelling activity?" | Plan Data Modelling (scope, stakeholders, notation) |
| "Who validates that the model is correct?" | Business Subject Matter Expert (SME) / Data Steward |
| "How is business meaning confirmed in a model?" | Scenario walkthrough / data population review |

---

*Day 05 Supplementary File | DAMA-DMBOK2 Chapter 5 | CDMP Exam Preparation*
*Malaysian Context: PDPA 2010 (Act 709) | BNM RMIT 2020 | MyDIGITAL Blueprint*
*Prepared as part of 17-Day CDMP Study Programme*
