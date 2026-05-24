# Day 03 — Data Governance Scenario Practice Workbook: Answers & Analysis
**DAMA-DMBOK2 | Chapter 3 | Supplementary Material**

> *"Data governance is not a one-time thing. Governing data requires an ongoing programme focused on ensuring that an organisation gets value from its data and reduces risks related to data."*
> — DAMA-DMBOK2, Chapter 3

---

## How to Use This Document

Each scenario is answered at four levels:
1. **Model Answer** — the workbook's own guidance, reproduced for reference
2. **Expanded DAMA Analysis** — deep alignment to DMBOK2 Chapter 3 concepts, roles, and processes
3. **Malaysian Context** — how this scenario presents in Malaysian corporate and regulatory settings
4. **CDMP Exam Angle** — what the exam is testing and the precise framing expected in answers

---

## Governance Roles — Quick Reference

Before working through the scenarios, align on role definitions from DMBOK2 Chapter 3:

| Role | DAMA Definition | Decision Authority |
|------|-----------------|--------------------|
| **Data Governance Council (DGC)** | Senior governance body; reviews, approves, and adopts policies, standards, architecture | Highest — final authority |
| **Data Stewardship Steering Committee** | Coordinates stewardship activities across domains; manages issue escalation | Enterprise coordination |
| **Data Owner** | A Business Data Steward with **approval authority** for decisions about data in their domain | Domain-level decision rights |
| **Business Data Steward** | Subject matter expert accountable for a subset of data; facilitates alignment; defines and controls data | Facilitates and recommends |
| **Technical Data Steward** | IT professional (DBA, BI Specialist, DQ Analyst, Metadata Admin) implementing standards and controls | Technical implementation |
| **Data Custodian** | Responsible for the safe custody, transport, and storage of data; implements and maintains security controls | Technical enforcement |
| **Coordinating Data Steward** | Leads and represents stewardship teams across business units; critical in large organisations | Cross-team coordination |

---

## CDMP Data Governance Principles — Reference

| DG Principle | Meaning |
|-------------|---------|
| **Leadership & Strategy** | DG starts with committed leadership; guided by data strategy aligned to business strategy |
| **Business-driven** | DG is a business programme, not IT; governs IT data decisions as much as business interactions |
| **Shared Responsibility** | DG is jointly owned by business data stewards AND technical data management professionals |
| **Multi-layered** | DG operates at enterprise, divisional, and local levels simultaneously |
| **Framework-based** | Accountabilities and interactions must be defined in an operating framework |
| **Principle-based** | Guiding principles underpin all DG policy; principles are articulated before policy is written |

---

## Scenario 1 — Unclear Data Ownership

**Scenario:** A business team discovers a data quality issue in a critical sales report, but no one can identify who owns the underlying dataset.

---

### Questions & Answers

**Q1: What is the data governance issue?**

**Model Answer:** Lack of defined data ownership leads to unresolved data quality issues.

**Expanded DAMA Analysis:**

This scenario represents one of the most fundamental and common data governance failures — **undefined data ownership**. DMBOK2 Chapter 3 is explicit: every data domain must have a named **Data Owner** with approval authority for decisions about that data.

The issue has two compounding layers:

| Layer | Detail |
|-------|--------|
| **Structural gap** | No Data Owner was ever formally assigned to the sales dataset — the operating framework has a gap |
| **Consequence** | Because ownership is unclear, no one has the authority or accountability to prioritise, assign resources to, or approve a resolution to the quality issue |

This is precisely what DAMA describes as a governance failure under the **Accountability** principle — data management without defined decision rights. The data quality issue itself may be minor, but the inability to resolve it reveals a structural governance problem that will repeat across every dataset with no named owner.

DAMA also notes in Chapter 3 that *"Data governance ensures data is properly managed without directly executing data management."* The absence of a Data Owner means there is no governance oversight of this dataset at all — execution is happening without any oversight layer.

**Q2: Which role should be responsible for resolving this?**

**Model Answer:** Data Owner, supported by the Data Steward.

**Expanded DAMA Analysis:**

