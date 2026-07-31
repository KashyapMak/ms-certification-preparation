# DP-800 Robust Study Material - Expanded Version

**Exam:** DP-800: Developing AI-Enabled Database Solutions  
**Certification:** Microsoft Certified: SQL AI Developer Associate  
**Generated:** 31 July 2026  
**Purpose:** Single Markdown study pack with concepts, syntax, decision trees, examples, and last-mile missing topics so you do not need to jump back to Microsoft Learn at the last moment.

> This guide merges and expands the two provided DP-800 notes and adds the previously missing samples/details: advanced data types, full-text search, JSON_CONTAINS, full REGEXP family, correlated query patterns, Query Store plan forcing, Query Performance Insight, Azure Monitor, DAB CLI, GraphQL, database scoped credentials, AI SQL functions, vector index decision scenarios, search evaluation metrics, deadlock workflows, and exam decision trees.

---

## Exam Weighting and Study Strategy

| Domain | Weight | What to master |
|---|---:|---|
| Design and develop database solutions | 35-40% | Data types, tables, indexes, JSON, programmability, advanced T-SQL, AI-assisted development |
| Secure, optimize, and deploy database solutions | 35-40% | Security, encryption, RLS, performance, Query Store, CI/CD, DAB, Azure integration |
| Implement AI capabilities in database solutions | 25-30% | Models, embeddings, vector search, hybrid search, RRF, RAG |

**Exam mindset:** DP-800 is mostly scenario-based. When a question gives a business requirement, identify the keyword: history, tamper-proof, semantic, keyword, passwordless, drift, regression, blocking, REST, GraphQL, embedding, or RAG.

---

# Domain 1 - Design and Develop Database Solutions

## 1. Design and Implement Database Objects

### 1.1 Data Types - Exam Complete View

#### Integer and Numeric Types

| Data type | Size | Range / behavior | Exam use case |
|---|---:|---|---|
| `BIT` | 1 bit | 0, 1, or NULL | True/false flags |
| `TINYINT` | 1 byte | 0 to 255 | Small positive counters |
| `SMALLINT` | 2 bytes | -32,768 to 32,767 | Small numeric domain |
| `INT` | 4 bytes | About +/- 2 billion | Standard keys and counters |
| `BIGINT` | 8 bytes | Very large integer range | Large fact tables, huge sequences |
| `DECIMAL(p,s)` / `NUMERIC(p,s)` | 5-17 bytes | Exact precision | Money-like exact calculations |
| `MONEY` / `SMALLMONEY` | 8 / 4 bytes | Currency-like | Legacy/simple currency, but decimal often preferred |
| `FLOAT` / `REAL` | Approximate | Approximate numeric | Scientific calculations, not exact finance |

```sql
CREATE TABLE dbo.EmployeePay
(
    EmployeeID INT NOT NULL PRIMARY KEY,
    IsActive BIT NOT NULL DEFAULT 1,
    Salary DECIMAL(12,2) NOT NULL,
    BonusRate DECIMAL(5,4) NULL
);
```

**Exam trap:** For financial or exact calculations, prefer `DECIMAL`/`NUMERIC`, not `FLOAT`.

#### String and Binary Types

| Type | Max size | Use case |
|---|---:|---|
| `CHAR(n)` | 8,000 bytes | Fixed-length non-Unicode |
| `VARCHAR(n)` | 8,000 bytes | Variable non-Unicode |
| `VARCHAR(MAX)` | 2 GB | Large non-Unicode text |
| `NCHAR(n)` | 4,000 characters | Fixed-length Unicode |
| `NVARCHAR(n)` | 4,000 characters | Variable Unicode |
| `NVARCHAR(MAX)` | 2 GB | Large Unicode, JSON text |
| `BINARY(n)` | 8,000 bytes | Fixed binary |
| `VARBINARY(n)` | 8,000 bytes | Variable binary |
| `VARBINARY(MAX)` | 2 GB | Files, images, encrypted payloads |

```sql
CREATE TABLE dbo.CustomerProfile
(
    CustomerID INT NOT NULL PRIMARY KEY,
    DisplayName NVARCHAR(100) NOT NULL,
    ProfileJson NVARCHAR(MAX) NULL,
    ProfilePhoto VARBINARY(MAX) NULL
);
```

**Exam tip:** Use `NVARCHAR` for multilingual data and JSON payloads.

#### Date and Time Types

| Type | Use case |
|---|---|
| `DATE` | Date only |
| `TIME` | Time only |
| `DATETIME` | Legacy date and time |
| `DATETIME2(p)` | Preferred, high precision |
| `DATETIMEOFFSET` | Time zone offset required |

```sql
CreatedAt DATETIME2(7) NOT NULL DEFAULT SYSUTCDATETIME()
```

#### Other Important Types

| Type | Use case | Example |
|---|---|---|
| `UNIQUEIDENTIFIER` | Distributed unique IDs | `DEFAULT NEWID()` or `NEWSEQUENTIALID()` |
| `XML` | XML document storage/query | Legacy XML integrations |
| `SQL_VARIANT` | Different data types in one column | Rare, avoid unless required |
| `VECTOR(n)` | Embedding vectors | Semantic search |

```sql
CREATE TABLE dbo.DistributedCustomer
(
    CustomerID UNIQUEIDENTIFIER NOT NULL DEFAULT NEWID() PRIMARY KEY,
    CustomerName NVARCHAR(200) NOT NULL
);
```

**Exam scenario:** Need globally unique IDs across distributed systems. Answer: `UNIQUEIDENTIFIER`. Use `NEWSEQUENTIALID()` when insert locality matters and sequential GUID is acceptable.

---

## 1.2 Index Design and Selection Scenarios

### Rowstore Indexes

```sql
CREATE CLUSTERED INDEX IX_Orders_OrderDate
ON dbo.Orders(OrderDate);

CREATE NONCLUSTERED INDEX IX_Orders_CustomerID
ON dbo.Orders(CustomerID)
INCLUDE (OrderDate, TotalAmount);
```

| Requirement | Recommended design |
|---|---|
| One-row lookup by email/customer ID | Nonclustered index |
| Frequent date range query | Clustered or nonclustered index on date |
| Avoid Key Lookup | Nonclustered index with `INCLUDE` columns |
| `ORDER BY` frequently used | Index aligned with sort order |
| Low-selectivity column, e.g., IsActive | Usually not useful alone |
| Multi-column filters | Composite index ordered by selectivity and query predicates |

### Composite Index Example

```sql
CREATE NONCLUSTERED INDEX IX_Orders_Customer_Date
ON dbo.Orders(CustomerID, OrderDate DESC)
INCLUDE (TotalAmount, Status);
```

**Exam tip:** Column order matters. Equality predicates usually come before range predicates.

### Filtered Index Example

```sql
CREATE NONCLUSTERED INDEX IX_Orders_OpenOrders
ON dbo.Orders(CustomerID, OrderDate)
WHERE Status = 'Open';
```

**Use when:** a small subset of rows is queried frequently.

### Columnstore Indexes

```sql
CREATE CLUSTERED COLUMNSTORE INDEX CCI_FactSales
ON dbo.FactSales;

CREATE NONCLUSTERED COLUMNSTORE INDEX NCCI_Sales_Analytics
ON dbo.Orders(CustomerID, OrderDate, TotalAmount, ProductID);
```

| Requirement | Best answer |
|---|---|
| Analytics over millions of rows | Clustered columnstore |
| Mixed OLTP and analytics | Nonclustered columnstore |
| Heavy point lookups | Rowstore index |
| High-frequency updates | Avoid columnstore as default |

---

## 1.3 Specialized Tables

### Memory-Optimized Tables

```sql
CREATE TABLE dbo.HighFreqTelemetry
(
    SessionID INT NOT NULL PRIMARY KEY NONCLUSTERED,
    DeviceID INT NOT NULL,
    Payload VARCHAR(500) NOT NULL
)
WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA);
```

| Durability | Meaning | Best for |
|---|---|---|
| `SCHEMA_AND_DATA` | Schema and data persist | Critical low-latency OLTP |
| `SCHEMA_ONLY` | Data lost after restart | Session state, transient cache |

### Temporal Tables

```sql
CREATE TABLE dbo.Employee
(
    EmployeeID INT PRIMARY KEY,
    Name NVARCHAR(100) NOT NULL,
    Salary DECIMAL(18,2) NOT NULL,
    ValidFrom DATETIME2 GENERATED ALWAYS AS ROW START NOT NULL,
    ValidTo DATETIME2 GENERATED ALWAYS AS ROW END NOT NULL,
    PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
)
WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.EmployeeHistory));

SELECT *
FROM dbo.Employee
FOR SYSTEM_TIME AS OF '2026-06-01T10:00:00';
```

**Use when:** historical row state, point-in-time analysis, accidental recovery, audit-style history.

### Ledger Tables

```sql
CREATE TABLE dbo.FinancialAuditTrail
(
    TransactionID INT IDENTITY PRIMARY KEY,
    AccountID INT NOT NULL,
    Amount DECIMAL(18,2) NOT NULL
)
WITH (LEDGER = ON (LEDGER_TYPE = APPEND_ONLY));
```

| Requirement | Answer |
|---|---|
| Track history | Temporal table |
| Prove data was not tampered with | Ledger table |
| Insert-only compliance trail | Append-only ledger |

### External Tables

```sql
CREATE EXTERNAL TABLE dbo.ExternalSales
(
    SaleID INT,
    Amount DECIMAL(18,2)
)
WITH
(
    LOCATION = '/salesdata/*.parquet',
    DATA_SOURCE = MyAzureStorageSource,
    FILE_FORMAT = ParquetFormat
);
```

**Use when:** query files or lakehouse data in place without copying data into SQL.

### Graph Tables

```sql
CREATE TABLE dbo.Person
(
    ID INT PRIMARY KEY,
    Name NVARCHAR(100)
) AS NODE;

CREATE TABLE dbo.FriendOf AS EDGE;

SELECT p2.Name AS FriendName
FROM dbo.Person AS p1,
     dbo.FriendOf AS f,
     dbo.Person AS p2
WHERE MATCH(p1-(f)->p2)
  AND p1.Name = N'Alice';
```

**Use when:** the relationship pattern is the core query, e.g., multi-hop paths, social networks, fraud rings, dependencies.

---

## 1.4 JSON Columns, JSON Indexing, and JSON Functions

### JSON Storage Pattern

```sql
CREATE TABLE dbo.CustomerOrders
(
    OrderID INT PRIMARY KEY,
    OrderDetails NVARCHAR(MAX) NOT NULL,
    CustomerZip AS JSON_VALUE(OrderDetails, '$.Shipping.ZipCode')
);

CREATE INDEX IX_CustomerOrders_CustomerZip
ON dbo.CustomerOrders(CustomerZip);
```

### JSON Function Cheat Sheet

| Function | Purpose | Returns |
|---|---|---|
| `JSON_VALUE` | Extract scalar | Text/scalar |
| `JSON_QUERY` | Extract object or array | JSON fragment |
| `OPENJSON` | Shred JSON into rows | Rowset |
| `JSON_OBJECT` | Build JSON object | JSON text |
| `JSON_ARRAY` | Build JSON array | JSON text |
| `JSON_ARRAYAGG` | Aggregate values into JSON array | JSON array |
| `JSON_CONTAINS` | Test whether JSON contains a value/path where supported | Boolean-like predicate |

