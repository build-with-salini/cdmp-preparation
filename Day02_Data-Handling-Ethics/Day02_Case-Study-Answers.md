# Day 02 — Data Ethics Case Study Workbook: Answers & Analysis
**DAMA-DMBOK2 | Chapter 2 | Supplementary Material**

> *"Each case mirrors the reasoning style found in the CDMP exam — where success depends not on memorizing definitions but on demonstrating fairness, transparency, and accountability in data decisions."*
> — Data Ethics Case Study Workbook

---

## How to Use This Document

Each case study is answered at three levels:
1. **Model Answer** — the workbook's own guidance, reproduced for reference
2. **Expanded Analysis** — a deeper breakdown connecting the scenario to DMBOK2 Chapter 2 concepts and the specific ethical risks at play
3. **Malaysian Context** — how this scenario manifests in a Malaysian corporate setting with relevant regulatory links
4. **CDMP Exam Angle** — what the exam is testing with this type of question and how to frame your answer

---

## Ethical Principles Reference

| Principle | One-Line Summary |
|-----------|-----------------|
| **Fairness** | Avoid bias or discrimination in data processes |
| **Transparency** | Be open about how and why data is used |
| **Accountability** | Assign responsibility for data decisions |
| **Consent** | Obtain informed permission for data use |
| **Privacy** | Protect individuals' rights and information |
| **Stewardship** | Manage data as a valuable, trusted asset |
| **Lawfulness** | Follow all applicable laws and regulations |

---

## Case Study 1 — Customer Consent and Purpose Limitation

**Scenario:** A retail company wants to reuse customer purchase data to predict new product interests. The original consent form did not mention marketing analytics.

### Discussion Questions & Answers

**Q1: What ethical principle is at risk?**

**Model Answer:** Transparency and Consent.

**Expanded Analysis:**

Two principles are directly violated:

*Consent* is the primary violation. The customer provided personal data for a specific, stated purpose — processing their purchase transactions. Reusing that data for marketing analytics is a different purpose. DAMA's Chapter 2 is explicit: when data is reused beyond its original scope, new consent is required. The OECD's **Use Limitation Principle** (1980) and GDPR's **Purpose Limitation Principle** both establish this as a foundational rule. Customers have the right to expect their data will only be used for what they agreed to.

*Transparency* is the secondary violation. The original consent form did not disclose the marketing analytics use — this is a failure of openness. Even if the company now believes it has a legitimate interest in the analytics use, the lack of disclosure at collection point means customers were not given the information they needed to make an informed decision.

*Lawfulness* is also implicated — under PDPA 2010, processing personal data for a purpose beyond what was disclosed at collection is a potential breach of the Notice & Choice Principle and the General Principle.

**Q2: What actions could the company take to remain compliant?**

**Model Answer:** Obtain explicit new consent or anonymize data before reuse.

**Expanded Analysis:**

There are three defensible paths, in order of ethical preference:

| Option | Description | When Appropriate |
|--------|-------------|-----------------|
| **Re-consent** | Contact customers and explicitly request consent for the new analytics purpose, with a clear opt-in mechanism | Preferred when the customer relationship is active and direct communication is possible |
| **Anonymisation** | Aggregate and fully anonymise the purchase data so no individual can be identified, then use for analytics | Appropriate when individual-level analysis is not required — but anonymisation must be tested, not assumed |
| **Legitimate Interests Assessment (LIA)** | Conduct a formal assessment to determine whether the analytics use qualifies as a legitimate interest that does not override customer rights | Acceptable under GDPR in some jurisdictions, but PDPA 2010 requires more explicit consent — use with caution in Malaysia |

The option of simply proceeding without action is not acceptable. Neither is burying a new consent clause in a routine T&C update email with a pre-ticked box.

**Q3: What governance control should flag this issue?**

**Model Answer:** Data Governance Council or Privacy Officer review.

**Expanded Analysis:**