The correct role hierarchy for this resolution involves three actors, each with a distinct function:

| Role | Immediate Responsibility |
|------|-------------------------|
| **Business Data Steward** | First responder — logs the issue formally, attempts to identify who currently manages the dataset in practice, facilitates cross-team discussion about ownership |
| **Data Owner** (once identified or newly assigned) | Holds approval authority — decides how the quality issue is prioritised and resolved; approves any data corrections or process changes |
| **Data Governance Council** | If no owner can be identified through the stewardship process, the DGC must formally assign ownership as a governance decision — this is part of its legislative function |

DAMA distinguishes clearly: the Data Steward *facilitates and executes*; the Data Owner *decides and approves*. In this scenario, if no owner exists, one must be assigned — and that assignment is a DGC governance act, not a technical decision.

**Q3: What is the correct escalation path?**

**Model Answer:** Escalate to the Data Governance Council if ownership is unclear.

**Expanded DAMA Analysis:**

DMBOK2 Chapter 3 defines a formal issue escalation path. This scenario falls under the **Authority** issue category (one of the eight DAMA issue management categories) — it is a question of decision rights and procedures:

```
STEP 1: Business Data Steward
        Logs the issue formally in the issue management system
        Attempts to identify the dataset owner through existing documentation,
        system-of-record records, and stakeholder inquiry
        └─ If owner identified → engage Data Owner directly → resolve
        └─ If owner not identified → escalate to Step 2

STEP 2: Data Stewardship Steering Committee
        Coordinates cross-functional inquiry
        Reviews governance documentation for any implicit ownership assignments
        └─ If ownership can be assigned → formalise and document → resolve
        └─ If still unresolved → escalate to Step 3

STEP 3: Data Governance Council
        Exercises its legislative function — formally assigns a Data Owner
        Documents the assignment in the governance operating framework
        Reviews whether other datasets may have the same gap (systemic issue)
        └─ Root cause: operating framework incomplete — DGC commissions
           a data ownership register review across all critical datasets
```

The resolution does not end with fixing the immediate quality issue. The DGC must also commission a **data ownership register** audit to identify other datasets with no named owner — preventing the same failure from recurring.

**Q4: Which CDMP principle applies?**

**Model Answer:** Accountability + Stewardship.

**Expanded DAMA Analysis:**

| Principle | How It Applies |
|-----------|---------------|
| **Accountability** | Primary — no named Data Owner means no one is accountable for the dataset's quality, accuracy, or use. Accountability requires named, documented decision rights |
| **Stewardship** | Secondary — data must be managed as a valuable asset with care and integrity. An unowned dataset is an unmanaged asset — it cannot be properly stewarded |
| **Framework-based (DG Principle)** | The operating framework failed to assign ownership — the framework itself must be updated as part of remediation |
| **Shared Responsibility (DG Principle)** | This scenario shows what happens when neither IT nor the business takes ownership — shared responsibility requires both sides to be named, not assumed |

**CDMP Exam Angle:**

This is a **Type 6 (Role/Responsibility)** and **Type 4 (Process/Framework)** question. The exam will present this scenario and ask: *"What should be done first?"* The correct answer is NOT to fix the data quality issue directly — it is to **identify or assign the Data Owner through the formal governance process**. Fixing data without governance approval is exactly the anti-pattern DAMA warns against. The data quality fix follows *after* ownership is established.

**Malaysian Context:**

In Malaysian GLCs and financial institutions, this scenario is very common on merger and acquisition integrations — where datasets from acquired entities have no clear owner in the new group structure. BNM's RMIT framework requires financial institutions to have documented data ownership for all data used in regulatory reporting. A BNM examination finding that a critical regulatory dataset has no named owner is a significant governance gap requiring immediate remediation.

---

## Scenario 2 — Policy Non-Compliance

**Scenario:** An analytics team begins building dashboards using sensitive customer data without going through the company's required data access approval workflow.

---

### Questions & Answers

**Q1: Which governance rule is being ignored?**

**Model Answer:** Violation of data access and usage policy.

**Expanded DAMA Analysis:**