### JSON Examples

```sql
DECLARE @json NVARCHAR(MAX) = N'{"customer":{"name":"Kashyap"},"tags":["Premium","SQL"],"orders":[{"id":101,"qty":5},{"id":102,"qty":2}]}';

SELECT JSON_VALUE(@json, '$.customer.name') AS CustomerName;
SELECT JSON_QUERY(@json, '$.tags') AS TagsArray;

SELECT *
FROM OPENJSON(@json, '$.orders')
WITH
(
    OrderID INT '$.id',
    Quantity INT '$.qty'
);

SELECT JSON_OBJECT('Name':'Kashyap', 'Skill':'SQL AI') AS JsonObjectExample;
SELECT JSON_ARRAY('SQL', 'Azure SQL', 'Fabric') AS JsonArrayExample;
```

### JSON_CONTAINS Pattern

```sql
SELECT OrderID
FROM dbo.CustomerOrders
WHERE JSON_CONTAINS(OrderDetails, '"Premium"', '$.Tags') = 1;
```

**Exam tip:** If syntax varies by platform/version, focus on the concept: use `JSON_CONTAINS` to check whether a JSON document contains a value at a path, and use `OPENJSON` when you need to turn JSON arrays into rows.

---

## 1.5 Constraints and Sequences

```sql
CREATE TABLE dbo.Department
(
    DeptID INT NOT NULL PRIMARY KEY,
    DeptName NVARCHAR(100) NOT NULL UNIQUE
);

CREATE TABLE dbo.Employee
(
    EmployeeID INT NOT NULL PRIMARY KEY,
    DeptID INT NOT NULL,
    Email NVARCHAR(255) NULL UNIQUE,
    Salary DECIMAL(12,2) NOT NULL CHECK (Salary > 0),
    Status VARCHAR(20) NOT NULL DEFAULT 'Active',
    CONSTRAINT FK_Employee_Department
        FOREIGN KEY (DeptID) REFERENCES dbo.Department(DeptID)
);
```

```sql
CREATE SEQUENCE dbo.InvoiceNumberSeq
    START WITH 10000
    INCREMENT BY 1
    MINVALUE 10000
    NO CACHE;

INSERT INTO dbo.Invoices(InvoiceID, Amount)
VALUES (NEXT VALUE FOR dbo.InvoiceNumberSeq, 499.99);
```

| Requirement | Feature |
|---|---|
| Unique row identifier | Primary key |
| Relationship enforcement | Foreign key |
| Limit allowed values | Check constraint |
| Auto value when omitted | Default constraint |
| Generate reusable numbers across tables | Sequence |

---

## 1.6 Partitioning

```sql
CREATE PARTITION FUNCTION PF_OrderDate (DATE)
AS RANGE RIGHT FOR VALUES ('2025-01-01', '2026-01-01');

CREATE PARTITION SCHEME PS_OrderDate
AS PARTITION PF_OrderDate
TO (FG_2024, FG_2025, FG_2026);

CREATE TABLE dbo.OrdersPartitioned
(
    OrderID INT NOT NULL,
    OrderDate DATE NOT NULL,
    Amount DECIMAL(18,2) NOT NULL
)
ON PS_OrderDate(OrderDate);
```

**Exam scenarios:**

- Query only recent partitions: partition elimination.
- Archive one year quickly: partition switch.
- Large table maintenance: partition by date.

---

# 2. Programmability Objects

## Views and Indexed Views

```sql
CREATE VIEW dbo.vwEmployeePublic
AS
SELECT EmployeeID, Name, DeptID
FROM dbo.Employee;
```

```sql
CREATE VIEW dbo.vw_DailySales
WITH SCHEMABINDING
AS
SELECT
    OrderDate,
    COUNT_BIG(*) AS TotalOrders,
    SUM(TotalAmount) AS TotalRevenue
FROM dbo.Orders
GROUP BY OrderDate;

CREATE UNIQUE CLUSTERED INDEX CIX_vw_DailySales
ON dbo.vw_DailySales(OrderDate);
```

**Use indexed views for:** expensive pre-aggregations that need fast repeated reads.

## Scalar Functions and Inline Table-Valued Functions

```sql
CREATE FUNCTION dbo.fnBonus(@Salary DECIMAL(10,2))
RETURNS DECIMAL(10,2)
AS
BEGIN
    RETURN @Salary * 0.10;
END;
```

```sql
CREATE FUNCTION dbo.fnOrdersByCustomer(@CustomerID INT)
RETURNS TABLE
AS
RETURN
(
    SELECT OrderID, OrderDate, TotalAmount
    FROM dbo.Orders
    WHERE CustomerID = @CustomerID
);
```

**Exam trap:** Inline TVFs are often better optimized than scalar UDFs in large row-by-row operations.

## Stored Procedures

```sql
CREATE PROCEDURE dbo.uspGetOrders
    @CustomerID INT
AS
BEGIN
    SET NOCOUNT ON;

    SELECT OrderID, OrderDate, TotalAmount
    FROM dbo.Orders
    WHERE CustomerID = @CustomerID;
END;
```

## Triggers

```sql
CREATE TRIGGER dbo.trg_AuditEmployeeSalaryUpdate
ON dbo.Employee
AFTER UPDATE
AS
BEGIN
    SET NOCOUNT ON;

    IF UPDATE(Salary)
    BEGIN
        INSERT INTO dbo.SalaryAuditLog(EmployeeID, OldSalary, NewSalary, ModifiedDate)
        SELECT d.EmployeeID, d.Salary, i.Salary, SYSUTCDATETIME()
        FROM deleted AS d
        INNER JOIN inserted AS i
            ON d.EmployeeID = i.EmployeeID;
    END;
END;
```

---

# 3. Advanced T-SQL

## CTEs and Recursive CTEs

```sql
WITH SalesCTE AS
(
    SELECT CustomerID, SUM(TotalAmount) AS TotalSales
    FROM dbo.Orders
    GROUP BY CustomerID
)
SELECT *
FROM SalesCTE
WHERE TotalSales > 10000;
```

```sql
WITH OrgChart AS
(
    SELECT EmployeeID, ManagerID, Title, 1 AS Level
    FROM dbo.Employee
    WHERE ManagerID IS NULL

    UNION ALL

    SELECT e.EmployeeID, e.ManagerID, e.Title, o.Level + 1
    FROM dbo.Employee AS e
    INNER JOIN OrgChart AS o
        ON e.ManagerID = o.EmployeeID
)
SELECT * FROM OrgChart;
```

## Window Functions

```sql
SELECT
    EmployeeID,
    DepartmentID,
    Salary,
    ROW_NUMBER() OVER (PARTITION BY DepartmentID ORDER BY Salary DESC) AS RowNum,
    RANK() OVER (PARTITION BY DepartmentID ORDER BY Salary DESC) AS RankNum,
    DENSE_RANK() OVER (PARTITION BY DepartmentID ORDER BY Salary DESC) AS DenseRankNum,
    LAG(Salary) OVER (PARTITION BY DepartmentID ORDER BY Salary DESC) AS PreviousSalary,
    LEAD(Salary) OVER (PARTITION BY DepartmentID ORDER BY Salary DESC) AS NextSalary,
    SUM(Salary) OVER (PARTITION BY DepartmentID ORDER BY Salary DESC) AS RunningTotal
FROM dbo.Employee;
```

| Function | Exam point |
|---|---|
| `ROW_NUMBER` | Always unique sequence |
| `RANK` | Ties share rank, gaps exist |
| `DENSE_RANK` | Ties share rank, no gaps |
| `LAG` | Previous row |
| `LEAD` | Next row |
| `SUM() OVER` | Running or partition aggregate |

## Regular Expression Functions

| Function | Purpose |
|---|---|
| `REGEXP_LIKE` | Boolean pattern test |
| `REGEXP_REPLACE` | Replace matching text |
| `REGEXP_SUBSTR` | Extract matching substring |
| `REGEXP_INSTR` | Return match position |
| `REGEXP_COUNT` | Count matches |
| `REGEXP_MATCHES` | Return match details where supported |
| `REGEXP_SPLIT_TO_TABLE` | Split string into rows where supported |

```sql
SELECT *
FROM dbo.Users
WHERE REGEXP_LIKE(Email, '^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$');

SELECT REGEXP_REPLACE(PhoneNumber, '[^0-9]', '') AS DigitsOnly
FROM dbo.Customers;

SELECT REGEXP_SUBSTR('Order-12345-UK', '[0-9]+') AS OrderNumber;

SELECT REGEXP_COUNT('SQL,Azure,Fabric,SQL', 'SQL') AS SqlCount;

SELECT *
FROM REGEXP_SPLIT_TO_TABLE('SQL,Azure,Fabric', ',');
```

**Exam tip:** Use regex for pattern-based validation/extraction; use fuzzy matching for approximate similarity.

## Fuzzy Matching

```sql
SELECT
    CustomerID,
    Name,
    EDIT_DISTANCE('Jonathan', Name) AS EditDistance,
    EDIT_DISTANCE_SIMILARITY('Jonathan', Name) AS EditSimilarity,
    JARO_WINKLER_DISTANCE('Jonathan', Name) AS JaroWinkler
FROM dbo.Customers
WHERE JARO_WINKLER_DISTANCE('Jonathan', Name) > 0.85;
```

| Requirement | Best function |
|---|---|
| Count edits between two strings | `EDIT_DISTANCE` |
| Percentage-like similarity | `EDIT_DISTANCE_SIMILARITY` |
| Short names with transpositions | `JARO_WINKLER_DISTANCE` |

## Correlated Query Patterns

### EXISTS Pattern

```sql
SELECT c.CustomerID, c.CustomerName
FROM dbo.Customers AS c
WHERE EXISTS
(
    SELECT 1
    FROM dbo.Orders AS o
    WHERE o.CustomerID = c.CustomerID
);
```

### NOT EXISTS Anti-Join Pattern

```sql
SELECT c.CustomerID, c.CustomerName
FROM dbo.Customers AS c
WHERE NOT EXISTS
(
    SELECT 1
    FROM dbo.Orders AS o
    WHERE o.CustomerID = c.CustomerID
);
```

### Correlated Aggregate Pattern

```sql
SELECT e.EmployeeID, e.DepartmentID, e.Salary
FROM dbo.Employee AS e
WHERE e.Salary >
(
    SELECT AVG(e2.Salary)
    FROM dbo.Employee AS e2
    WHERE e2.DepartmentID = e.DepartmentID
);
```

**Exam tip:** A correlated subquery references columns from the outer query.

## TRY/CATCH Error Handling

```sql
BEGIN TRY
    BEGIN TRANSACTION;

    UPDATE dbo.Accounts SET Balance = Balance - 100 WHERE AccountID = 1;
    UPDATE dbo.Accounts SET Balance = Balance + 100 WHERE AccountID = 2;

    COMMIT TRANSACTION;
END TRY
BEGIN CATCH
    IF @@TRANCOUNT > 0
        ROLLBACK TRANSACTION;

    SELECT ERROR_NUMBER() AS ErrorNumber,
           ERROR_MESSAGE() AS ErrorMessage;

    THROW;
END CATCH;
```

---

# 4. AI-Assisted Development with GitHub Copilot, Fabric Copilot, and MCP

## Copilot Security Rules