This type of issue should be caught by multiple governance layers before the analytics project proceeds:

| Governance Layer | How It Catches This |
|-----------------|---------------------|
| **Data Governance Council (DGC)** | Any new use of existing data should require DGC review — specifically a check that the proposed use falls within the consented purpose |
| **Privacy Officer / Data Protection Officer** | The DPO must review proposed data uses for PDPA compliance. Purpose creep is a standard DPO red flag |
| **SDLC Data Review Gate** | Analytics projects should include a data governance checkpoint in the project lifecycle — "what is the lawful basis for using this data?" |
| **Data Lineage / Metadata** | The consent scope should be documented as Metadata on the dataset — so when an analyst queries customer purchase data, the system surfaces the consent limitation |

### Malaysian Context

A Malaysian e-commerce retailer (e.g., Lazada MY, Shopee MY) collects purchase data under a consent form that mentions order fulfillment. If the marketing team decides to use that data for a recommender engine or targeted campaign without updating consent:

- This violates **PDPA 2010 — General Principle** (processing without consent) and **Notice & Choice Principle** (purpose not disclosed)
- The **PDPC (Personal Data Protection Commissioner)** can investigate complaints and impose penalties
- Brand trust damage in Malaysia's competitive e-commerce market can be significant

### CDMP Exam Angle

This is a **Type 3 (Scenario-Based)** question testing **Consent** and **Transparency**. The exam will present a similar situation and ask: "What is the FIRST thing the organisation should do?" The correct answer is always to halt the analytics use and review whether lawful consent exists — not to proceed and add a disclosure footnote later.

---

## Case Study 2 — Algorithmic Bias in Hiring

**Scenario:** An HR analytics team uses a historical recruitment dataset to train an AI screening model. It rejects more women than men.

### Discussion Questions & Answers

**Q1: What ethical issues are present?**

**Model Answer:** Bias, lack of fairness and inclusivity.

**Expanded Analysis:**

The ethical issues are layered and compound each other:

**Biased training data → biased model outputs**
The historical recruitment dataset reflects past hiring decisions — which were themselves made by humans who may have had implicit or explicit gender biases. When a model is trained on this history, it learns to replicate those biases. The model is not "neutral" — it is a systematic codification of historical discrimination.

**Disparate impact**
The outcome — more women rejected than men for equivalent qualifications — is a **disparate impact** result. Under most fair employment frameworks, disparate impact is treated as discrimination even if there was no discriminatory intent. The ethical issue exists regardless of whether the model was built with malicious intent.

**Lack of human oversight**
If the model's outputs are applied without human review, there is no mechanism to catch or correct discriminatory outcomes. Automated discrimination at scale causes harm faster and more efficiently than individual human decision-making.

**Q2: Which DMBOK principle applies?**

**Model Answer:** Fairness and Accountability.

**Expanded Analysis:**

| Principle | How It Applies |
|-----------|---------------|
| **Fairness** | Primary — the model produces discriminatory outcomes that disadvantage women. Positive duty to identify and correct bias exists |
| **Accountability** | Who is responsible for the model's outcomes? The HR analytics team, the model owner, and the governance body that approved deployment all share accountability |
| **Transparency** | Can the model explain why a candidate was rejected? If not, candidates and regulators cannot assess whether the decision was fair |
| **Stewardship** | The training data was not properly audited before use — poor data stewardship enabled the bias |

**Q3: How could governance mitigate bias risk?**

**Model Answer:** Review training data, apply bias detection, document results, and report findings.

**Expanded Analysis:**

A complete governance response involves pre-deployment, deployment, and post-deployment controls:

| Phase | Governance Action |
|-------|------------------|
| **Pre-deployment** | Audit training dataset for demographic representation; apply bias detection algorithms; document methodology; require DGC ethics review before go-live |
| **At deployment** | Require human review for all model-influenced decisions; document decision logic in a model card; establish a Model Owner accountable for ongoing performance |
| **Post-deployment** | Monitor rejection rates by gender, ethnicity, age quarterly; establish a feedback mechanism for candidates to challenge decisions; annual bias audit |
| **Escalation** | Define thresholds: if disparate impact ratio falls below 0.8 (the EEOC "4/5ths rule" standard), escalate to DGC and pause automated screening |

