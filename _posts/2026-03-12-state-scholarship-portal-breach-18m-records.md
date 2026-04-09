---
layout: post
title: "State Government Scholarship Portal Breach: 18.2 Million Aadhaar Records and Student Data Sold on Dark Web"
subtitle: "Independent verification of a critical breach targeting a southern Indian state's e-Governance scholarship platform. 146 GB exfiltrated from three AWS RDS instances, including Aadhaar numbers, banking details, and minor student data — listed for USD 4,000 on a prominent cybercrime forum."
date: 2026-03-12
category: "Data Breach Intelligence"
author: "Sw4pn33"
author_role: "Threat Intelligence Researcher"
readtime: "18"
tags: [data-breach, OSINT, India, Aadhaar, scholarship, e-Governance, AWS, dark-web, HUMINT, student-data, PII]
---

## Executive Summary

On **15 February 2026**, a threat actor gained unauthorized access to the backend infrastructure of a **state government scholarship portal** operated by a southern Indian state's e-Governance agency. The portal serves as the unified platform for processing scholarship applications for students across the state.

The breach resulted in the exfiltration of approximately **146 gigabytes** of data spanning **215 database tables** from **three database servers** hosted on cloud infrastructure. The compromised dataset includes highly sensitive personal information belonging to millions of students, their parents and guardians, and administrative users.

| Metric | Value |
|--------|-------|
| National ID Records | **18.2M** |
| Phone Numbers | **15.9M** |
| Email Addresses | **2.8M** |

The stolen data was subsequently listed for sale on a prominent cybercrime forum for **USD $4,000**, offered as an exclusive "single buyer" sale with escrow protection. The listing included detailed field descriptions and sample data as proof of authenticity.

Through **human intelligence (HUMINT)** gathering, the researcher was able to independently verify the breach claims by identifying critical misconfigurations in the portal's infrastructure. We confirmed that the attack vector exploited **sensitive configuration exposure** combined with **insufficient access controls** on cloud-hosted database services, allowing unauthorized external access to production databases containing the exact dataset described in the forum listing.

> **CRITICAL FINDING:** At the time of this report, the underlying vulnerability that enabled the initial breach **has not been fully remediated**. While some access restrictions have been partially implemented, the core misconfiguration that led to the exposure of sensitive infrastructure credentials remains a concern and requires immediate attention.

---

## Incident Overview

### Target: State Government Scholarship Portal

The affected system is a **unified state scholarship portal** operated by the e-Governance agency of a major southern Indian state. The portal serves as the centralized digital platform for:

- Student scholarship application processing and management
- Eligibility verification through national ID (Aadhaar) integration
- Parent and guardian information collection for means-tested scholarships
- Financial disbursement through integrated banking systems
- Administrative user management for educational institutions

| Property | Detail |
|----------|--------|
| Target Type | State Government Web Application |
| Sector | Education / Government Services |
| Hosting | Cloud-hosted (Amazon Web Services) |
| Database System | PostgreSQL (Amazon RDS) |
| User Base | Millions of students and educational institutions statewide |

### Timeline of Events

| Date | Event |
|------|-------|
| **15 Feb 2026** | Threat actor gains unauthorized access to three production database servers and exfiltrates 146 GB of data across 215 tables |
| **~Late Feb 2026** | Complete dataset is listed for sale on a prominent cybercrime forum, with sample data and schema details provided as proof of access |
| **~Early Mar 2026** | Through HUMINT, the researcher identifies the dark web listing and begins independent verification |
| **Mar 2026** | Verification complete. Attack vector and vulnerable infrastructure components are identified and confirmed. This report is compiled |

### Breach Discovery

The breach was discovered through **proactive dark web monitoring and human intelligence operations**. During routine surveillance of cybercrime forums, the researcher identified a listing offering a large-scale Indian government database for sale. Cross-referencing the listing details with publicly available information about government scholarship portals confirmed the target.

Subsequent HUMINT-driven investigation led to the independent discovery and verification of the attack vector, confirming that the breach was genuine and the data authentic.