This scenario involves a **Conformance** issue — one of DAMA's eight issue management categories. The analytics team is violating the data access approval workflow, which is a formally adopted governance policy.

Three distinct governance rules are being bypassed simultaneously:

| Rule Being Violated | DAMA Source | Risk Created |
|--------------------|-------------|--------------|
| **Data access approval policy** | DG policy requiring Data Owner approval before accessing sensitive data | Unauthorised access to customer PII; potential PDPA breach |
| **SDLC data governance gate** | DMBOK2 Ch.3: every project with significant data must capture DG requirements in planning phase | Dashboard built on ungoverned data — no lineage, quality validation, or security review |
| **Data classification and handling standards** | Sensitive customer data has specific handling requirements | Data exposed in dashboards without appropriate masking or access controls |

DAMA Chapter 3 explicitly states: *"Every project with a significant data component should capture data management requirements early in the SDLC (planning and design phases)."* The analytics team skipped this entirely.

**Q2: What should be the correct process?**

**Model Answer:** Data Custodian enforces access controls; Data Owner approves usage.

**Expanded DAMA Analysis:**

The correct process has three sequential gates before data access is granted:

```
STAGE 1 — REQUEST
  Analytics team submits a formal Data Access Request specifying:
  • Which dataset(s) are needed
  • The specific business purpose
  • How the data will be used (dashboard, model, report)
  • Who will have access to the output
  • Retention period for the derived data

STAGE 2 — REVIEW & APPROVAL
  Data Steward reviews the request:
  • Is the stated purpose legitimate?
  • Does it conflict with any existing policies?
  • Does it require Data Owner approval or DGC oversight?

  Data Owner approves or rejects:
  • Has approval authority — this is the decision point
  • May impose conditions (e.g., data must be masked, access limited to named individuals)

  Data Custodian validates technical feasibility:
  • Can access be provisioned in accordance with the approved conditions?

STAGE 3 — PROVISIONING & MONITORING
  Data Custodian provisions access with appropriate controls
  Access is logged and monitored
  Periodic review of ongoing access rights
```

In this scenario, the analytics team jumped directly to provisioning and building — skipping Stages 1 and 2 entirely.

**Q3: Which governance roles should intervene?**

**Model Answer:** Data Custodian enforces access controls; notify Data Steward and escalate to DGC if repeated.

**Expanded DAMA Analysis:**

| Role | Immediate Intervention |
|------|----------------------|
| **Data Custodian** | Immediately revoke or suspend the unauthorised data access; this is their core enforcement responsibility |
| **Business Data Steward** | Log the violation formally in the issue management system; initiate the formal data access request process retrospectively; determine whether any data has already been exposed inappropriately |
| **Data Owner** | Review what data was accessed and whether any harm has resulted; decide whether to retrospectively approve (with conditions) or require the dashboard to be taken down |
| **Data Governance Council** | If this is a repeated pattern (the workbook hints "if repeated") — escalate as a systemic policy conformance failure; review whether the access approval workflow is sufficiently embedded in the SDLC; consider whether the analytics team requires governance training |

**Q4: Which CDMP principle applies?**

**Model Answer:** Policy Enforcement + Data Protection.

**Expanded DAMA Analysis:**

| Principle | How It Applies |
|-----------|---------------|
| **Accountability** | Primary — who is responsible for ensuring the analytics team follows the access approval policy? The Data Owner, Data Steward, and team manager all share accountability |
| **Stewardship** | Sensitive customer data must be managed with care and integrity — bypassing access controls is a stewardship failure |
| **Lawfulness** | PDPA 2010 — the Disclosure Principle prohibits access to personal data by unauthorised parties. Bypassing approval workflows may create a PDPA compliance exposure |
| **Compliance (DG Principle)** | Chapter 3 lists "Compliance — ensuring the organisation can meet data-related regulatory compliance requirements" as a core DG programme scope item |

**CDMP Exam Angle:**

This is a **Type 4 (Process/Framework)** and **Type 3 (Scenario)** question. The exam trap is answering "notify the analytics team" as the first step. The correct DAMA first step is **immediate enforcement action** — the Data Custodian suspends access. Governance then follows: log, investigate, remediate, escalate if systemic. Soft notification without enforcement is not a governance response — it is a governance failure.