### Malaysian Context

Under Malaysia's **Employment Act 1955** and **Industrial Relations Act 1967**, employment decisions must not discriminate on protected grounds. While Malaysia does not yet have a dedicated AI fairness regulation, BNM's **CCRIS (Central Credit Reference Information System)** governance principles and the emerging **Malaysian AI Governance Framework (AIGF)** by MDEC set expectations for fairness in algorithmic decision-making.

A Malaysian bank's HR team using a biased screening model for hiring would face reputational risk if the disparate impact became public — and potential regulatory scrutiny if the bias mirrored demographics that overlap with race or religion categories protected under Malaysian law.

### CDMP Exam Angle

This is a **Type 3 (Scenario)** and **Type 10 (Judgment)** question. The exam will ask what the data professional should do first — the correct answer is NOT "deploy the model and monitor." It is to halt deployment, audit training data for bias, document findings, and obtain governance approval before proceeding. The positive duty to address bias is the key concept.

---

## Case Study 3 — Social Listening and Privacy

**Scenario:** Your marketing team mines social media posts to identify customer sentiment, including personal comments and usernames.

### Discussion Questions & Answers

**Q1: Which ethical boundaries are being crossed?**

**Model Answer:** Misuse of public personal data without consent.

**Expanded Analysis:**

The "it's public data" argument is the most common misconception in social media analytics — and it is ethically and legally flawed:

**Public ≠ Consented for all uses**
When a person posts on social media, they consent to that platform's terms of service. They do not consent to having their comments harvested by a third-party organisation and processed for commercial sentiment analysis. The context in which data was shared (public social conversation) is different from the context in which it is being used (commercial intelligence gathering). This is the concept of **contextual integrity** — data flows are ethical when they match the norms of the context in which information was shared.

**Username = Personal Data**
A username linked to an account is personal data under PDPA — it can identify an individual. Processing it without consent and without disclosure is a PDPA violation.

**Personal comments may be sensitive**
Social media posts can reveal health information, political views, religious beliefs, or financial situations — all potentially sensitive data categories deserving heightened protection.

**Q2: What principle(s) are in conflict?**

**Model Answer:** Privacy and Respect for Individuals.

**Expanded Analysis:**

| Principle | Conflict |
|-----------|---------|
| **Privacy** | Individuals retain privacy interests in their personal data even when posted publicly — contextual integrity applies |
| **Consent** | No consent was obtained for the commercial processing of personal posts and usernames |
| **Fairness** | If sentiment analysis is used to make decisions affecting customers (e.g., credit, service tiers), individuals are being assessed on data they did not know would be used for this purpose |
| **Lawfulness** | Platform Terms of Service typically prohibit scraping for commercial purposes — mining may violate both platform ToS and PDPA |

**Q3: What is an acceptable ethical alternative?**

**Model Answer:** Aggregate or anonymize; ensure compliance with platform policies.

**Expanded Analysis:**

| Alternative | Description | Ethical Assessment |
|-------------|-------------|-------------------|
| **Aggregate sentiment only** | Count positive/negative sentiment by topic at group level — no individual usernames or posts retained | Acceptable — individual privacy preserved |
| **Licensed data** | Use platform-licensed data APIs that are structured for commercial analytics with appropriate ToS | Acceptable — lawful basis exists |
| **First-party feedback** | Use opt-in surveys, ratings, and reviews where customers knowingly provide feedback | Preferred — genuine consent exists |
| **Full anonymisation before processing** | Strip usernames and any identifying information before any human analyst sees the data | Acceptable if anonymisation is tested and robust |
| **Do not retain individual records** | Perform analysis in memory and discard individual records — only aggregate outputs are stored | Acceptable for aggregate sentiment purposes |