---

## Breach Impact Analysis

### Scale & Statistics

The breach represents one of the largest government data exposures in India in recent years, with the following key metrics as reported by the threat actor and independently verified:

| Metric | Value |
|--------|-------|
| Total Data Volume | **146 GB** (CSV format) |
| Database Tables | **215 tables** |
| Database Servers Compromised | **3 servers** |
| Unique Phone Numbers | **15,954,000** (de-duplicated) |
| Unique National ID (Aadhaar) Numbers | **18,258,000** (de-duplicated) |
| Unique Email Addresses | **2,820,000** (de-duplicated) |
| Student-Parent Records | **2,652,000** (de-duplicated) |
| Web Account Records | **2,790,000** (de-duplicated) |
| Asking Price | **USD $4,000** |
| Sale Type | Exclusive (single buyer), escrow-protected |

### Database Infrastructure Compromised

The threat actor compromised **three separate database instances**, all hosted as managed PostgreSQL databases on Amazon Web Services (AWS) Relational Database Service (RDS). Our independent verification confirmed the use of AWS RDS infrastructure through examination of exposed configuration artifacts.

The three database instances appear to have served different functional roles within the portal's architecture, including primary application data, secondary/replica data, and administrative/analytical data stores.

### Student Personal Data Exposure

The most extensive data category consists of personal information belonging to scholarship applicants (primarily students). The following fields were confirmed to be present in the compromised dataset:

| Data Field | Category | Sensitivity |
|------------|----------|-------------|
| Student Name (Full) | PII | **HIGH** |
| Father's Name | PII | **HIGH** |
| Mother's Name | PII | **HIGH** |
| Aadhaar Number | National ID | **CRITICAL** |
| Gender | Demographic | MEDIUM |
| Parent Income | Financial | **HIGH** |
| Mobile Phone Number | Contact | **HIGH** |
| Email Address | Contact | **HIGH** |
| Full Residential Address | PII | **HIGH** |
| Educational District | Location | MEDIUM |
| PIN Code | Location | MEDIUM |
| Bank Account Number | Financial | **CRITICAL** |
| Bank Name | Financial | **HIGH** |
| IFSC Code | Financial | **HIGH** |
| School Name | Educational | MEDIUM |
| Institute District Name | Educational | MEDIUM |
| University Name | Educational | LOW |
| Admission Year | Educational | LOW |

### Parent/Guardian Data Exposure

A distinct dataset of 2,652,000 parent/guardian records was also compromised, containing:

- **Father's Name** and **Mother's Name**
- **Parent Mobile Number** — enabling targeted phishing campaigns
- **Family Annual Income** — highly sensitive financial information that can be used for social engineering and targeted fraud

### Web Account & Credential Exposure

Approximately **2,790,000 web account records** were compromised, including:

- **Full Name** (account holder)
- **Email Address**
- **Username**
- **Password Hash** — hashing algorithm and salt strength unknown; if weak hashing was used (e.g., MD5, SHA-1 without salt), mass credential recovery is trivially achievable
- **Mobile Number**

> **CREDENTIAL RISK:** Exposed password hashes, combined with associated email addresses and usernames, create an immediate risk for credential stuffing attacks across other platforms where affected users may have reused their passwords.

### Payment & Financial Data Exposure

The forum listing references **"basic information about payment data"** as an additional category within the compromised dataset. Combined with the student records containing bank account numbers, IFSC codes, and parent income information, this breach exposes a comprehensive financial profile of affected individuals that could facilitate:

- Fraudulent banking transactions using account numbers and IFSC codes
- Identity-based loan fraud using Aadhaar + financial data combinations
- Scholarship fund diversion through administrative account takeover
- Targeted phishing using verified financial institution details

---

## Data Classification & Sensitivity

### PII Categories Exposed