**Malaysian Context:**

Under **PDPA 2010**, the Security Principle requires organisations to take "practical steps to protect personal data from any loss, misuse, modification, unauthorised or accidental access or disclosure." An analytics team accessing sensitive customer data without approval may create a **PDPA security breach** — even if no external party received the data. Malaysian organisations that have experienced PDPC enforcement actions frequently cite "internal unauthorised access" as a root cause. BNM RMIT also requires financial institutions to have documented access control frameworks with audit trails.

---

## Scenario 3 — Conflicting Definitions

**Scenario:** Finance and Marketing have different definitions for 'Active Customer', resulting in inconsistent KPI reporting across teams.

---

### Questions & Answers

**Q1: What governance area is impacted?**

**Model Answer:** Lack of standardized business glossary definitions.

**Expanded DAMA Analysis:**

This scenario impacts **three interconnected governance areas**:

| Governance Area | Impact |
|----------------|--------|
| **Metadata Management** | The Business Glossary — the primary governance artefact for business term definitions — is either absent, incomplete, or not being used as the system of record for 'Active Customer' |
| **Data Quality** | Inconsistent definitions produce inconsistent metrics. Both KPI reports may be technically accurate against their respective definitions — but they contradict each other, making neither trustworthy for enterprise decision-making |
| **Data Governance — Standardisation** | DG's legislative function includes defining and enforcing data standards. Conflicting definitions across business units is a direct indication that the standardisation function of governance has not been exercised for this term |

DAMA Chapter 3 states: *"A glossary is necessary because people use words differently. Developing and documenting standard data definitions reduces ambiguity and improves communication."* The Business Glossary is not optional infrastructure — it is the mechanism by which this exact problem is prevented.

The deeper root cause is that 'Active Customer' was never subjected to the Business Glossary process: *steward facilitates → stakeholder groups provide input → Data Owner approves → DGC adopts → term is published as the enterprise standard.*

**Q2: How should this conflict be resolved?**

**Model Answer:** Data Steward facilitates alignment; Data Owner approves the official definition.

**Expanded DAMA Analysis:**

DAMA prescribes a structured resolution process for definitional conflicts:

```
STEP 1 — DOCUMENT THE CONFLICT
  Business Data Steward logs the conflict formally
  Documents both current definitions:
  • Finance: "Active Customer" = customer with at least one transaction in last 12 months
  • Marketing: "Active Customer" = customer who has opened an email or made a purchase in 6 months
  Documents the business impact: which decisions are affected by the inconsistency?

STEP 2 — CONVENE A CROSS-FUNCTIONAL ALIGNMENT WORKSHOP
  Business Data Steward facilitates
  Stakeholders: Finance, Marketing, Sales, senior business representatives
  Objective: understand WHY each definition was adopted; identify business use cases
  each definition was designed to serve

STEP 3 — DRAFT ENTERPRISE DEFINITION(S)
  Options:
  A) Single unified definition that serves both teams' needs
  B) One primary enterprise definition + documented sub-definitions
     for specific use cases (e.g., "Active Customer (Financial)" vs
     "Active Customer (Marketing Engagement)")
  Option B is often more pragmatic — forcing a single definition may
  not serve legitimate different business purposes

STEP 4 — DATA OWNER APPROVAL
  The Data Owner for Customer data reviews and approves the official definition(s)
  This is a formal governance decision — documented with rationale

STEP 5 — DGC ADOPTION (if disagreement persists or enterprise-wide impact)
  If Finance and Marketing cannot agree, escalate to DGC
  DGC exercises its judicial function — resolves the conflict by ruling
  The adopted definition is published to the Business Glossary

STEP 6 — PUBLISH, COMMUNICATE, ENFORCE
  Updated Business Glossary entry published with:
  • Official definition + any approved sub-definitions
  • Rationale for the decision
  • Effective date
  • Name of approving Data Owner
  • Review date
  All downstream reports and KPIs are updated to use the official definition
```