### Malaysian Context

Under **PDPA 2010**, collecting personal data (including usernames) from social media for commercial processing without consent is a potential breach. The **MCMC (Malaysian Communications and Multimedia Commission)** also has jurisdiction over digital data practices. Malaysian social media users have filed complaints with PDPC about scraping of their content by commercial entities.

Additionally, most major platforms (Facebook/Meta, Instagram, TikTok, X) explicitly prohibit scraping of user content for commercial purposes in their ToS — giving organisations a **Lawfulness** problem in addition to the ethics issues.

### CDMP Exam Angle

This is a **Type 3 (Scenario)** question. The exam trap is assuming that because data is publicly visible, it is freely usable. The correct DAMA answer emphasises contextual integrity, the definition of personal data (usernames qualify), and the requirement for either consent or proper anonymisation before commercial use.

---

## Case Study 4 — Cross-Border Data Transfers

**Scenario:** A financial firm transfers customer data from the EU to the US for analytics without reviewing data transfer agreements.

### Discussion Questions & Answers

**Q1: What regulation or principle is relevant here?**

**Model Answer:** Lawfulness and Accountability.

**Expanded Analysis:**

**GDPR Chapter V** (Articles 44-49) governs international data transfers from the EU. The core rule: personal data may only be transferred to a third country if that country provides an adequate level of data protection, or if appropriate safeguards are in place (e.g., Standard Contractual Clauses, Binding Corporate Rules, or an adequacy decision).

The United States does not have a blanket GDPR adequacy decision — transfers to the US require specific mechanisms. Transferring customer data EU→US for analytics without reviewing applicable agreements is a direct GDPR violation — and under GDPR, fines can reach 4% of global annual turnover.

From a DAMA perspective, this also violates:

| Principle | Violation |
|-----------|----------|
| **Lawfulness** | No legal basis established for the cross-border transfer |
| **Accountability** | The governance function failed to review and approve the data transfer arrangement |
| **Transparency** | Data subjects were likely not informed that their data would be transferred internationally |
| **Stewardship** | The data was not managed with care — cross-border flows require documented governance |

**Q2: What governance process should exist?**

**Model Answer:** Data Governance Committee oversight and data transfer assessments.

**Expanded Analysis:**

| Governance Process | Description |
|-------------------|-------------|
| **Data Transfer Impact Assessment** | Formal assessment of the legal basis, data subjects affected, safeguards in place, and residual risks for every international transfer |
| **DGC / Legal Counsel Review** | All cross-border data transfers must be reviewed and approved by the Data Governance Council and Legal before execution |
| **Data Transfer Agreement Register** | A maintained register of all cross-border data flows, their legal basis, and the agreements in place |
| **Vendor Due Diligence** | Any third-party processor in a foreign jurisdiction must sign a Data Processing Agreement (DPA) that includes appropriate transfer mechanisms |
| **Regular Review** | Transfer arrangements must be reviewed when regulations change — e.g., Schrems II (2020) invalidated the EU-US Privacy Shield, creating compliance gaps for organisations that relied on it |

**Q3: How can accountability be ensured?**

**Model Answer:** Apply Standard Contractual Clauses (SCCs) and inform data subjects.

**Expanded Analysis:**

| Accountability Mechanism | Detail |
|-------------------------|--------|
| **Standard Contractual Clauses (SCCs)** | The EU's approved contractual mechanism for EU→non-adequate-country transfers; must use current 2021 versions post-Schrems II |
| **Data Subject Notification** | Privacy notices must disclose international transfers — to which countries and under what safeguards |
| **DPO Sign-off** | Data Protection Officer must formally approve all cross-border transfer arrangements |
| **Board-level Accountability** | Under BNM RMIT, senior management and boards of Malaysian financial institutions are accountable for data governance, including cross-border flows |
| **Audit Trail** | Document who approved the transfer, what assessment was performed, and what safeguards are in place |