| Category | Records | Classification | Risk Level |
|----------|---------|----------------|------------|
| National ID (Aadhaar) | 18,258,000 | Sensitive Personal Data | **CRITICAL** |
| Phone Numbers | 15,954,000 | Personal Data | **HIGH** |
| Email Addresses | 2,820,000 | Personal Data | **HIGH** |
| Banking Details | Millions (est.) | Sensitive Financial Data | **CRITICAL** |
| Residential Addresses | Millions (est.) | Personal Data | **HIGH** |
| Credential Data (Hashes) | 2,790,000 | Authentication Secrets | **CRITICAL** |
| Family Income Data | 2,652,000 | Sensitive Financial Data | **HIGH** |

### National ID & Identity Documents

The exposure of **18.2 million Aadhaar numbers** represents the most critical aspect of this breach. Under India's Aadhaar Act (2016), Aadhaar numbers are classified as **sensitive personal data**. Unauthorized collection, storage, or disclosure of Aadhaar information is a punishable offense under Section 29 of the Aadhaar Act, carrying penalties of up to three years' imprisonment and a fine of up to INR 10 lakhs (approximately USD $12,000).

When combined with full names, addresses, phone numbers, and banking details, these Aadhaar numbers enable complete identity reconstruction — sufficient for opening fraudulent bank accounts, obtaining SIM cards, or conducting financial transactions in the victim's name.

### Minor/Student Data Implications

> **CHILD DATA EXPOSURE:** As a scholarship portal serving students from school through university level, a significant portion of the affected individuals are likely **minors under the age of 18**. The exposure of minors' personal data, including Aadhaar numbers, addresses, school names, and parent information, carries additional legal implications under India's **Digital Personal Data Protection Act (DPDPA), 2023**, which mandates enhanced protection for children's data and verifiable parental consent.

The compromised data — particularly the combination of student names, school names, addresses, and parent contact information — creates a severe risk profile for minors, including potential for:

- Identity fraud that may go undetected for years until the minor reaches adulthood
- Targeted social engineering using verified school and family information
- Physical safety risks due to exposed residential addresses of minors

### Financial & Banking Data

The combination of bank account numbers, IFSC codes, Aadhaar numbers, and personal details provides a complete financial identity profile. This data enables:

- Direct financial fraud through UPI, NEFT, or RTGS transfers
- Aadhaar-linked bank account exploitation
- KYC fraud using verified identity-financial data pairs
- Government subsidy and DBT (Direct Benefit Transfer) diversion

### Sensitivity Rating

| Metric | Rating |
|--------|--------|
| Overall Sensitivity | **CRITICAL** |
| Data Sensitivity Score | **9.4 / 10** |
| Abuse Potential | **EXTREME** |

The dataset achieves the highest sensitivity rating due to the convergence of: (a) nationally unique identifiers (Aadhaar), (b) financial instrument details, (c) authentication credentials, (d) minor/child data, and (e) the sheer volume of affected individuals.

---

## Vulnerability Assessment (Sanitized)

> **RESPONSIBLE DISCLOSURE NOTICE:** This section provides a high-level description of the vulnerabilities exploited in this breach. Specific technical details including endpoints, file paths, credentials, and step-by-step exploitation methodology have been intentionally omitted to prevent further exploitation. Full technical details are available upon request to authorized parties involved in remediation.

### Nature of Vulnerability

The breach was facilitated by a chain of two distinct security failures:

**Vulnerability 1 — Sensitive Configuration Exposure (CWE-200, CWE-538)**

A backend configuration file containing production environment variables was accessible to unauthorized users through a web-facing path on a related government portal. This file contained plaintext credentials for multiple database services, internal API keys, and infrastructure connection details.

**Vulnerability 2 — Insufficient Access Controls on Cloud Database Services (CWE-284)**

Of the three cloud-hosted database instances referenced in the exposed configuration, two were protected by network-level access restrictions (AWS Security Groups) that limited connectivity to internal/VPC sources only. However, the third database instance had **no such access restrictions configured**, allowing direct connections from any external IP address using the exposed credentials.

### Affected Components