**Q3: Which artefact must be updated?**

**Model Answer:** The Business Glossary.

**Expanded DAMA Analysis:**

The **Business Glossary** is the primary artefact — but it is not the only one that must be updated:

| Artefact | Update Required |
|----------|----------------|
| **Business Glossary** | Primary — the term 'Active Customer' must have an approved, enterprise-wide definition entry including: definition, synonyms, approved sub-definitions, business rules, Data Owner, effective date, review cycle |
| **KPI / Metric Definitions Register** | Any KPI that uses 'Active Customer' as an input must be updated to reference the approved Glossary definition explicitly |
| **Data Dictionary** | Technical metadata in each system (CRM, finance system, data warehouse) must be aligned to the agreed business definition |
| **Report Specifications** | Finance and Marketing report specifications must be updated to reference the official definition and document any approved exceptions |
| **Data Quality Rules** | DQ rules that validate 'Active Customer' records must be updated to reflect the agreed definition criteria |

**Q4: Which CDMP principle applies?**

**Model Answer:** Standardization + Metadata Management.

**Expanded DAMA Analysis:**

| Principle | How It Applies |
|-----------|---------------|
| **Metadata Management** | Primary — the Business Glossary is a core Metadata management artefact. DMBOK2 Principle 4: "It takes Metadata to manage data." Without agreed definitions, data cannot be governed consistently |
| **Standardisation (DG Principle)** | Data standards must be defined and enforced by the DGC. A business term used across the enterprise without a DGC-approved standard definition is a governance failure |
| **Shared Responsibility (DG Principle)** | The resolution requires both Finance and Marketing to co-own the agreed definition — neither team can unilaterally define an enterprise term |
| **Multi-layered (DG Principle)** | The conflict originated at a local/departmental level; resolution requires enterprise-level governance authority (Data Owner approval, DGC adoption) |

**CDMP Exam Angle:**

This is a **Type 3 (Scenario)** and **Type 6 (Role/Responsibility)** question. The exam will ask: *"What is the FIRST action to take when two teams use different definitions for the same business term?"* The correct answer is **engage the Business Data Steward to facilitate a cross-functional alignment process** — not to pick one team's definition, not to ask IT to pick, and not to let both definitions co-exist. The DAMA answer always prioritises a facilitated, structured process leading to a single enterprise standard approved by the Data Owner.

**Malaysian Context:**

This scenario is extremely common in Malaysian conglomerates and GLCs where business units have developed independently. A Petronas subsidiary, a Maybank division, or a Telekom Malaysia business unit may each define "customer" differently after years of separate operation. When these entities are consolidated into group-level reporting, conflicting definitions produce reconciliation failures that can affect Board-level reporting. The resolution — a cross-divisional Business Glossary process with CDO sponsorship — is exactly the federated DG model DAMA prescribes.

---

## Scenario 4 — Data Quality Issue Not Logged

**Scenario:** A system frequently generates customer records with missing email addresses, but teams fix them manually instead of reporting the issue formally.

---

### Questions & Answers

**Q1: What governance failure occurred?**

**Model Answer:** Data quality issues are not being logged or escalated properly.

**Expanded DAMA Analysis:**

This scenario has two compounding governance failures — one visible and one hidden:

**Visible failure: Issue Management bypass**
The teams are resolving data quality problems informally — manually fixing records without logging the issue, without root-cause analysis, and without any governance record. This violates DAMA's **Issue Management** process (Chapter 3, Section 2.10), which requires that issues be: *identified, quantified, prioritised, and resolved* through a documented process.

**Hidden failure: Root cause never addressed**
Manual fixes treat symptoms, not causes. The system *frequently* generates records with missing email addresses — this is a **recurring, systemic issue**. Without formal logging, no one can:
- See the pattern across time
- Quantify the volume and business impact
- Assign root-cause analysis
- Hold the system or process owner accountable for fixing the source problem

DAMA Chapter 3 is explicit: *"Solving issues also proves that data can be managed and its quality improved. Successful issue management requires control mechanisms that demonstrate the work effort and impact of resolution."* Manual workarounds do none of these things.

