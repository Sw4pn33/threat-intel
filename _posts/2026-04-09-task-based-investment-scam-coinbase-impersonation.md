---
layout: post
title: "Task-Based Investment Scam Impersonating Coinbase India: UPI Trail Reveals Maharashtra-Based Fraud Network"
subtitle: "Investigation into a pig butchering operation using a legitimate Indian company registration number, Malaysian domain infrastructure, and organised money mule networks to defraud victims through a fake task-based earning platform."
date: 2026-04-09
category: "Financial Fraud Investigation"
author: "Sw4pn33"
author_role: "Threat Intelligence Researcher"
readtime: "15"
tags: [pig-butchering, task-scam, UPI-fraud, OSINT, India, money-mule, Coinbase-impersonation]
---

## Executive Summary

This report documents a task-based investment fraud operation — a variant of the "pig butchering" scam model — that has defrauded at least two identified victims of a combined **INR 16,92,560** (approximately USD 20,000). The operation uses the real Corporate Identity Number (CIN) of **Coinbase India Private Limited** to impersonate the company and build credibility with targets.

The scam infrastructure uses Malaysian-registered `.my` domains to complicate Indian legal jurisdiction, recruits victims through WhatsApp, migrates them to Telegram for ongoing control, and routes deposits through a mule bank account.

Through UPI (Unified Payments Interface) validation and open-source intelligence, this investigation has identified **15 real individuals** connected to the scam's Telegram infrastructure. All 15 are based in **Maharashtra, India**, with banking concentrated in the Aurangabad-Nanded-Marathwada region.

This report presents only verified technical evidence, financial indicators, and actionable intelligence for law enforcement agencies.

---

## Identified Victims

### Victim 1: Shiva Prasad Kar

The primary victim, **Shiva Prasad Kar** (platform username: `Gunusiva123`), has a trapped balance of **INR 12,59,827.8** on the scam platform. Evidence screenshots provided by the victim show the platform interface, the locked withdrawal, and the artificial credit score barrier.

<figure class="evidence-figure">
<img src="{{ '/assets/images/posts/2026-04-09-task-scam/12-platform-profile-page.jpeg' | relative_url }}" alt="Scam platform profile showing victim's account details">
<figcaption>Fig 1: Victim's account on the scam platform (metabaseonehome.my) showing username Gunusiva123, real balance of INR 12,59,827.8, and a credit score of 88 — which the platform claims must be 90 to enable withdrawals.</figcaption>
</figure>

### Victim 2: Vivek Kumar Jain

A second victim, **Vivek Kumar Jain** from Shivpuri, Madhya Pradesh, was identified through a Dainik Bhaskar news report. Jain reported a loss of **INR 4,32,733** and filed an FIR at Physical Thana, Shivpuri. He was recruited into a WhatsApp group named **"Suntec Pvt Ltd - Simple Tasks Income"**.

**Combined confirmed loss: INR 16,92,560.** Given the 170+ phone numbers found in the scam's Telegram contacts, the actual victim count is likely higher.

---

## Modus Operandi

### Phase 1: WhatsApp Recruitment

The victim receives an unsolicited WhatsApp message from **"Ananya Sharma"** — a fabricated identity using what appears to be an Amazon employee profile picture. The message offers part-time income through simple online tasks (product ratings, reviews) at INR 150-500 per task.

The scammer operates from the phone number **+91 7057684173** (Maharashtra area code). Initial small payouts of INR 500-2000 are made to build trust.

<figure class="evidence-figure">
<img src="{{ '/assets/images/posts/2026-04-09-task-scam/06-ananya-whatsapp-profile.jpeg' | relative_url }}" alt="WhatsApp chat with Ananya Sharma showing platform withdrawal issue being shared">
<figcaption>Fig 2: WhatsApp conversation between victim Shiva Prasad Kar and the scammer "Ananya Sharma" (Amazon DP). The victim is sharing a screenshot of the withdrawal problem from the scam platform.</figcaption>
</figure>

### Phase 2: Migration to Telegram and the Fake Trading Platform

Once trust is established, the victim is directed to a Telegram account for "customer support." The scammer shares a direct link to `@Customercare00120` on Telegram, branded as **"Customer Support 015"** with a Coinbase logo as the profile picture.