| Component | Issue | Severity |
|-----------|-------|----------|
| Web Application Layer | Sensitive environment configuration accessible via web path | **CRITICAL** |
| Cloud Database Instance #1 | Credentials exposed; access restricted to internal network only | **HIGH** |
| Cloud Database Instance #2 | Credentials exposed; access restricted to internal network only | **HIGH** |
| Cloud Database Instance #3 | Credentials exposed; **no network access restrictions — publicly accessible** | **CRITICAL** |

### Exploitation Complexity

| Factor | Assessment |
|--------|-----------|
| Attack Complexity | **LOW** — No advanced tooling, zero-day exploits, or social engineering required |
| Privileges Required | **NONE** — The exposed configuration was accessible without authentication |
| User Interaction | **NONE** — Fully automated exploitation is possible |
| Skill Level Required | **BASIC** — Fundamental knowledge of web application reconnaissance and database client tools sufficient |

> **EXPLOITATION ASSESSMENT:** The low complexity and zero-prerequisite nature of this attack chain means that any individual with basic technical knowledge who discovers the exposed configuration could replicate the breach. This significantly increases the risk of additional unauthorized access beyond the known threat actor.

### Root Cause Analysis

The root causes of this breach are attributable to multiple failures in security best practices:

1. **Insecure Deployment Practices** — Sensitive configuration files containing production credentials were deployed to web-accessible paths, violating the principle of least exposure. Environment variables and secrets should never be stored in files accessible through web servers.

2. **Inconsistent Network Security Policies** — While two of three database instances had appropriate network-level access restrictions (Security Groups), the third was left with unrestricted public access. This inconsistency suggests a lack of standardized security policy enforcement across infrastructure components.

3. **Plaintext Credential Storage** — Database credentials were stored in plaintext within the configuration file rather than using a secrets management service (e.g., AWS Secrets Manager, HashiCorp Vault).

4. **Absence of Security Auditing** — The misconfiguration appears to have existed for an extended period without detection, indicating a lack of regular security audits, configuration reviews, or automated security scanning.

5. **No Database Access Monitoring** — The exfiltration of 146 GB of data from the unprotected database instance suggests insufficient monitoring of database access patterns, query volumes, and data egress.

### Current Patch Status

> **PARTIALLY REMEDIATED:** As of the date of this report, independent verification indicates that some access controls have been adjusted. However, the foundational issues — particularly the exposure of configuration artifacts on related infrastructure — may not be fully addressed. **Comprehensive remediation should be treated as an emergency priority.**

---

## Intelligence Collection

### Source Methodology

This intelligence was gathered through a combination of:

- **Dark Web Monitoring (DARKINT)** — Routine surveillance of cybercrime forums and marketplaces identified the initial breach listing
- **Human Intelligence (HUMINT)** — Interpersonal intelligence gathering provided additional context about the breach, including the attack methodology, database technology stack, and hosting infrastructure
- **Open Source Intelligence (OSINT)** — Correlation with publicly available information about government portal infrastructure confirmed the target identity
- **Technical Verification** — Independent technical assessment confirmed the existence of the reported vulnerabilities and validated the authenticity of the breach claims

### Dark Web Listing Summary

The breach data was listed on a **prominent English-language cybercrime forum** known for hosting large-scale data breach listings. The forum post included:

- Identification of the target portal and date of breach
- Detailed statistics on data volume and record counts
- Complete list of database field names as proof of access
- Categorization of data into four groups: student data, parent data, web accounts, and payment data
- Sample data excerpts for buyer verification

<figure class="evidence-figure">
<img src="{{ '/assets/images/posts/2026-03-12-scholarship-breach/forum-listing.png' | relative_url }}" alt="Redacted forum listing showing the breach announcement">
<figcaption>Fig 1: Threat actor's forum listing advertising the compromised database. Identifying information, URLs, and contact details have been redacted.</figcaption>
</figure>

<figure class="evidence-figure">
<img src="{{ '/assets/images/posts/2026-03-12-scholarship-breach/sample-data.png' | relative_url }}" alt="Redacted sample data shared by the threat actor">
<figcaption>Fig 2: Sample data posted by the threat actor as proof of access. All personally identifiable information has been obscured.</figcaption>
</figure>