The governance failure also violates the **Sustainability** characteristic of good DG — the organisation cannot sustain data quality without a feedback loop from issues to root-cause remediation.

**Q2: What process should be followed?**

**Model Answer:** Use the formal Data Quality Issue Management process and track via DQ KPIs.

**Expanded DAMA Analysis:**

DAMA prescribes a formal issue management lifecycle. For data quality issues specifically:

```
STEP 1 — LOG THE ISSUE
  Business Data Steward or any team member logs the issue in the
  governance issue management system with:
  • Issue description: customer records generated with missing email field
  • Frequency: how often does this occur? (quantify)
  • Business impact: which processes are affected by missing email data?
  • Date first observed vs date first reported (often these differ — the gap
    is itself a governance finding)

STEP 2 — CLASSIFY AND PRIORITISE
  Data Steward classifies the issue:
  • Issue type: Data Quality (completeness dimension — missing required field)
  • Priority: based on business impact (email is critical for marketing,
    customer comms, and PDPA contact preference management)

STEP 3 — ROOT-CAUSE ANALYSIS
  Data Steward coordinates with Technical Data Steward / Data Custodian
  to identify WHY the system generates records without email addresses:
  • Is the email field not mandatory in the source system?
  • Is there a system integration that drops the email field in transit?
  • Is the data entry process allowing records to be saved without email?

STEP 4 — RESOLUTION
  Data Owner approves the remediation approach:
  Option A: Fix the source system (make email mandatory / fix integration)
  Option B: Implement a data quality rule that flags/blocks records at ingestion
  Option C: Both — fix source + add downstream validation

STEP 5 — TRACK AND CLOSE
  Data Quality KPIs are updated to track the resolution:
  • Completeness rate for email field (% of records with valid email)
  • Trend over time — is the fix working?
  Issue is formally closed only when the root cause is resolved
  and KPIs confirm sustained improvement
```

**Q3: Which metrics should be used to track this issue?**

**Model Answer:** Track via DQ KPIs.

**Expanded DAMA Analysis:**

This issue involves the **Completeness** dimension of Data Quality. DAMA's Data Quality dimensions provide the framework for the right metrics:

| Metric | Definition | Target |
|--------|-----------|--------|
| **Email Completeness Rate** | % of customer records with a non-null, valid-format email address | ≥ 98% (define based on business need) |
| **New Record Completeness** | % of records created in the current period with a valid email | Tracks whether the source fix is working |
| **Issue Recurrence Rate** | Number of records requiring manual email correction per period | Should trend to zero after root-cause fix |
| **Time to Resolution** | Average time from issue identification to root-cause fix | Governance KPI — tracks DG programme effectiveness |
| **Manual Fix Volume** | Number of manual corrections made (before governance logging was enforced) | Baseline measure — should drop after formal process is in place |

These metrics should be reported on the **Data Governance Scorecard** (Chapter 3, Section 3.5) — so the DGC can see the trend and hold the process owner accountable for resolution.

**Q4: Which CDMP principle applies?**

**Model Answer:** Data Quality Management + Accountability.

**Expanded DAMA Analysis:**

| Principle | How It Applies |
|-----------|---------------|
| **Data Quality Management** | Primary — the completeness dimension is failing (missing email addresses). DMBOK2 Principle 3: "Managing data means managing the quality of data." The absence of a formal quality issue process means the problem cannot be systematically improved |
| **Accountability** | The teams fixing records manually have implicitly accepted responsibility — but without formal logging, there is no accountability for finding and fixing the root cause. Someone must own the resolution |
| **Stewardship** | Managing data as a valuable asset requires treating recurring quality issues as systemic problems, not routine maintenance tasks. Manual workarounds are not stewardship — they are data triage |
| **Measured (DG Essential Characteristic)** | A DG programme must demonstrate value through measurable improvement. Without logging, the DG programme cannot demonstrate that quality is improving — undermining its ability to sustain executive support |

**CDMP Exam Angle:**