<figure class="evidence-figure">
<img src="{{ '/assets/images/posts/2026-04-09-task-scam/09-telegram-customercare-link.jpeg' | relative_url }}" alt="Scammer sharing Telegram customer support link">
<figcaption>Fig 3: "Ananya Sharma" sharing the Telegram link to @Customercare00120 ("Customer Support 015") which uses a Coinbase-branded profile picture. This is the primary scam handler account on Telegram.</figcaption>
</figure>

The victim is then onboarded onto the platform at `metabaseonehome.my`, which is configured as a Progressive Web App (PWA) mimicking a mobile trading application.

<figure class="evidence-figure">
<img src="{{ '/assets/images/posts/2026-04-09-task-scam/10-whatsapp-customer-support-coinbase.jpeg' | relative_url }}" alt="WhatsApp Customer Support with Coinbase branding">
<figcaption>Fig 4: The scam's WhatsApp "Customer Support" account using a Coinbase-branded profile picture and showing as "online." The first message was sent on March 19, confirming the operation was active in March 2026.</figcaption>
</figure>

### Phase 3: Deposit Collection and Credit Score Trap

Victim deposits are directed to a specific bank account. Once significant amounts are deposited, the platform blocks withdrawals using an artificial "credit score" system — the score is manipulated below the required threshold (90), and the victim is told they must deposit more to "recover" their credit score.

<figure class="evidence-figure">
<img src="{{ '/assets/images/posts/2026-04-09-task-scam/02-withdrawal-blocked-credit-score.jpeg' | relative_url }}" alt="Platform withdrawal page showing blocked withdrawal">
<figcaption>Fig 5: The scam platform's withdrawal interface. Shows current balance of INR 12,59,827.8, the linked Axis Bank account (910010029465849), and the red warning: "Your credit score is less than 90.0, you cannot apply for withdrawal." This is the core extraction mechanism.</figcaption>
</figure>

The platform also sends automated system messages demanding "replenishment orders" — essentially demanding additional deposits under threat of further credit score reduction:

<figure class="evidence-figure">
<img src="{{ '/assets/images/posts/2026-04-09-task-scam/03-system-replenishment-message.jpeg' | relative_url }}" alt="System message about replenishment orders">
<figcaption>Fig 6: A system message from the scam platform stating: "There are multiple replenishment orders in the account... 12 points will be deducted... The amount is 300,000 rupees (1 point 150,000 rupees). Credit score as a warning." This automated pressure drives victims to deposit more money.</figcaption>
</figure>

### Phase 4: Social Engineering Escalation

When the victim questions the withdrawal block, "Ananya Sharma" reinforces the credit score narrative through WhatsApp, claiming the victim's own "mistakes" caused the deduction:

<figure class="evidence-figure">
<img src="{{ '/assets/images/posts/2026-04-09-task-scam/04-ananya-credit-score-deduction.jpeg' | relative_url }}" alt="Scammer blaming victim for credit score deduction">
<figcaption>Fig 7: "Ananya Sharma" telling the victim: "Your credit score is deducted because of your own mistakes... you need 90 credit score purchasing credit score is compulsory to withdraw your all funds at once." This is a classic pressure tactic to extract more money.</figcaption>
</figure>

The scammer then escalates with threats of account freezing, using the term **"wind control"** — a direct translation from the Chinese term 风控 (fēng kòng, meaning risk control), which is a known indicator of Chinese-origin scam scripts adapted for the Indian market:

<figure class="evidence-figure">
<img src="{{ '/assets/images/posts/2026-04-09-task-scam/05-ananya-wind-control-frozen.jpeg' | relative_url }}" alt="Scammer using wind control terminology">
<figcaption>Fig 8: "Ananya Sharma" threatening: "the account will be frozen wind control and your credit score will be deducted for this account... kindly follow the pattern to withdraw all funds safely." The term "wind control" is a direct translation from Chinese fraud scripts (风控).</figcaption>
</figure>

The Telegram "Customer Support" account also confirms the credit score requirement, displaying the platform's popup warning:

<figure class="evidence-figure">
<img src="{{ '/assets/images/posts/2026-04-09-task-scam/11-telegram-credit-score-confirmation.jpeg' | relative_url }}" alt="Telegram support confirming credit score requirement">
<figcaption>Fig 9: The Telegram "Customer Support" account (using Coinbase branding) confirming: "Your account is normal and your funds are ready to withdraw you just need to increase the credit score to 90." The popup shows the account username Gunusiva123 with the same credit score warning.</figcaption>
</figure>

---

## Company Impersonation: Coinbase India CIN

A critical element of this scam is the use of a real, verifiable Corporate Identity Number to create legitimacy. The platform displays CIN **U72200DL2022FTC401873**, which belongs to an actually registered Indian company.

<figure class="evidence-figure">
<img src="{{ '/assets/images/posts/2026-04-09-task-scam/01-mca-company-info.jpeg' | relative_url }}" alt="MCA Company Information showing CIN details">
<figcaption>Fig 10: Company information from MCA records showing CIN U72200DL2022FTC401873. The registration details are real — but the address displayed on the scam platform ("2nd Floor, B-5, Netaji Subash Place, Wazirpur, New Delhi 110034") does NOT match the actual registered office address on MCA records.</figcaption>
</figure>

**Verified facts from the MCA portal:**

| Attribute | MCA Record |
|---|---|
| **CIN** | U72200DL2022FTC401873 |
| **Company Status** | Active |
| **Registration Number** | 401873 |
| **Date of Incorporation** | 18 July 2022 |
| **RoC** | RoC-Delhi |
| **Authorised Capital** | INR 2,51,00,000 |
| **Company Category** | Company limited by Shares |
| **Sub-Category** | Subsidiary of company incorporated outside India |
| **Activity** | Software publishing, consultancy and supply |
| **Listing Status** | Unlisted |
| **Date of Last Balance Sheet** | 31 March 2024 |

**What this tells us:** The CIN is real and belongs to a legitimate registered entity. The company's stated activity is software — there is nothing about trading or financial services in its registration. The victim himself noticed this discrepancy and confronted the scammer:

<figure class="evidence-figure">
<img src="{{ '/assets/images/posts/2026-04-09-task-scam/07-victim-questioning-registration.jpeg' | relative_url }}" alt="Victim questioning the company registration">
<figcaption>Fig 11: Victim Shiva Prasad Kar questioning "Ananya Sharma": "As per your registration your company is a software developer company and there nothing about trading in your registration. Then how you deal with trading activity by in this company name..." — a direct challenge to the scam's legitimacy.</figcaption>
</figure>

The scammer's response was a fabricated explanation about "B2B cooperation with Coinbase and Amazon":

<figure class="evidence-figure">
<img src="{{ '/assets/images/posts/2026-04-09-task-scam/08-ananya-b2b-cooperation-claim.jpeg' | relative_url }}" alt="Scammer claiming B2B cooperation">
<figcaption>Fig 12: "Ananya Sharma" claiming: "So basically our company cooperates with coinbase and amazon B2B. We boost the client's product on Amazon... Merchants pay us commissions for this, and in return, we share the profit with you." This is a fabricated explanation that does not correspond to any real business activity.</figcaption>
</figure>

<div class="callout callout-red">
<strong>Important clarification:</strong> The CIN U72200DL2022FTC401873 belongs to a real, registered Indian entity. This investigation does NOT accuse the registered company or its directors of involvement in this scam. The scammers are impersonating/misusing this company's registration details without authorisation. The registered company's actual office address differs from the address displayed on the scam platform.
</div>

---

## Domain Infrastructure

### Primary Domain: metabaseonehome.my