- Never paste passwords, connection strings, tokens, customer secrets, or PII into prompts.
- Review all generated SQL for missing schema names, wrong table names, and unsafe dynamic SQL.
- Use least privilege when connecting AI tools to database context.
- For generated database changes, validate through SQL Database Projects and pull requests.

## GitHub Copilot Instruction File

Path:

```text
.github/copilot-instructions.md
```

Example:

```markdown
# SQL Project Instructions

- Generate T-SQL for SQL Server 2025, Azure SQL, and Fabric SQL where compatible.
- Always use schema-qualified object names.
- Avoid SELECT * in production examples.
- Use parameterized stored procedures.
- Add TRY/CATCH for transactional code.
- Never include secrets, credentials, or connection strings.
- Prefer set-based SQL over row-by-row cursors.
```

## MCP Scenario Notes

| Scenario | Best answer |
|---|---|
| Copilot needs access to SQL Server metadata | Connect to MCP server endpoint |
| AI tool needs only schema, not data | Scope MCP to metadata/read-only views |
| AI tool requires secure SQL access | Managed Identity and least privilege |
| Reduce data exposure | Limit tables, columns, rows, and tool permissions |

---

# Domain 2 - Secure, Optimize, and Deploy Database Solutions

# 5. Implement Data Security and Compliance

## Always Encrypted

```sql
CREATE TABLE dbo.CustomerSecure
(
    CustomerID INT NOT NULL PRIMARY KEY,
    SSN NVARCHAR(20) COLLATE Latin1_General_BIN2
    ENCRYPTED WITH
    (
        COLUMN_ENCRYPTION_KEY = CEK1,
        ENCRYPTION_TYPE = DETERMINISTIC,
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256'
    )
);
```

| Encryption type | Same plaintext gives | Search support | Security |
|---|---|---|---|
| Deterministic | Same ciphertext | Equality | Good |
| Randomized | Different ciphertext | No equality search | Stronger |

**Exam answer:** Protect data from DBAs/admins: Always Encrypted.

## Column-Level Encryption

```sql
OPEN SYMMETRIC KEY SalesKey
DECRYPTION BY CERTIFICATE SalesCert;

SELECT EncryptByKey(Key_GUID('SalesKey'), N'Sensitive Data');
```

| Feature | Always Encrypted | Column-level encryption |
|---|---|---|
| Client-side | Yes | No |
| DB engine can access plaintext | No, normally | Potentially yes |
| T-SQL encryption functions | No | Yes |

## Dynamic Data Masking

```sql
ALTER TABLE dbo.Customers
ALTER COLUMN Email ADD MASKED WITH (FUNCTION = 'email()');

ALTER TABLE dbo.Customers
ALTER COLUMN CreditCard ADD MASKED WITH (FUNCTION = 'partial(2,"XXXX-XXXX-",4)');
```

**Exam trap:** DDM hides display values but does not encrypt data.

## Row-Level Security

```sql
CREATE SCHEMA Security;
GO

CREATE FUNCTION Security.fn_TenantAccessPredicate(@TenantID INT)
RETURNS TABLE
WITH SCHEMABINDING
AS
RETURN
    SELECT 1 AS fn_securityPredicate_result
    WHERE @TenantID = CAST(SESSION_CONTEXT(N'TenantID') AS INT);
GO

CREATE SECURITY POLICY Security.TenantIsolationPolicy
ADD FILTER PREDICATE Security.fn_TenantAccessPredicate(TenantID)
ON dbo.Orders
WITH (STATE = ON);
```

**Use when:** same table, different users/tenants see different rows.

## Object-Level Permissions

```sql
GRANT SELECT, INSERT ON dbo.Orders TO SalesUsers;
DENY DELETE ON dbo.Orders TO SalesUsers;
REVOKE INSERT ON dbo.Orders FROM SalesUsers;
```

`DENY` usually overrides `GRANT`.

## Passwordless Authentication and Managed Identity

```sql
CREATE USER [id-my-app-prod] FROM EXTERNAL PROVIDER;
GRANT SELECT, INSERT ON dbo.Orders TO [id-my-app-prod];
```

| Requirement | Best answer |
|---|---|
| Azure Function connects to Azure SQL without password | Managed Identity |
| Avoid secrets in source control | Managed Identity / Key Vault |
| App connects using Entra identity | Microsoft Entra authentication |

## Auditing

Audit targets:

- Azure Storage
- Log Analytics
- Event Hubs

**Use when:** compliance tracking, login monitoring, data-access investigation, permission-change tracking.

## Endpoint Security

| Endpoint | Controls |
|---|---|
| Model endpoint | Managed Identity, private endpoint, scoped credential |
| REST endpoint | AuthN/AuthZ, least privilege, throttling |
| GraphQL endpoint | Entity permissions, restrict mutations, limit schema exposure |
| MCP endpoint | Read-only where possible, scoped tools, audit logs |

---

# 6. Optimize Database Performance

## Configuration and Workload Matching

| Workload | Design |
|---|---|
| OLTP | Rowstore indexes, short transactions, normalized schema, In-Memory OLTP if needed |
| Data warehouse | Columnstore, partitioning, star schema |
| Mixed HTAP | Rowstore plus nonclustered columnstore |

```sql
SELECT *
FROM dbo.FactSales
OPTION (MAXDOP 4);
```

## Isolation Levels and Concurrency

| Isolation level | Prevents dirty reads | Prevents non-repeatable reads | Prevents phantom reads | Notes |
|---|---|---|---|---|
| Read Uncommitted | No | No | No | Fast, least safe |
| Read Committed | Yes | No | No | Default |
| Repeatable Read | Yes | Yes | No | Locks rows longer |
| Serializable | Yes | Yes | Yes | Most restrictive |
| Snapshot | Yes | Yes | Versioned reads | Reduces blocking |

```sql
ALTER DATABASE CurrentDB SET READ_COMMITTED_SNAPSHOT ON;
```

**Exam tip:** Reader/writer blocking problem often points to RCSI or Snapshot isolation.

## Execution Plan Operators

| Operator | Interpretation | Common fix |
|---|---|---|
| Index Seek | Efficient targeted access | Usually good |
| Index Scan | Reads many index rows | May be okay for large returns |
| Table Scan | Reads whole table | Add selective index if appropriate |
| Key Lookup | Needs extra columns | Add `INCLUDE` columns |
| Sort | Expensive sort | Index aligned with order |
| Hash Match | Large joins/aggregates | Check join/index/cardinality |

## DMVs

```sql
-- Active requests and waits
SELECT session_id, status, blocking_session_id, wait_type, wait_time, command
FROM sys.dm_exec_requests;

-- Top CPU queries
SELECT TOP 20
    total_worker_time,
    execution_count,
    total_elapsed_time
FROM sys.dm_exec_query_stats
ORDER BY total_worker_time DESC;

-- Index usage
SELECT *
FROM sys.dm_db_index_usage_stats;
```

## Query Store and Plan Forcing

**Scenario:** Query became slow after deployment or statistics/plan change. Use Query Store to compare historical plans and force a known good plan.

```sql
ALTER DATABASE CurrentDB SET QUERY_STORE = ON;

EXEC sp_query_store_force_plan
    @query_id = 101,
    @plan_id = 12;
```

Undo force:

```sql
EXEC sp_query_store_unforce_plan
    @query_id = 101,
    @plan_id = 12;
```

**Workflow:**

```text
Query slowed down
  -> Open Query Store
  -> Compare runtime stats and plans
  -> Identify previous good plan
  -> Force plan
  -> Monitor
```

## Query Performance Insight

| Tool | Best for |
|---|---|
| Execution plan | Single-query operator analysis |
| DMVs | Current activity and waits |
| Query Store | Historical plan/runtime regression |
| Query Performance Insight | Azure portal visual view of top resource-consuming queries |
| Azure Monitor | Platform metrics, alerts, logs |

## Blocking Workflow

```text
Session waiting
  -> Check blocking_session_id in sys.dm_exec_requests
  -> Identify blocker SQL text and transaction
  -> Review indexes and isolation level
  -> Shorten transaction or use row versioning
```

## Deadlock Troubleshooting Workflow

```text
Deadlock graph captured
  -> Identify victim
  -> Identify resources and lock modes
  -> Identify inconsistent object access order
  -> Add or tune indexes to reduce lock footprint
  -> Keep transactions short
  -> Add retry logic in application
```

**Exam tip:** Blocking is one-way waiting. Deadlock is circular waiting and SQL Server chooses a victim.

## Parameter Sniffing

```sql
CREATE PROCEDURE dbo.usp_GetOrders
    @CustomerID INT
AS
BEGIN
    SELECT *
    FROM dbo.Orders
    WHERE CustomerID = @CustomerID
    OPTION (RECOMPILE);
END;
```

| Symptom | Likely issue | Possible fix |
|---|---|---|
| Same proc fast for one parameter, slow for another | Parameter sniffing | `OPTION (RECOMPILE)`, `OPTIMIZE FOR`, review indexes/statistics |
| Table scan with selective predicate | Missing index/statistics | Add index/update stats |
| Slow after plan change | Regression | Query Store force previous good plan |

---

# 7. CI/CD with SQL Database Projects

## SQL Database Project Structure

```text
DatabaseProject/
  Tables/
  Views/
  Stored Procedures/
  Functions/
  Security/
  Post-Deployment/
  Database.sqlproj
```

**Benefits:** version control, repeatable builds, DACPAC deployment, schema drift detection, code review.

## SDK-Style SQL Project

Modern SQL project format for simplified builds and CI/CD integration.

## Testing Strategy

| Test | Purpose |
|---|---|
| Unit test | Individual stored procedure/function behavior |
| Integration test | End-to-end database workflow |
| Build validation | Project compiles to DACPAC |
| Deployment validation | DACPAC deploys to isolated test database |

## Reference Data / Static Data

```sql
MERGE INTO dbo.OrderStatus AS Target
USING
(
    VALUES (1, 'Pending'), (2, 'Completed'), (3, 'Cancelled')
) AS Source(StatusID, StatusName)
ON Target.StatusID = Source.StatusID
WHEN MATCHED THEN
    UPDATE SET Target.StatusName = Source.StatusName
WHEN NOT MATCHED THEN
    INSERT(StatusID, StatusName)
    VALUES(Source.StatusID, Source.StatusName);
```

## SqlPackage Commands

```bash
SqlPackage /Action:Build /SourceFile:Database.sqlproj

SqlPackage /Action:DeployReport \
  /SourceFile:bin/Output.dacpac \
  /TargetConnectionString:"..." \
  /OutputPath:drift-report.xml

SqlPackage /Action:Publish \
  /SourceFile:bin/Output.dacpac \
  /TargetConnectionString:"..."
```

## Deployment Controls

- Branch policies
- Pull request approvals
- Build validation
- Manual approvals for production
- Code owners
- Secrets from Key Vault or secure variables
- Managed Identity/federated identity for deployment agents when possible

---

# 8. Integrate SQL Solutions with Azure Services

## Azure Monitor, Application Insights, and Log Analytics

```text
Azure SQL / App / DAB
  -> Diagnostic settings
  -> Log Analytics Workspace
  -> KQL queries, alerts, dashboards
```

| Requirement | Tool |
|---|---|
| Application traces and dependency calls | Application Insights |
| Query logs and diagnostics | Log Analytics |
| Metrics and alerts | Azure Monitor |
| Stream audit events | Event Hubs |

