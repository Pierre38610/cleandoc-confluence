# Security, Architecture & Atlassian Ecoscanner / Privacy Questionnaire Reference

This document summarizes the security posture of **CleanDoc — Stale-Page & Offboarding Cleaner for Confluence** and provides exact answers for the **Atlassian Marketplace Security & Privacy Assessment** and **Ecoscanner** checks.

- **Publisher & Security Contact:** Pierre Cassagnettes — CleanDoc (`pierrecassagnettes+cleandoc@gmail.com`)
- **Public Homepage:** `https://pierre38610.github.io/cleandoc-confluence/`
- **Privacy Policy:** `https://pierre38610.github.io/cleandoc-confluence/privacy.html`
- **Terms of Service (EULA):** `https://pierre38610.github.io/cleandoc-confluence/terms.html`
- **Security Architecture Page:** `https://pierre38610.github.io/cleandoc-confluence/security.html`

---

## 1. Architecture Security Summary

| Security Control | Implementation in CleanDoc |
|---|---|
| **Hosting Platform** | 100% Atlassian Forge (`nodejs22.x`), zero external servers or VPS |
| **Runs on Atlassian Eligibility** | **YES** — Zero `external.fetch` permissions in `manifest.yml`; zero remote backends |
| **Database** | Atlassian Forge SQL (`engine: mysql`), tenant-isolated automatically by Forge |
| **SQL Injection Protection** | 100% parameterized queries via `sql.prepare(...).bindParams(...)` |
| **Data Residency** | Native Forge Data Residency support (no external egress) |
| **Authentication & AuthZ** | Handled natively by Forge Runtime (`asUser()` / `asApp()` scoped OAuth 2.0) |
| **Vulnerability Hygiene** | Minimal dependencies (`@forge/*` + `react`); zero `eval()`, zero dynamic HTML injection |
| **Auditability** | Every bulk archive, bulk reassign, and whitelist action writes an immutable row in `audit_logs` |

---

## 2. Scopes Used in `manifest.yml` (Principle of Least Privilege)

| Scope | Why It Is Strictly Necessary |
|---|---|
| `read:page:confluence` | Read page metadata (`lastModified`, `parentId`, `ownerId`, `body-format=storage`) to evaluate staleness and extract Jira keys |
| `write:page:confluence` | Update `ownerId` via `PUT /wiki/api/v2/pages/{id}` during offboarding reassignment |
| `write:confluence-content` | Call `POST /wiki/rest/api/content/archive` and add `evergreen` whitelist labels |
| `read:space:confluence` | Resolve space keys, space names, and homepage IDs (to avoid flagging space homepages as orphans) |
| `read:user:confluence` / `read:confluence-user` | Query `/wiki/rest/api/user/bulk` to check `accountStatus` (`active` vs `inactive`/`closed`) |
| `read:confluence-space.summary` | Poll Confluence async archive task status (`/wiki/rest/api/longtask/{id}`) |
| `read:content-details:confluence` / `search:confluence` | Query CQL search (`/wiki/rest/api/content/search`) and assignable users for incremental stale scanning |
| `read:jira-work` | Query `/rest/api/3/search/jql` (or `/rest/api/3/issue/{key}`) to check whether linked Jira issues are resolved (`resolutiondate`) |

---

## 3. Ready-to-Paste Answers for Atlassian Marketplace Security Questionnaire

1. **Does your app store, process, or transmit customer data outside of Atlassian Cloud?**
   - **Answer:** **No.** CleanDoc runs exclusively on Atlassian Forge (`nodejs22.x`) using Atlassian Forge SQL. It defines zero `external.fetch` permissions in `manifest.yml` and makes zero outbound calls to any third-party servers, APIs, or analytics providers.
2. **Does your app qualify for "Runs on Atlassian"?**
   - **Answer:** **Yes.** All compute runs inside Forge Functions and UI Kit 2 (`render: native`), all persistence uses Forge SQL, and there is zero external egress.
3. **Does your app store Confluence page body content?**
   - **Answer:** **No.** Page body storage XML is read transiently in memory during scheduled/manual scans solely to detect Jira macro issue keys, and is never persisted to Forge SQL or logs.
4. **How do you prevent SQL Injection in Forge SQL?**
   - **Answer:** Every DML query in `src/db/repository.ts` uses `sql.prepare(query).bindParams(...)` with positional `?` placeholders. Dynamic sorting or filtering maps strictly to allowlisted column names.
5. **How does your app handle authentication and authorization?**
   - **Answer:** All UI requests pass through `@forge/resolver` inside Atlassian's authenticated Forge bridge. Interactive user-initiated operations use `api.asUser()` where appropriate or verify tenant/license context; scheduled triggers operate strictly within the installed tenant context via `api.asApp()`.
6. **What happens to tenant data upon uninstallation?**
   - **Answer:** All data resides exclusively inside tenant-scoped Forge SQL tables managed by Atlassian Forge, which are automatically deprovisioned when the app is uninstalled.
7. **Does your app send data to external AI / LLM APIs?**
   - **Answer:** **No.** The Rovo Pollution Score (`0–100`) is computed deterministically inside Forge Functions using inactivity age, owner account status, orphan status, and resolved Jira link counts.
8. **What is your security vulnerability response SLA?**
   - **Answer:** Critical/High security vulnerabilities affecting the app or dependencies are patched and deployed via `forge deploy` within **24–48 hours**, with notification sent to affected customers if required.