### Malaysian Context

Malaysian financial institutions operating in the EU (e.g., Maybank's London operations, CIMB's EU presence) must comply with GDPR for EU resident data. Simultaneously, **PDPA 2010 Section 129** restricts transfers of personal data outside Malaysia unless the destination country provides "adequate protection" or exceptions apply.

A Malaysian fintech with EU customers sending data to a US analytics provider faces a **dual compliance burden**: GDPR for the EU→US transfer AND PDPA for the Malaysia→US transfer. Both require documented safeguards.

### CDMP Exam Angle

This is a **Type 4 (Process/Framework)** and **Type 2 (Principle-Based)** question. The exam will ask what the organisation should have done before the transfer. The correct sequence is: assess → document lawful basis → execute appropriate safeguard (SCC/BCR) → inform data subjects → maintain register. Proceeding without this process is a Lawfulness violation.

---

## Case Study 5 — Over-Collection in Data Projects

**Scenario:** A data team collects more attributes than necessary 'just in case' they're useful later.

### Discussion Questions & Answers

**Q1: Which principle is violated?**

**Model Answer:** Stewardship and Purpose Limitation.

**Expanded Analysis:**

**Data Minimisation** (called **Purpose Limitation** in the workbook) is one of the most fundamental data ethics principles — enshrined in GDPR, the OECD framework, and PDPA:

*You should collect only the data you need for the specific purpose you have stated.*

"Just in case" collection is a direct violation because:

| Violation | Detail |
|-----------|--------|
| **No stated purpose** | If the purpose for collecting an attribute is "we might find it useful later," there is no specific, declared purpose — a core PDPA requirement |
| **Excess privacy risk** | Every additional attribute collected increases the privacy risk surface — more data means more harm if breached |
| **Consent overreach** | Customers consented to provide data for a specific purpose — not to have additional attributes collected speculatively |
| **Storage and quality costs** | Unnecessary data incurs storage costs, complicates data quality management, and creates compliance risk during audits |
| **Stewardship failure** | Good stewardship means managing data to its minimum necessary footprint — not accumulating data as a hedge |

**Q2: What should governance enforce?**

**Model Answer:** Data Collection Policy and periodic audits.

**Expanded Analysis:**

| Governance Control | Description |
|-------------------|-------------|
| **Data Collection Policy** | Mandatory policy requiring a stated, specific purpose for every attribute collected — approved by Data Owner before collection begins |
| **Privacy Impact Assessment (PIA)** | Required before any new data collection — identifies whether proposed data points are necessary and proportionate |
| **Data Minimisation Review Gate** | SDLC checkpoint: before a project goes to build, a data governance review confirms only necessary attributes are in scope |
| **Periodic Data Attribute Audits** | Quarterly or annual review of collected attributes against stated purpose — unused attributes flagged for deletion |
| **Automated Data Profiling** | Tooling that identifies attributes with very low usage rates — candidates for removal |

**Q3: What's the ethical response?**

**Model Answer:** Limit data to minimum required; delete unnecessary fields.

**Expanded Analysis:**

The ethical response is a three-part remediation:

**Immediate:** Stop collecting attributes that do not have a documented, specific purpose.

**Retrospective:** Audit existing datasets to identify "just in case" attributes — assess each against the stated data collection purpose. Delete those that cannot be justified.

**Structural:** Embed data minimisation as a design principle — data architects and analysts are trained to ask "do we need this?" not "is it available?"

In practice, this means:
- Each attribute in a dataset must have a documented business purpose in the data dictionary
- Attributes with no documented purpose within 90 days of collection are flagged for deletion
- Data collection forms and API requests are reviewed against the minimum necessary standard before implementation

### Malaysian Context