Example KQL pattern:

```kusto
AzureDiagnostics
| where ResourceProvider == "MICROSOFT.SQL"
| summarize Count = count() by Category, bin(TimeGenerated, 1h)
```

## Data API Builder - DAB

DAB exposes SQL database objects as REST and GraphQL endpoints without custom API code.

### DAB CLI Commands

```bash
dab init --database-type mssql --connection-string "@env('SQL_CONN_STR')"
dab add Customer --source dbo.Customers --permissions "authenticated:read"
dab add Order --source dbo.Orders --permissions "authenticated:read,create,update"
dab start
```

### DAB Configuration Example

```json
{
  "$schema": "https://github.com/Azure/data-api-builder/releases/download/v0.10.0/dab.draft-01.schema.json",
  "data-source": {
    "database-type": "mssql",
    "connection-string": "@env('SQL_CONN_STR')"
  },
  "runtime": {
    "rest": { "enabled": true, "path": "/api" },
    "graphql": { "enabled": true, "path": "/graphql" }
  },
  "entities": {
    "Customer": {
      "source": "dbo.Customers",
      "permissions": [
        { "role": "authenticated", "actions": ["read"] }
      ],
      "mappings": {
        "CustomerID": "id",
        "FullName": "name"
      }
    },
    "Order": {
      "source": "dbo.Orders",
      "permissions": [
        { "role": "authenticated", "actions": ["read", "create"] }
      ]
    }
  }
}
```

### REST Samples

```text
GET /api/Customer
GET /api/Customer/id/10
GET /api/Customer?$filter=City eq 'London'
GET /api/Customer?$top=10&$skip=20
```

### GraphQL Samples

```graphql
{
  customers {
    items {
      id
      name
    }
  }
}
```

GraphQL relationship example:

```graphql
{
  customers {
    items {
      id
      name
      orders {
        items {
          orderId
          amount
        }
      }
    }
  }
}
```

### DAB Exam Scenarios

| Requirement | Answer |
|---|---|
| Expose table as REST quickly | DAB entity with REST enabled |
| Expose related data in GraphQL | DAB GraphQL relationships |
| Restrict who can read or mutate | Entity permissions |
| Avoid huge result sets | Pagination |
| Improve repeated read latency | Data caching |
| Expose stored procedure | Configure procedure source/entity |

## Change Handling

| Feature | Captures | Best use |
|---|---|---|
| Change Tracking | Primary keys / changed rows | Lightweight sync |
| CDC | Full insert/update/delete details | ETL, audit-like history |
| CES | Streaming change events | Event-driven pipelines |
| Azure Functions SQL trigger | Runs code on row changes | Embedding updates |
| Logic Apps | Low-code workflow | Business process integration |

```text
Change Tracking = What changed
CDC = What changed plus details
CES = Streaming changes
```

---

# Domain 3 - Implement AI Capabilities in Database Solutions

# 9. Models and Embeddings

## Model Evaluation

| Requirement | Model choice |
|---|---|
| Lowest latency/cost | Smaller model |
| Complex reasoning | Larger model |
| Images/documents/audio | Multimodal model |
| Multiple languages | Multilingual model |
| Automation/API response | Structured output / JSON mode |

## External Models

```text
SQL workflow
  -> External model / REST endpoint
  -> Azure OpenAI or other model provider
  -> Result returned to database/application
```

## Embedding Column Selection

| Column/data | Embed? | Reason |
|---|---:|---|
| Product description | Yes | Contains semantic meaning |
| Knowledge article body | Yes | Searchable natural language |
| FAQ answer | Yes | User questions map to answers |
| Support ticket text | Yes | Semantic classification/search |
| Customer ID | No | Identifier, no meaning |
| Invoice number | No | Identifier, no meaning |
| Status code | No | Categorical, use filters |
| Foreign key | No | Relationship, not semantic text |

## Chunking

| Strategy | Use when | Trade-off |
|---|---|---|
| Fixed-size | Quick/simple implementation | Can split meaning |
| Sentence-based | Need cleaner semantic boundaries | More parsing |
| Paragraph-based | Docs have clear paragraphs | Uneven chunk sizes |
| Semantic chunking | Highest retrieval quality | More cost/complexity |

```text
Document
  -> Split into chunks
  -> Add metadata: DocumentID, Page, Section, SecurityLabel
  -> Generate embedding per chunk
  -> Store vector
```

## Embedding Maintenance

| Method | Latency | Impact | Best scenario |
|---|---|---|---|
| Trigger | Immediate | Adds write latency | Small critical tables |
| Change Tracking | Low/medium | Lightweight | Poll changed keys |
| CDC | Medium | More storage | Detailed change processing |
| CES | Near real time | Event pipeline | Streaming AI updates |
| Azure Function SQL trigger | Near real time | Decoupled | Serverless embedding regeneration |
| Logic Apps | Workflow-oriented | Low-code | Business process integration |
| Foundry | Enterprise AI lifecycle | Platform setup | Model/app orchestration |

## SQL AI Functions - Conceptual Syntax

> Exact syntax can vary by platform/version. DP-800 usually tests what the function is for and where it fits in the architecture.

### AI_GENERATE_CHUNKS

```sql
SELECT *
FROM AI_GENERATE_CHUNKS
(
    source_text => @DocumentText,
    chunk_type => 'paragraph',
    chunk_size => 800,
    overlap => 100
);
```

**Purpose:** Split large text into model-friendly chunks before embedding.

### AI_GENERATE_EMBEDDINGS

```sql
UPDATE dbo.KnowledgeChunk
SET Embedding = AI_GENERATE_EMBEDDINGS(ChunkText USING MODEL = 'text-embedding-model')
WHERE Embedding IS NULL;
```

**Purpose:** Convert text into a vector representation.

### VECTOR_SEARCH

```sql
SELECT TOP 10 *
FROM VECTOR_SEARCH
(
    TABLE = dbo.KnowledgeChunk,
    COLUMN = Embedding,
    QUERY_VECTOR = @QueryEmbedding,
    METRIC = 'cosine',
    TOP_N = 10
);
```

**Purpose:** Retrieve nearest vectors using vector-aware search capability where supported.

---

# 10. Intelligent Search

## Full-Text Search - Complete Exam Samples

### Create Full-Text Catalog and Index

```sql
CREATE FULLTEXT CATALOG ProductFTCatalog;

CREATE FULLTEXT INDEX ON dbo.Product
(
    ProductName LANGUAGE 1033,
    Description LANGUAGE 1033
)
KEY INDEX PK_Product
ON ProductFTCatalog;
```

### CONTAINS

```sql
SELECT ProductID, ProductName
FROM dbo.Product
WHERE CONTAINS(Description, '"running shoes"');
```

**Use when:** exact word/phrase/prefix/proximity logic matters.

### FREETEXT

```sql
SELECT ProductID, ProductName
FROM dbo.Product
WHERE FREETEXT(Description, 'comfortable footwear for jogging');
```

**Use when:** natural language meaning within full-text engine is desired.

| Function | Behavior |
|---|---|
| `CONTAINS` | Precise keyword, phrase, prefix, Boolean-style conditions |
| `FREETEXT` | Looser natural language matching |

## Vector Data Type and Search

```sql
CREATE TABLE dbo.ProductCatalog
(
    ProductID INT PRIMARY KEY,
    ProductName NVARCHAR(200) NOT NULL,
    Description NVARCHAR(MAX) NOT NULL,
    ProductEmbedding VECTOR(1536) NULL
);
```

```sql
DECLARE @QueryEmbedding VECTOR(1536) = N'[0.012, -0.045, 0.231]';

SELECT TOP 5
    ProductID,
    ProductName,
    VECTOR_DISTANCE('cosine', @QueryEmbedding, ProductEmbedding) AS Distance
FROM dbo.ProductCatalog
ORDER BY Distance ASC;
```

### Vector Functions

| Function | Purpose |
|---|---|
| `VECTOR_DISTANCE` | Calculate distance/similarity metric |
| `VECTOR_NORMALIZE` | Normalize vector length |
| `VECTORPROPERTY` | Inspect vector metadata such as dimension count |
| `VECTOR_SEARCH` | Search nearest vectors where supported |

```sql
SELECT VECTORPROPERTY(ProductEmbedding, 'dimensions') AS Dimensions
FROM dbo.ProductCatalog;
```

## Vector Metrics

| Metric | Best for | Exam note |
|---|---|---|
| Cosine | Text embeddings | Most common for semantic text |
| Euclidean / L2 | Geometric distance | Sensitive to magnitude |
| Dot product | Normalized vectors | Fast in many vector systems |

## ANN vs ENN and Vector Index Selection

| Dataset / Requirement | Recommendation |
|---|---|
| Small dataset, maximum accuracy | ENN |
| Millions of vectors, fast retrieval | ANN |
| High recall and low latency | HNSW |
| Very large partitioned vector sets | IVF or platform-specific scalable ANN |
| Disk-friendly large vector search | DiskANN where available |

**Memory:** ANN = Approximate and Accelerated. ENN = Exact.

## Hybrid Search and RRF

```sql
WITH FullTextResults AS
(
    SELECT
        ProductID,
        ROW_NUMBER() OVER (ORDER BY SearchScore DESC) AS RankFTS
    FROM dbo.ProductFTSResults
),
VectorResults AS
(
    SELECT
        ProductID,
        ROW_NUMBER() OVER (ORDER BY VectorDistance ASC) AS RankVector
    FROM dbo.ProductVectorResults
)
SELECT
    COALESCE(f.ProductID, v.ProductID) AS ProductID,
    ISNULL(1.0 / (60 + f.RankFTS), 0.0) +
    ISNULL(1.0 / (60 + v.RankVector), 0.0) AS RRFScore
FROM FullTextResults AS f
FULL OUTER JOIN VectorResults AS v
    ON f.ProductID = v.ProductID
ORDER BY RRFScore DESC;
```

| Requirement | Search choice |
|---|---|
| Exact code/name/keyword | Full-text search |
| Meaning/synonym/concept | Vector search |
| Best production relevance | Hybrid search |
| Combine different rankings | RRF |

## Search Evaluation Metrics

| Metric | Meaning |
|---|---|
| Precision | Of returned results, how many are relevant |
| Recall | Of all relevant results, how many were found |
| Recall@K | Relevant results found in top K |
| MRR | Mean reciprocal rank of first relevant result |
| NDCG | Ranking quality with graded relevance |
| Latency | Response time |
| Throughput | Queries per second |

**Exam tip:** Hybrid search improves relevance but may increase latency and complexity. ANN improves latency but may slightly reduce exact recall.

---

# 11. Retrieval-Augmented Generation - RAG

## RAG Architecture

```text
User question
  -> Generate query embedding
  -> Retrieve top chunks from SQL vector search
  -> Optional full-text search
  -> RRF reranking
  -> Apply security filters/RLS
  -> Convert rows to JSON
  -> Build grounded prompt
  -> Call model endpoint
  -> Parse response
  -> Return answer
```

## Database Scoped Credential for External REST Calls

**Exam-important:** Before calling a secured model endpoint through `sp_invoke_external_rest_endpoint`, you normally need a secure credential configuration.

```sql
CREATE DATABASE SCOPED CREDENTIAL [https://my-openai-resource.openai.azure.com]
WITH IDENTITY = 'Managed Identity';
```

