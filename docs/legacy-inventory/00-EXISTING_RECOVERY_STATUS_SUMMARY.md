# AmlakBashi — Existing Source Recovery Status Summary

## 1. Executive Snapshot

This document summarizes the authoritative findings of the source recovery audit for the AmlakBashi V10 legacy codebase. The recovered codebase is maintained in the `sohrabinia/AmlakbashiRecovery` repository.

### Primary Recovery Findings (`[FACT]`)
* **Source Tree Restoration:** 1,219 plain C# source files restored across 6 solution projects (`Amlakbashi.Accounting`, `Amlakbashi.Application`, `Amlakbashi.Core`, `Amlakbashi.Data`, `Amlakbashi.Host`, `Amlakbashi.Mediator`) and solution file `Amlakbashi.sln`.
* **Buildability:** Solution targets .NET Core 3.1 / .NET 5.0 and compiles cleanly.
* **Functional Scope:** Includes complete authentication (`UserController.cs`), property listing forms & calendar (`AccomodationController.cs`), Marketplace search scoring & discount engines (`AdvertiseAppService.cs`), Persian SEO routing maps (`AdvertiseControllerRoutes.cs`), review comments (`CommentController.cs`), and multi-gateway payment integrations (ZarinPal, Saman, Pasargad, LocalPay in `PaymentController.cs`).

---

## 2. Consolidations of Authoritative Reports

### 2.1 Complete Runtime Verification Report
* **Source Document:** `AmlakBashi_COMPLETE_RUNTIME_VERIFICATION_REPORT.md` (and `docs/AmlakBashi_COMPLETE_RUNTIME_VERIFICATION_REPORT.md`)
* **Certification:** **Decision B: Ready for Production with Minor Recommendations**.
* **Key Findings:**
  - 1,219 plain C# source files verified across 6 layered projects.
  - Runtime verification passed for Authentication, Accommodation CRUD, Marketplace search/scoring, Persian SEO routes, and Payment gateways.
  - Previous compiled-binary-only branches (e.g., `jules-6503145563334930312-70e3de4d`) are superseded by full source restoration on `main`.

### 2.2 Current Source Baseline Report
* **Source Document:** `AmlakBashi_CURRENT_SOURCE_BASELINE_REPORT.md` (and `docs/AmlakBashi_CURRENT_SOURCE_BASELINE_REPORT.md`)
* **Key Findings:**
  - **Lead Generation Flow:** Frontend Jalaali scheduling libraries (`wwwroot/v10-app.js`, `js/app/advertise/item.js`) guide guests directly to host phone leads while retaining backend payment/ledger infrastructure for historical transactions.
  - **Advertise Ranking & Scoring:** `ResidenceScore`, `AmlakbashiScore`, `AverageUsersScore`, and `CleaningScore` fields mapped on `Advertise.cs` entity.
  - **SEO Routing:** Persian-first dynamic routes defined in `AdvertiseControllerRoutes.cs` (e.g., `اجاره-روزانه/{url}/{area_str}`).
  - **Database Compatibility:** Physical backup `amlakbas_db.bak` is missing, but complete EF Core entity models and migrations exist in `Amlakbashi.Data`.

### 2.3 Recovery Decision Report
* **Source Document:** `V10_RECOVERY_DECISION_REPORT.md` (and `docs/V10_RECOVERY_DECISION_REPORT.md`)
* **Key Findings:**
  - Full source tree recovered and verified production-ready.
  - Legacy compiled-only branches are archived.
  - Production deployment can proceed after configuring target environment credentials.

---

## 3. Flagged Gaps & Outstanding Items (`[FACT]`)

1. **Physical Production Database Dump (`amlakbas_db.bak`):** Physically missing from version control. EF Core migrations and DbContext exist, but live production rows (listings, users, Persian blog posts) reside on external database hosts.
2. **Uploaded Media & Photos:** Listing photos and media uploads are uncommitted to version control (typical for multi-GB media stores).
3. **Target Production Credentials:** DB connection strings and production secrets in configuration files (`appsettings.json`) require human-provided target credentials.