In Malaysia, the PDPA's **General Principle** requires a lawful basis for processing — speculative collection has no basis. The **Notice & Choice Principle** requires disclosure of purpose at collection — "just in case" is not a disclosable purpose. A PDPC audit finding that an organisation holds personal data with no documented purpose can result in enforcement action.

Malaysian organisations building data lakes face this risk acutely — data is often ingested from source systems without a clear use case, creating a compliance liability that grows with every ingestion cycle.

### CDMP Exam Angle

This is a **Type 3 (Scenario)** and **Type 6 (Role/Responsibility)** question. The exam will present over-collection as a data management practice and ask which principle is violated. The answer is **Stewardship** (managing data with care and integrity, not accumulating it) combined with **Privacy** (data minimisation). The governance response is always: policy + audit + deletion.

---

## Case Study 6 — AI Explainability and Transparency

**Scenario:** A bank deploys an AI model to determine loan approvals. Customers are denied loans but cannot see why.

### Discussion Questions & Answers

**Q1: What ethical issues arise?**

**Expanded Analysis:**

| Ethical Issue | Detail |
|--------------|--------|
| **Lack of explainability** | Customers affected by the model's decision cannot understand or challenge it — a fundamental violation of the right to explanation |
| **No recourse** | Without an explanation, customers cannot identify errors, provide correcting information, or appeal the decision |
| **Potential hidden bias** | A black-box model that cannot be explained also cannot be audited for bias — Fairness cannot be verified |
| **Regulatory non-compliance** | GDPR Article 22 gives individuals the right not to be subject to solely automated decisions with significant effects, without explanation. Malaysian BNM RMIT requires model explainability for credit decisions |
| **Trust erosion** | Customers who are denied credit without explanation lose trust in the institution — with significant reputational consequences |

**Q2: What principle applies?**

**Model Answer:** Transparency and Accountability.

**Expanded Analysis:**

| Principle | Application |
|-----------|-------------|
| **Transparency** | Primary — customers must be able to understand the basis for decisions that materially affect them. Explainability is the operationalisation of transparency in AI systems |
| **Accountability** | Who owns the model? Who is responsible when it produces wrong or harmful decisions? If no one can explain the model, no one can be held accountable for its outputs |
| **Fairness** | If the model cannot be explained, its fairness cannot be verified — bias may be present and undetected |
| **Lawfulness** | BNM RMIT and emerging AI governance frameworks in Malaysia require explainability for credit decisions. GDPR Article 22 is relevant for EU-connected operations |

**Q3: What corrective action should be taken?**

**Model Answer:** Provide model explanations, human review, and clear communication to customers.

**Expanded Analysis:**

| Corrective Action | Detail |
|------------------|--------|
| **Model Documentation (Model Card)** | Document the model's purpose, training data, performance metrics, known limitations, and fairness testing results |
| **Explainability Layer** | Implement an explainability framework (e.g., SHAP — SHapley Additive exPlanations, or LIME) that can produce human-readable explanations for individual decisions |
| **Customer Communication** | Every denial must be accompanied by a written explanation of the primary factors that contributed to the decision — in plain language, not model jargon |
| **Human Review Right** | Establish a process for customers to request human review of automated decisions — this is a GDPR requirement and ethical best practice |
| **Governance Approval** | The DGC and Risk function must formally approve AI models used in credit decisions before deployment — including review of explainability and fairness documentation |
| **Ongoing Monitoring** | Post-deployment: monitor decision distribution by demographic group; track customer complaints related to AI decisions; annual model audit |

### Malaysian Context

**BNM RMIT 2020** requires financial institutions to ensure that models used in credit and risk decisions are explainable and auditable. A Malaysian bank deploying a black-box AI loan model without explainability documentation would fail a BNM examination — specifically under the Model Risk Management requirements.

The **Malaysian AI Governance Framework (AIGF)** published by MDEC explicitly lists explainability and human oversight as core principles for AI systems affecting individuals. As Malaysia's regulatory environment evolves, unexplainable AI in credit decisions will face increasing scrutiny.