| Attribute | Value |
|---|---|
| **Domain** | metabaseonehome.my |
| **Registry Domain ID** | DO_40a723e95a4f4c9cc7b8e2770deab089-MYNIC |
| **TLD** | .my (Malaysia) |
| **Registrar** | Dynadot LLC (San Mateo, California, USA) |
| **Registrar IANA ID** | 472 |
| **Created** | 30 January 2026 |
| **Last Updated** | 30 March 2026 |
| **Expires** | 30 January 2027 |
| **Domain Status** | clientTransferProhibited (transfer-locked by registrant) |
| **Nameservers** | ns1.dyna-ns.net, ns2.dyna-ns.net |
| **WHOIS Privacy** | Super Privacy Service LTD c/o Dynadot |
| **Registrant Contact** | Redacted — proxy address at PO Box 701, San Mateo, CA 94401 |
| **Registrant Phone** | +1.6505854708 (Dynadot privacy proxy — not the actual registrant) |
| **Current IP** | 185.53.179.128 (Team Internet AG parking IP) |
| **Status** | Parked / Offline (HTTP returns 403, HTTPS times out) |
| **Security Vendors** | 11 of 29 vendors flag as phishing |
| **Trust Score** | 1/100 (Gridinsoft) |
| **Wayback Machine** | No archived snapshots |
| **DNSSEC** | Unsigned |

The IP `185.53.179.128` is Dynadot's default parking address hosting approximately 496,605 domains. This is **not** the scammer's operational server — it indicates the platform's hosting has been decommissioned and the domain now points to the registrar's default parking page.

#### WHOIS Timeline Analysis

The WHOIS record reveals an important operational timeline:

- **30 January 2026** — Domain registered. This aligns with the scam becoming active in early 2026.
- **30 March 2026** — Domain record last updated. This is significant: the scam platform was already offline/parked by this date, yet someone actively modified the domain configuration just 10 days before this report. This could indicate the operator was attempting to migrate infrastructure, redirect the domain to a new server, or simply managing the domain before abandoning it.
- **30 January 2027** — Expiration date. The domain was paid for a full year, indicating planned long-term operation — not a quick throwaway domain.

The `clientTransferProhibited` status means the registrant actively locked the domain against transfers, suggesting they intend to retain control of it.

#### Investigative Leads for Law Enforcement

The WHOIS privacy shield hides the actual registrant behind Dynadot's "Super Privacy Service LTD" proxy. All contact details (name, phone, email, address) in the WHOIS record belong to Dynadot's proxy service — **not** the scammer. However, Dynadot retains the real registrant's identity and payment details behind this shield.

**Actionable paths to unmask the registrant:**

1. **Dynadot Abuse Report** — File an abuse complaint at `abuse@dynadot.com` (phone: +1.6502620100) citing phishing classification by 11 security vendors. Dynadot is obligated under ICANN policy to investigate.
2. **Dynadot Contact Request** — Dynadot provides a registrant contact form that forwards messages to the actual domain owner without revealing their identity. This can be used to confirm the domain is still actively managed.
3. **Legal Subpoena to Dynadot LLC** — A court order or MLAT request served to Dynadot LLC (San Mateo, California) would compel disclosure of the actual registrant's name, email, payment method (credit card or cryptocurrency), IP address used during registration, and all login IP history. The **Registry Domain ID** (`DO_40a723e95a4f4c9cc7b8e2770deab089-MYNIC`) is the unique identifier Dynadot can use to pull the complete registrant record.
4. **MYNIC (Malaysian Registry)** — Since `.my` domains are administered by MYNIC Berhad (Malaysia), a parallel request to MYNIC can provide additional registration data that may not be covered by Dynadot's privacy proxy. MYNIC maintains its own registrant records as the registry operator.

<div class="callout callout-blue">
<strong>Key lead:</strong> The March 30 WHOIS update proves someone was still actively managing this domain just 10 days ago. If law enforcement acts quickly, Dynadot's logs will contain the IP address used for that most recent login — which could directly identify the operator or their VPN/proxy infrastructure.
</div>

### Secondary Domain: rnmuoqmxbi.my

A second domain found in the evidence. DNS resolution fails entirely — it has either expired or been taken down.

The `.my` (Malaysian) TLD was likely chosen because Indian law enforcement faces jurisdictional challenges with Malaysian domain registries, and the registrar (Dynadot) being US-based adds another legal layer. However, both Dynadot (US) and MYNIC (Malaysia) are reachable through standard international legal cooperation channels — MLAT for Dynadot, and direct request to MYNIC under Malaysian law.

---

## Financial Infrastructure

Deposits were directed to:

| Attribute | Value |
|---|---|
| **Bank** | Axis Bank |
| **Account Number** | 910010029465849 |
| **Visible in** | Platform withdrawal page (Fig 5) |

This account number is directly visible in the screenshot of the scam platform's withdrawal interface. No public fraud reports were found for this specific account at the time of investigation.

---

## UPI-Based Identity Resolution

The most significant findings came from validating phone numbers extracted from the scam's Telegram infrastructure against India's UPI payment system. When a phone number has a registered UPI address, validation returns the **account holder's name** and **bank IFSC code**.

### Primary Handler: "Changdev"

The phone number **+91 7057684173** — linked to Telegram account `@Customercare00120` and WhatsApp identity "Ananya Sharma" — was validated against multiple UPI handles:

| UPI Address | Registered Name | IFSC | Bank |
|---|---|---|---|
| 7057684173@ybl | **Changdev** | MAHG0000001 | Maharashtra Gramin Bank |
| 7057684173@paytm | **Changdev** | MAHG0000001 | Maharashtra Gramin Bank |
| 7057684173@axl | **Changdev** | MAHG0000001 | Maharashtra Gramin Bank |
| 7057684173@ibl | **Changdev** | MAHG0000001 | Maharashtra Gramin Bank |

All four UPI handles consistently return **"Changdev"** with IFSC **MAHG0000001** — the Maharashtra Gramin Bank RTGS Head Office at CIDCO, Aurangabad, Maharashtra.

This individual operated under the fabricated identity "Ananya Sharma" on WhatsApp and "Customer Support 015" on Telegram.

### Customer Support Number: +91 9485770643

This number (Tamil Nadu area code) returned **no registered UPI IDs** across 26 tested handles. This suggests it may be a prepaid or VoIP number used only for receiving calls.

### Connected Persons from Telegram Group

85 of the 170+ phone numbers from the scam's Telegram contacts were scanned via UPI validation. **14 additional individuals** were identified:

| # | Phone | Name | Bank | IFSC |
|---|---|---|---|---|
| 1 | 7038279697 | Anand Dattarao Jagdale | SBI | SBIN0004877 |
| 2 | 9422359693 | Anushka Ashutosh Salunkhe | Bank of India | BKID0001215 |
| 3 | 7057149397 | Ashwini Amol Gangurde | UCO Bank | UCBA0001311 |
| 4 | 9604927771 | Prasad Vijaykumar Shelke | ICICI Bank | ICIC0003246 |
| 5 | 7276466067 | Sayali Sandip Londhe | Maharashtra Bank | MAHB0000623 |
| 6 | 8999399660 | Smita Manish Bhaganagare | SBI | SBIN0004762 |
| 7 | 7020825437 | Sagar Mahadev Chaugule | Maharashtra Bank | MAHB0000998 |
| 8 | 7066662221 | Pratiksha Purushottam Andurkar | SBI | SBIN0021843 |
| 9 | 7620429445 | Navin Bhikhu Gahala | SBI | SBIN0000354 |
| 10 | 9890254133 | Mathew John Almeida | Bassein Catholic Bank | BACB0000003 |
| 11 | 9373289893 | Ashvini Sharad Andhale | Union Bank | UBIN0547875 |
| 12 | 7028055660 | Pankaj Kanwal | HDFC Bank | HDFC0000088 |
| 13 | 7972965779 | Jugdar Priti Kanifnath | HDFC Bank | HDFC0000621 |
| 14 | 8999511160 | Nagma Kausar Mohammadyounus | SBI | SBIN0000433 |

<div class="callout callout-yellow">
<strong>Note on these individuals:</strong> These 14 persons were identified solely because their phone numbers appeared in the scam's Telegram group contacts and their UPI addresses returned registered names. Their exact role — whether they are victims, unknowing mule account holders, or active participants — cannot be determined from UPI data alone. Further investigation (bank statements, CDR analysis) is needed to establish individual roles. This report does not accuse any of these individuals of criminal activity.
</div>

### Geographic Pattern