Alternative conceptual pattern with secret:

```sql
CREATE DATABASE SCOPED CREDENTIAL MyExternalApiCredential
WITH IDENTITY = 'HTTPEndpointHeaders',
SECRET = '{"api-key":"<stored-securely-not-in-code>"}';
```

**Exam preference:** Managed Identity is usually preferred over static keys/secrets when supported.

## Convert SQL Data to JSON

```sql
DECLARE @ContextJson NVARCHAR(MAX) =
(
    SELECT TOP 5
        ChunkID,
        DocumentTitle,
        ChunkText
    FROM dbo.KnowledgeChunk
    WHERE SecurityLabel <= SESSION_CONTEXT(N'UserSecurityLevel')
    ORDER BY VECTOR_DISTANCE('cosine', @QueryEmbedding, Embedding) ASC
    FOR JSON PATH
);
```

## Call Model Endpoint

```sql
DECLARE @RequestBody NVARCHAR(MAX) = JSON_OBJECT
(
    'messages': JSON_ARRAY
    (
        JSON_OBJECT
        (
            'role':'system',
            'content':'Answer only from the provided context. If not in context, say you do not know.'
        ),
        JSON_OBJECT
        (
            'role':'user',
            'content':CONCAT('Context: ', @ContextJson, ' Question: ', @UserQuestion)
        )
    ),
    'temperature':0.2
);

DECLARE @Response NVARCHAR(MAX);

EXEC sp_invoke_external_rest_endpoint
    @url = N'https://my-openai-resource.openai.azure.com/openai/deployments/my-chat-model/chat/completions?api-version=2024-02-01',
    @method = N'POST',
    @payload = @RequestBody,
    @credential = [https://my-openai-resource.openai.azure.com],
    @response = @Response OUTPUT;

SELECT JSON_VALUE(@Response, '$.result.choices[0].message.content') AS Answer;
```

## RAG Security Checklist

- Apply RLS before retrieving context.
- Use least privilege for SQL and model endpoint access.
- Do not send unnecessary PII to the model.
- Prefer Managed Identity and private networking.
- Log prompts/responses only according to policy.
- Ground prompt with instruction to answer only from context.
- Include citations/source IDs in returned context where possible.

---

# Last-Mile Exam Decision Trees

## History vs Tamper-Proof

```text
Need historical row versions?
  -> Temporal table

Need cryptographic proof against tampering?
  -> Ledger table

Need insert-only immutable log?
  -> Append-only ledger
```

## Search Selection

```text
Need exact keyword or phrase?
  -> Full-text search

Need meaning/synonym search?
  -> Vector search

Need best relevance with both keyword and meaning?
  -> Hybrid search + RRF
```

## Encryption and Data Protection

```text
Need to hide display only?
  -> Dynamic Data Masking

Need to protect data from DBAs/admins?
  -> Always Encrypted

Need T-SQL encryption inside database?
  -> Column-level encryption

Need secure Azure service access without passwords?
  -> Managed Identity
```

## Change Processing

```text
Need lightweight changed row keys?
  -> Change Tracking

Need detailed row changes?
  -> CDC

Need streaming event pipeline?
  -> CES

Need serverless response to SQL changes?
  -> Azure Functions SQL trigger
```

## Performance Troubleshooting

```text
Single slow query?
  -> Execution plan

Current blocking/waits?
  -> DMVs

Regression over time?
  -> Query Store

Azure portal top consumers?
  -> Query Performance Insight

Platform metrics/alerts/logs?
  -> Azure Monitor + Log Analytics
```

## Deployment Governance

```text
Need schema as code?
  -> SQL Database Project

Need deployable artifact?
  -> DACPAC

Need detect manual changes?
  -> Schema drift report

Need protect production?
  -> Branch policies, approvals, code owners
```

---

# Scenario Cheat Sheet

| Requirement | Best answer |
|---|---|
| Date-range queries on large table | Clustered/nonclustered index on date, possibly partitioning |
| Analytics over millions of rows | Columnstore index |
| Avoid Key Lookup | INCLUDE columns |
| JSON property filtering | Computed column + index |
| Query external lake data | External table |
| Historical point-in-time rows | Temporal table |
| Tamper-evident records | Ledger table |
| Many-to-many path traversal | Graph tables |
| Hide sensitive values in results | Dynamic Data Masking |
| Protect data from DBA | Always Encrypted |
| Tenant-level row filtering | Row-Level Security |
| Passwordless Azure access | Managed Identity |
| Query regression after deployment | Query Store plan comparison/force plan |
| Reader/writer blocking | Snapshot isolation/RCSI |
| Circular waiting | Deadlock troubleshooting |
| API without custom code | Data API Builder |
| GraphQL over SQL | DAB GraphQL endpoint |
| Lightweight sync changes | Change Tracking |
| Detailed row history for ETL | CDC |
| Streaming data changes | CES |
| Generate embeddings after row change | Azure Functions SQL trigger |
| Search exact wording | Full-text search |
| Search by meaning | Vector search |
| Best search relevance | Hybrid search + RRF |
| Large vector dataset | ANN index such as HNSW/IVF |
| Small exact vector comparison | ENN |
| Internal knowledge assistant | RAG |
| Send SQL rows to model | `FOR JSON PATH` |
| Call model from SQL | `sp_invoke_external_rest_endpoint` + scoped credential |

---

# Mini Practice Questions

## Domain 1

1. A product catalog stores flexible attributes that vary by category. You need to search by one JSON property efficiently. What should you implement?  
   **Answer:** Store JSON in `NVARCHAR(MAX)`, expose the property through a computed column using `JSON_VALUE`, and index the computed column.

2. A financial application must prove records were not tampered with. What table type should you choose?  
   **Answer:** Ledger table.

3. A reporting table has 500 million rows and queries mostly perform aggregations. What index type is most appropriate?  
   **Answer:** Clustered columnstore index.

4. You need to find customers whose names are similar to `Jon Smyth`. What feature should you use?  
   **Answer:** Fuzzy matching functions such as `EDIT_DISTANCE_SIMILARITY` or `JARO_WINKLER_DISTANCE`.

5. A query needs previous month sales on the same row as current month sales. What function should you use?  
   **Answer:** `LAG()` window function.

## Domain 2

1. Support staff should see masked credit card values but DBAs can retain access. What feature should you use?  
   **Answer:** Dynamic Data Masking.

2. An Azure Function needs SQL access without passwords. What should you use?  
   **Answer:** Managed Identity and Entra authentication.

3. A stored procedure became slow only for certain parameter values. What is the likely issue?  
   **Answer:** Parameter sniffing.

4. A query performed well yesterday but is slow today after plan change. What should you use?  
   **Answer:** Query Store to compare plans and force the previous good plan if appropriate.

5. You need REST and GraphQL endpoints over SQL tables without custom API code. What should you use?  
   **Answer:** Data API Builder.

## Domain 3

1. Which columns should be embedded: product description, invoice number, support ticket text, status code?  
   **Answer:** Product description and support ticket text.

2. A semantic search over millions of vectors must be low latency. ANN or ENN?  
   **Answer:** ANN, commonly with HNSW/IVF depending on platform.

3. You need exact keyword plus semantic meaning. What search pattern should you use?  
   **Answer:** Hybrid search with RRF.

4. SQL rows must be sent to a language model as context. What T-SQL format is commonly used?  
   **Answer:** `FOR JSON PATH`.

5. What is required to call a secured model endpoint through SQL REST integration?  
   **Answer:** `sp_invoke_external_rest_endpoint` with a secure database scoped credential/managed identity where supported.

---

# Final High-Probability Topics to Memorize

- Clustered index: one per table.
- Nonclustered index: lookup/filter support.
- INCLUDE columns: reduce Key Lookup.
- Columnstore: analytics.
- Temporal: history.
- Ledger: tamper evidence.
- Graph: `NODE`, `EDGE`, `MATCH`.
- JSON: `JSON_VALUE`, `JSON_QUERY`, `OPENJSON`, `JSON_CONTAINS`.
- Regex: validation/extraction/splitting.
- Fuzzy matching: approximate names/text.
- RLS: predicate function + security policy.
- Always Encrypted: client-side protection.
- DDM: display masking, not encryption.
- Managed Identity: passwordless.
- Query Store: historical regression and plan forcing.
- Query Performance Insight: Azure portal top query view.
- Deadlock: circular wait, victim selected.
- SQL Database Project: database schema as code.
- DAB: REST/GraphQL without custom code.
- Change Tracking: lightweight changed keys.
- CDC: detailed row changes.
- CES: streaming changes.
- Embedding: numeric meaning representation.
- Chunking: split before embedding.
- Vector dimensions must match embedding model output.
- Cosine distance: common for text embeddings.
- ANN: scalable and fast.
- ENN: accurate but slower.
- Hybrid search + RRF: strongest search answer.
- RAG: retrieve context, then generate.
- `sp_invoke_external_rest_endpoint`: call model endpoint.
- Database scoped credential: secure external endpoint access.

---

# 7-Day Last-Moment Revision Plan

| Day | Focus |
|---:|---|
| 1 | Tables, data types, indexes, constraints, partitioning |
| 2 | Specialized tables, JSON, graph, programmability, advanced T-SQL |
| 3 | Security: encryption, DDM, RLS, permissions, auditing, endpoint security |
| 4 | Performance: execution plans, DMVs, Query Store, blocking, deadlocks, parameter sniffing |
| 5 | CI/CD, SQL Database Projects, DAB, Azure Monitor, change handling |
| 6 | Models, embeddings, chunking, vector type/functions/indexes, full-text/vector/hybrid search |
| 7 | RAG, database scoped credentials, decision trees, practice questions, weak areas |

---

## Source and Validation Notes

This Markdown file was regenerated from the two provided user files and expanded against the DP-800 exam skill areas. It is designed as a practical, exam-focused study material and not a replacement for hands-on practice.


---

# Expanded Scenario Cheat Sheet - Full Version

## Database Object Selection

| Requirement | Best Answer | Why |
|---|---|---|
| Need a unique row identifier | Primary Key | Enforces uniqueness and non-nullability |
| Need to enforce parent-child relationships | Foreign Key | Enforces referential integrity |
| Need to enforce business rules such as salary > 0 | CHECK constraint | Validates data at write time |
| Need a value when insert omits a column | DEFAULT constraint | Automatically supplies value |
| Need unique values on non-primary column | UNIQUE constraint | Prevents duplicates |
| Need shared number generator across multiple tables | SEQUENCE | Independent database object |
| Need identity-like value tied to one table | IDENTITY | Table-specific auto-numbering |
| Need flexible attributes per row | JSON column | Supports semi-structured data |
| Need fast filtering on JSON property | Computed column + index | Extracts JSON path and indexes it |
| Need to query external data lake files | External table | Query in place without loading |
| Need automatic row history | Temporal table | Maintains current and history tables |
| Need tamper-evident history | Ledger table | Cryptographic verification |
| Need insert-only audit log | Append-only ledger | Blocks update/delete |
| Need ultra-low latency OLTP | Memory-optimized table | In-Memory OLTP design |
| Need many-to-many relationship traversal | Graph tables | NODE, EDGE, MATCH |
| Need AI embedding storage | VECTOR(n) | Stores vectors for semantic search |

## Data Type Selection