### Sale Conditions

| Parameter | Detail |
|-----------|--------|
| Asking Price | **USD $4,000** |
| Sale Type | Exclusive — "sales in one hands" (single buyer) |
| Escrow | Available ("escrow +++") |
| Contact Method | Encrypted messaging platform (details redacted) |
| Data Format | CSV export from PostgreSQL tables |

The relatively low asking price of $4,000 for a dataset of this magnitude (18M+ national IDs) may indicate urgency to sell, awareness of limited buyer pool for Indian government data, or that the threat actor has already retained a copy for their own use.

### Intelligence Confidence Level

| Assessment | Confidence | Basis |
|------------|-----------|-------|
| Breach is genuine | **CONFIRMED** | Independently verified through technical assessment |
| Data volume claims accurate | **HIGH** | Database schema and sample data consistent with claimed volumes |
| Attack vector as described | **CONFIRMED** | Independently discovered and verified the same vulnerability chain |
| Data has been sold | **UNKNOWN** | No evidence of sale completion; listing may still be active |

---

## Risk Assessment

### Identity Theft & Fraud

**Risk Level: CRITICAL**

With 18.2 million Aadhaar numbers paired with full names, addresses, dates of birth, phone numbers, and banking details, this breach provides all necessary components for comprehensive identity fraud. Threat actors can:

- Open fraudulent bank accounts using Aadhaar eKYC
- Apply for loans and credit facilities under victims' identities
- Register new SIM cards using Aadhaar-based verification
- Divert government benefits (DBT) to fraudulent accounts
- Create synthetic identities combining real and fabricated data elements

### Credential Reuse Attacks

**Risk Level: HIGH**

The 2.79 million compromised web account records — including usernames, email addresses, and password hashes — present an immediate credential stuffing risk. Research consistently shows that 65-80% of users reuse passwords across multiple services. If the password hashing implementation is weak, attackers can recover plaintext passwords and launch automated credential stuffing campaigns against banking portals, email services, social media platforms, and other government services.

### Financial Fraud

**Risk Level: CRITICAL**

The combination of bank account numbers, IFSC codes, Aadhaar numbers, and personal information enables direct financial fraud through multiple vectors. UPI-based fraud is particularly concerning as Aadhaar-linked bank accounts can be targeted for unauthorized transactions. The exposure of family income data further enables social engineering attacks tailored to the victim's economic profile.

### Social Engineering

**Risk Level: HIGH**

The richness of the compromised dataset makes it exceptionally valuable for targeted social engineering campaigns. Attackers can craft highly convincing phishing communications using verified details such as school names, university names, admission years, scholarship application numbers, and family member names. Scholarship-related phishing is particularly effective as victims are conditioned to share personal information in this context.

### Reputational Impact

**Risk Level: HIGH**

This breach represents a significant failure in the state government's responsibility to protect citizen data entrusted to it through a mandatory digital governance platform. The reputational impact extends to:

- Public trust in digital government services and e-Governance initiatives
- Confidence in the state's cloud infrastructure security practices
- India's broader Digital India program credibility
- Potential diplomatic implications if the data is sold to foreign intelligence services

### Overall Risk Rating

| Risk Factor | Rating | Score (1-10) |
|-------------|--------|-------------|
| Data Sensitivity | **CRITICAL** | 9.5 |
| Affected Population Size | **CRITICAL** | 9.0 |
| Exploitation Ease | **CRITICAL** | 9.5 |
| Financial Impact Potential | **CRITICAL** | 9.0 |
| Minor/Child Data Involved | **CRITICAL** | 9.5 |
| Remediation Status | **HIGH** | 8.0 |
| **COMPOSITE RISK RATING** | **CRITICAL** | **9.1 / 10** |

---

## Recommendations

### Immediate Containment (0-72 Hours)

The following actions should be treated as emergency measures:

