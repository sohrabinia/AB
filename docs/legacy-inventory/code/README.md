# Legacy Inventory — Application Code & Project Structures

## Status: VERIFIED ABSENT IN THIS GIT REPOSITORY'S FULL HISTORY

### Overview
This directory records the project tree, module dependencies, routing/URL logic, SEO generation code, and legacy functional capabilities (`Amlakbashi.Accounting`, `Amlakbashi.Application`, `Amlakbashi.Core`, `Amlakbashi.Data`, `Amlakbashi.Host`, `Amlakbashi.Mediator`).

### Status & Findings
* **Git Repository History (`[FACT]`):** Following `git fetch --unshallow`, full history inspection confirmed 4 commits total starting at root commit `e68bd933b494a2b24beb9ae304ccdce748bc83b6`. Zero application source files (`.cs`, `.csproj`, `.sln`, `.js`, `.py`, `.php`) exist anywhere in the Git history of `sohrabinia/AB`.
* **Scope Boundary (`[FACT]`):** Verified absent **specifically within this GitHub repository's full Git history**. This does not mean legacy code does not exist elsewhere; the application source code lives on external servers, private repositories, or unlinked infrastructure.

### Functional Scope (Inferred from System Context)
- Persian real estate property listing engine (sale, rent, mortgage).
- Category and location taxonomy (Iran provinces, cities, neighborhoods).
- Boosted listing mechanism ("نردبان" / ladder system).
- Accounting & ledger integration (`Amlakbashi.Accounting`).
- SMS gateway integration for user OTP/auth.