| Requirement | Best Answer | Exam Note |
|---|---|---|
| Unicode or multilingual text | `NVARCHAR` | 2 bytes per character in common SQL Server storage model |
| Non-Unicode text | `VARCHAR` | Smaller when Unicode not needed |
| Large JSON/text | `NVARCHAR(MAX)` | Up to 2 GB |
| Exact financial value | `DECIMAL(p,s)` | Avoid `FLOAT` for money |
| Approximate scientific value | `FLOAT` / `REAL` | Approximate, not exact |
| Boolean flag | `BIT` | 0, 1, or NULL |
| Standard integer key | `INT` | Common default integer type |
| Very large counter | `BIGINT` | Large fact tables or large sequences |
| Date and time | `DATETIME2` | Preferred over legacy `DATETIME` |
| Time zone offset | `DATETIMEOFFSET` | Stores offset awareness |
| Distributed globally unique ID | `UNIQUEIDENTIFIER` | Use `NEWID()` or `NEWSEQUENTIALID()` |
| File, image, encrypted binary payload | `VARBINARY(MAX)` | Binary large object |
| XML document | `XML` | XML-specific storage/querying |
| Embedding vector | `VECTOR(n)` | n must match model dimensions |

## Index Selection

| Requirement | Best Answer | Why |
|---|---|---|
| Range query by date | Clustered or nonclustered index on date | Supports ordered range access |
| Frequent single-row lookup by email | Nonclustered index | Fast seek |
| Query has Key Lookup | Add INCLUDE columns | Covers missing selected columns |
| Query filters by multiple columns | Composite index | Supports combined predicates |
| Query filters only active/open rows | Filtered index | Smaller targeted index |
| Large analytics table | Clustered columnstore index | Compression and batch analytics |
| OLTP table needing analytics | Nonclustered columnstore index | HTAP pattern |
| JSON property search | Computed column index | Indexes extracted JSON value |
| Full-text document search | Full-text index | Enables CONTAINS/FREETEXT |
| Semantic search | Vector index | Accelerates similarity search |
| Small vector table requiring exact result | ENN | Exact but slower |
| Millions of vectors requiring low latency | ANN | Approximate but scalable |

## Security Selection

| Requirement | Best Answer | Why |
|---|---|---|
| Hide sensitive value in result set | Dynamic Data Masking | Display masking only |
| Encrypt data so DBA cannot see plaintext | Always Encrypted | Client-side encryption |
| Need equality search over encrypted value | Deterministic Always Encrypted | Same plaintext gives same ciphertext |
| Need strongest encrypted confidentiality | Randomized Always Encrypted | Same plaintext gives different ciphertext |
| Need T-SQL encryption/decryption functions | Column-level encryption | Uses keys and functions in DB |
| Users see only their tenant/region rows | Row-Level Security | Predicate function + policy |
| Restrict table/procedure access | GRANT/DENY/REVOKE | Object-level permission control |
| Azure service accesses SQL without secret | Managed Identity | Passwordless access |
| Store secrets securely for pipelines | Azure Key Vault | Secret management |
| Track security and data access activity | Auditing | Compliance and investigation |
| Secure model endpoint | Managed Identity/private endpoint/scoped credential | Least privilege and no static secret |
| Secure DAB GraphQL exposure | Entity permissions | Limits reads/mutations |
| Secure MCP access to SQL | Least privilege + scoped MCP tools | Limits AI agent access |

## Performance Troubleshooting Selection

| Symptom | Think | Best First Tool / Fix |
|---|---|---|
| One query is slow | Bad plan/index/cardinality | Execution plan |
| Query was fast before, slow now | Plan regression | Query Store |
| Stored procedure fast for one parameter, slow for another | Parameter sniffing | Query Store, `OPTION(RECOMPILE)`, `OPTIMIZE FOR` |
| Sessions waiting on one blocking session | Blocking | `sys.dm_exec_requests`, shorten transaction, RCSI |
| Two sessions wait on each other | Deadlock | Deadlock graph, consistent lock order |
| Large scans with selective predicate | Missing index | Add selective index |
| Key Lookup repeated many times | Non-covering index | Add `INCLUDE` columns |
| High sort cost | Missing ordered index | Create index matching ORDER BY |
| Reader/writer blocking | Locking isolation conflict | Snapshot/RCSI |
| Azure portal shows top CPU query | Expensive query | Query Performance Insight |
| Need platform alerts/log queries | Monitoring | Azure Monitor + Log Analytics |

## CI/CD and Governance Selection

| Requirement | Best Answer | Why |
|---|---|---|
| Store schema as code | SQL Database Project | Declarative source-controlled database model |
| Build deployable database artifact | DACPAC | Standard SQL deployment artifact |
| Validate schema compiles | Build validation | CI quality gate |
| Test stored procedure behavior | Unit tests | Object-level testing |
| Test API/procedure/database flow | Integration tests | End-to-end validation |
| Manage lookup/status data | Post-deployment MERGE | Controlled static data |
| Detect manual production changes | Schema drift report | Identifies out-of-band changes |
| Protect production branch | Branch policy | Prevents unreviewed changes |
| Require specific review owners | CODEOWNERS | Governance control |
| Deploy after approval | Pipeline approval gate | Production control |
| Keep secrets out of Git | Key Vault / secure variables | Secure deployment |
| Resolve conflicting DB changes | Pull request and build validation | Review and merge safely |

## DAB and Azure Integration Selection

| Requirement | Best Answer | Why |
|---|---|---|
| Expose SQL tables quickly as REST | Data API Builder | No custom API code |
| Expose SQL as GraphQL | DAB GraphQL endpoint | Built-in GraphQL runtime |
| Expose view through API | DAB entity over view | Maps DB object to endpoint |
| Expose stored procedure | DAB procedure entity | API over procedure |
| Limit API actions | DAB permissions | Controls read/create/update/delete/execute |
| Prevent huge responses | Pagination | `$top`, `$skip`, page settings |
| Search/filter API data | DAB filtering/searching | Query endpoint efficiently |
| Reduce repeated DB calls | DAB caching | Improves latency/throughput |
| Monitor app/API telemetry | Application Insights | Request/dependency telemetry |
| Query diagnostic logs | Log Analytics | KQL analysis |
| Alert on metrics/logs | Azure Monitor | Operational monitoring |
| Stream changes | CES | Event-driven integration |
| Lightweight sync | Change Tracking | Changed row keys |
| Detailed changes | CDC | Insert/update/delete history |
| Serverless embedding regeneration | Azure Functions SQL trigger | Reacts to SQL changes |
| Low-code workflow | Logic Apps | Business automation |

## AI, Embeddings, Search, and RAG Selection

| Requirement | Best Answer | Why |
|---|---|---|
| Search exact keyword/phrase | Full-text search | Lexical search |
| Search meaning/synonyms | Vector search | Semantic similarity |
| Best search relevance | Hybrid search | Combines lexical + semantic |
| Merge full-text/vector rankings | RRF | Combines rank lists |
| Store embeddings | `VECTOR(n)` | Native vector storage |
| Fast vector search at scale | ANN index | Low latency for many vectors |
| Exact vector result on small data | ENN | Exhaustive accurate search |
| Text embedding metric | Cosine distance | Common for semantic text |
| Normalize vectors | `VECTOR_NORMALIZE` | Standardize vector magnitude |
| Inspect vector dimensions | `VECTORPROPERTY` | Metadata validation |
| Retrieve nearest vectors | `VECTOR_SEARCH` | Semantic retrieval where supported |
| Split document before embedding | Chunking | Improves retrieval quality |
| Generate vector from text | Embedding model / `AI_GENERATE_EMBEDDINGS` | Meaning representation |
| Ground LLM with enterprise data | RAG | Reduces hallucination |
| Send SQL context to model | `FOR JSON PATH` | Structure data for prompt |
| Call model endpoint from SQL | `sp_invoke_external_rest_endpoint` | External model invocation |
| Secure external call | Database scoped credential / Managed Identity | Secure authentication |

---

# Expanded Decision Trees

## Data Protection Decision Tree

```text
Data protection requirement
  |
  |-- Only hide value in query result?
  |     -> Dynamic Data Masking
  |
  |-- Protect plaintext from DBA/admin?
  |     -> Always Encrypted
  |        |-- Need equality search?
  |              -> Deterministic encryption
  |        |-- Need strongest confidentiality?
  |              -> Randomized encryption
  |
  |-- Need encryption/decryption inside T-SQL?
  |     -> Column-level encryption
  |
  |-- Need row filtering per user/tenant?
  |     -> Row-Level Security
  |
  |-- Need passwordless service access?
        -> Managed Identity
```

## Table Type Decision Tree

```text
Table requirement
  |
  |-- Track every historical row version?
  |     -> Temporal table
  |
  |-- Prove data has not been tampered with?
  |     -> Ledger table
  |
  |-- Inserts only, no update/delete allowed?
  |     -> Append-only ledger
  |
  |-- Ultra-low latency OLTP?
  |     -> Memory-optimized table
  |
  |-- Query external lake/blob/lakehouse data?
  |     -> External table
  |
  |-- Model relationships as paths?
        -> Graph table
```

## Search Decision Tree

```text
Search requirement
  |
  |-- Exact keyword, phrase, prefix, Boolean text?
  |     -> Full-text search with CONTAINS
  |
  |-- Natural language full-text matching?
  |     -> FREETEXT
  |
  |-- Semantic meaning/synonyms?
  |     -> Vector search
  |
  |-- Need both exact match and semantic meaning?
  |     -> Hybrid search
  |
  |-- Need to combine ranks from both methods?
        -> Reciprocal Rank Fusion
```

## Vector Index Decision Tree

```text
Vector search workload
  |
  |-- Small dataset or strict accuracy required?
  |     -> ENN
  |
  |-- Large dataset and low latency required?
  |     -> ANN
  |        |-- Need fast high-recall graph style index?
  |              -> HNSW
  |        |-- Need partition/scalable index pattern?
  |              -> IVF
  |        |-- Disk-optimized vector workload supported?
                -> DiskANN where available
```

## Change Processing Decision Tree

```text
Change handling requirement
  |
  |-- Need only to know which rows changed?
  |     -> Change Tracking
  |
  |-- Need detailed before/after or operation history?
  |     -> CDC
  |
  |-- Need streaming events to downstream systems?
  |     -> CES
  |
  |-- Need serverless action after SQL row changes?
  |     -> Azure Functions SQL trigger
  |
  |-- Need low-code workflow integration?
        -> Azure Logic Apps
```

## RAG Decision Tree

```text
Need AI answer from enterprise data?
  -> RAG
     |
     |-- Large documents?
     |     -> Chunk first
     |
     |-- Need semantic retrieval?
     |     -> Generate embeddings and use vector search
     |
     |-- Need exact terms also?
     |     -> Hybrid search
     |
     |-- Need combined ranking?
     |     -> RRF
     |
     |-- Need model prompt from SQL rows?
     |     -> FOR JSON PATH
     |
     |-- Need secure model call from SQL?
           -> sp_invoke_external_rest_endpoint + database scoped credential
```

---

# Syntax Pack - Last-Minute Copy/Paste Samples

## Full-Text Search

