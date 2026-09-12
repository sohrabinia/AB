# AmlakBashi — Existing SQL Maintenance Scripts & Database Configuration

## 1. Database Connection & Configuration References

* **Configuration File Location:** `Amlakbashi.Host/appsettings.json` and `Amlakbashi.Host/appsettings.Development.json`
* **DbContext Connection Keys:**
  - `ConnectionStrings:DefaultConnection` -> Targets `AmlakbashiDB` (SQL Server)
  - `ConnectionStrings:IdentityConnection` -> Targets ASP.NET Identity database
  - `ConnectionStrings:JobDbConnection` -> Targets Hangfire background job database
* **Credential Protection (`[FACT]`):** Target connection string passwords are omitted or configured via environment variable overrides. Live production database access requires credentials supplied by the human system owner.

---

## 2. Preserved SQL Maintenance Scripts

The repository contains 3 legacy SQL scripts at root used for user data cleanup, deduplication, and XML export before database migration.

### 2.1 `GenerateDeletedUsersXML.sql`
* **Purpose:** Identifies duplicate user accounts by mobile number (`MainMobile`), isolates superseded duplicate rows, and outputs their records as an XML document (`FOR XML PATH`) prior to deletion.
* **Verbatim Content:**
```sql
DECLARE @duplicatedMobile TABLE (MainMobile nvarchar(100));
DECLARE @deletedUsers TABLE (UserID bigint);

INSERT INTO @duplicatedMobile
SELECT MainMobile FROM Users WHERE MainMobile IN
  (SELECT MainMobile FROM Users GROUP BY MainMobile HAVING COUNT(*) > 1)
GROUP BY MainMobile;

WITH cte AS (
    SELECT UserID, MainMobile, CreateDate,
        ROW_NUMBER() OVER (
            PARTITION BY MainMobile
            ORDER BY MainMobile, State, email DESC, CreateDate
        ) row_num
    FROM Users
    WHERE MainMobile IN (SELECT MainMobile FROM @duplicatedMobile)
)
INSERT INTO @deletedUsers
SELECT UserID FROM cte WHERE row_num > 1;

SELECT * FROM Users WHERE UserID IN (SELECT UserID FROM @deletedUsers) FOR XML PATH;
```

---

### 2.2 `RemoveDuplicateUsers.sql`
* **Purpose:** Performs full entity relationship re-mapping and deduplication for duplicate user accounts. It re-assigns foreign key references across 20+ tables (`Reserves`, `Advertises`, `ActionLogs`, `BankCards`, `BlogPosts`, `Carts`, `Payments`, `CreditTransactions`, `PrizeCreditTransactions`, `Chats`, `Comments`, `DiscountCoupons`, `Files`, `Posts`, `ReportItems`, `SupportChats`, `UserFavorites`) to the primary active target `UserID`, recalculates ledger transaction balances, and purges duplicate user rows.
* **Verbatim Script Overview:**
  - Identifies duplicate `MainMobile` groups.
  - Re-links all transactional records to `TargetUserID` (row_num = 1).
  - Recalculates `CreditTransactions` and `PrizeCreditTransactions` balances sequentially via T-SQL cursor.
  - Purges merged `UserID` entries from `Users`.

---

### 2.3 `RemoveNullUsers.sql`
* **Purpose:** Cleans up orphaned support chats and invalid user records lacking a primary mobile phone number.
* **Verbatim Content:**
```sql
DELETE SupportChats WHERE UserID IN (SELECT UserID FROM Users WHERE MainMobile IS NULL);
DELETE Users WHERE MainMobile IS NULL;
```
