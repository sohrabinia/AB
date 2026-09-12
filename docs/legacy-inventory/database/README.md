# Legacy Inventory — Database & Content Tables

## Status: INACCESSIBLE / VERIFIED ABSENT IN WORKSPACE

### Overview
This directory is designated for lossless data dumps and schema records of legacy database tables (property listings, categories, locations, Persian articles/blog posts, transaction logs, system configuration).

### Status & Findings
* **Local Workspace SQL / Dump Files:** `VERIFIED ABSENT` (`find /app -name "*.sql"` returned 0 files).
* **Production Database Instance:** `INACCESSIBLE` (no database host IP, port, connection string, or read-replica credentials available).
* **Tracked Tables:** 0 tables available in current workspace session.

### Required Prerequisites for Database Audit
1. Read-only database connection credentials (host, port, DB name, username, password) OR a sanitized SQL/bak dump file.
2. Schema documentation or table export (`.json` / `.csv` per table).

### Preservation Rules Applied
When database access is granted:
- All columns, data types, constraints, row counts, and exact cell values must be exported without transformation.
- Orphaned or obsolete tables must be recorded and preserved, never dropped.