All 15 identified individuals (including the primary handler) bank in **Maharashtra**. The names — Jagdale, Salunkhe, Gangurde, Shelke, Londhe, Bhaganagare, Chaugule, Andurkar — are distinctly Marathi. The banking IFSC codes point to branches across Aurangabad, Nanded, Mahad, and other Maharashtra locations.

---

## Assessment

Based on the collected evidence:

- **At least two victims** have been identified with combined losses of INR 16,92,560
- **The platform** used a real CIN (U72200DL2022FTC401873) that belongs to a registered Indian company to create false legitimacy
- **The address** displayed on the scam platform does not match the company's actual MCA-registered address
- **The primary handler** ("Changdev", Maharashtra Gramin Bank, Aurangabad) operated under the fake identity "Ananya Sharma"
- **The scam scripts** contain Chinese-origin terminology ("wind control" from 风控) adapted for the Indian market
- **The domain** metabaseonehome.my is now parked/offline but was flagged by 11 security vendors as phishing
- **All 15 UPI-identified persons** are Maharashtra-based, suggesting a domestically operated fraud ring

### What This Report Cannot Confirm

- The total number of victims (likely higher than two)
- Whether the 14 connected persons are victims, mules, or associates
- The identity behind the Axis Bank mule account (requires bank KYC disclosure)
- Who registered the domain metabaseonehome.my (WHOIS is privacy-shielded)
- Whether the operation has connections to larger organised crime networks

---

## Indicators of Compromise

### Domains

```
metabaseonehome.my    (primary — parked/offline, WHOIS updated 30 March 2026)
                      Registry ID: DO_40a723e95a4f4c9cc7b8e2770deab089-MYNIC
                      Registrar: Dynadot LLC (IANA ID 472)
                      Abuse: abuse@dynadot.com / +1.6502620100

rnmuoqmxbi.my         (secondary — DNS resolution fails)
```

### Phone Numbers

```
+91 7057684173    (Primary handler — UPI name: "Changdev")
+91 9485770643    (Customer support — no UPI registered)
```

### Financial

```
Axis Bank Account: 910010029465849
UPI: 7057684173@ybl, @paytm, @axl, @ibl (all resolve to "Changdev", MAHG0000001)
```

### Telegram

```
Username: @Customercare00120
User ID: 5703776448
Display Name: "Customer Support 015"
```

### Brand Abuse

```
CIN Used: U72200DL2022FTC401873
Fake Address: 2nd Floor, B-5, Netaji Subash Place, Wazirpur, New Delhi 110034
```

---

## Recommended Actions for Law Enforcement

**Immediate:**
- Section 91 CrPC notice to Axis Bank for KYC of account 910010029465849
- Section 91 CrPC notice to Maharashtra Gramin Bank (MAHG0000001) for full KYC linked to phone 7057684173
- CDR (Call Detail Records) request for +91 7057684173

**Short-term:**
- Telegram Law Enforcement request for IP logs of User ID 5703776448
- Transaction history for Axis Bank account 910010029465849
- Cross-reference with FIR filed at Physical Thana, Shivpuri (Victim 2)

**Medium-term:**
- MLAT request to Dynadot LLC for metabaseonehome.my registrant details
- MYNIC abuse report for both .my domains
- Notification to the registered company about CIN misuse

---

## Methodology

All findings are derived from open-source intelligence and publicly available data:

1. **UPI validation** — Phone numbers validated against India's UPI infrastructure to identify registered names and bank IFSC codes
2. **DNS analysis** — Standard DNS resolution and reverse IP lookups
3. **WHOIS records** — Public domain registration data
4. **MCA portal** — Company registration verification through the Ministry of Corporate Affairs
5. **Security vendor databases** — Domain reputation checked across threat intelligence feeds
6. **Published news reports** — Victim identification through media articles
7. **Evidence screenshots** — Provided by the investigating officer, showing the scam platform interface, WhatsApp conversations, and Telegram interactions

No systems were accessed without authorisation during this investigation. No exploitation was attempted.

<div class="post-tags">
<span>financial-fraud</span>
<span>pig-butchering</span>
<span>task-scam</span>
<span>UPI-fraud</span>
<span>OSINT</span>
<span>India</span>
<span>money-mule</span>
<span>brand-impersonation</span>
<span>Maharashtra</span>
</div>