For individual customers: under PDPA's **Access Principle**, a data subject can request access to information about them used in processing — including the basis for automated decisions. If the bank cannot provide this, it is in breach.

### CDMP Exam Angle

This is a **Type 3 (Scenario)** and **Type 10 (Judgment)** question. The exam will ask: "A bank uses an AI model for loan decisions and cannot explain its outputs. What should the data management professional do?" The correct answer is NOT "accept this as a limitation of AI." It is to require explainability documentation, implement human review, and escalate the absence of a model governance framework to the DGC. The combination of Transparency + Accountability is the correct framing.

---

## Reflection — Connecting Theory to Practice

The workbook's final reflection questions, answered with a CDMP exam and Malaysian practice lens:

**Which of these cases reflects a challenge in your organisation?**

For most Malaysian organisations, Case Study 5 (Over-Collection) and Case Study 1 (Purpose Creep/Consent) are the most common. Data lakes filled with "just in case" data, and analytics teams reusing customer data without re-consent, are endemic patterns in both large corporates and technology companies.

Case Study 6 (AI Explainability) is increasingly relevant as Malaysian banks and insurers deploy machine learning models for credit and underwriting decisions under BNM scrutiny.

**How could your governance framework respond?**

The governance response to all six cases follows the same structure:

| Step | Action |
|------|--------|
| 1 | Identify: Which principle is violated? |
| 2 | Halt: Stop the practice immediately if it poses ongoing harm |
| 3 | Assess: Perform a formal review (PIA, Data Transfer Assessment, Bias Audit) |
| 4 | Remediate: Fix the root cause — not just the symptom |
| 5 | Prevent: Update policy, governance controls, and SDLC gates so this cannot recur |
| 6 | Monitor: Establish ongoing checks to detect future violations |

**What new controls or policies could strengthen ethical data practices?**

| Control | Case(s) Addressed |
|---------|------------------|
| Data Collection Policy with mandatory purpose documentation | Cases 1, 5 |
| Bias Audit requirement for all ML models before deployment | Cases 2, 6 |
| Social Media Data Governance Policy | Case 3 |
| Cross-Border Data Transfer Register and approval process | Case 4 |
| Model Governance Framework (explainability + human review) | Cases 2, 6 |
| Privacy Impact Assessment gate in SDLC | Cases 1, 3, 5 |
| Annual ethics training + sign-off for all data practitioners | All cases |

---

## Case Study Summary Table

| # | Case | Primary Principle(s) | Secondary Principle(s) | Governance Control | Key Action |
|---|------|----------------------|------------------------|-------------------|------------|
| 1 | Customer Consent & Purpose Limitation | Consent, Transparency | Lawfulness | DGC / Privacy Officer review | Re-obtain consent or anonymise before reuse |
| 2 | Algorithmic Bias in Hiring | Fairness, Accountability | Transparency, Stewardship | Ethics review before deployment | Audit training data; apply bias detection; human review |
| 3 | Social Listening & Privacy | Privacy, Consent | Lawfulness, Fairness | Social media data policy | Aggregate/anonymise; comply with platform ToS |
| 4 | Cross-Border Data Transfers | Lawfulness, Accountability | Transparency, Privacy | Data transfer assessment + DGC approval | Apply SCCs; inform data subjects; maintain register |
| 5 | Over-Collection | Stewardship, Privacy | Consent, Lawfulness | Data collection policy + periodic audits | Limit to minimum required; delete unnecessary fields |
| 6 | AI Explainability | Transparency, Accountability | Fairness, Lawfulness | Model governance framework + DGC approval | Provide model explanations; implement human review |

---

*References: DAMA-DMBOK2 Revised Edition, Chapter 2 | Data Ethics Case Study Workbook | PDPA 2010 (Act 709) | GDPR 2016 | BNM RMIT 2020 | MDEC Malaysian AI Governance Framework | OECD Fair Information Processing Standards 1980*