```sql
CREATE FULLTEXT CATALOG ProductFTCatalog;

CREATE FULLTEXT INDEX ON dbo.Product
(
    ProductName LANGUAGE 1033,
    Description LANGUAGE 1033
)
KEY INDEX PK_Product
ON ProductFTCatalog;

SELECT ProductID, ProductName
FROM dbo.Product
WHERE CONTAINS(Description, '"running shoes"');

SELECT ProductID, ProductName
FROM dbo.Product
WHERE FREETEXT(Description, 'comfortable footwear for jogging');
```

## JSON Property Indexing

```sql
CREATE TABLE dbo.Orders
(
    OrderID INT PRIMARY KEY,
    OrderJson NVARCHAR(MAX) NOT NULL,
    CustomerCity AS JSON_VALUE(OrderJson, '$.customer.city')
);

CREATE INDEX IX_Orders_CustomerCity
ON dbo.Orders(CustomerCity);
```

## JSON Functions

```sql
DECLARE @json NVARCHAR(MAX) = N'{"name":"Kashyap","skills":["SQL","AI"],"address":{"city":"London"}}';

SELECT JSON_VALUE(@json, '$.name') AS Name;
SELECT JSON_QUERY(@json, '$.skills') AS Skills;

SELECT *
FROM OPENJSON(@json, '$.skills');

SELECT JSON_OBJECT('name':'Kashyap', 'exam':'DP-800') AS JsonObject;
SELECT JSON_ARRAY('SQL', 'Azure SQL', 'Fabric') AS JsonArray;
```

## REGEXP Functions

```sql
SELECT *
FROM dbo.Users
WHERE REGEXP_LIKE(Email, '^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$');

SELECT REGEXP_REPLACE(PhoneNumber, '[^0-9]', '') AS DigitsOnly
FROM dbo.Customers;

SELECT REGEXP_SUBSTR('Order-12345-UK', '[0-9]+') AS OrderNumber;

SELECT REGEXP_INSTR('Order-12345-UK', '[0-9]+') AS MatchStart;

SELECT REGEXP_COUNT('SQL,Azure,Fabric,SQL', 'SQL') AS SqlCount;

SELECT *
FROM REGEXP_SPLIT_TO_TABLE('SQL,Azure,Fabric', ',');
```

## Correlated Queries

```sql
SELECT c.CustomerID, c.CustomerName
FROM dbo.Customers AS c
WHERE EXISTS
(
    SELECT 1
    FROM dbo.Orders AS o
    WHERE o.CustomerID = c.CustomerID
);

SELECT e.EmployeeID, e.DepartmentID, e.Salary
FROM dbo.Employee AS e
WHERE e.Salary >
(
    SELECT AVG(e2.Salary)
    FROM dbo.Employee AS e2
    WHERE e2.DepartmentID = e.DepartmentID
);
```

## Query Store Plan Forcing

```sql
ALTER DATABASE CurrentDB SET QUERY_STORE = ON;

EXEC sp_query_store_force_plan
    @query_id = 101,
    @plan_id = 12;

EXEC sp_query_store_unforce_plan
    @query_id = 101,
    @plan_id = 12;
```

## RLS with SESSION_CONTEXT

```sql
EXEC sp_set_session_context @key = N'TenantID', @value = 10;

CREATE FUNCTION Security.fn_TenantPredicate(@TenantID INT)
RETURNS TABLE
WITH SCHEMABINDING
AS
RETURN
    SELECT 1 AS fn_securityPredicate_result
    WHERE @TenantID = CAST(SESSION_CONTEXT(N'TenantID') AS INT);

CREATE SECURITY POLICY Security.TenantPolicy
ADD FILTER PREDICATE Security.fn_TenantPredicate(TenantID)
ON dbo.Orders
WITH (STATE = ON);
```

## DAB CLI and Config

```bash
dab init --database-type mssql --connection-string "@env('SQL_CONN_STR')"
dab add Customer --source dbo.Customers --permissions "authenticated:read"
dab add Order --source dbo.Orders --permissions "authenticated:read,create,update"
dab start
```

```json
{
  "data-source": {
    "database-type": "mssql",
    "connection-string": "@env('SQL_CONN_STR')"
  },
  "runtime": {
    "rest": { "enabled": true, "path": "/api" },
    "graphql": { "enabled": true, "path": "/graphql" }
  },
  "entities": {
    "Customer": {
      "source": "dbo.Customers",
      "permissions": [
        { "role": "authenticated", "actions": ["read"] }
      ]
    }
  }
}
```

## GraphQL Query Sample

```graphql
{
  customers {
    items {
      id
      name
      orders {
        items {
          orderId
          amount
        }
      }
    }
  }
}
```

## Vector Search

```sql
CREATE TABLE dbo.ProductCatalog
(
    ProductID INT PRIMARY KEY,
    ProductName NVARCHAR(200),
    Description NVARCHAR(MAX),
    ProductEmbedding VECTOR(1536)
);

DECLARE @QueryEmbedding VECTOR(1536) = N'[0.012, -0.045, 0.231]';

SELECT TOP 5
    ProductID,
    ProductName,
    VECTOR_DISTANCE('cosine', @QueryEmbedding, ProductEmbedding) AS Distance
FROM dbo.ProductCatalog
ORDER BY Distance ASC;
```

## RAG External Endpoint Credential and Call

```sql
CREATE DATABASE SCOPED CREDENTIAL [https://my-openai-resource.openai.azure.com]
WITH IDENTITY = 'Managed Identity';

DECLARE @ContextJson NVARCHAR(MAX) =
(
    SELECT TOP 5 ChunkID, ChunkText
    FROM dbo.KnowledgeChunk
    ORDER BY VECTOR_DISTANCE('cosine', @QueryEmbedding, Embedding) ASC
    FOR JSON PATH
);

DECLARE @RequestBody NVARCHAR(MAX) = JSON_OBJECT
(
    'messages': JSON_ARRAY
    (
        JSON_OBJECT('role':'system', 'content':'Answer only from provided context.'),
        JSON_OBJECT('role':'user', 'content':CONCAT('Context: ', @ContextJson, ' Question: ', @Question))
    ),
    'temperature':0.2
);

DECLARE @Response NVARCHAR(MAX);

EXEC sp_invoke_external_rest_endpoint
    @url = N'https://my-openai-resource.openai.azure.com/openai/deployments/my-chat-model/chat/completions?api-version=2024-02-01',
    @method = N'POST',
    @payload = @RequestBody,
    @credential = [https://my-openai-resource.openai.azure.com],
    @response = @Response OUTPUT;

SELECT JSON_VALUE(@Response, '$.result.choices[0].message.content') AS Answer;
```

---

# Expanded TOP 150 Must-Memorize DP-800 Facts

## Database Design and Data Types

1. DP-800 covers SQL Server, Azure SQL, and SQL databases in Microsoft Fabric.
2. The exam is scenario-based, not just syntax-based.
3. Use `NVARCHAR` for Unicode and multilingual text.
4. Use `VARCHAR` only when Unicode is not needed.
5. Use `NVARCHAR(MAX)` for large JSON and large Unicode text.
6. Use `VARBINARY(MAX)` for large binary payloads.
7. Use `DECIMAL` or `NUMERIC` for exact financial values.
8. Avoid `FLOAT` for exact money calculations.
9. Use `DATETIME2` instead of legacy `DATETIME` where possible.
10. Use `DATETIMEOFFSET` when time zone offset matters.
11. Use `UNIQUEIDENTIFIER` for distributed unique IDs.
12. `NEWID()` creates a random GUID.
13. `NEWSEQUENTIALID()` creates a more insert-friendly sequential GUID.
14. `VECTOR(n)` stores embedding vectors.
15. Vector dimension must match the embedding model output.

## Indexes

16. A table can have only one clustered index.
17. A table can have multiple nonclustered indexes.
18. Clustered indexes are useful for range queries.
19. Nonclustered indexes are useful for lookups and joins.
20. Included columns reduce Key Lookups.
21. Composite index column order matters.
22. Equality predicates generally come before range predicates in composite index design.
23. Filtered indexes are useful for frequently queried subsets.
24. Columnstore indexes are for analytics and aggregation.
25. Clustered columnstore is common for fact tables.
26. Nonclustered columnstore supports HTAP scenarios.
27. Columnstore is not the default for high-frequency OLTP updates.
28. Full-text indexes support `CONTAINS` and `FREETEXT`.
29. Vector indexes accelerate semantic similarity search.
30. ANN is faster and more scalable than ENN for large vector data.

## Specialized Tables

31. Memory-optimized tables support low-latency OLTP.
32. `SCHEMA_AND_DATA` preserves memory-optimized data.
33. `SCHEMA_ONLY` loses data after restart.
34. Temporal tables store current and historical rows.
35. Temporal tables are best for point-in-time reconstruction.
36. Ledger tables provide tamper evidence.
37. Append-only ledger prevents update and delete operations.
38. External tables query data outside SQL storage.
39. Graph tables use node and edge tables.
40. `MATCH` traverses graph relationships.

## JSON

41. SQL commonly stores JSON in `NVARCHAR(MAX)`.
42. `JSON_VALUE` returns a scalar.
43. `JSON_QUERY` returns an object or array.
44. `OPENJSON` converts JSON into rows.
45. `JSON_OBJECT` creates a JSON object.
46. `JSON_ARRAY` creates a JSON array.
47. `JSON_ARRAYAGG` aggregates values into a JSON array.
48. `JSON_CONTAINS` checks JSON containment where supported.
49. Index JSON properties with computed columns.
50. Use `OPENJSON` when JSON arrays must become relational rows.

## Constraints and Programmability

51. Primary key means unique and not null.
52. Foreign key enforces referential integrity.
53. Unique constraint prevents duplicate values.
54. Check constraint enforces a rule.
55. Default constraint supplies a value automatically.
56. Sequence is independent of a table.
57. Identity is tied to a table.
58. Views simplify and secure data access.
59. Indexed views persist view results physically.
60. Scalar functions return one value.
61. Inline table-valued functions return a table.
62. Inline TVFs are often optimizer-friendly.
63. Stored procedures encapsulate reusable logic.
64. Triggers fire automatically after or instead of DML.
65. `inserted` and `deleted` pseudo tables are used in triggers.

## Advanced T-SQL

66. CTEs exist only for the next statement.
67. Recursive CTEs are useful for hierarchies.
68. `ROW_NUMBER` always gives unique sequence numbers.
69. `RANK` leaves gaps after ties.
70. `DENSE_RANK` does not leave gaps after ties.
71. `LAG` returns previous row value.
72. `LEAD` returns next row value.
73. `SUM() OVER` can create running totals.
74. Correlated subqueries reference the outer query.
75. `EXISTS` is common for correlated existence checks.
76. `TRY...CATCH` handles T-SQL errors.
77. Use `THROW` to re-raise original error context.
78. Transactions should roll back in CATCH if `@@TRANCOUNT > 0`.
79. Regex is for pattern matching and extraction.
80. Fuzzy matching is for approximate similarity.

## Regex and Fuzzy Matching

81. `REGEXP_LIKE` tests whether a string matches a pattern.
82. `REGEXP_REPLACE` replaces matching text.
83. `REGEXP_SUBSTR` extracts matching text.
84. `REGEXP_INSTR` returns the position of a match.
85. `REGEXP_COUNT` counts matches.
86. `REGEXP_MATCHES` returns matched values where supported.
87. `REGEXP_SPLIT_TO_TABLE` splits text into rows where supported.
88. `EDIT_DISTANCE` returns edit distance; lower is closer.
89. `EDIT_DISTANCE_SIMILARITY` returns similarity percentage.
90. `JARO_WINKLER_DISTANCE` is useful for names and short strings.

