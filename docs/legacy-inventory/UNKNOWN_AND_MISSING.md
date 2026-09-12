# AmlakBashi — Unresolved Dependencies & Action Items Register

## 1. Top Outstanding Dependency: Production Database Credentials / Backup (`[FACT]`)

* **Category:** Production Database & Live Content Data
* **Current Status:** **INACCESSIBLE** (Requires human-provided credentials or database backup file)
* **Details:**
  - The legacy application source code (`AmlakbashiRecovery`) is 100% recovered, compiles cleanly, and includes all EF Core entity models and database migrations (`Amlakbashi.Data`).
  - However, live production data (active property listings, Persian blog posts, user accounts, transaction histories) resides exclusively inside the live production SQL Server instance.
* **Prerequisite to Resolve:**
  - The human owner must provide one of the following:
    1. A SQL Server database backup dump (`.bak` or `.sql` dump).
    2. Read-only database connection credentials (host IP/domain, port, DB name, username, password).

---

## 2. Production Media & User Upload Storage (`[FACT]`)

* **Category:** Media & Property Photo Storage
* **Current Status:** **INACCESSIBLE** (Stored on production web server disk)
* **Details:**
  - Source code audit of `FileController.cs` confirms that uploaded property photos are stored on disk under `Amlakbashi.Host/wwwroot/Uploads/Residence/` and cached in `wwwroot/content/imgcache/`.
  - These multi-GB user upload files are stored on server disk and excluded from Git version control.
* **Prerequisite to Resolve:**
  - A compressed zip/tar archive of the production server's `wwwroot/Uploads/` directory or object storage volume.

---

## 3. Live Site Crawl & Sandbox Network Boundary (`[FACT]`)

* **Category:** Live Website Page Crawl & Sitemaps
* **Current Status:** **INACCESSIBLE** (Sandbox Container Egress Firewall Timeout)
* **Details:**
  - HTTP request attempts to `https://www.amlakbashi.com/` and `https://www.amlakbashi.com/sitemap.xml` resolved to IPs `185.143.233.238` and `185.143.234.238`.
  - Outbound TCP connections to port 443 timed out (`curl: (28)`), confirming container network egress policy restrictions in the sandbox environment.
* **Prerequisite to Resolve:**
  - Whitelist container egress to `185.143.233.238:443` / `185.143.234.238:443` OR provide WGET static HTML page crawl archive.

---

## 4. Phase 0 Completion Summary

* **Application Source Code:** `100% RECOVERED & VERIFIED` (`sohrabinia/AmlakbashiRecovery`, 1,219 C# files, 6 projects, .NET 8 compatible).
* **Database Maintenance Scripts:** `100% PRESERVED` (`GenerateDeletedUsersXML.sql`, `RemoveDuplicateUsers.sql`, `RemoveNullUsers.sql`).
* **Remaining Non-Code Assets:** Require human-provided DB backup/credentials, server media directory backup, or external crawl archive as logged above.
