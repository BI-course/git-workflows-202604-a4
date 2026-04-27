# Data Governance and Access to PII

## Overview

**Data governance** refers to the set of policies, processes, standards, and responsibilities that ensure data is managed properly across an organization. It defines who can access data, how it is stored, how long it is retained, and how it is protected — especially when it involves **Personally Identifiable Information (PII)**.

---

## What is PII?

**Personally Identifiable Information (PII)** is any data that can be used to identify a specific individual, either on its own or in combination with other information.

### Examples of PII

| Category         | Examples                                      |
|------------------|-----------------------------------------------|
| Direct Identifiers | Full name, National ID, passport number     |
| Contact Information | Email address, phone number, home address |
| Financial Data   | Bank account number, credit card details      |
| Biometric Data   | Fingerprints, facial recognition data         |
| Online Identifiers | IP address, cookies, login credentials     |
| Health Data      | Medical records, insurance information        |

---

## Key Data Governance Principles

### 1. Data Ownership
Every dataset must have an assigned **data owner** — a person or team responsible for its accuracy, access control, and compliance.

### 2. Data Classification
Data should be classified by sensitivity level to determine how it is handled:

| Classification | Description                          | Example              |
|----------------|--------------------------------------|----------------------|
| Public         | Freely shareable                     | Company website info |
| Internal       | For staff use only                   | Internal reports     |
| Confidential   | Restricted access                    | HR records           |
| Restricted/PII | Highest protection required          | Customer ID data     |

### 3. Access Control
Access to data — especially PII — should follow the **Principle of Least Privilege (PoLP)**: users are granted only the minimum access they need to perform their job.

- **Role-Based Access Control (RBAC)** — access granted based on job role.
- **Attribute-Based Access Control (ABAC)** — access based on user attributes and data sensitivity.

### 4. Data Minimization
Collect only the data that is strictly necessary for the intended purpose. Avoid storing PII unnecessarily.

### 5. Data Retention and Deletion
Define how long PII is retained and ensure it is securely deleted when no longer needed, in line with legal requirements.

### 6. Audit and Monitoring
All access to PII should be logged and regularly audited to detect unauthorized access or misuse.

---

## Legal and Regulatory Frameworks

Organizations handling PII must comply with applicable data protection laws:

| Regulation | Region        | Key Requirements                              |
|------------|---------------|-----------------------------------------------|
| GDPR       | European Union| Consent, right to erasure, breach notification|
| CCPA       | California, USA| Consumer rights over personal data           |
| HIPAA      | USA           | Protection of health-related PII              |
| Kenya Data Protection Act (2019) | Kenya | Lawful processing, data subject rights |

---

## PII Access Best Practices

1. **Encrypt PII at rest and in transit** — use AES-256 for storage and TLS for transmission.
2. **Anonymize or pseudonymize data** where full PII is not required for analysis.
3. **Implement Multi-Factor Authentication (MFA)** for systems storing PII.
4. **Conduct regular Data Protection Impact Assessments (DPIAs)** for high-risk processing.
5. **Train staff** on data handling policies and breach reporting procedures.
6. **Establish a breach response plan** — including notification timelines (e.g., 72 hours under GDPR).

---

## Data Governance Roles

| Role                    | Responsibility                                      |
|-------------------------|-----------------------------------------------------|
| Data Owner              | Accountable for data quality and access decisions   |
| Data Steward            | Enforces governance policies day-to-day             |
| Data Custodian          | Manages technical storage and security              |
| Data Protection Officer (DPO) | Ensures regulatory compliance (required under GDPR) |
| End User                | Uses data within permitted scope                    |

---

## Summary

Effective data governance ensures that PII is handled responsibly, securely, and in compliance with legal requirements. Organizations that invest in strong governance frameworks reduce the risk of data breaches, maintain customer trust, and avoid regulatory penalties.

---

## References

- Kenya Data Protection Act, 2019. [Office of the Data Protection Commissioner](https://www.odpc.go.ke)
- European Parliament. (2016). *General Data Protection Regulation (GDPR)*. [gdpr.eu](https://gdpr.eu)
- NIST. (2020). *Guide to Protecting the Confidentiality of Personally Identifiable Information (PII)*. SP 800-122.
