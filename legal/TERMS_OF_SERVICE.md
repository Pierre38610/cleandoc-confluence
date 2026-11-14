# Terms of Service (EULA) — CleanDoc (Stale-Page & Offboarding Cleaner for Confluence)

**Effective Date:** November 2026  
**Publisher:** Pierre Cassagnettes — CleanDoc (Independent Software Vendor, France)  
**Support & Legal Contact:** `pierrecassagnettes+cleandoc@gmail.com`

---

## 1. Acceptance of Terms

By installing or using **CleanDoc — Stale-Page & Offboarding Cleaner for Confluence** ("the App") from the Atlassian Marketplace, you ("Customer") agree to these Terms of Service ("Terms") in addition to the **Atlassian Marketplace Terms of Use** and **Atlassian Cloud Terms of Service**.

If you are installing the App on behalf of an organization, you represent that you have authority to bind that organization.

---

## 2. License Grant & Pricing Tiers

Subject to compliance with these Terms and active Marketplace licensing:
- **Free Tier (`1–10` Confluence users):** CleanDoc is provided free of charge for Confluence Cloud instances with up to 10 active users.
- **Trial & Paid Subscription (`11+` Confluence users):** Instances with more than 10 users receive a 30-day free Marketplace evaluation, after which an active paid Atlassian Marketplace subscription is required to execute bulk write actions (bulk archive, bulk owner reassignment, whitelisting).
- Billing, invoicing, renewals, refunds, and applicable taxes/VAT are processed exclusively by **Atlassian** as Merchant of Record.

---

## 3. Customer Responsibilities & Safe Operation

CleanDoc provides administrative tools to scan Confluence pages, identify stale or orphaned pages, detect deactivated owners, and perform **bulk archiving** and **bulk ownership reassignment**:
1. **Review Before Bulk Actions:** Archiving pages moves them to Confluence's Space Archive (recoverable by Space Admins); updating page ownership creates a new page version in Confluence. Customers are responsible for reviewing flagged pages and configuring `excludeLabels` (e.g., `evergreen`, `compliance-locked`, `legal-archive`) before executing bulk actions.
2. **Permissions:** Bulk actions execute with Confluence REST API permissions granted during installation and require appropriate space/archive permissions.
3. **No Legal/Compliance Guarantee:** While CleanDoc provides CSV audit log exports to assist with internal governance and ISO 27001 / SOC 2 reviews, the App is a productivity and lifecycle management tool and does not constitute legal or regulatory compliance certification.

---

## 4. Intellectual Property

All source code, UI designs, scoring algorithms (Rovo Pollution Score), and documentation associated with CleanDoc remain the exclusive intellectual property of the Publisher. The Customer retains 100% ownership and control of all Confluence content and metadata in their Atlassian tenant.

---

## 5. Support & Availability

- Support is provided via email (`pierrecassagnettes+cleandoc@gmail.com`) and the support portal listed on the Atlassian Marketplace listing.
- Target initial response time: within **2 business days** (Monday–Friday, CET/CEST).
- Because CleanDoc runs 100% on Atlassian Forge serverless infrastructure, runtime availability depends on Atlassian Cloud & Forge platform SLAs.

---

## 6. Limitation of Liability & Disclaimer

TO THE MAXIMUM EXTENT PERMITTED BY APPLICABLE LAW:
- THE APP IS PROVIDED "AS IS" AND "AS AVAILABLE" WITHOUT WARRANTIES OF ANY KIND, EXPRESS OR IMPLIED.
- IN NO EVENT SHALL THE PUBLISHER BE LIABLE FOR ANY INDIRECT, INCIDENTAL, SPECIAL, CONSEQUENTIAL, OR PUNITIVE DAMAGES, OR ANY LOSS OF DATA, PROFITS, OR REVENUE.
- THE PUBLISHER'S TOTAL AGGREGATE LIABILITY UNDER THESE TERMS SHALL NOT EXCEED THE TOTAL SUBSCRIPTION FEES RECEIVED BY THE PUBLISHER FROM CUSTOMER VIA ATLASSIAN MARKETPLACE DURING THE TWELVE (12) MONTHS PRECEDING THE CLAIM.

---

## 7. Governing Law

These Terms are governed by the laws of **France** (without prejudice to mandatory consumer/data protection laws where applicable), and disputes not resolved amicably shall be submitted to the competent courts of France.