1. **Rotate All Credentials** — Immediately rotate all database passwords, API keys, and service account credentials that were present in the exposed configuration. This includes all three database instances, regardless of their current network access status.

2. **Restrict Database Network Access** — Enforce network-level access restrictions (AWS Security Groups) on all database instances to allow connections only from authorized application servers within the VPC. No database instance should accept connections from public IP addresses.

3. **Remove Exposed Configuration** — Identify and remove all instances of sensitive configuration files accessible through web-facing paths across all related portals and subdomains.

4. **Enable Database Audit Logging** — Immediately enable comprehensive audit logging on all database instances to detect any ongoing unauthorized access.

5. **Force Password Reset** — Force a password reset for all 2.79 million web accounts whose credentials were compromised.

### Infrastructure Hardening (1-4 Weeks)

1. **Implement Secrets Management** — Migrate all credentials and sensitive configuration to a dedicated secrets management service (e.g., AWS Secrets Manager, AWS Parameter Store with encryption). Eliminate all plaintext credential storage in configuration files.

2. **Deploy Web Application Firewall (WAF)** — Implement a WAF to prevent directory traversal, path enumeration, and unauthorized access to backend resources.

3. **Network Segmentation** — Implement strict network segmentation between web-facing application servers and backend database infrastructure. Database servers should reside in private subnets with no direct internet exposure.

4. **Automated Security Scanning** — Deploy automated vulnerability scanning and configuration auditing tools to continuously monitor for security misconfigurations across all cloud infrastructure.

5. **Implement Database Activity Monitoring** — Deploy real-time database activity monitoring to detect anomalous query patterns, bulk data exports, and unauthorized access attempts.

6. **Encrypt Data at Rest** — Enable encryption at rest for all database instances using AWS KMS-managed keys.

### Affected Individual Notification (1-2 Weeks)

Under India's Digital Personal Data Protection Act (DPDPA), 2023, and general data protection principles, the data fiduciary (state government) has an obligation to notify affected individuals of the breach. Recommended actions:

- Issue a public advisory through the portal and state government channels
- Send individual notifications via SMS to the 15.9 million compromised phone numbers
- Provide guidance on password changes, credit monitoring, and Aadhaar biometric locking via the UIDAI portal
- Establish a dedicated helpline for breach-related inquiries
- Advise all affected users to enable Aadhaar biometric lock through mAadhaar app or UIDAI website

### Regulatory Reporting

- **CERT-In** — Report the incident to the Indian Computer Emergency Response Team as mandated under the IT Act, 2000 and CERT-In Directions (April 2022), which require breach reporting within 6 hours of becoming aware
- **UIDAI** — Notify the Unique Identification Authority of India regarding the Aadhaar data exposure
- **Data Protection Board** — When fully operational under DPDPA 2023, notify the Data Protection Board of India
- **State Cyber Crime Cell** — File a formal complaint for investigation and potential prosecution under IT Act Sections 43, 66, and 72A

### Long-Term Security Posture (1-6 Months)

1. **Security Audit Program** — Establish quarterly third-party security assessments of all government portal infrastructure, including penetration testing and configuration reviews

2. **DevSecOps Integration** — Integrate automated security testing into the software development and deployment lifecycle to catch misconfigurations before they reach production

3. **Zero-Trust Architecture** — Adopt zero-trust principles for all government cloud infrastructure, requiring identity verification and least-privilege access for every connection

4. **Incident Response Plan** — Develop and regularly test a comprehensive incident response plan specifically for data breach scenarios

5. **Employee Security Training** — Implement mandatory security awareness training for all personnel involved in portal development, deployment, and maintenance

6. **Dark Web Monitoring** — Establish continuous dark web monitoring through specialized threat intelligence services to detect any future listings or data distribution related to this breach

---

## Appendix

### Appendix A — Vulnerability Verification Evidence

