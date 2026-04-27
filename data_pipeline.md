# Data Pipeline Architectures: ETL, ELT, and EtLT

## Overview
Data pipelines define how raw data moves from source systems to storage or analytics targets. The three dominant patterns — **ETL**, **ELT**, and **EtLT** — differ in *where* and *when* transformation occurs. This distinction has major implications for regulatory compliance, data governance, auditability, and legal defensibility across industries such as finance, healthcare, and telecommunications.

Understanding these differences is critical for organisations that must satisfy frameworks such as **GDPR**, **HIPAA**, **PCI-DSS**, **SOX**, and local regulations like Kenya's **Data Protection Act (2019)**.

## Pipeline Patterns

### 1. ETL — Extract, Transform, Load
Data is extracted from source systems, transformed in a dedicated middleware layer, and only the cleaned/compliant result is loaded into the target warehouse.
- **Tools:** Informatica, Talend, AWS Glue, Apache NiFi
- **Use in compliance:** Stripping PII before it enters storage; enforcing masking rules at ingestion time
- **Characteristics:** Transformation happens outside the warehouse; raw records are not retained after load

**Compliance strengths:**
- PII/PHI is anonymised or pseudonymised before reaching the warehouse, reducing breach exposure
- Simplifies GDPR Right to Erasure (Art. 17) — sensitive data was never stored
- Clear, single-stage transformation is easier to document for auditors

**Compliance weaknesses:**
- Raw records are discarded, making it unsuitable where original data retention is legally required (e.g., SOX 7-year retention, FINRA)
- Transformation logic lives in middleware, which can be opaque to compliance auditors
- Scaling pressure may create incentives to skip compliance steps

---

### 2. ELT — Extract, Load, Transform
Raw data is loaded directly into a modern cloud data warehouse, and transformations are performed inside the warehouse using SQL-based tools.
- **Tools:** dbt, Snowflake, Google BigQuery, Amazon Redshift, Databricks
- **Use in compliance:** Retaining full audit trails; enabling reproducible, version-controlled transformation logic
- **Characteristics:** Raw data is preserved in a raw zone; transformations are transparent and auditable via SQL

**Compliance strengths:**
- Full raw record retention satisfies legal hold and audit trail requirements (SOX, FINRA, FDA 21 CFR Part 11)
- SQL transformations in version-controlled tools (dbt + Git) are fully reproducible and auditable
- Column-level data lineage supports GDPR Article 5 accountability and CCPA compliance

**Compliance weaknesses:**
- Raw PII/PHI/CHD lands in cloud storage, increasing the scope of HIPAA, PCI-DSS, and GDPR obligations
- Right to Erasure is operationally complex — data may exist across raw zones, backups, and derived tables
- Data residency risk — raw PII loading to cloud regions may violate cross-border transfer laws (GDPR Chapter V, Kenya DPA)

---

### 3. EtLT — Extract, small-transform, Load, Transform
A hybrid approach: lightweight compliance-critical transformations (masking, tokenisation, encryption) are applied before loading, followed by full business-logic transformations inside the warehouse.
- **Tools:** Combination of ETL middleware (for small-t) + dbt/Snowflake/BigQuery (for big-T)
- **Use in compliance:** Organisations facing multiple simultaneous regulatory obligations (e.g., HIPAA + SOX, GDPR + PCI-DSS)
- **Characteristics:** PII is masked before the warehouse; masked raw records and full SQL lineage are both retained

**Compliance strengths:**
- PII never enters the warehouse unmasked, minimising breach impact and regulatory scope
- Masked raw records are retained, satisfying legal hold and audit trail requirements
- Separation of concerns — security team owns the small-t compliance gateway; data engineers own big-T analytics logic
- Embeds Privacy-by-Design into the pipeline architecture (GDPR Art. 25)

**Compliance weaknesses:**
- Two transformation layers create two audit surfaces, increasing compliance documentation overhead
- Risk of PII leakage if the small-t step does not cover all sensitive fields
- Requires coordinating multiple toolsets, increasing misconfiguration risk

---

## Comparison by Legal Requirement

| Legal Requirement | ETL | ELT | EtLT |
|---|---|---|---|
| PII/PHI never stored unmasked | ✅ | ⚠️ Requires controls | ✅ |
| Raw record retention (SOX, FINRA) | ❌ | ✅ | ✅ |
| GDPR Right to Erasure | ✅ Easy | ❌ Complex | ⚠️ Moderate |
| Reproducible audit trail | ⚠️ | ✅ | ✅ |
| Data residency / cross-border control | ✅ | ⚠️ | ✅ |
| PCI-DSS cardholder data protection | ✅ | ❌ High risk | ✅ |
| Fraud detection / full history needed | ❌ | ✅ | ✅ |

---

## Industry-Specific Compliance Fit

### Healthcare (HIPAA / Kenya Health Act)
PHI must be protected at all stages. Raw records must be auditable. EtLT is the strongest fit — PHI is masked before the warehouse, while a complete masked audit trail is retained for regulatory review.

### Financial Services (SOX, PCI-DSS, FINRA / CBK Guidelines)
Seven-year retention of financial records rules out pure ETL. Cardholder data protection rules against storing raw records in ELT without strong controls. EtLT satisfies both by tokenising sensitive fields before load while preserving full record history.

### Telecommunications (TCPA, Kenya Electronic Communications Act, GDPR)
Call Detail Records (CDRs) must be retained per regulation, eliminating ETL. Subscriber PII must be protected, creating risk with raw-zone ELT. EtLT pseudonymises subscriber data before load while retaining CDR history.

### E-Commerce & Retail (GDPR, CCPA, PCI-DSS)
Right to Erasure and Right to Portability create competing demands — erasure favours ETL, portability favours ELT. EtLT resolves this through tokenisation: individual records can be erased by invalidating their token, while the full dataset structure is preserved.

## Conclusion
No single pipeline architecture is universally compliant. The right choice depends on which legal obligations dominate, what data the pipeline handles, and how the organisation balances privacy, auditability, scalability, and data utility. In multi-regulatory environments, **EtLT** provides the most robust compliance posture by combining the privacy guarantees of ETL with the auditability and scalability of ELT.
