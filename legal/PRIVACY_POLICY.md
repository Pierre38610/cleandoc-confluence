# Privacy Policy — CleanDoc (Stale-Page & Offboarding Cleaner for Confluence)

**Effective Date:** November 2026  
**Publisher / Data Processor:** Pierre Cassagnettes — CleanDoc (Independent Software Vendor, France / European Union)  
**Contact Email:** `pierrecassagnettes+cleandoc@gmail.com`  

---

## 1. Zero-Egress "Runs on Atlassian" Architecture

CleanDoc is built 100% natively on **Atlassian Forge** (`nodejs22.x` runtime) with **Forge SQL** storage and **zero external network egress** (`permissions.external.fetch` is completely absent from `manifest.yml`).

This means:
- **Your Confluence and Jira data never leaves Atlassian's cloud infrastructure.**
- **We operate no external servers, no third-party databases, no external analytics trackers, and no LLM/AI endpoints.**
- Your Atlassian **Data Residency** pinning (e.g., EU, US, Germany, Australia) is natively respected by Forge SQL.

---

## 2. Categories of Data Processed

CleanDoc accesses only the minimum Confluence and Jira metadata required to perform content lifecycle scanning and offboarding cleanup inside your tenant:

| Data Category | Exact Fields Stored in Forge SQL | Purpose |
|---|---|---|
| **Page Metadata** | `page_id`, `space_key`, `space_id`, `title`, `page_url`, `last_modified_at`, `is_orphan`, `rovo_pollution_score`, `status` | Identify stale/orphan pages and calculate Rovo Readiness Score |
| **Page Ownership** | `owner_account_id`, `owner_display_name`, `owner_status`, `reassigned_to_account_id` | Detect deactivated/offboarded owners and perform bulk owner reassignment |
| **Jira Issue Keys** | `linked_jira_keys` (e.g. `PROJ-123`), `resolved_jira_keys` | Flag pages referencing resolved/closed Jira tickets |
| **Audit Logs** | `action_type`, `actor_account_id`, `actor_display_name`, `affected_count`, `page_ids`, `created_at` | Provide an exportable compliance log (ISO 27001 / SOC 2) |
| **App Configuration** | `stale_days_threshold`, `exclude_labels`, scan cursor checkpoints, aggregate counters | Persist administrator rules and incremental scan progress |

### What CleanDoc Does NOT Store
- CleanDoc **never stores Confluence page body HTML/content** inside Forge SQL. Storage XML is parsed transiently in memory during a scan solely to extract Jira macro issue keys (`[A-Z]+-\d+`), then immediately discarded.
- CleanDoc does **not** store user emails, passwords, IP addresses, or payment card information (all billing is handled exclusively by Atlassian Marketplace as Merchant of Record).

---

## 3. Data Retention & Deletion

- All metadata stored in Forge SQL remains strictly inside your Atlassian Forge tenant environment while the app is installed.
- Administrators can whitelist or archive pages at any time.
- **Uninstallation:** When an administrator uninstalls CleanDoc from a Confluence Cloud site, Atlassian automatically schedules and executes deletion of the tenant's Forge SQL database according to Atlassian Forge platform data lifecycle policies.
- **Data Subject / Erasure Requests:** Because CleanDoc only retains Atlassian `accountId` and `displayName` references within tenant-isolated Forge SQL tables, site administrators may request manual purge or contact `pierrecassagnettes+cleandoc@gmail.com` for assistance within 72 hours.

---

## 4. Subprocessors

CleanDoc uses **zero external subprocessors**. All compute and SQL storage run exclusively on **Atlassian Forge** (Atlassian Pty Ltd / Atlassian US, Inc.).

---

## 5. GDPR & International Transfers

For customers in the European Economic Area (EEA), UK, and Switzerland:
- Atlassian acts as the underlying cloud platform subprocessor under Atlassian's Data Processing Addendum (DPA).
- Because CleanDoc makes zero outbound network calls outside Atlassian Forge, no cross-border data transfers to publisher-controlled servers occur.

---

## 6. Security & Contact

For security reports, GDPR inquiries, or vulnerability disclosures, contact:  
`pierrecassagnettes+cleandoc@gmail.com`