<figure class="evidence-figure">
<img src="{{ '/assets/images/posts/2026-03-12-scholarship-breach/exposed-config.png' | relative_url }}" alt="Sanitized configuration artifact showing database connection details">
<figcaption>Fig 3: Configuration artifact discovered during independent verification, showing multiple cloud database connection configurations. All credentials, hostnames, and identifying details have been redacted. Note the presence of three distinct database connection blocks pointing to cloud-hosted RDS instances.</figcaption>
</figure>

### Appendix B — Exposed Data Field Inventory

| Category | Fields |
|----------|--------|
| Student Personal Data | student_name, father_name, mother_name, aadhaar, gender, parent_income, mobile_phone, email, full_address, name_of_the_educational_district, pin_code, account_no, bank_name, ifsc_code, school_name, institute_district_name, university_name, institute_name, admission_year, and more |
| Parent/Guardian Data | FatherName, MotherName, ParentMobileNo, FamilyAnnualIncome |
| Web Account Data | name, email, username, password_hash, mobile |
| Payment Data | Details not fully enumerated in listing; references to "basic information about payment data" |

### Appendix C — Risk Scoring Methodology

| Score Range | Rating | Definition |
|-------------|--------|-----------|
| 9.0 - 10.0 | **CRITICAL** | Imminent, widespread harm; immediate action required |
| 7.0 - 8.9 | **HIGH** | Significant harm likely; urgent remediation needed |
| 4.0 - 6.9 | **MEDIUM** | Moderate harm possible; remediation recommended |
| 1.0 - 3.9 | **LOW** | Limited harm; address in normal operations |

### Appendix D — References

1. CERT-In Directions (2022). "Directions relating to information security practices, procedure, prevention, response and reporting of cyber incidents." Ministry of Electronics & IT, Government of India.
2. Digital Personal Data Protection Act (2023). Government of India.
3. Aadhaar (Targeted Delivery of Financial and Other Subsidies, Benefits and Services) Act, 2016. Government of India.
4. MITRE CWE-200: Exposure of Sensitive Information to an Unauthorized Actor.
5. MITRE CWE-284: Improper Access Control.
6. MITRE CWE-538: Insertion of Sensitive Information into Externally-Accessible File or Directory.
7. AWS Security Best Practices — Amazon RDS Security Group Configuration Guidelines.
8. OWASP Top 10 (2021) — A05:2021 Security Misconfiguration.

### Appendix E — Glossary

| Term | Definition |
|------|-----------|
| Aadhaar | India's 12-digit unique identity number issued by UIDAI to residents |
| AWS RDS | Amazon Relational Database Service — managed cloud database hosting |
| CERT-In | Indian Computer Emergency Response Team |
| CWE | Common Weakness Enumeration — standardized vulnerability classification |
| DARKINT | Dark web intelligence — intelligence gathered from dark web sources |
| DBT | Direct Benefit Transfer — Indian government subsidy disbursement system |
| DPDPA | Digital Personal Data Protection Act, 2023 (India) |
| HUMINT | Human Intelligence — intelligence gathered through interpersonal sources |
| IFSC | Indian Financial System Code — bank branch identifier |
| OSINT | Open Source Intelligence — intelligence from publicly available sources |
| PII | Personally Identifiable Information |
| POCSO | Protection of Children from Sexual Offences Act, 2012 |
| PostgreSQL | Open-source relational database management system |
| TLP | Traffic Light Protocol — information sharing classification standard |
| UIDAI | Unique Identification Authority of India |
| UPI | Unified Payments Interface — Indian real-time payment system |
| VPC | Virtual Private Cloud — isolated cloud network environment |
| WAF | Web Application Firewall |

---

*Report ID: CTI-2026-0215-SSP | Version: 1.0 | Classification: TLP:CLEAR (Public Version)*

*This is the public version of the original TLP:AMBER report. All identifying information including portal URLs, database hostnames, credentials, and specific state identification have been redacted. The original classified report is available to authorized parties upon request.*

*All findings are based on open-source intelligence, human intelligence, and independent technical verification. No systems were compromised during this research — the researcher identified and verified the existence of vulnerabilities through observation of publicly accessible artifacts only.*