## AI-Assisted Development

91. Generated SQL must be reviewed and tested.
92. Do not paste secrets or PII into prompts.
93. Copilot instruction files guide repository-level generation.
94. `.github/copilot-instructions.md` stores GitHub Copilot instructions.
95. MCP connects AI tools to external context and tools.
96. MCP access should be least privilege.
97. Use read-only metadata access where possible.
98. Copilot in Fabric can assist with Fabric SQL development.
99. AI hallucination risk means schema and syntax must be validated.
100. Permission boundaries matter for AI-assisted tools.

## Security

101. Always Encrypted is client-side encryption.
102. Column-level encryption uses database-side keys/functions.
103. Deterministic Always Encrypted supports equality search.
104. Randomized Always Encrypted provides stronger confidentiality.
105. Dynamic Data Masking is not encryption.
106. DDM only masks query results for unauthorized users.
107. RLS filters rows automatically.
108. RLS uses a predicate function and security policy.
109. RLS predicate functions require `WITH SCHEMABINDING`.
110. Managed Identity enables passwordless Azure service access.
111. Microsoft Entra authentication avoids SQL passwords.
112. `GRANT` gives permission.
113. `DENY` explicitly blocks permission.
114. `REVOKE` removes permission.
115. `DENY` generally overrides `GRANT`.
116. Auditing records security and data access events.
117. Log Analytics can store SQL audit/diagnostic logs.
118. Event Hubs can stream audit events.
119. Secure model endpoints with Managed Identity/private endpoints where possible.
120. Secure GraphQL/REST endpoints with authentication and least privilege.

## Performance

121. Execution plans are best for single-query analysis.
122. DMVs show current activity and historical aggregated stats.
123. Query Store stores query plans and runtime history.
124. Query Store can identify regressions.
125. Query Store can force a known good plan.
126. Query Performance Insight shows top resource-consuming Azure SQL queries.
127. Index seek is usually better than table scan.
128. Key Lookup often means missing included columns.
129. Snapshot isolation reduces reader/writer blocking.
130. RCSI applies row versioning to read committed behavior.
131. Blocking is one session waiting on locks.
132. Deadlock is circular waiting.
133. SQL Server chooses a deadlock victim.
134. Parameter sniffing causes different performance for different parameter values.
135. `OPTION(RECOMPILE)` can mitigate parameter sniffing for specific queries.

## CI/CD and Azure Integration

136. SQL Database Projects represent schema as code.
137. SDK-style SQL projects are modern SQL project models.
138. DACPAC is a database deployment artifact.
139. Static/reference data can be managed with post-deployment MERGE scripts.
140. Schema drift means target database differs from source-controlled model.
141. Use branch policies and pull request approvals for governance.
142. Use Code Owners for mandatory reviewers.
143. Store secrets in Key Vault or secure pipeline variables, not Git.
144. DAB exposes REST and GraphQL endpoints over SQL without custom API code.
145. DAB can expose tables, views, and stored procedures.
146. DAB supports permissions, pagination, filtering, searching, and caching.
147. Application Insights captures application telemetry.
148. Azure Monitor provides metrics and alerts.
149. Change Tracking is lightweight and shows which rows changed.
150. CDC stores detailed insert/update/delete changes.

## AI, Search, and RAG

151. Embeddings are numeric representations of meaning.
152. Similar meanings have nearby vectors.
153. Embed descriptive text, not IDs.
154. Chunk large documents before embedding.
155. Semantic chunking gives high quality but costs more.
156. Azure Functions SQL trigger is common for embedding updates.
157. CES is suitable for streaming AI pipelines.
158. Full-text search is lexical.
159. Vector search is semantic.
160. Hybrid search combines full-text and vector search.
161. RRF combines rankings from multiple search systems.
162. Cosine distance is common for text embeddings.
163. Lower vector distance usually means more similar.
164. `VECTOR_NORMALIZE` normalizes vector magnitude.
165. `VECTORPROPERTY` returns vector metadata.
166. `VECTOR_SEARCH` performs vector retrieval where supported.
167. ENN is exact but slower.
168. ANN is approximate but faster.
169. HNSW is a common ANN index.
170. IVF is another ANN strategy.
171. RAG retrieves context before generation.
172. RAG reduces hallucinations when implemented correctly.
173. `FOR JSON PATH` is used to send SQL rows to a model.
174. `sp_invoke_external_rest_endpoint` can call external model endpoints.
175. Database scoped credentials secure external REST calls.

---

# Final 50 Practice Questions - Scenario Style

## Domain 1

1. You need to keep every previous version of employee salary rows for audit and point-in-time reporting. What should you use?  
   **Answer:** Temporal table.

2. You need to prove that financial transaction rows have not been tampered with. What should you use?  
   **Answer:** Ledger table.

3. You need a flexible product attribute column where attributes differ by product type. What should you use?  
   **Answer:** JSON stored in `NVARCHAR(MAX)`.

4. You need efficient filtering by `$.shipping.postcode` in a JSON column. What should you create?  
   **Answer:** Computed column using `JSON_VALUE`, then index it.

5. A table has millions of rows and is used mostly for aggregation reporting. Which index is best?  
   **Answer:** Clustered columnstore index.

6. An OLTP table also needs real-time analytics without changing the table to columnstore. What index can help?  
   **Answer:** Nonclustered columnstore index.

7. A query has repeated Key Lookups in the execution plan. What should you consider?  
   **Answer:** Add included columns to cover the query.

8. You need to model people and relationships between them with multi-hop queries. What should you use?  
   **Answer:** Graph tables and `MATCH`.

9. You need unique numbers shared across invoice and credit note tables. What should you use?  
   **Answer:** Sequence.

10. You need to split a huge order table by year for manageability and faster elimination. What should you use?  
    **Answer:** Partitioning.

## Domain 1 Advanced T-SQL

11. Query needs previous month's sales on each row. What function?  
    **Answer:** `LAG`.

12. Query needs rank with gaps after ties. What function?  
    **Answer:** `RANK`.

13. Query needs rank without gaps after ties. What function?  
    **Answer:** `DENSE_RANK`.

14. Query needs to parse an array into rows. What function?  
    **Answer:** `OPENJSON`.

15. Query needs email format validation. What function family?  
    **Answer:** `REGEXP_LIKE`.

16. Query needs approximate customer name matching. What function family?  
    **Answer:** Fuzzy matching, such as `EDIT_DISTANCE_SIMILARITY` or `JARO_WINKLER_DISTANCE`.

17. Query references an outer table column inside a subquery. What is this called?  
    **Answer:** Correlated subquery.

18. A transaction should roll back on error and rethrow the error. What construct?  
    **Answer:** `TRY...CATCH`, `ROLLBACK`, and `THROW`.

## Domain 2 Security

19. Support users must see masked email addresses only. What should you use?  
    **Answer:** Dynamic Data Masking.

20. DBAs must not see plaintext national ID values. What should you use?  
    **Answer:** Always Encrypted.

21. Encrypted values must support equality lookup. Which encryption type?  
    **Answer:** Deterministic Always Encrypted.

22. Same table must show different tenant rows to different users. What should you use?  
    **Answer:** Row-Level Security.

23. Azure App Service must connect to Azure SQL without password secrets. What should you use?  
    **Answer:** Managed Identity.

24. A user has GRANT SELECT but is also explicitly denied SELECT. What happens?  
    **Answer:** `DENY` overrides `GRANT`.

25. You need to track permission changes and data access for compliance. What should you enable?  
    **Answer:** Auditing.

## Domain 2 Performance

26. A query became slow after a deployment due to a new plan. What tool helps?  
    **Answer:** Query Store.

27. You need to force a previous good plan. What procedure can be used?  
    **Answer:** `sp_query_store_force_plan`.

28. Multiple users are waiting behind one long transaction. What issue is this?  
    **Answer:** Blocking.

29. Two transactions wait on each other's resources. What issue is this?  
    **Answer:** Deadlock.

30. A stored procedure is fast for one customer ID and slow for another. What is likely?  
    **Answer:** Parameter sniffing.

31. Readers and writers block each other frequently. What isolation option may help?  
    **Answer:** Snapshot isolation or RCSI.

32. You need top resource-consuming queries in Azure portal. What tool?  
    **Answer:** Query Performance Insight.

## Domain 2 CI/CD and Azure Integration

33. You need schema in Git with repeatable deployments. What should you use?  
    **Answer:** SQL Database Project.

34. You need a deployment artifact for SQL schema. What is commonly used?  
    **Answer:** DACPAC.

35. Production database was manually changed outside the project. What is this called?  
    **Answer:** Schema drift.

36. Lookup table values need to be kept in source control. How?  
    **Answer:** Static/reference data with post-deployment scripts, often `MERGE`.

37. Need REST and GraphQL endpoints over SQL without custom code. What service/tool?  
    **Answer:** Data API Builder.

38. Need to avoid returning huge API result sets. What DAB capability?  
    **Answer:** Pagination.

39. Need query diagnostics in KQL. What service?  
    **Answer:** Log Analytics.

40. Need application telemetry. What service?  
    **Answer:** Application Insights.

## Domain 3 AI

41. Which columns should be embedded: product description or product ID?  
    **Answer:** Product description.

42. A 200-page PDF must be used for semantic search. What step comes before embeddings?  
    **Answer:** Chunking.

43. Need immediate embedding update but can tolerate write overhead. What method?  
    **Answer:** Trigger.

44. Need lightweight embedding update detection. What method?  
    **Answer:** Change Tracking.

45. Need detailed change history for downstream processing. What method?  
    **Answer:** CDC.

46. Need streaming changes to AI pipeline. What method?  
    **Answer:** CES.

47. Need exact keyword search for product names. What search type?  
    **Answer:** Full-text search.

48. Need semantic search for synonyms and meaning. What search type?  
    **Answer:** Vector search.

49. Need best relevance using both keyword and semantic search. What pattern?  
    **Answer:** Hybrid search with RRF.

50. Need current enterprise data to ground an LLM answer. What architecture?  
    **Answer:** RAG.

---

# Final Revision Checklist

Before the exam, confirm you can explain each of the following without notes:

- Temporal vs Ledger vs CDC vs Auditing.
- Always Encrypted vs Column-level Encryption vs DDM.
- RLS predicate function and security policy.
- Clustered vs Nonclustered vs Columnstore vs Vector index.
- JSON_VALUE vs JSON_QUERY vs OPENJSON vs JSON_CONTAINS.
- REGEXP functions vs fuzzy matching functions.
- Query Store vs DMVs vs Execution Plan vs Query Performance Insight.
- Blocking vs Deadlock.
- Parameter sniffing and `OPTION(RECOMPILE)`.
- SQL Database Project, DACPAC, schema drift, and post-deployment reference data.
- DAB REST/GraphQL configuration and entity permissions.
- Change Tracking vs CDC vs CES vs Azure Functions SQL trigger.
- Embeddings, chunking, VECTOR(n), vector metrics, ANN vs ENN.
- Full-text vs Vector vs Hybrid search.
- RRF ranking.
- RAG flow, `FOR JSON PATH`, `sp_invoke_external_rest_endpoint`, and database scoped credentials.

