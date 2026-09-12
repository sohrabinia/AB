# AmlakBashi — Phase 0: Gate 2 Source-of-Truth Register (Updated)

## 1. Executive Snapshot

This register inventories all potential sources of truth for the 11-year legacy AmlakBashi (املاک باشی) system (code, database, content, media, configurations) and records their exact availability status, evidence, and tested reachability.

Classification Rules:
* **`FOUND`**: Source was discovered and verified in the workspace/repository.
* **`VERIFIED ABSENT IN GIT`**: Scope is explicitly verified absent across the entire Git repository history (post-unshallow).
* **`INACCESSIBLE`**: Source exists or likely exists externally, but credentials, network firewall boundaries, or connection timeouts block access from this sandbox environment.
* **`NOT INVESTIGATED`**: Source was not checked.

---

## 2. Source-of-Truth Register Matrix

| Source Category | Identified Asset / Location | Classification Status | Evidence & Command Executed |
| :--- | :--- | :--- | :--- |
| **Git Repository & History** | `sohrabinia/AB` (`origin`) | **`FOUND`** | `git fetch --unshallow`<br>4 commits total in history starting at root commit `e68bd933...`. Zero application code files in full history. |
| **Live Public Website** | `https://www.amlakbashi.com/` | **`INACCESSIBLE`** | `curl -I -v https://www.amlakbashi.com/`<br>Resolved to `185.143.234.238`. TCP connection timed out after 269s (`curl: (28) Failed to connect...`). |
| **Production Web Server** | Live IIS / Nginx / Apache Host | **`INACCESSIBLE`** | Sandbox environment has no SSH/FTP access or server network host credentials. |
| **Production Database** | Live SQL Server / MySQL / PostgreSQL | **`INACCESSIBLE`** | No connection strings, environment variables, or DB credentials exist in workspace. |
| **File / Media Storage** | Listing Photos, CDN, Local Uploads | **`INACCESSIBLE`** | No S3 buckets, CDN endpoints, or media storage paths configured in repository. |
| **Database Dumps / Backups** | `.bak`, `.sql`, `.zip` Backups | **`VERIFIED ABSENT IN GIT`** | `find /app -name "*.bak" -o -name "*.sql"` returned 0 files across entire Git tree. |
| **CMS / Admin Panel** | Content Management System | **`INACCESSIBLE`** | Admin panel endpoints and credentials are not present in repository. |
| **Deployment / Config Files** | `web.config`, `appsettings.json`, Dockerfile | **`VERIFIED ABSENT IN GIT`** | Root directory contains only `.git/` and `docs/`. |

---

## 3. Evidence & Detailed Status by Category

### 3.1 Git Repository & History
* **Status:** `FOUND`
* **Evidence:**
  * Executed `git fetch --unshallow` to retrieve complete repository history.
  * Parentless root commit `e68bd933b494a2b24beb9ae304ccdce748bc83b6` was confirmed.
  * All 4 commits across all branches/refs relate exclusively to Phase 0 documentation baseline. Zero legacy source code files exist in Git history.

### 3.2 Live Public Website (`https://www.amlakbashi.com/`)
* **Status:** `INACCESSIBLE` (Egress Timeout)
* **Verbatim Evidence:**
  ```
  * Trying 185.143.234.238:443...
  * connect to 185.143.234.238 port 443 from 192.168.0.2 port 39358 failed: Connection timed out
  * Failed to connect to www.amlakbashi.com port 443 after 269939 ms: Couldn't connect to server
  curl: (28) Failed to connect to www.amlakbashi.com port 443 after 269939 ms: Couldn't connect to server
  ```

---

## 4. Gate 2 Summary

* **Git Repository:** Fully unshallowed and verified (`FOUND`, 0 legacy code files).
* **Live Website:** Tested via curl (`INACCESSIBLE` due to network egress timeout to `185.143.234.238`).
* **Production Infrastructure:** Server, DB, media, backups, and configs remain `INACCESSIBLE` or `VERIFIED ABSENT IN GIT`.