This is a **Type 3 (Scenario)** and **Type 4 (Process/Framework)** question. The exam will ask what the organisation should do when it discovers teams are manually fixing data quality issues informally. The exam trap is answering "train the teams to fix the issue correctly." The correct DAMA answer is to **implement formal issue logging and root-cause analysis** — changing the process, not just the people doing the workaround. The governance fix (log → analyse → resolve root cause → track KPI) is always preferred over the manual fix (patch symptom → repeat indefinitely).

**Malaysian Context:**

This scenario maps directly to a common pattern in Malaysian banking and financial services — where operations teams manually correct customer data in CRM or core banking systems without logging the issue. BNM RMIT requires financial institutions to have a **data quality management framework** with documented issue tracking. During BNM examinations, examiners frequently ask: "Show me your data quality issue log and root-cause analysis for the past 12 months." An organisation with no formal logging cannot answer this question — and cannot demonstrate regulatory compliance.

---

## Scenario Summary Table

| # | Scenario | DG Issue Category | Primary Role | Escalation Path | CDMP Principles |
|---|----------|------------------|--------------|-----------------|-----------------|
| 1 | Unclear Data Ownership | Authority | Data Owner (to be assigned) | Steward → Steering Committee → DGC | Accountability + Stewardship |
| 2 | Policy Non-Compliance | Conformance | Data Custodian + Data Owner | Steward logs → DGC if repeated | Accountability + Lawfulness + Stewardship |
| 3 | Conflicting Definitions | Conflicts | Business Data Steward (facilitates) | Steward → Data Owner → DGC if unresolved | Standardisation + Metadata Management |
| 4 | DQ Issue Not Logged | Data Quality | Business Data Steward (logs + coordinates) | Formal Issue Management → DGC for systemic issues | Data Quality Management + Accountability |

---

## The DAMA Issue Escalation Path — Master Reference

All four scenarios follow variations of the same escalation path defined in DMBOK2 Chapter 3:

```
LEVEL 1 — LOCAL RESOLUTION
  Business Data Steward + Technical Data Steward
  → Most issues resolved here
  → Issues must be LOGGED even when resolved locally

LEVEL 2 — DATA STEWARDSHIP STEERING COMMITTEE
  → Escalated when: cross-functional conflict, resource needed,
    or local resolution failed
  → Coordinates across business units and domains

LEVEL 3 — DATA GOVERNANCE COUNCIL
  → Escalated when: decision rights unclear (Scenario 1),
    policy violated repeatedly (Scenario 2),
    definitional conflict persists (Scenario 3),
    systemic root-cause not being fixed (Scenario 4)
  → Exercises legislative (policy), judicial (conflict resolution),
    or executive (sponsorship) function as appropriate

LEVEL 4 — CORPORATE GOVERNANCE / EXECUTIVE MANAGEMENT
  → Escalated when: DGC cannot resolve, regulatory breach identified,
    or strategic data asset at risk
```

---

## Applying This to the CDMP Exam — Key Rules

| Exam Rule | Detail |
|-----------|--------|
| **Always log first** | In any governance scenario, the first action is to formally log the issue — not to fix it immediately. Logging enables tracking, accountability, and root-cause analysis |
| **Governance before execution** | Data quality fixes, data access grants, and definition changes all require governance approval before execution — not after |
| **DGC is the final authority** | When a scenario involves unresolved ownership, persistent conflict, or policy violation, the DGC is always the correct escalation destination |
| **Data Owner decides; Data Steward facilitates** | In role questions, the Data Steward facilitates, coordinates, and recommends — the Data Owner approves. Never confuse these two |
| **Business-driven, not IT-driven** | Any scenario where IT is presented as the decision-maker for data ownership, definitions, or quality standards is presenting an anti-pattern |
| **Root cause, not symptom** | The DAMA answer always addresses root cause — systemic fixes, policy changes, or operating model corrections — not one-time manual workarounds |

---

*References: DAMA-DMBOK2 Revised Edition, Chapter 3 | PDPA 2010 (Act 709) | BNM Risk Management in Technology (RMIT) 2020 | Data Governance Scenario Practice Workbook*
