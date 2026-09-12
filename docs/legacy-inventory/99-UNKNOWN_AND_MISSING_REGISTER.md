# AmlakBashi — Phase 0: Gate 3 Unknown and Missing Register

## 1. Overview

This register records every unresolved item, unknown component, and missing asset required to complete full lossless documentation of the 11-year legacy AmlakBashi system, along with the specific prerequisites needed to resolve each item.

---

## 2. Detailed Unknown and Missing Register

### Item 1: Primary Legacy Source Code Repository / Backup
* **Category:** Application Source Code
* **Status:** MISSING from `sohrabinia/AB` Git repository
* **Impact:** High — Modernization cannot proceed without baseline source code.
* **Prerequisite to Resolve:**
  1. Locate original legacy source code repository (e.g. TFS, Bitbucket, private GitHub, or server webroot zip).
  2. Grant read access or commit historical source code into a designated branch.

### Item 2: Production Database Connection / SQL Export
* **Category:** Database & Content
* **Status:** INACCESSIBLE in sandbox environment
* **Impact:** High — All property listings, Persian articles, taxonomy, and user data reside in the live database.
* **Prerequisite to Resolve:**
  1. Provide read-only database credentials (host, port, DB name, credentials) OR a sanitized SQL/bak database dump file.

### Item 3: Live Website Domain & Page Crawl Target
* **Category:** Live Website & Content
* **Status:** INACCESSIBLE in sandbox environment
* **Impact:** High — Live website URLs, SEO meta tags, canonical rules, and Persian page copy are unmapped.
* **Prerequisite to Resolve:**
  1. Provide target domain URL (e.g., `amlakbashi.com` or live IP address).
  2. Enable outbound crawling access or provide static web page archive files.

### Item 4: Media & Image Upload Storage
* **Category:** Media Assets
* **Status:** INACCESSIBLE in sandbox environment
* **Impact:** Medium — Real estate photos and document attachments are uninventoried.
* **Prerequisite to Resolve:**
  1. Provide storage bucket credentials (S3/CDN) or server media path access (`/uploads`).

### Item 5: Production Hosting Infrastructure & IIS/Nginx Configuration
* **Category:** Infrastructure & Deployment
* **Status:** INACCESSIBLE in sandbox environment
* **Impact:** Medium — Rewrite rules, SSL configs, routing, and server specs are unverified.
* **Prerequisite to Resolve:**
  1. Provide server access or web server configuration files (`web.config`, `nginx.conf`).

---

## 3. Mandatory Gate Completion Declaration

Per Section 6 of the Master Prompt:

### Phase 0 Completion Status: **NO-GO** (For Modernization / Phase 1)

**Rationale:**
1. The `sohrabinia/AB` Git repository contains zero application source files, zero database schemas, zero media assets, and zero configuration files.
2. Production database, server host, live public website, and media storage are **INACCESSIBLE** within the sandboxed execution environment.
3. While all discoverable workspace assets and Git history have been 100% losslessly inventoried without paraphrasing or data loss, modernization (Phase 1) **CANNOT** begin until external source code and database assets are provided to the project team.
