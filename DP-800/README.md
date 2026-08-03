# DP-800 Robust Study Material - Expanded Version

**Exam:** DP-800: Developing AI-Enabled Database Solutions  
**Certification:** Microsoft Certified: SQL AI Developer Associate  
**Generated:** 31 July 2026  
**Purpose:** Single Markdown study pack with concepts, syntax, decision trees, examples, and last-mile missing topics so you do not need to jump back to Microsoft Learn at the last moment.

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

### Index Types Overview - Description, Usage, and Scenario Selection

<table>
<tr><th>Index / Storage Type</th><th>What It Is</th><th>Best Use Case</th><th>When NOT To Use</th><th>Exam Scenario Keywords</th><th>Best Answer Clue</th></tr>
<tr><td>Clustered Rowstore Index</td><td>The table rows are stored in the logical order of the clustered key. A table can have only one clustered index.</td><td>OLTP tables, range queries, primary access path, date or ID based lookups.</td><td>Large analytical scans and aggregations are the dominant workload.</td><td>Range search, ordered data, one primary access path, OLTP lookup.</td><td>Choose when the table needs efficient ordered row access.</td></tr>
<tr><td>Nonclustered Rowstore Index</td><td>A separate B-tree structure that stores key columns and points back to the base table rows.</td><td>Point lookups, filtering, joins, alternate search keys.</td><td>Huge aggregations over many columns and millions of rows.</td><td>Find by email, filter by CustomerID, join by key.</td><td>Choose for selective predicates and lookup queries.</td></tr>
<tr><td>Included Columns</td><td>Non-key columns stored at the leaf level of a nonclustered index.</td><td>Cover queries and avoid repeated Key Lookup operations.</td><td>Columns are not returned or needed by the query.</td><td>Execution plan shows many Key Lookups.</td><td>Add selected columns as INCLUDE columns.</td></tr>
<tr><td>Composite Index</td><td>An index with multiple key columns in a defined order.</td><td>Queries filtering by multiple columns, such as CustomerID and OrderDate.</td><td>Column order does not match query predicates.</td><td>Multiple filters, equality plus range predicate.</td><td>Equality columns usually before range columns.</td></tr>
<tr><td>Filtered Index</td><td>An index over only a subset of rows that match a filter predicate.</td><td>Frequently queried subset such as active, open, pending, or non-null rows.</td><td>Queries do not include the same filter condition.</td><td>Only active rows, open orders, pending tasks.</td><td>Use when the filtered subset is much smaller than the table.</td></tr>
<tr><td>Clustered Columnstore Index</td><td>The table is stored by columns instead of rows, with high compression and batch processing.</td><td>Data warehouse/fact tables, reporting, BI dashboards, large aggregations.</td><td>Heavy OLTP point lookups and high-frequency updates are the primary workload.</td><td>Millions/billions of rows, SUM, AVG, COUNT, analytics.</td><td>Choose for analytics-first tables.</td></tr>
<tr><td>Nonclustered Columnstore Index</td><td>A secondary columnstore index on a rowstore table.</td><td>Mixed HTAP workloads where OLTP lookups must remain but analytics need acceleration.</td><td>Pure OLTP workload with no large analytical queries.</td><td>Preserve rowstore lookup, dashboard query scans many rows.</td><td>Choose when you need analytics without replacing clustered rowstore.</td></tr>
<tr><td>Full-Text Index</td><td>Special index for linguistic word and phrase search over text columns.</td><td>Exact phrase, word forms, product/document search.</td><td>Structured numeric/date lookups or semantic similarity search.</td><td>CONTAINS, FREETEXT, exact phrase, related forms.</td><td>Choose for lexical text search.</td></tr>
<tr><td>Vector Index</td><td>Index structure for approximate vector similarity search over embeddings.</td><td>Semantic search over embeddings at scale.</td><td>Exact keyword or phrase matching is required.</td><td>Embeddings, semantic, cosine, ANN, VECTOR_SEARCH.</td><td>Choose for meaning/synonym search.</td></tr>
</table>

**Quick index decision:** Rowstore = transactional lookup. Columnstore = analytical aggregation. Full-text = words and phrases. Vector = meaning and embeddings.



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

### Specialized Table Types Overview - Description, Usage, and Scenario Selection

<table>
<tr><th>Table Type</th><th>What It Is</th><th>Best Use Case</th><th>When NOT To Use</th><th>Exam Keywords</th></tr>
<tr><td>Memory-Optimized Table</td><td>A table stored using In-Memory OLTP structures for low-latency high-concurrency workloads.</td><td>Hot OLTP workloads, session state, high insert/update concurrency.</td><td>Audit history, tamper proofing, external file querying, or graph traversal.</td><td>Low latency, high throughput, In-Memory OLTP.</td></tr>
<tr><td>Temporal Table</td><td>A system-versioned table that automatically keeps current and historical row versions.</td><td>Point-in-time reconstruction, row history, accidental recovery.</td><td>Need cryptographic proof against tampering.</td><td>History, AS OF, previous version, point in time.</td></tr>
<tr><td>Ledger Table</td><td>A tamper-evident table that provides cryptographic verification of data changes.</td><td>Financial records, compliance records, provenance where tamper evidence matters.</td><td>Only normal history is required without tamper proofing.</td><td>Tamper evident, cryptographic, prove unchanged.</td></tr>
<tr><td>Append-Only Ledger Table</td><td>A ledger table where rows can be inserted but not updated or deleted.</td><td>Immutable event log or provenance trail.</td><td>Rows must be corrected or updated later.</td><td>Insert only, immutable after insert, provenance.</td></tr>
<tr><td>External Table</td><td>A SQL table definition over external data such as files in a lake/storage location.</td><td>Query data in place without loading it into the database.</td><td>Need frequent transactional writes into the table.</td><td>Parquet, Data Lake, external files, query in place.</td></tr>
<tr><td>Graph Node Table</td><td>A table representing entities in a graph model.</td><td>People, products, suppliers, accounts, devices.</td><td>Normal flat reporting or simple lookup.</td><td>Node, entity, graph.</td></tr>
<tr><td>Graph Edge Table</td><td>A table representing relationships between graph nodes.</td><td>Knows, supplies, depends on, connected to, purchased with.</td><td>Simple one-table filtering is enough.</td><td>Edge, relationship, multi-hop.</td></tr>
</table>

**Quick table decision:** Temporal = history. Ledger = tamper evidence. External = external files. Graph = relationships and hops. Memory optimized = low-latency OLTP.



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

### JSON Feature Overview - Description, Usage, and Scenario Selection

<table>
<tr><th>JSON Feature</th><th>What It Is</th><th>Use When</th><th>When NOT To Use</th><th>Exam Keywords</th></tr>
<tr><td>JSON stored in NVARCHAR(MAX)</td><td>SQL Server stores JSON text in character columns and queries it with JSON functions.</td><td>Flexible attributes, semi-structured payloads, API request/response data.</td><td>Strictly relational fixed schema is better and no flexibility is needed.</td><td>Flexible attributes, JSON payload, semi-structured.</td></tr>
<tr><td>JSON_VALUE</td><td>Extracts a scalar value from a JSON document.</td><td>Read values like status, customer ID, zip code, price.</td><td>Need object or array output.</td><td>Scalar, property, filter by JSON field.</td></tr>
<tr><td>JSON_QUERY</td><td>Extracts an object or array from a JSON document.</td><td>Need nested object or array as JSON fragment.</td><td>Need scalar string/number/date value.</td><td>Array, object, JSON fragment.</td></tr>
<tr><td>OPENJSON</td><td>Converts JSON object or array into relational rows.</td><td>Need one row per item in a JSON array.</td><td>Only one scalar property is required.</td><td>Expand array, one row per item, CROSS APPLY.</td></tr>
<tr><td>Computed Column + Index</td><td>Extracts a JSON scalar into a computed column and indexes it.</td><td>Frequently filter/search by a JSON property.</td><td>Ad hoc JSON properties rarely queried.</td><td>Efficient JSON filter, search by JSON property.</td></tr>
<tr><td>FOR JSON PATH</td><td>Formats query results as JSON with alias-controlled property names.</td><td>API output, RAG context, relational rows converted to JSON.</td><td>Need normal relational result set.</td><td>JSON context, LLM grounding, output as JSON.</td></tr>
<tr><td>INCLUDE_NULL_VALUES</td><td>Keeps null properties in JSON output.</td><td>Downstream parser expects consistent property shape.</td><td>Omitting nulls is acceptable.</td><td>Include null properties, fixed JSON schema.</td></tr>
<tr><td>WITHOUT_ARRAY_WRAPPER</td><td>Returns a single JSON object instead of an array for one-row output.</td><td>One-row context object is expected at top level.</td><td>Multiple rows are returned.</td><td>Single row, top-level JSON object.</td></tr>
</table>

**Quick JSON decision:** Scalar property = JSON_VALUE. Object/array = JSON_QUERY. Array to rows = OPENJSON. Query result to JSON = FOR JSON PATH.



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


## 2. Programmability Objects

### Programmability Object Overview - Description, Usage, and Scenario Selection

<table>
<tr><th>Object Type</th><th>What It Is</th><th>Use When</th><th>When NOT To Use</th><th>Exam Keywords</th></tr>
<tr><td>View</td><td>A saved SELECT statement that exposes a reusable logical result set.</td><td>Simplify joins, hide columns, expose read-only shape, security abstraction.</td><td>Need parameters or procedural logic.</td><td>Reusable query, no parameters, expose selected columns.</td></tr>
<tr><td>Indexed View</td><td>A view physically materialized by a unique clustered index.</td><td>Repeated expensive aggregations or precomputed results.</td><td>High-write tables where maintenance overhead is unacceptable.</td><td>Pre-aggregate, repeated reads, materialized result.</td></tr>
<tr><td>Scalar Function</td><td>A function that returns one value.</td><td>Reusable calculation in SELECT, WHERE, expressions.</td><td>Need to return a rowset.</td><td>Single value, calculation, expression.</td></tr>
<tr><td>Inline Table-Valued Function</td><td>A parameterized function that returns a table from one SELECT.</td><td>Composable rowset source, joins, CROSS APPLY, parameterized reusable query.</td><td>Need multiple procedural steps or data modifications.</td><td>Return rowset, used in joins, avoid return table variable.</td></tr>
<tr><td>Multi-Statement TVF</td><td>A function that builds and returns a table variable using multiple statements.</td><td>Need table output with procedural multi-step logic.</td><td>Requirement says avoid declaring a return table variable.</td><td>Multiple statements, return table variable.</td></tr>
<tr><td>Stored Procedure</td><td>A programmable object that can run multiple statements, modify data, use transactions, and return result sets/output parameters.</td><td>Data modification, transaction workflows, application operations, DAB execute/mutation.</td><td>Need a composable rowset directly in a JOIN.</td><td>Insert/update/delete, transaction, output parameter, execute.</td></tr>
<tr><td>AFTER Trigger</td><td>DML trigger that runs after INSERT, UPDATE, or DELETE completes but before commit.</td><td>Audit, validation, enforce business rules while preserving original DML unless validation fails.</td><td>Need to replace the original operation.</td><td>After insert/update, inserted table, preserve original action.</td></tr>
<tr><td>INSTEAD OF Trigger</td><td>DML trigger that runs instead of the original DML operation.</td><td>Custom write behavior, updatable views, replace original DML logic.</td><td>Requirement says original operation should proceed unless validation fails.</td><td>Instead of original action, replace DML.</td></tr>
</table>

**Quick programmability decision:** Single value = scalar function. Parameterized rowset = inline TVF. Data modification/transaction = stored procedure. Validate after insert/update = AFTER trigger. Replace DML = INSTEAD OF trigger.



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


## 3. Advanced T-SQL

### Advanced T-SQL Feature Overview - Description, Usage, and Scenario Selection

<table>
<tr><th>Feature</th><th>What It Is</th><th>Use When</th><th>When NOT To Use</th><th>Exam Keywords</th></tr>
<tr><td>CTE</td><td>A named temporary result set available to the next statement.</td><td>Improve readability of a complex query.</td><td>Need reusable stored object across multiple statements.</td><td>WITH, simplify query, next statement only.</td></tr>
<tr><td>Recursive CTE</td><td>A CTE that references itself to traverse hierarchical data.</td><td>Org chart, bill of materials, parent-child hierarchy.</td><td>Only one level of relationship is needed.</td><td>Hierarchy, manager, parent-child, depth.</td></tr>
<tr><td>Window Function</td><td>Function that calculates over a set of rows related to the current row.</td><td>Ranking, previous/next row, running totals, partitioned aggregates.</td><td>Need to collapse rows into grouped output only.</td><td>OVER, PARTITION BY, LAG, LEAD, ROW_NUMBER.</td></tr>
<tr><td>Correlated Subquery</td><td>A subquery that references columns from the outer query.</td><td>Existence checks, per-row aggregate comparison.</td><td>Independent subquery can answer the question simpler.</td><td>EXISTS, NOT EXISTS, outer query reference.</td></tr>
<tr><td>TRY/CATCH</td><td>T-SQL error handling structure.</td><td>Transactions need rollback and error rethrow.</td><td>No error handling or transaction safety requirement.</td><td>Rollback on error, THROW, @@TRANCOUNT.</td></tr>
<tr><td>Regular Expression Function</td><td>Pattern-based text validation, extraction, replacement, counting, or splitting.</td><td>Strict text pattern such as SKU, email, phone, code.</td><td>Approximate typo matching is required.</td><td>Pattern, extract code, case-insensitive, regex.</td></tr>
<tr><td>Fuzzy Matching Function</td><td>Compares approximate text similarity or edit distance.</td><td>Typos, similar names, approximate search.</td><td>Need exact phrase or strict pattern.</td><td>Similar to, typo, 70 percent similar, edit distance.</td></tr>
<tr><td>Graph MATCH</td><td>Graph pattern matching over node and edge tables.</td><td>Relationship traversal and multi-hop query.</td><td>Simple relational filter or aggregate.</td><td>Node, edge, MATCH, SHORTEST_PATH.</td></tr>
</table>

**Quick T-SQL decision:** Hierarchy = recursive CTE. Previous/next row = LAG/LEAD. Pattern extraction = regex. Typo similarity = fuzzy matching. Relationship path = graph MATCH.



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


## 5. Implement Data Security and Compliance

### Security Feature Overview - Description, Usage, and Scenario Selection

<table>
<tr><th>Security Feature</th><th>What It Is</th><th>Use When</th><th>When NOT To Use</th><th>Exam Keywords</th></tr>
<tr><td>Always Encrypted</td><td>Client-side encryption where database engine normally cannot see plaintext.</td><td>Protect sensitive data from DBAs/admins; maintain separation of data and key access.</td><td>Only display masking is needed.</td><td>DBA cannot view plaintext, Key Vault, column encryption setting.</td></tr>
<tr><td>Deterministic Always Encrypted</td><td>Same plaintext produces same ciphertext.</td><td>Exact equality search on encrypted data.</td><td>Strongest confidentiality is required and equality search is not needed.</td><td>Exact-match search, encrypted identifier.</td></tr>
<tr><td>Randomized Always Encrypted</td><td>Same plaintext produces different ciphertext.</td><td>Higher confidentiality for values not searched by equality.</td><td>Need equality lookup on the encrypted column.</td><td>More secure, no search, sensitive date.</td></tr>
<tr><td>Column-Level Encryption</td><td>Database-side encryption using T-SQL keys and encryption functions.</td><td>Need encrypt/decrypt logic inside T-SQL.</td><td>Need to prevent DB engine/admins from accessing plaintext.</td><td>EncryptByKey, DecryptByKey, certificate.</td></tr>
<tr><td>Dynamic Data Masking</td><td>Masks query result display for unauthorized users.</td><td>Hide values in result sets while keeping data unchanged.</td><td>Need real encryption or protection from privileged users.</td><td>Masked email, partial credit card, display only.</td></tr>
<tr><td>Row-Level Security</td><td>Predicate-based row filtering and write blocking.</td><td>Tenant/user/region-level row access control in the same table.</td><td>Need column masking or encryption only.</td><td>TenantID, SESSION_CONTEXT, filter predicate, block predicate.</td></tr>
<tr><td>Object-Level Permissions</td><td>GRANT, DENY, REVOKE permissions on securables.</td><td>Least privilege access to tables, views, procedures, schemas.</td><td>Need row-by-row filtering.</td><td>Grant SELECT on one table, execute procedure.</td></tr>
<tr><td>Managed Identity</td><td>Passwordless Azure identity for services accessing resources.</td><td>App/SQL server calls Azure SQL or Azure OpenAI without secrets.</td><td>Resource/service does not support MI or no identity configured.</td><td>Passwordless, no secrets, service-to-service.</td></tr>
<tr><td>Service Connector</td><td>Azure service that can configure connection, identity, database user, and permissions.</td><td>Need passwordless app-to-SQL connection with minimal manual setup.</td><td>You need full manual custom configuration.</td><td>Minimize manual identity and database permission configuration.</td></tr>
<tr><td>Auditing</td><td>Captures database events for monitoring, investigation, and compliance.</td><td>Track logins, permission changes, data access, compliance events.</td><td>Need query performance regression history.</td><td>Audit records, KQL, Log Analytics, current and future databases.</td></tr>
</table>

**Quick security decision:** Hide display = DDM. Protect from DBA = Always Encrypted. Tenant rows = RLS. Passwordless = Managed Identity/Service Connector. Compliance logs = Auditing.



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


## 6. Optimize Database Performance

### Performance Feature and DMV Overview - Description, Usage, and Scenario Selection

<table>
<tr><th>Tool / Feature</th><th>What It Is</th><th>Use When</th><th>When NOT To Use</th><th>Exam Keywords</th></tr>
<tr><td>Actual Execution Plan</td><td>The real runtime query plan with actual row counts and operators.</td><td>Diagnose one slow query and understand seeks, scans, joins, key lookups, sorts.</td><td>Need current server-wide waiting sessions only.</td><td>Actual plan, operator, Key Lookup, estimated vs actual.</td></tr>
<tr><td>Estimated Execution Plan</td><td>Optimizer's predicted plan without running the query.</td><td>Preview plan shape when running query is expensive or unsafe.</td><td>Need actual runtime row counts.</td><td>Estimated plan, before execution.</td></tr>
<tr><td>sys.dm_exec_requests</td><td>DMV showing currently executing requests.</td><td>Active slowdown, live CPU, reads, wait type, wait time, blocking session ID.</td><td>Need historical cached aggregate statistics.</td><td>Currently running, active requests, blocking_session_id.</td></tr>
<tr><td>sys.dm_exec_query_stats</td><td>DMV with aggregate performance stats for cached query plans.</td><td>Find top CPU, elapsed time, logical reads across cached plans.</td><td>Need live request-level waits.</td><td>Top CPU queries, execution_count, total_worker_time.</td></tr>
<tr><td>sys.dm_os_wait_stats</td><td>Server-level cumulative wait statistics.</td><td>Understand overall wait profile.</td><td>Need to identify which session is blocking now.</td><td>Wait totals, wait categories.</td></tr>
<tr><td>sys.dm_db_missing_index_details</td><td>DMV with optimizer missing-index suggestions.</td><td>Investigate potential missing indexes.</td><td>Blindly create indexes or diagnose live blocking.</td><td>Missing index recommendation.</td></tr>
<tr><td>sys.dm_db_index_usage_stats</td><td>DMV showing index seeks, scans, lookups, and updates.</td><td>Review whether indexes are used or only maintained.</td><td>Need exact query operator path.</td><td>Index usage, unused index, seeks/scans.</td></tr>
<tr><td>Query Store</td><td>Feature storing query plans and runtime history over time.</td><td>Plan regression, compare historical plans, force known good plan.</td><td>Need live request wait details.</td><td>Slow after deployment, previous good plan, force plan.</td></tr>
<tr><td>Query Performance Insight</td><td>Azure portal view of top resource-consuming queries.</td><td>Need portal-based view of high CPU/DTU/resource queries.</td><td>Need direct T-SQL DMV query or operator-level tuning.</td><td>Azure portal, top consumers.</td></tr>
<tr><td>Azure Monitor</td><td>Azure monitoring platform for metrics and alerts.</td><td>Platform metrics, alerts, dashboards.</td><td>Need query plan details.</td><td>Metrics, alert rules, monitoring.</td></tr>
<tr><td>Log Analytics</td><td>Workspace for logs queried with KQL.</td><td>Diagnostic logs, audit logs, KQL alerting.</td><td>Need index seek vs scan analysis.</td><td>KQL, logs, diagnostic queries.</td></tr>
<tr><td>Application Insights</td><td>Application telemetry and dependency monitoring.</td><td>Trace app requests, dependencies, failures, SQL call duration from app side.</td><td>Need SQL internal operator tuning only.</td><td>Application traces, dependency calls.</td></tr>
<tr><td>RCSI / Snapshot Isolation</td><td>Row versioning isolation to reduce reader/writer blocking.</td><td>Readers and writers block each other.</td><td>Need strict locking semantics or cannot support version store impact.</td><td>Reader/writer blocking, row versioning.</td></tr>
<tr><td>Columnstore Index</td><td>Column-based compressed index for analytical scans and aggregates.</td><td>Large dashboard/reporting queries, COUNT/SUM/AVG over many rows.</td><td>Hot OLTP point lookup workload only.</td><td>600 million rows, dashboard, aggregate scan.</td></tr>
</table>

**Quick performance decision:** Live issue = sys.dm_exec_requests. Plan regression = Query Store. One query operator analysis = execution plan. Azure top consumers = Query Performance Insight. Logs/KQL = Log Analytics.



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


## 7. CI/CD with SQL Database Projects

### CI/CD Feature Overview - Description, Usage, and Scenario Selection

<table>
<tr><th>Feature / Artifact</th><th>What It Is</th><th>Use When</th><th>When NOT To Use</th><th>Exam Keywords</th></tr>
<tr><td>SQL Database Project</td><td>Source-controlled declarative model of database schema.</td><td>Need schema as code, review, build validation, repeatable deployment.</td><td>One-off unmanaged manual changes.</td><td>Schema in Git, database project, source control.</td></tr>
<tr><td>SDK-Style SQL Project</td><td>Modern SQL project format that builds cross-platform with .NET SDK.</td><td>Ubuntu/GitHub Actions runners, fewer manual project-file updates.</td><td>Visual Studio-only legacy workflow is explicitly required.</td><td>Ubuntu runner, dotnet build, SDK-style.</td></tr>
<tr><td>DACPAC</td><td>Deployable artifact containing database schema model.</td><td>Build once and publish to target environments.</td><td>Need editable object source files only.</td><td>Deployable artifact, .dacpac.</td></tr>
<tr><td>SqlPackage Publish</td><td>Publishes a DACPAC to a target database.</td><td>Deploy built project to test/prod database.</td><td>Need to extract current live DB schema.</td><td>Deploy DACPAC, publish to database.</td></tr>
<tr><td>SqlPackage Extract</td><td>Creates a DACPAC or project model from an existing database.</td><td>Initialize project from current database or capture schema.</td><td>Deploy project changes to target.</td><td>Extract schema from database.</td></tr>
<tr><td>Schema Compare / Drift Detection</td><td>Compares project and live database differences.</td><td>Manual production change must be reconciled back to source control.</td><td>Blindly accept all live differences.</td><td>Schema drift, approved hotfix, exclude unwanted table.</td></tr>
<tr><td>Post-Deployment Script</td><td>Script executed after schema deployment.</td><td>Reference/static data such as lookup statuses.</td><td>Schema object creation should be modeled normally.</td><td>MERGE reference data, static data.</td></tr>
<tr><td>GitHub Environment Secret</td><td>Secret scoped to a GitHub environment such as production.</td><td>Production-only deployment credential.</td><td>Non-sensitive configuration values.</td><td>Production environment, protect connection string.</td></tr>
<tr><td>Pull Request Workflow</td><td>Review and validation process before merge.</td><td>Branch policies, security scans, build/test gates.</td><td>Emergency manual change without source reconciliation.</td><td>PR review, branch policy, required checks.</td></tr>
</table>

**Quick CI/CD decision:** Source schema = SQL project. Deployable artifact = DACPAC. Deploy DACPAC = SqlPackage Publish. Existing DB to model = Extract. Production-only credential = environment secret.



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


## 8. Integrate SQL Solutions with Azure Services

### Azure Integration and DAB Overview - Description, Usage, and Scenario Selection

<table>
<tr><th>Feature / Service</th><th>What It Is</th><th>Use When</th><th>When NOT To Use</th><th>Exam Keywords</th></tr>
<tr><td>Data API Builder</td><td>Tool/runtime that exposes database objects through REST and GraphQL with minimal custom code.</td><td>Expose tables, views, or procedures as API endpoints quickly.</td><td>Need highly custom business API logic outside database.</td><td>REST, GraphQL, minimal custom API code.</td></tr>
<tr><td>DAB REST Entity</td><td>DAB entity exposed as REST endpoint.</td><td>CRUD-style HTTP API over database object.</td><td>Client specifically needs GraphQL shape/query.</td><td>REST endpoint, GET, POST, filter, top, skip.</td></tr>
<tr><td>DAB GraphQL Entity</td><td>DAB entity exposed through GraphQL schema.</td><td>Client needs GraphQL query/mutation and relational navigation.</td><td>Plain REST endpoint requirement only.</td><td>GraphQL endpoint, query, mutation.</td></tr>
<tr><td>DAB Stored Procedure Entity</td><td>DAB mapping over a stored procedure.</td><td>Expose existing procedure, especially transactional operation.</td><td>Simple table read is enough.</td><td>Existing stored procedure, checkout, one API call.</td></tr>
<tr><td>DAB Permissions</td><td>Role/action based access for entities.</td><td>Restrict read/create/update/delete/execute.</td><td>Need row filtering inside database only.</td><td>Read-only entity, execute permission.</td></tr>
<tr><td>DAB fields.exclude</td><td>Field-level exclusion from API exposure.</td><td>Hide protected columns such as CostPrice/InternalNotes.</td><td>Need to filter rows by tenant.</td><td>Protected fields, hide from GraphQL.</td></tr>
<tr><td>DAB Cache L1</td><td>In-memory local instance cache.</td><td>Single instance or local low-latency cache.</td><td>Must share cache across multiple instances.</td><td>Local cache.</td></tr>
<tr><td>DAB Cache L1L2</td><td>Local plus distributed cache.</td><td>Multiple app instances need shared cached responses.</td><td>No distributed cache configured.</td><td>Distributed cache, shared across instances.</td></tr>
<tr><td>Application Insights</td><td>Application performance and dependency telemetry.</td><td>Trace app/API calls and SQL dependencies.</td><td>Need database audit KQL only.</td><td>App traces, dependency calls.</td></tr>
<tr><td>Log Analytics</td><td>Workspace for querying logs with KQL.</td><td>Diagnostics, audit logs, alert rules.</td><td>Need application distributed tracing only.</td><td>KQL, diagnostic logs.</td></tr>
<tr><td>Azure Monitor</td><td>Metrics, alerts, and dashboards across Azure resources.</td><td>Platform monitoring and alerting.</td><td>Need query text/operator analysis.</td><td>Metrics, alerts, dashboard.</td></tr>
<tr><td>Change Tracking</td><td>Lightweight mechanism to identify changed rows.</td><td>Sync process needs changed keys only.</td><td>Need full before/after details.</td><td>Lightweight sync, changed rows.</td></tr>
<tr><td>CDC</td><td>Captures detailed insert/update/delete changes.</td><td>ETL and detailed change processing.</td><td>Need event-stream delivery to multiple consumers.</td><td>Detailed changes, operation history.</td></tr>
<tr><td>Change Event Streaming</td><td>Streams SQL changes to downstream event consumers.</td><td>Near-real-time decoupled multi-consumer processing.</td><td>Simple polling of changed keys is enough.</td><td>Event stream, near real time, multiple consumers.</td></tr>
</table>

**Quick integration decision:** No-code REST/GraphQL = DAB. App telemetry = Application Insights. KQL diagnostics = Log Analytics. Changed keys = Change Tracking. Detailed changes = CDC. Event-driven changes = CES.



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


## 9. Models and Embeddings

### Models and Embeddings Overview - Description, Usage, and Scenario Selection

<table>
<tr><th>Feature</th><th>What It Is</th><th>Use When</th><th>When NOT To Use</th><th>Exam Keywords</th></tr>
<tr><td>Chat / Completion Model</td><td>Generates natural language or structured text output.</td><td>Need answer, category, priority, route queue, JSON response, reasoning.</td><td>Need numeric vector for similarity search.</td><td>Generate values, structured output, assistant response.</td></tr>
<tr><td>Embedding Model</td><td>Converts text into numeric vector representation of meaning.</td><td>Semantic search, similarity, RAG retrieval.</td><td>Need readable category/priority values directly.</td><td>Embedding, semantic, vector.</td></tr>
<tr><td>External Model</td><td>Database object representing an external AI model endpoint.</td><td>SQL procedures/functions invoke model-integrated workloads.</td><td>Application calls model directly and SQL does not need model object.</td><td>CREATE/ALTER EXTERNAL MODEL, model endpoint.</td></tr>
<tr><td>Database Scoped Credential</td><td>Database credential used to authenticate to external endpoints.</td><td>Keep API keys out of procedure code or use Managed Identity.</td><td>No external call is made from SQL.</td><td>Credential, HTTPEndpointHeaders, Managed Identity.</td></tr>
<tr><td>AI_GENERATE_CHUNKS</td><td>AI function concept for splitting large text into chunks.</td><td>Need chunk text before embeddings.</td><td>Small text already fits retrieval and model limits.</td><td>Chunking, large documents.</td></tr>
<tr><td>AI_GENERATE_EMBEDDINGS</td><td>AI function concept for generating embedding vectors from text.</td><td>Store semantic vectors for search.</td><td>Need categorical business fields as output.</td><td>Generate embeddings, vector column.</td></tr>
<tr><td>VECTOR(n)</td><td>Native vector data type with fixed dimension.</td><td>Store embeddings and validate dimension count.</td><td>Only raw JSON vector text is needed outside SQL search.</td><td>VECTOR(768), VECTOR(1536), dimensions.</td></tr>
<tr><td>Related Embedding Table</td><td>Separate table storing one vector per source chunk.</td><td>Regenerate embeddings/chunks without modifying source table.</td><td>One short text field per row and no chunking needs.</td><td>One vector per chunk, related embeddings table.</td></tr>
</table>

**Quick AI decision:** Need similarity = embedding model. Need category/priority text = chat model. Need secure SQL external call = database scoped credential. Need long document retrieval = chunks plus embeddings.



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


## 10. Intelligent Search

### Intelligent Search Overview - Description, Usage, and Scenario Selection

<table>
<tr><th>Search Feature</th><th>What It Is</th><th>Use When</th><th>When NOT To Use</th><th>Exam Keywords</th></tr>
<tr><td>LIKE</td><td>Basic pattern matching with wildcards.</td><td>Simple substring/prefix matching on small/simple scenarios.</td><td>Need linguistic full-text ranking or semantic meaning.</td><td>Starts with, contains simple pattern.</td></tr>
<tr><td>CONTAINS</td><td>Full-text predicate for exact word, phrase, prefix, or Boolean-style text matches.</td><td>Exact phrase like "mountain bike" or precise keyword conditions.</td><td>Need synonym/meaning beyond words.</td><td>Exact phrase, full-text, keyword.</td></tr>
<tr><td>FREETEXT</td><td>Full-text predicate for natural language / linguistic forms.</td><td>Related word forms such as ride, riding, rode.</td><td>Need exact phrase enforcement.</td><td>Related forms, natural language full-text.</td></tr>
<tr><td>FREETEXTTABLE / CONTAINSTABLE</td><td>Full-text ranking table-valued functions.</td><td>Need ranked full-text result list to combine with other ranking.</td><td>Only Boolean filter is needed.</td><td>Ranked full-text results, RANK.</td></tr>
<tr><td>Vector Search</td><td>Semantic similarity search over embeddings.</td><td>Meaning, synonyms, concept search, RAG retrieval.</td><td>Exact code/name/phrase search is required.</td><td>Semantic, embedding, cosine.</td></tr>
<tr><td>VECTOR_DISTANCE</td><td>Calculates exact distance between vectors, often over candidate rows.</td><td>Small data sets or exact nearest-neighbor comparison.</td><td>Millions of vectors with low latency requirement.</td><td>Exact search, distance calculation.</td></tr>
<tr><td>VECTOR_SEARCH</td><td>Vector index based candidate retrieval.</td><td>Large vector data and approximate nearest-neighbor search.</td><td>Strict exact result required on small data.</td><td>ANN, vector index, low CPU, recall target.</td></tr>
<tr><td>Hybrid Search</td><td>Combines full-text and vector search.</td><td>Need both exact terms and semantic meaning for better relevance.</td><td>Only exact ID lookup is needed.</td><td>Keyword plus semantic, one retrieval workflow.</td></tr>
<tr><td>RRF</td><td>Reciprocal Rank Fusion combines rankings from different search systems.</td><td>Merge full-text ranks and vector ranks without comparing raw scores.</td><td>Only one search result list exists.</td><td>Combine rankings, do not compare raw scores.</td></tr>
<tr><td>Search Evaluation Metrics</td><td>Precision, recall, MRR, NDCG, latency, throughput.</td><td>Evaluate retrieval relevance and performance.</td><td>Need only write query syntax.</td><td>Recall@K, relevance, ranking quality.</td></tr>
</table>

**Quick search decision:** Exact words = CONTAINS. Linguistic word forms = FREETEXT. Meaning = vector search. Both keyword and meaning = hybrid + RRF.



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


## 11. Retrieval-Augmented Generation - RAG

### RAG Component Overview - Description, Usage, and Scenario Selection

<table>
<tr><th>RAG Component</th><th>What It Is</th><th>Use When</th><th>When NOT To Use</th><th>Exam Keywords</th></tr>
<tr><td>RAG Architecture</td><td>Retrieves trusted context before generating an answer.</td><td>Answer must use current enterprise/database facts.</td><td>All required text is already supplied in prompt.</td><td>Ground answer, current data, enterprise facts.</td></tr>
<tr><td>Chunking</td><td>Splitting large content into retrievable text units.</td><td>Documents are long or cover multiple topics.</td><td>Text is already short and focused.</td><td>Large document, chunk size, overlap.</td></tr>
<tr><td>Structural Chunking</td><td>Chunks based on document headings/sections.</td><td>Manuals with clear headings and section citations.</td><td>Free-form narratives without reliable structure.</td><td>Headings, sections, citations.</td></tr>
<tr><td>Hierarchical Chunking</td><td>Stores small chunks plus parent/procedure context.</td><td>Need exact step retrieval plus surrounding context.</td><td>Simple short FAQ entries.</td><td>Procedure, exact steps, surrounding context.</td></tr>
<tr><td>Semantic Chunking</td><td>Splits text by meaning/topic boundaries.</td><td>Free-form narratives that shift topics.</td><td>Strictly structured documents where headings are reliable.</td><td>Free-form, topic shifts, retrieval quality.</td></tr>
<tr><td>FOR JSON PATH</td><td>Converts SQL rows to JSON for prompt context.</td><td>Send relational data to LLM as structured context.</td><td>Application expects normal rowset.</td><td>Retrieval context, JSON array, aliases as property names.</td></tr>
<tr><td>OPENJSON WITH nvarchar(max)</td><td>Extracts long scalar values from JSON response.</td><td>Assistant answer can exceed 4,000 characters.</td><td>Only short scalar is needed.</td><td>Preserve long answer, first chat choice.</td></tr>
<tr><td>sp_invoke_external_rest_endpoint</td><td>SQL procedure to call external REST endpoints.</td><td>Database invokes model endpoint directly.</td><td>Application layer calls model and SQL has no external call.</td><td>Call model from SQL, external REST endpoint.</td></tr>
<tr><td>Database Scoped Credential</td><td>Credential used by SQL external REST call.</td><td>Secure model endpoint with Managed Identity or stored API header.</td><td>No secured external endpoint is used.</td><td>Managed Identity, HTTPEndpointHeaders, credential.</td></tr>
<tr><td>RLS before retrieval</td><td>Apply row security before selecting context.</td><td>User-specific data must not leak into model prompt.</td><td>All context is public and unrestricted.</td><td>Security filters, tenant context, authorized rows.</td></tr>
</table>

**Quick RAG decision:** Need current DB facts = RAG. SQL rows to prompt = FOR JSON PATH. Long model answer extraction = OPENJSON WITH nvarchar(max). Secure SQL-to-model call = scoped credential.



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



---

## Practice Exam Gap Addendum - Details Added from Latest Practice Exam Screenshots

**Purpose:** This addendum keeps every existing section above unchanged and adds the missing scenario-level details observed in the latest practice exam screenshots. The focus is on exact exam choices, decision patterns, and copy/paste syntax samples that were not covered deeply enough in the original study material.

### Gap Summary from Practice Exam Review

<table>
<tr><th>Area</th><th>Missing or Short Detail</th><th>Where to Study in This Addendum</th></tr>
<tr><td>Security</td><td>RLS block predicates for insert/update tenant enforcement</td><td>RLS Filter and Block Predicates</td></tr>
<tr><td>Security</td><td>Service Connector passwordless setup and RBAC vs database permissions distinction</td><td>Passwordless Access with Service Connector</td></tr>
<tr><td>Security</td><td>Server-level auditing to Log Analytics for current and future databases</td><td>Auditing Scope and Destination</td></tr>
<tr><td>Security</td><td>DAB GraphQL field exclusion and endpoint security details</td><td>DAB GraphQL Field-Level Security</td></tr>
<tr><td>AI security</td><td>Managed Identity for Azure OpenAI calls from SQL logical server</td><td>Secure Model Endpoint Invocation</td></tr>
<tr><td>CI/CD</td><td>Git branch workflow, schema drift reconciliation, test deployment, environment secrets</td><td>SQL Project CI/CD Practice Patterns</td></tr>
<tr><td>DAB</td><td>Stored procedure as GraphQL mutation, caching TTL and L1L2 cache</td><td>DAB Stored Procedures, Mutations, and Caching</td></tr>
<tr><td>Performance</td><td>Live DMV selection, deadlock access order, Key Lookup remedies</td><td>Performance Practice Patterns</td></tr>
<tr><td>Indexing</td><td>Nonclustered columnstore for large aggregate dashboard while preserving rowstore lookup</td><td>Columnstore Practice Scenarios</td></tr>
<tr><td>Partitioning</td><td>Monthly RANGE RIGHT partitions, aligned indexes, partition switching</td><td>Partitioning Practice Scenario</td></tr>
<tr><td>AI models</td><td>External model lifecycle, ALTER model, credential with API key, runtime permission</td><td>External Models in SQL</td></tr>
<tr><td>Vector search</td><td>VECTOR(768) vs VECTOR(1536), structured filters, cosine vector index</td><td>Vector Storage and Index Design</td></tr>
<tr><td>Hybrid search</td><td>FREETEXTTABLE + VECTOR_SEARCH + FULL OUTER JOIN + RRF</td><td>Hybrid Search Query Pattern</td></tr>
<tr><td>RAG JSON</td><td>OPENJSON for long model answers, INCLUDE_NULL_VALUES, WITHOUT_ARRAY_WRAPPER</td><td>RAG JSON Handling</td></tr>
<tr><td>Chunking</td><td>Structural, hierarchical, and semantic chunking differences</td><td>Advanced Chunking Strategy</td></tr>
<tr><td>Graph</td><td>SHORTEST_PATH, FOR PATH aliases, GRAPH PATH aggregations</td><td>Graph Table Query Patterns</td></tr>
<tr><td>Programmability</td><td>Stored procedure output parameters, triggers using inserted, inline TVF with CROSS APPLY, scalar function choice</td><td>Programmability Practice Patterns</td></tr>
<tr><td>AI-assisted tools</td><td>Fabric item-scoped MCP, metadata-only MCP permissions, SSMS Azure custom model</td><td>AI-Assisted Tooling Practice Patterns</td></tr>
</table>

## Security Missing Details

### RLS Filter and Block Predicates

**Practice exam pattern:** A multitenant app uses a shared database user and sets `SESSION_CONTEXT(N'TenantID')`. Tenants must read, update, and delete only their own rows, and must not insert or update rows for another tenant.

**Correct answer:** Use a filter predicate plus block predicates after insert and after update.

<table>
<tr><th>Requirement</th><th>Predicate Needed</th><th>Why</th></tr>
<tr><td>Read only own rows</td><td>FILTER PREDICATE</td><td>Limits rows visible to SELECT, UPDATE, and DELETE operations.</td></tr>
<tr><td>Delete only own rows</td><td>FILTER PREDICATE</td><td>Rows from another tenant are not visible as target rows.</td></tr>
<tr><td>Prevent insert for another tenant</td><td>BLOCK PREDICATE AFTER INSERT</td><td>Validates the final inserted TenantID value.</td></tr>
<tr><td>Prevent update that changes TenantID to another tenant</td><td>BLOCK PREDICATE AFTER UPDATE</td><td>Validates the final updated TenantID value.</td></tr>
</table>

```sql
CREATE SECURITY POLICY Security.TenantIsolationPolicy
ADD FILTER PREDICATE Security.fn_TenantAccessPredicate(TenantID)
ON dbo.Orders,
ADD BLOCK PREDICATE Security.fn_TenantAccessPredicate(TenantID)
ON dbo.Orders AFTER INSERT,
ADD BLOCK PREDICATE Security.fn_TenantAccessPredicate(TenantID)
ON dbo.Orders AFTER UPDATE
WITH (STATE = ON);
```

**Exam trap:** Filter-only RLS does not stop an insert that supplies another TenantID. Block-only RLS does not restrict read visibility.

### Passwordless Access with Service Connector

**Practice exam pattern:** Azure App Service or Azure Container Apps connects to Azure SQL. The current connection string contains a SQL username and password. The requirement says remove secrets and minimize manual identity/database-permission configuration.

**Correct answer:** Use Service Connector to create the Azure SQL connection by using a system-assigned managed identity.

<table>
<tr><th>Option</th><th>Exam Interpretation</th></tr>
<tr><td>Enable managed identity only</td><td>Incomplete. You still need database user and permissions.</td></tr>
<tr><td>Manually replace connection string with Active Directory Default</td><td>Passwordless, but does not minimize manual setup.</td></tr>
<tr><td>Assign SQL DB Contributor Azure RBAC</td><td>Controls Azure resource management, not SQL data access.</td></tr>
<tr><td>Use Service Connector</td><td>Best when the question asks to automate identity and database-permission configuration.</td></tr>
</table>

**Memory:** Azure RBAC manages the Azure SQL resource. SQL database permissions manage data access inside the database.

### Auditing Scope and Destination

<table>
<tr><th>Requirement</th><th>Best Answer</th><th>Why</th></tr>
<tr><td>Audit current and future databases on a logical server</td><td>Server-level auditing</td><td>Avoids configuring each database individually.</td></tr>
<tr><td>Security team uses KQL queries and alert rules</td><td>Log Analytics workspace</td><td>Supports query-based monitoring and alerts.</td></tr>
<tr><td>Stream audit events to external SIEM</td><td>Event Hubs</td><td>Use when the scenario emphasizes event streaming.</td></tr>
<tr><td>Long-term raw archive</td><td>Azure Storage</td><td>Use when the scenario emphasizes retention/archive.</td></tr>
</table>

### Object-Level Permissions - Least Privilege

**Practice exam pattern:** Role needs read access to only one table in a schema.

```sql
GRANT SELECT ON dbo.Customers TO Role1;
```

<table>
<tr><th>Permission</th><th>Use / Trap</th></tr>
<tr><td>SELECT ON dbo.Customers</td><td>Correct for reading only one table.</td></tr>
<tr><td>SELECT ON SCHEMA::dbo</td><td>Too broad because it grants access to all current and future applicable objects in dbo.</td></tr>
<tr><td>VIEW DEFINITION</td><td>Metadata visibility, not row access.</td></tr>
<tr><td>CONTROL</td><td>Object management-level permission, too broad.</td></tr>
</table>

### DAB GraphQL Field-Level Security

**Practice exam pattern:** Authenticated users can query an entity, but protected fields such as `InternalNotes` and `CostPrice` must not be accessible through GraphQL.

**Correct answer:** Configure the authenticated role with read action and a `fields.exclude` list.

```json
{
  "entities": {
    "Order": {
      "source": "dbo.Orders",
      "permissions": [
        {
          "role": "authenticated",
          "actions": [
            {
              "action": "read",
              "fields": {
                "exclude": [ "InternalNotes", "CostPrice" ]
              }
            }
          ]
        }
      ]
    }
  }
}
```

**Exam trap:** Disabling GraphQL introspection reduces schema discovery but does not enforce field-level authorization.

### Secure Model Endpoint Invocation

**Practice exam pattern:** SQL stored procedure calls Azure OpenAI by using `sp_invoke_external_rest_endpoint`. API key must be removed, SQL logical server has managed identity, and only an application database principal should start embedding requests.

Correct actions:
- Assign Cognitive Services User role to the SQL logical server managed identity at the Azure OpenAI resource scope.
- Create a database scoped credential that uses Managed Identity.
- Grant EXECUTE on the stored procedure to a database role containing the application principal.

```sql
CREATE DATABASE SCOPED CREDENTIAL [https://my-openai-resource.openai.azure.com]
WITH IDENTITY = 'Managed Identity';

CREATE ROLE EmbeddingRequestExecutor;
ALTER ROLE EmbeddingRequestExecutor ADD MEMBER [app-service-identity];
GRANT EXECUTE ON dbo.GetEmbedding TO EmbeddingRequestExecutor;
```

**Exam trap:** Assigning Cognitive Services User to the application identity is wrong when SQL Server is the caller to Azure OpenAI. The SQL logical server managed identity makes the external call.

## SQL Project CI/CD Missing Details

### Git Feature Branch Workflow

<table>
<tr><th>Step</th><th>Command</th><th>Why</th></tr>
<tr><td>Before editing object file</td><td><code>git checkout -b feature/add-column1</code></td><td>Isolates the schema change from main.</td></tr>
<tr><td>After committing the change</td><td><code>git push origin feature/add-column1</code></td><td>Makes the branch available for pull-request review.</td></tr>
</table>

### SDK-Style SQL Project from Existing Database

**Practice exam pattern:** Ubuntu runner, .NET SDK installed, store objects as editable source files, minimize manual project-file updates.

**Correct answer:** Create an SDK-style SQL database project, extract schema into `.sql` files, and run `dotnet build`.

**Avoid:** Original Visual Studio database project when cross-platform CI is required. Avoid committing only `.dacpac` when the requirement says editable source files.

### Schema Drift Reconciliation

**Practice exam pattern:** Production hotfix added an approved column directly in the database. Monitoring tool created another table that must be excluded. Need source-control reconciliation and reviewer inspection.

Correct sequence:
1. Compare live database to SQL project.
2. Apply only the approved `Column1` change to the project.
3. Do not apply the monitoring table.
4. Commit and build the project.
5. Generate a deployment script for review.
6. Publish after approval.

**Exam trap:** Extracting the whole live database into the project would also bring unwanted drift into source control.

### CI Validation with Test Database

<table>
<tr><th>Need</th><th>Action</th></tr>
<tr><td>Deploy latest DACPAC to test database</td><td><code>sqlpackage Publish</code></td></tr>
<tr><td>Run C# database integration tests</td><td><code>dotnet test</code></td></tr>
<tr><td>Stop workflow on test failure</td><td>Let <code>dotnet test</code> fail the job.</td></tr>
</table>

### GitHub Environment Secrets for Production

**Practice exam pattern:** Deploy job targets a GitHub environment named `production`. Connection string must be protected and only available to production deployments.

**Correct answer:** Create a GitHub environment secret named `AZURE_SQL_CONNECTION_STRING` in the `production` environment and reference it from the deploy job.

<table>
<tr><th>Secret Type</th><th>Use</th></tr>
<tr><td>Repository secret</td><td>Protected but available broadly within repository workflows.</td></tr>
<tr><td>Environment secret</td><td>Scoped to jobs targeting that environment. Best for production-only credentials.</td></tr>
<tr><td>Repository/environment variable</td><td>Not appropriate for sensitive credentials.</td></tr>
</table>

## DAB Missing Details

### DAB Stored Procedure as GraphQL Mutation

**Practice exam pattern:** Existing stored procedure performs checkout by inserting an order and updating inventory in one transaction. API must pass values through GraphQL and complete changes in one call.

**Correct answer:** A stored-procedure entity with parameter mappings, GraphQL operation mutation, and execute permission.

```json
{
  "entities": {
    "Checkout": {
      "source": {
        "type": "stored-procedure",
        "object": "dbo.Procedure1",
        "parameters": {
          "CustomerID": "@CustomerID",
          "ProductID": "@ProductID",
          "Quantity": "@Quantity"
        }
      },
      "graphql": {
        "operation": "mutation"
      },
      "permissions": [
        { "role": "authenticated", "actions": [ "execute" ] }
      ]
    }
  }
}
```

**Exam trap:** GraphQL query is for read operations. Use mutation when the stored procedure changes data.

### DAB Entity Caching

**Practice exam pattern:** Global cache TTL is 5 seconds. An entity needs one-minute response caching shared across multiple application instances with distributed cache.

<table>
<tr><th>Requirement</th><th>Setting</th></tr>
<tr><td>Cache for one minute</td><td>TTL = 60</td></tr>
<tr><td>Shared across instances</td><td>Cache level = L1L2</td></tr>
<tr><td>Override global TTL</td><td>Configure cache on the entity</td></tr>
</table>

```json
{
  "runtime": {
    "cache": {
      "enabled": true,
      "ttl-seconds": 5
    }
  },
  "entities": {
    "Entity1": {
      "source": "dbo.Entity1",
      "cache": {
        "enabled": true,
        "ttl-seconds": 60,
        "level": "L1L2"
      }
    }
  }
}
```

**Memory:** L1 is local in-memory cache. L1L2 uses local plus distributed cache, suitable for multiple instances.

## Performance and Indexing Missing Details

### Live DMV Selection

<table>
<tr><th>Need</th><th>DMV</th><th>Why</th></tr>
<tr><td>Currently running requests with CPU, logical reads, wait type, wait time, blocking session</td><td><code>sys.dm_exec_requests</code></td><td>Live request-level activity.</td></tr>
<tr><td>Cached aggregate query stats</td><td><code>sys.dm_exec_query_stats</code></td><td>Historical aggregates for cached plans.</td></tr>
<tr><td>Wait-statistic totals</td><td><code>sys.dm_os_wait_stats</code></td><td>Server-level wait totals, not current request list.</td></tr>
<tr><td>Missing-index suggestions</td><td><code>sys.dm_db_missing_index_details</code></td><td>Index recommendations, not active slowdown detail.</td></tr>
</table>

```sql
SELECT
    session_id,
    status,
    command,
    cpu_time,
    logical_reads,
    wait_type,
    wait_time,
    blocking_session_id
FROM sys.dm_exec_requests
WHERE session_id <> @@SPID;
```

### Deadlock Access Order

**Practice exam pattern:** Two procedures update the same two tables in opposite order and fail with error 1205.

**Correct fix:** Make both procedures access objects in the same order while keeping one explicit transaction.

<table>
<tr><th>Option</th><th>Exam Result</th></tr>
<tr><td>Use same table update order</td><td>Correct. Reduces circular wait.</td></tr>
<tr><td>Set DEADLOCK_PRIORITY LOW</td><td>Does not prevent deadlock, only makes session more likely victim.</td></tr>
<tr><td>Set SERIALIZABLE</td><td>Can increase locks and deadlock risk.</td></tr>
<tr><td>Commit after first table</td><td>Breaks atomic transaction requirement.</td></tr>
</table>

### Key Lookup Remedy

**Practice exam pattern:** Query seeks on `IX_Orders_CustomerID` but performs repeated Key Lookup for returned columns. Estimated and actual row counts are similar.

**Correct answer:** Add returned columns as included columns to the existing nonclustered index.

```sql
CREATE NONCLUSTERED INDEX IX_Orders_CustomerID
ON dbo.Orders(CustomerID)
INCLUDE (OrderDate, TotalAmount, ShippingAddress);
```

**Exam trap:** Updating statistics is not the first answer when estimated and actual row counts are already similar.

### Columnstore Practice Scenario

**Practice exam pattern:** A 600-million-row event table has a clustered rowstore primary key for single-row lookups. A dashboard scans 120 million rows and aggregates by customer, severity, and day without using XML payload.

**Correct answer:** Create a nonclustered columnstore index on only the analytical columns.

```sql
CREATE NONCLUSTERED COLUMNSTORE INDEX NCCI_EventLog_Dashboard
ON dbo.EventLog(CreatedAt, CustomerID, Severity, DurationMs);
```

<table>
<tr><th>Why</th><th>Explanation</th></tr>
<tr><td>Preserves EventID lookups</td><td>Existing clustered rowstore primary key remains.</td></tr>
<tr><td>Supports aggregate scans</td><td>Columnstore is optimized for large analytic scans and aggregation.</td></tr>
<tr><td>Avoids XML payload</td><td>Nonclustered columnstore can include selected columns only.</td></tr>
<tr><td>Minimizes app changes</td><td>No need to change query contract.</td></tr>
</table>

### Partitioning Practice Scenario

**Practice exam pattern:** 3-TB `Sales.Orders`, most queries filter by `OrderDate`, 36 months retained, completed months archived by partition switching, use RANGE RIGHT.

**Correct design:** Monthly `OrderDate` partitions, clustered primary key includes partition column, and nonclustered indexes are aligned.

```sql
CREATE PARTITION FUNCTION PF_Orders_OrderDate(date)
AS RANGE RIGHT FOR VALUES
(
    '2026-01-01', '2026-02-01', '2026-03-01'
    -- continue monthly boundaries
);

CREATE PARTITION SCHEME PS_Orders_OrderDate
AS PARTITION PF_Orders_OrderDate
ALL TO ([PRIMARY]);

CREATE TABLE Sales.Orders
(
    OrderID bigint NOT NULL,
    OrderDate date NOT NULL,
    CustomerID int NOT NULL,
    Amount decimal(18,2) NOT NULL,
    CONSTRAINT PK_Orders PRIMARY KEY CLUSTERED (OrderID, OrderDate)
) ON PS_Orders_OrderDate(OrderDate);

CREATE INDEX IX_Orders_Customer
ON Sales.Orders(CustomerID, OrderDate)
ON PS_Orders_OrderDate(OrderDate);
```

**Exam trap:** Quarterly partitions do not allow monthly switching. Nonpartitioned nonclustered indexes are not aligned for partition maintenance.

## Vector, Models, Embeddings, and Search Missing Details

### Vector Storage and Index Design

**Practice exam pattern:** Product catalog has 2 million rows. 768-dimensional and 1,536-dimensional embeddings both meet relevance target. Need reduced storage/cost, reject wrong dimensions, filter by CategoryID and Price, and use indexed cosine search.

**Correct answer:** Use `VECTOR(768)`, structured `CategoryID` and `Price` columns with a B-tree index, and a cosine vector index.

<table>
<tr><th>Design Choice</th><th>Why</th></tr>
<tr><td><code>VECTOR(768)</code></td><td>Smaller dimension meets relevance and reduces storage/distance cost.</td></tr>
<tr><td>Fixed dimension</td><td>Rejects embeddings with unexpected dimension count.</td></tr>
<tr><td>Structured filter columns</td><td>Category and Price are relational filters, not semantic text.</td></tr>
<tr><td>B-tree on filters</td><td>Efficient equality/range filtering.</td></tr>
<tr><td>Cosine vector index</td><td>Common metric for text embeddings.</td></tr>
</table>

### Approximate Vector Search for Large Text Embedding Tables

<table>
<tr><th>Scenario</th><th>Best Answer</th></tr>
<tr><td>Millions of text embeddings, high CPU from scanning all vectors</td><td>Use ANN with <code>VECTOR_SEARCH</code>.</td></tr>
<tr><td>Recall target allows 0.95 rather than perfect recall</td><td>Approximate search is acceptable.</td></tr>
<tr><td>Text embeddings</td><td>Use cosine distance.</td></tr>
<tr><td>Strict exact result on small set</td><td>Use ENN with <code>VECTOR_DISTANCE</code>.</td></tr>
</table>

### External Models in SQL

**Practice exam pattern:** Stored procedures reference existing external model `Model1`. Need to point it to a new Azure OpenAI embeddings deployment, keep procedure definitions unchanged, keep API key out of procedure code/query calls, and grant runtime-only access.

Correct actions:
- Alter the existing external model to use the new deployment endpoint.
- Store API key in a database-scoped credential using `HTTPEndpointHeaders` if managed identity is not configured.
- Grant `EXECUTE ANY EXTERNAL ENDPOINT` to the runtime role.

```sql
CREATE DATABASE SCOPED CREDENTIAL MyEmbeddingCredential
WITH IDENTITY = 'HTTPEndpointHeaders',
SECRET = '{"api-key":"<stored-securely>"}';

ALTER EXTERNAL MODEL Model1
WITH
(
    LOCATION = 'https://my-openai-resource.openai.azure.com/openai/deployments/Deployment1/embeddings?api-version=2024-02-01',
    CREDENTIAL = MyEmbeddingCredential
);

GRANT EXECUTE ANY EXTERNAL ENDPOINT TO Role1;
```

**Exam trap:** Creating a new model requires stored procedure changes. Granting `ALTER ANY EXTERNAL MODEL` is too broad for runtime invocation.

### Structured AI Output vs Embeddings

**Practice exam pattern:** Need AI-generated values for columns such as Category, Priority, and RouteQueue. Prototype used embeddings for similarity search.

**Correct answer:** Invoke a chat endpoint by using `sp_invoke_external_rest_endpoint` and parse the JSON response in T-SQL.

**Why:** Embeddings produce vectors for similarity search, not parseable business column values.

```sql
DECLARE @response nvarchar(max);

EXEC sp_invoke_external_rest_endpoint
    @url = N'https://my-openai-resource.openai.azure.com/openai/deployments/chat/completions?api-version=2024-02-01',
    @method = N'POST',
    @payload = @requestBody,
    @credential = [https://my-openai-resource.openai.azure.com],
    @response = @response OUTPUT;

SELECT
    JSON_VALUE(@response, '$.result.choices[0].message.content') AS ModelOutput;
```

### Embedding Flow for Multi-Paragraph Descriptions

**Practice exam pattern:** Product descriptions contain multiple paragraphs. Need focused embeddings, ability to change chunk size/regenerate without modifying the product table, and SQL vector operations.

**Correct answer:** Use Description, generate chunks, store one vector per chunk in a related embeddings table.

```sql
CREATE TABLE dbo.ProductEmbeddingChunk
(
    ProductID int NOT NULL,
    ChunkID int NOT NULL,
    ChunkText nvarchar(max) NOT NULL,
    Embedding vector(1536) NOT NULL,
    CreatedAt datetime2 NOT NULL DEFAULT SYSUTCDATETIME(),
    CONSTRAINT PK_ProductEmbeddingChunk PRIMARY KEY (ProductID, ChunkID),
    CONSTRAINT FK_ProductEmbeddingChunk_Product FOREIGN KEY (ProductID)
        REFERENCES dbo.Product(ProductID)
);
```

**Exam trap:** Do not store vectors as JSON if SQL vector operations are required.

### Advanced Chunking Strategy

<table>
<tr><th>Document Type</th><th>Best Chunking Strategy</th><th>Why</th></tr>
<tr><td>Product manuals with consistent headings, numbered sections, and citations</td><td>Structural chunking</td><td>Use natural document sections and preserve citations.</td></tr>
<tr><td>Troubleshooting runbooks with multi-page procedures</td><td>Hierarchical chunking</td><td>Supports exact step retrieval plus surrounding procedure context.</td></tr>
<tr><td>Support case narratives with free-form shifting topics</td><td>Semantic chunking</td><td>Finds topic boundaries when document structure is unreliable.</td></tr>
<tr><td>Simple quick baseline</td><td>Fixed-size chunking</td><td>Easy but may split meaning.</td></tr>
<tr><td>Paragraph documents</td><td>Paragraph-based chunking</td><td>Good when paragraph boundaries carry meaning.</td></tr>
</table>

### Embedding Maintenance with Multiple Consumers

**Practice exam pattern:** Thousands of article inserts/updates per hour. Semantic search service and analytics enrichment service must process changes independently, near real time, outside database transaction.

**Correct answer:** Change Event Streaming.

<table>
<tr><th>Method</th><th>Exam Meaning</th></tr>
<tr><td>Triggers</td><td>Immediate but inside transaction path. Adds write latency.</td></tr>
<tr><td>Change Tracking</td><td>Lightweight changed keys, often polled.</td></tr>
<tr><td>CDC</td><td>Detailed change capture, useful for ETL/history.</td></tr>
<tr><td>Change Event Streaming</td><td>Near real-time event stream, decoupled, supports multiple downstream consumers.</td></tr>
</table>

### Hybrid Search Query Pattern

**Practice exam pattern:** Full-text index finds exact terms, natural-language searches miss articles with different wording. Need include results returned by either full-text or vector search, use vector index, and produce one ranking without comparing raw scores to vector distances.

**Correct answer:** `FREETEXTTABLE` + `VECTOR_SEARCH` + `FULL OUTER JOIN` + RRF.

```sql
WITH FullTextRanked AS
(
    SELECT
        ft.[KEY] AS ArticleID,
        ROW_NUMBER() OVER (ORDER BY ft.[RANK] DESC) AS RankFTS
    FROM FREETEXTTABLE(dbo.Article, Body, @SearchText) AS ft
),
VectorRanked AS
(
    SELECT
        vs.ArticleID,
        ROW_NUMBER() OVER (ORDER BY vs.distance ASC) AS RankVector
    FROM VECTOR_SEARCH
    (
        TABLE = dbo.Article,
        COLUMN = BodyVector,
        QUERY_VECTOR = @QueryEmbedding,
        METRIC = 'cosine',
        TOP_N = 100
    ) AS vs
)
SELECT
    COALESCE(f.ArticleID, v.ArticleID) AS ArticleID,
    ISNULL(1.0 / (60 + f.RankFTS), 0.0) +
    ISNULL(1.0 / (60 + v.RankVector), 0.0) AS RRFScore
FROM FullTextRanked AS f
FULL OUTER JOIN VectorRanked AS v
    ON f.ArticleID = v.ArticleID
ORDER BY RRFScore DESC;
```

<table>
<tr><th>Query Choice</th><th>Why</th></tr>
<tr><td><code>FULL OUTER JOIN</code></td><td>Includes articles found by either method.</td></tr>
<tr><td><code>VECTOR_SEARCH</code></td><td>Uses vector index for semantic candidates.</td></tr>
<tr><td>RRF</td><td>Combines rank positions without comparing incompatible raw scores.</td></tr>
<tr><td>Avoid summed raw scores</td><td>Full-text ranks and vector distances are different scoring systems.</td></tr>
</table>

### Full-Text Exact Phrase and Linguistic Matching

**Practice exam pattern:** Return active products where Name contains exact phrase `mountain bike` and Description matches related forms of `ride`, such as riding, rides, rode.

```sql
SELECT ProductID, Name
FROM dbo.Product
WHERE CONTAINS(Name, N'"mountain bike"')
  AND FREETEXT(Description, N'ride')
  AND IsActive = 1;
```

<table>
<tr><th>Requirement</th><th>Predicate</th></tr>
<tr><td>Exact phrase</td><td><code>CONTAINS(Name, N'"mountain bike"')</code></td></tr>
<tr><td>Linguistic matching / related forms</td><td><code>FREETEXT(Description, N'ride')</code></td></tr>
<tr><td>Simple wildcard pattern</td><td><code>LIKE</code>, but not linguistic full-text matching.</td></tr>
</table>

## RAG JSON Missing Details

### Extract Long Assistant Answers from Chat Response

**Practice exam pattern:** Store only the assistant message content from first chat choice. Preserve answers longer than 4,000 characters.

**Correct answer:** Use `OPENJSON` with `nvarchar(max)` in the `WITH` clause.

```sql
DECLARE @answer nvarchar(max);

SELECT @answer = GeneratedAnswer
FROM OPENJSON(@response, '$.result.choices[0]')
WITH
(
    GeneratedAnswer nvarchar(max) '$.message.content'
);

INSERT dbo.RagResponse(RequestId, AnswerText)
VALUES (@requestId, @answer);
```

**Exam trap:** `JSON_VALUE` returns `nvarchar(4000)`, so it can truncate long assistant responses.

### Multi-Row JSON Context with Null Properties

**Practice exam pattern:** Create one JSON array, one object per order row, aliases as property names, include null purchase order numbers.

```sql
DECLARE @context nvarchar(max);

SELECT @context =
(
    SELECT
        o.OrderID AS orderId,
        c.CustomerName AS customerName,
        o.PurchaseOrderNumber AS purchaseOrderNumber,
        o.TotalDue AS totalDue
    FROM dbo.OrderHeader AS o
    INNER JOIN dbo.Customer AS c
        ON o.CustomerID = c.CustomerID
    WHERE o.Status = N'Completed'
    ORDER BY o.OrderID
    FOR JSON PATH, INCLUDE_NULL_VALUES
);

SELECT @context AS RetrievalContext;
```

<table>
<tr><th>Option</th><th>Use</th></tr>
<tr><td><code>FOR JSON PATH</code></td><td>Explicit alias-controlled JSON array.</td></tr>
<tr><td><code>INCLUDE_NULL_VALUES</code></td><td>Includes properties even when value is null.</td></tr>
<tr><td><code>ROOT</code></td><td>Adds wrapper, not needed unless required.</td></tr>
<tr><td><code>WITHOUT_ARRAY_WRAPPER</code></td><td>Use only for single-row object output.</td></tr>
</table>

### Single-Row JSON Context at Top Level

**Practice exam pattern:** Query returns one row using `FOR JSON PATH`, null properties already preserved, downstream parser expects properties at top level rather than an array.

```sql
SELECT
    CustomerID AS customerId,
    CustomerName AS customerName,
    LoyaltyTier AS loyaltyTier
FROM dbo.Customer
WHERE CustomerID = @CustomerID
FOR JSON PATH, INCLUDE_NULL_VALUES, WITHOUT_ARRAY_WRAPPER;
```

**Exam tip:** Default `FOR JSON PATH` output is an array. Add `WITHOUT_ARRAY_WRAPPER` for a single object.

### RAG Use Case Selection

<table>
<tr><th>Feature</th><th>Best Fit?</th><th>Reason</th></tr>
<tr><td>Answer customer questions using current inventory, pricing, and compatibility from Azure SQL</td><td>RAG</td><td>Needs current business facts from database before generation.</td></tr>
<tr><td>Create slogans from fixed brief</td><td>Prompt-only generation</td><td>No retrieval of current data required.</td></tr>
<tr><td>Summarize policy text included in prompt</td><td>Prompt-only summarization</td><td>Context is already supplied.</td></tr>
<tr><td>Explain syntax from included documentation</td><td>Prompt-only if docs are supplied</td><td>No database retrieval required.</td></tr>
</table>

## Advanced T-SQL and Programmability Missing Details

### OPENJSON Array Expansion with Scalar Extraction

**Practice exam pattern:** JSON payload has scalar order status and customer ID, plus `items` array. Return one row per item for closed orders.

```sql
SELECT
    mo.OrderID,
    JSON_VALUE(mo.Payload, '$.customer.id') AS CustomerID,
    item.Sku,
    item.Quantity
FROM dbo.MobileOrders AS mo
CROSS APPLY OPENJSON(mo.Payload, '$.items')
WITH
(
    Sku nvarchar(50) '$.sku',
    Quantity int '$.qty'
) AS item
WHERE JSON_VALUE(mo.Payload, '$.orderStatus') = N'Closed';
```

**Exam tip:** Use `JSON_VALUE` for scalar root values and `CROSS APPLY OPENJSON` to expand arrays into rows.

### Recursive CTE for Hierarchy with Depth

```sql
WITH EmployeeHierarchy AS
(
    SELECT
        EmployeeID,
        ManagerID,
        DisplayName,
        0 AS Depth
    FROM dbo.Employee
    WHERE ManagerID IS NULL

    UNION ALL

    SELECT
        e.EmployeeID,
        e.ManagerID,
        e.DisplayName,
        h.Depth + 1 AS Depth
    FROM dbo.Employee AS e
    INNER JOIN EmployeeHierarchy AS h
        ON e.ManagerID = h.EmployeeID
)
SELECT EmployeeID, ManagerID, DisplayName, Depth
FROM EmployeeHierarchy;
```

**Exam trap:** The recursive join is child.ManagerID = parent.EmployeeID. Reversing it walks the hierarchy incorrectly.

### Window Function Named Window and Default Values

```sql
SELECT
    DeviceId,
    ReadingId,
    ReadingTime,
    Temperature,
    LAG(Temperature, 1, Temperature) OVER SensorWindow AS PreviousTemperature,
    LEAD(Temperature, 1, Temperature) OVER SensorWindow AS NextTemperature
FROM dbo.SensorReadings
WINDOW SensorWindow AS
(
    PARTITION BY DeviceId
    ORDER BY ReadingTime, ReadingId
);
```

<table>
<tr><th>Clause</th><th>Purpose</th></tr>
<tr><td><code>PARTITION BY DeviceId</code></td><td>Compare only within the same device.</td></tr>
<tr><td><code>ORDER BY ReadingTime, ReadingId</code></td><td>Defines chronological sequence and tie-breaker.</td></tr>
<tr><td>Third argument in <code>LAG/LEAD</code></td><td>Default value when adjacent row does not exist.</td></tr>
</table>

### Fuzzy Matching Candidate Reduction

**Practice exam pattern:** Product names can contain typos. Need names at least 70 percent similar to search term and reduce rows evaluated by fuzzy function.

```sql
SELECT ProductID, Name
FROM dbo.Products
WHERE CategoryID = @CategoryID
  AND IsActive = 1
  AND EDIT_DISTANCE_SIMILARITY(Name, @SearchTerm) >= 70;
```

**Exam tip:** Apply indexed relational filters first, then fuzzy matching. `EDIT_DISTANCE_SIMILARITY` returns a 0-to-100 score. `EDIT_DISTANCE` returns a distance, not a similarity percentage.

### REGEXP_SUBSTR Capture Group Extraction

**Practice exam pattern:** Message text contains codes like `SKU: AB-1234` or `sku: cd-5678`. Return only the code after the SKU prefix, case-insensitive, NULL if not found.

```sql
SELECT
    REGEXP_SUBSTR
    (
        MessageText,
        'sku:\s*([A-Z]{2}-[0-9]{4})',
        1,
        1,
        'i',
        1
    ) AS Code
FROM dbo.ProductMessages;
```

**Exam tip:** `REGEXP_INSTR` returns a position. `REGEXP_SUBSTR` returns the matching text. Use capture group 1 to avoid returning the SKU prefix.

### Constraints: CHECK vs DEFAULT

```sql
CREATE TABLE dbo.ReviewQueue
(
    ReviewID int IDENTITY(1,1) CONSTRAINT PK_ReviewQueue PRIMARY KEY,
    ProductID int NOT NULL,
    ReviewText nvarchar(1000) NOT NULL,
    Rating tinyint NOT NULL CONSTRAINT ReviewQueue_RatingRule
        CHECK (Rating BETWEEN 1 AND 5),
    HelpfulVotes int NOT NULL CONSTRAINT ReviewQueue_HelpfulVotesDefault
        DEFAULT (0)
);
```

<table>
<tr><th>Requirement</th><th>Constraint</th></tr>
<tr><td>Reject invalid rating outside 1-5</td><td>CHECK constraint</td></tr>
<tr><td>Populate omitted helpful-vote count during bulk import</td><td>DEFAULT constraint</td></tr>
<tr><td>Validate supplied helpful vote count is nonnegative</td><td>Optional CHECK, but does not populate omitted values.</td></tr>
</table>

### Stored Procedure Output Parameter Contract

**Practice exam pattern:** Service expects item rows as one result set and item count as scalar after procedure exits. If input is NULL, return empty result set and count 0.

```sql
CREATE OR ALTER PROCEDURE dbo.uspGetOrderItems
    @OrderID int,
    @ItemCount int OUTPUT
AS
BEGIN
    SET NOCOUNT ON;

    SET @ItemCount = 0;

    IF @OrderID IS NULL
    BEGIN
        SELECT OrderItemID, OrderID, ProductID, Quantity
        FROM dbo.OrderItems
        WHERE 1 = 0;
        RETURN;
    END;

    SELECT @ItemCount = COUNT(*)
    FROM dbo.OrderItems
    WHERE OrderID = @OrderID;

    SELECT OrderItemID, OrderID, ProductID, Quantity
    FROM dbo.OrderItems
    WHERE OrderID = @OrderID;
END;
```

**Exam trap:** Return codes are for execution status, not application data. Initialize output parameters on every execution path.

### AFTER Trigger with inserted Pseudo Table

```sql
CREATE OR ALTER TRIGGER Sales.tr_ValidateOrderCustomer
ON Sales.Orders
AFTER INSERT, UPDATE
AS
BEGIN
    SET NOCOUNT ON;

    IF (ROWCOUNT_BIG() = 0)
        RETURN;

    IF EXISTS
    (
        SELECT 1
        FROM inserted AS i
        INNER JOIN Sales.Customers AS c
            ON c.CustomerID = i.CustomerID
        WHERE c.AccountStatus = N'Blocked'
    )
    BEGIN
        THROW 50001, 'Blocked customer', 1;
    END;
END;
```

<table>
<tr><th>Choice</th><th>Reason</th></tr>
<tr><td>AFTER INSERT, UPDATE</td><td>Preserves original DML unless validation fails.</td></tr>
<tr><td><code>inserted</code></td><td>Contains new or changed rows only.</td></tr>
<tr><td><code>deleted</code></td><td>Old values, not suitable for validating new customer status.</td></tr>
<tr><td>INSTEAD OF trigger</td><td>Would replace original operation, not preserve it automatically.</td></tr>
</table>

### Inline TVF with CROSS APPLY

```sql
CREATE FUNCTION Sales.GetCustomerOrders
(
    @CustomerID int,
    @MinimumTotal decimal(18,2)
)
RETURNS TABLE
AS
RETURN
(
    SELECT OrderID, CustomerID, OrderDate, TotalAmount, Status
    FROM Sales.Orders
    WHERE CustomerID = @CustomerID
      AND TotalAmount >= @MinimumTotal
);
GO

SELECT
    c.CustomerName,
    o.OrderID,
    o.TotalAmount
FROM Sales.Customers AS c
CROSS APPLY Sales.GetCustomerOrders(c.CustomerID, 1000.00) AS o;
```

<table>
<tr><th>Requirement</th><th>Answer</th></tr>
<tr><td>Accept parameters and return a rowset</td><td>Inline table-valued function</td></tr>
<tr><td>Pass each customer row into function</td><td>CROSS APPLY</td></tr>
<tr><td>Retain customers with no matching orders</td><td>OUTER APPLY, if required</td></tr>
<tr><td>Avoid return table variable</td><td>Inline TVF, not multi-statement TVF</td></tr>
</table>

### Scalar Function for Reusable Expression

**Practice exam pattern:** Repeated calculation returns one `DECIMAL(12,2)` value and must be referenced directly in SELECT lists and WHERE predicates.

```sql
CREATE FUNCTION Sales.fnNetAmount
(
    @LineAmount decimal(12,2),
    @DiscountPct decimal(5,4)
)
RETURNS decimal(12,2)
AS
BEGIN
    RETURN CAST(@LineAmount * (1 - @DiscountPct) AS decimal(12,2));
END;
```

**Exam tip:** Use a scalar function for one reusable value. Use inline TVF for rowsets. Stored procedures are not directly embeddable in expressions.

## Graph Table Query Patterns

### Variable-Length Graph Traversal with SHORTEST_PATH

**Practice exam pattern:** Graph tables `Person` as node and `Knows` as directed edge. Starting from Person1, follow outgoing relationships. Return people reachable in one to three hops and minimum hop count.

```sql
SELECT
    StartPerson.Name AS StartPerson,
    LAST_VALUE(ReachablePerson.Name) WITHIN GROUP (GRAPH PATH) AS ReachablePerson,
    COUNT(ReachablePerson.Name) WITHIN GROUP (GRAPH PATH) AS Distance
FROM dbo.Person AS StartPerson,
     dbo.Knows FOR PATH AS k,
     dbo.Person FOR PATH AS ReachablePerson
WHERE MATCH
(
    SHORTEST_PATH(StartPerson(-(k)->ReachablePerson){1,3})
)
AND StartPerson.Name = N'Person1';
```

<table>
<tr><th>Syntax</th><th>Purpose</th></tr>
<tr><td><code>FOR PATH</code></td><td>Required for aliases participating in variable-length graph traversal.</td></tr>
<tr><td><code>SHORTEST_PATH</code></td><td>Returns minimum path within the specified hop range.</td></tr>
<tr><td><code>{1,3}</code></td><td>One to three hops.</td></tr>
<tr><td><code>WITHIN GROUP (GRAPH PATH)</code></td><td>Aggregates values along the graph path.</td></tr>
</table>

### Specialized Table Selection from Practice Exam

<table>
<tr><th>Requirement</th><th>Best Table Type</th><th>Why</th></tr>
<tr><td>Provenance events must be tamper-evident and immutable after insert</td><td>Append-only ledger table</td><td>Insert-only plus tamper evidence.</td></tr>
<tr><td>Historical sensor data remains as shared Parquet files in Azure Data Lake Storage</td><td>External table</td><td>Query in place without duplicating data.</td></tr>
<tr><td>Supplier/product/warehouse/carrier relationships need multi-hop traversal</td><td>Graph node and edge tables</td><td>Designed for relationship traversal.</td></tr>
<tr><td>Track row history only</td><td>Temporal table</td><td>History, not tamper-evidence/immutability.</td></tr>
<tr><td>High-performance OLTP</td><td>Memory-optimized table</td><td>Performance, not ledger/external/graph.</td></tr>
</table>

## AI-Assisted Tooling Missing Details

### Fabric Data Warehouse MCP Endpoint Scope

**Practice exam pattern:** Developer configures Fabric Data Warehouse MCP server endpoint for GitHub Copilot and does not want to specify warehouse context in every chat session.

**Correct answer:** Use an item-scoped Fabric Data Warehouse MCP endpoint.

<table>
<tr><th>Endpoint Scope</th><th>Exam Use</th></tr>
<tr><td>Item-scoped Fabric Data Warehouse MCP endpoint</td><td>Binds to a specific warehouse item.</td></tr>
<tr><td>Global Fabric Data Warehouse endpoint</td><td>Requires warehouse context separately.</td></tr>
<tr><td>SQL MCP Server endpoint for Azure SQL</td><td>Use for SQL Server/Azure SQL, not Fabric warehouse item context.</td></tr>
<tr><td>Fabric lakehouse MCP endpoint</td><td>Lakehouse scenario, not warehouse endpoint.</td></tr>
</table>

### MCP Least-Privilege Development Configuration

**Practice exam pattern:** Developers use GitHub Copilot Agent mode with committed `.vscode/mcp.json`. They only need object names, columns, and relationships. Development has masked sample data; production has customer data.

Correct configuration:
- Use the development endpoint.
- Authenticate with signed-in developer identity, not reusable secrets in the repository.
- Grant metadata-only permissions.

<table>
<tr><th>Requirement</th><th>Best Choice</th></tr>
<tr><td>Nonproduction context</td><td>Development MCP endpoint with masked sample data.</td></tr>
<tr><td>Attributable access</td><td>Browser sign-in / Microsoft Entra user context.</td></tr>
<tr><td>No reusable secrets in repo</td><td>Avoid connection strings and tokens in committed config.</td></tr>
<tr><td>Only object discovery</td><td>Metadata-only permissions.</td></tr>
</table>

### GitHub Copilot Instructions for Secure SQL Code

```markdown
# Repository Copilot Instructions

- Bind external values as SQL parameters in all generated data-access code.
- Do not concatenate user input into SQL command text.
- Require pull-request workflows to complete security scans before merge.
- Generated SQL changes must be reviewed through pull requests.
- Avoid secrets, connection strings, and customer data in prompts or generated examples.
```

**Exam trap:** Input validation alone is not enough to prevent SQL injection. Parameterization directly addresses SQL injection risk.

### SSMS 22 GitHub Copilot Chat Azure Custom Model

**Practice exam pattern:** Organization has an approved Azure OpenAI deployment for SQL refactoring prompts. Need to add approved deployment to Copilot Chat and keep built-in Copilot models available.

**Correct answer:** Add an Azure custom model that uses:
- Azure OpenAI deployment name as the Model ID.
- Azure OpenAI resource endpoint URL as the endpoint.

<table>
<tr><th>Field</th><th>Correct Value</th></tr>
<tr><td>Provider</td><td>Azure custom model</td></tr>
<tr><td>Model ID</td><td>Azure OpenAI deployment name, not base model name</td></tr>
<tr><td>Endpoint</td><td>Azure OpenAI resource endpoint URL, not resource group name</td></tr>
</table>

## Extra Practice Questions Added from Screenshot Gaps

### Security and DAB
- A tenant app uses RLS and must stop inserts for another tenant. What predicates are required? **Answer:** Filter predicate plus block predicates after insert and after update.
- A GraphQL endpoint must hide `InternalNotes` and `CostPrice`. What should you configure? **Answer:** Authenticated read action with `fields.exclude`.
- DAB cache must be shared across instances for 60 seconds. What settings? **Answer:** TTL 60 and cache level L1L2.
- Azure App Service must move to passwordless SQL access and minimize manual setup. What should you use? **Answer:** Service Connector with system-assigned managed identity.

### CI/CD
- Before editing a table file on main, what git command isolates the change? **Answer:** `git checkout -b feature/add-column1`.
- How do you make the branch available for pull request review? **Answer:** `git push origin feature/add-column1`.
- How do you deploy a built DACPAC to test before C# database tests? **Answer:** `sqlpackage Publish`, then `dotnet test`.
- A production hotfix should be kept but a monitoring table excluded. What should you do? **Answer:** Compare database to project, apply only the approved change to the project, commit, build, generate script, publish after approval.

### Performance
- Which DMV shows currently executing requests with waits and blocking session ID? **Answer:** `sys.dm_exec_requests`.
- A Key Lookup repeats many times after an index seek. What should you add? **Answer:** INCLUDE columns for returned columns.
- Two procedures update the same two tables in opposite order and deadlock. What reduces recurrence? **Answer:** Make object access order consistent.
- Large aggregates need speed while preserving clustered rowstore lookups. What index? **Answer:** Nonclustered columnstore index on analytical columns.

### AI, Search, and RAG
- Millions of text embeddings cause high CPU with `VECTOR_DISTANCE`. Recall target is 0.95. What should you use? **Answer:** ANN with `VECTOR_SEARCH` and cosine distance.
- Need exact keyword plus semantic results and one ranking. What pattern? **Answer:** `FREETEXTTABLE` + `VECTOR_SEARCH` + `FULL OUTER JOIN` + RRF.
- Chat response may exceed 4,000 characters. How should you extract first answer? **Answer:** `OPENJSON` with `nvarchar(max)` in the `WITH` clause.
- Single-row JSON must be top-level object. What option? **Answer:** `WITHOUT_ARRAY_WRAPPER`.
- Multi-row JSON context must include null values. What option? **Answer:** `FOR JSON PATH, INCLUDE_NULL_VALUES`.

### Advanced T-SQL and Graph
- Need one row per item from JSON array and scalar customer ID from root. What pattern? **Answer:** `JSON_VALUE` plus `CROSS APPLY OPENJSON`.
- Need all hierarchy levels with depth from top-level employees. What pattern? **Answer:** Recursive CTE starting where `ManagerID IS NULL` and joining child `ManagerID` to parent `EmployeeID`.
- Need one-to-three-hop graph traversal and minimum hop count. What graph syntax? **Answer:** `FOR PATH`, `SHORTEST_PATH`, and `WITHIN GROUP (GRAPH PATH)`.
- Need reusable parameterized rowset without return table variable. What object? **Answer:** Inline TVF; use `CROSS APPLY` when passing each outer row.

## Updated Must-Memorize Facts from Practice Exam

- RLS filter predicates control row visibility; block predicates control whether writes are allowed.
- For tenant enforcement, use filter predicate plus AFTER INSERT and AFTER UPDATE block predicates.
- Service Connector can automate managed identity, connection string, database user, and role setup for passwordless Azure SQL access.
- Azure RBAC permissions such as SQL DB Contributor do not grant SQL data access inside the database.
- Server-level Azure SQL auditing covers future databases on the logical server.
- Use Log Analytics when the requirement mentions KQL queries and alert rules.
- DAB GraphQL field security uses role actions with `fields.exclude`.
- DAB stored procedures that change data should be exposed as GraphQL mutations with execute permission.
- DAB L1L2 cache is used when cached responses must be shared across multiple instances.
- GitHub environment secrets are best for production-only deployment credentials.
- Schema drift reconciliation should bring only approved live changes back into the SQL project.
- `sqlpackage Publish` deploys a DACPAC; `dotnet test` runs C# tests.
- `sys.dm_exec_requests` is the live request DMV.
- Repeated Key Lookup after a good seek usually means the index needs INCLUDE columns.
- Deadlock recurrence is reduced by consistent object access order.
- Nonclustered columnstore can accelerate analytics while preserving rowstore primary-key lookups.
- Monthly partitioning is required when completed months are switched individually.
- Aligned indexes use the same partition scheme as the table.
- Prefer the smaller embedding dimension if relevance is equivalent.
- Fixed `VECTOR(n)` rejects embeddings with unexpected dimension count.
- Use structured columns and B-tree indexes for filters such as CategoryID and Price.
- Use cosine distance for most text embeddings.
- `VECTOR_SEARCH` uses vector index candidates; `VECTOR_DISTANCE` over all rows is exact scanning logic.
- RRF combines rank positions, not raw scores.
- Use `OPENJSON` with `nvarchar(max)` to extract long LLM answer content.
- `FOR JSON PATH, INCLUDE_NULL_VALUES` preserves null properties in multi-row JSON context.
- `WITHOUT_ARRAY_WRAPPER` returns a single JSON object for one-row context.
- Structural chunking follows document headings/sections.
- Hierarchical chunking supports exact child chunks plus broader parent context.
- Semantic chunking is strongest when text is free-form and topic boundaries are unclear.
- Change Event Streaming fits near-real-time, decoupled, multi-consumer embedding maintenance.
- `REGEXP_SUBSTR` extracts a match; `REGEXP_INSTR` returns a position.
- `EDIT_DISTANCE_SIMILARITY` returns a 0-to-100 similarity score.
- `SHORTEST_PATH` and `FOR PATH` are key graph query syntax for variable-length traversal.
- Inline TVFs return composable parameterized rowsets without a return table variable.
- Scalar functions return one value for expressions and predicates.
- Output parameters must be initialized and assigned on all stored procedure paths.
- Triggers should use `inserted` to validate new or changed rows in INSERT/UPDATE triggers.
- Item-scoped Fabric Data Warehouse MCP endpoints avoid repeatedly specifying warehouse context.
- For routine Copilot/MCP development, use nonproduction endpoints and metadata-only permissions.
- Azure custom model setup in SSMS uses Azure OpenAI deployment name as Model ID and the Azure OpenAI endpoint URL.


---

## Scenario Decision Expansion Pack - Usage, Selection, and Exam Traps

**Why this section was added:** The practice exam style is not only asking for syntax. It repeatedly asks you to choose the right database object, T-SQL object, security feature, performance tool, DAB configuration, AI model pattern, or RAG JSON pattern from a scenario. This section adds the missing **description, when to use, when not to use, common exam wording, and wrong-answer traps** across the study guide.

**How to use this section:** For last-minute revision, read each matrix as a decision engine. For each feature, remember:

1. What problem it solves.
2. What keyword in the question points to it.
3. What similar feature is a trap.
4. What implementation detail Microsoft expects.

---

# A. Database Object Selection - Detailed Usage Guide

## A1. Table Type Decision Matrix

<table>
<tr><th>Feature</th><th>Description</th><th>Use When</th><th>Do Not Use When</th><th>Exam Keywords</th><th>Common Trap</th></tr>
<tr><td>Regular rowstore table</td><td>Default relational table storage for OLTP workloads.</td><td>Transactional inserts, updates, point lookups, normalized application data.</td><td>Large analytical scans are the primary workload.</td><td>OLTP, frequent updates, single-row lookup.</td><td>Choosing columnstore for high-frequency OLTP updates.</td></tr>
<tr><td>Memory-optimized table</td><td>In-memory OLTP table for very low latency and high concurrency.</td><td>Latch/lock contention, high-throughput transactional workloads, session state.</td><td>General reporting or large scan analytics are the main requirement.</td><td>Low latency, high concurrency, In-Memory OLTP.</td><td>Using it to solve audit, history, or tamper-evidence requirements.</td></tr>
<tr><td>Temporal table</td><td>System-versioned table that automatically stores row history.</td><td>Need previous row versions, point-in-time query, accidental data recovery.</td><td>Need cryptographic proof that data was not tampered with.</td><td>History, as of time, point-in-time, previous versions.</td><td>Confusing temporal with ledger.</td></tr>
<tr><td>Ledger table</td><td>Tamper-evident table that supports cryptographic verification.</td><td>Need proof that records have not been changed without detection.</td><td>Only need normal historical reporting.</td><td>Tamper-evident, cryptographic proof, immutable evidence.</td><td>Choosing temporal when the requirement says prove no tampering.</td></tr>
<tr><td>Append-only ledger table</td><td>Ledger table that allows inserts only and prevents updates/deletes.</td><td>Provenance events, transaction journal, compliance log that must be immutable after insert.</td><td>Rows must be updated while retaining history.</td><td>Insert-only, immutable after insert, provenance events.</td><td>Choosing updatable ledger when updates are not allowed.</td></tr>
<tr><td>External table</td><td>Database object that queries external files/data without loading into internal tables.</td><td>Query Parquet/CSV/lake files in place.</td><td>Need high-frequency OLTP writes into the table.</td><td>External storage, data lake, Parquet, query in place.</td><td>Importing data when the requirement says leave files in storage.</td></tr>
<tr><td>Graph node and edge tables</td><td>Tables designed to model entities and relationships for graph traversal.</td><td>Multi-hop relationship traversal, social networks, fraud rings, supply-chain relationships.</td><td>Simple parent-child lookup or normal reporting is enough.</td><td>Node, edge, relationship path, multi-hop, MATCH.</td><td>Using many join tables when graph traversal is the core requirement.</td></tr>
<tr><td>Partitioned table</td><td>Table split into partitions by a partition function and scheme.</td><td>Large tables with date retention, partition elimination, partition switching, partition-level maintenance.</td><td>Small tables or queries do not filter by partition column.</td><td>Monthly archive, partition switch, large table, date range.</td><td>Using quarterly partitions when monthly switching is required.</td></tr>
</table>

### Table Type Decision Tree

```text
Need row history?
  -> Temporal table

Need tamper evidence?
  -> Ledger table
     -> Insert-only immutable events?
        -> Append-only ledger table

Need query files in Data Lake without loading?
  -> External table

Need relationship traversal across multiple hops?
  -> Graph node and edge tables

Need ultra-low-latency OLTP?
  -> Memory-optimized table

Need archive/switch/manage huge date-based table?
  -> Partitioned table
```

---

## A2. Data Type Selection - Scenario Usage

<table>
<tr><th>Requirement</th><th>Best Data Type</th><th>Reason</th><th>Trap</th></tr>
<tr><td>Exact financial amount</td><td>DECIMAL / NUMERIC</td><td>Exact precision and scale.</td><td>FLOAT is approximate and unsuitable for exact money.</td></tr>
<tr><td>Scientific approximation</td><td>FLOAT / REAL</td><td>Approximate numeric calculations.</td><td>Using DECIMAL when approximate range is more important.</td></tr>
<tr><td>Boolean flag</td><td>BIT</td><td>Stores 0, 1, or NULL.</td><td>Using VARCHAR for yes/no values.</td></tr>
<tr><td>Multilingual text</td><td>NVARCHAR</td><td>Unicode support.</td><td>Using VARCHAR when multilingual data is required.</td></tr>
<tr><td>Large JSON document</td><td>NVARCHAR(MAX)</td><td>SQL JSON functions operate on text JSON.</td><td>Storing JSON as XML or VARBINARY.</td></tr>
<tr><td>Embedding vector</td><td>VECTOR(n)</td><td>Native vector storage and vector operations.</td><td>Using JSON array if SQL vector search is required.</td></tr>
<tr><td>Distributed unique ID</td><td>UNIQUEIDENTIFIER</td><td>Globally unique identifiers.</td><td>Random GUIDs can fragment indexes; consider sequential GUIDs where appropriate.</td></tr>
<tr><td>Date/time with precision</td><td>DATETIME2</td><td>Preferred modern date/time type.</td><td>Using legacy DATETIME by default.</td></tr>
<tr><td>Date/time with offset</td><td>DATETIMEOFFSET</td><td>Preserves time zone offset.</td><td>Using DATETIME2 when offset is required.</td></tr>
<tr><td>Binary file or encrypted payload</td><td>VARBINARY(MAX)</td><td>Stores binary large objects.</td><td>Using VARCHAR/NVARCHAR for binary content.</td></tr>
</table>

---

# B. Programmability Objects - Functions, Procedures, Views, and Triggers

## B1. Function Types - Description, Usage, and Selection

### Scalar Function

**Description:** A user-defined function that returns exactly one scalar value such as `int`, `decimal`, `bit`, `date`, or `nvarchar`.

**Use when:**

- You need a reusable calculation.
- The result is one value.
- It must be referenced directly in a SELECT list, WHERE predicate, computed expression, or CHECK-like logic.

**Common scenario wording:**

> Repeatedly calculate a net amount and use it in SELECT lists and WHERE predicates.

**Example:**

```sql
CREATE FUNCTION Sales.fnNetAmount
(
    @LineAmount decimal(12,2),
    @DiscountPct decimal(5,4)
)
RETURNS decimal(12,2)
AS
BEGIN
    RETURN CAST(@LineAmount * (1 - @DiscountPct) AS decimal(12,2));
END;
GO

SELECT OrderLineID
FROM Sales.OrderLine
WHERE Sales.fnNetAmount(LineAmount, DiscountPct) > 1000.00;
```

**Do not choose scalar function when:**

- You must return multiple rows or columns.
- You need a rowset source for JOIN/APPLY.
- The question asks for a parameterized table result.

---

### Inline Table-Valued Function

**Description:** A function that returns a table using a single SELECT statement. It does not declare a return table variable.

**Use when:**

- You need reusable, parameterized rowset logic.
- The rowset must be used in queries and joins.
- The requirement says avoid declaring a return table variable.
- You need to pass values from each outer row by using `CROSS APPLY` or `OUTER APPLY`.

**Common scenario wording:**

> Accept a customer ID and minimum total, return orders as a rowset, and pass each customer row's ID to the reusable logic.

**Example:**

```sql
CREATE FUNCTION Sales.GetCustomerOrders
(
    @CustomerID int,
    @MinimumTotal decimal(18,2)
)
RETURNS TABLE
AS
RETURN
(
    SELECT OrderID, CustomerID, OrderDate, TotalAmount, Status
    FROM Sales.Orders
    WHERE CustomerID = @CustomerID
      AND TotalAmount >= @MinimumTotal
);
GO

SELECT c.CustomerName, o.OrderID, o.TotalAmount
FROM Sales.Customers AS c
CROSS APPLY Sales.GetCustomerOrders(c.CustomerID, 1000.00) AS o;
```

**Use `CROSS APPLY` when:** return only outer rows that produce function rows.

**Use `OUTER APPLY` when:** keep outer rows even if the function returns no rows.

**Do not choose inline TVF when:**

- You need multiple procedural statements before returning data.
- You need to return one scalar value only.
- You need to perform data modifications.

---

### Multi-Statement Table-Valued Function

**Description:** A function that declares a table variable, runs multiple statements, inserts into the return table, and returns it.

**Use when:**

- You must return a table and the logic cannot be expressed as one SELECT.
- You require procedural steps before returning a rowset.

**Example:**

```sql
CREATE FUNCTION Sales.GetOrderSummary(@CustomerID int)
RETURNS @Result TABLE
(
    CustomerID int,
    TotalOrders int,
    TotalAmount decimal(18,2)
)
AS
BEGIN
    INSERT INTO @Result(CustomerID, TotalOrders, TotalAmount)
    SELECT CustomerID, COUNT(*), SUM(TotalAmount)
    FROM Sales.Orders
    WHERE CustomerID = @CustomerID
    GROUP BY CustomerID;

    RETURN;
END;
```

**Exam trap:** If the requirement says **avoid declaring a return table variable**, choose an inline TVF, not a multi-statement TVF.

---

### Function Selection Matrix

<table>
<tr><th>Requirement</th><th>Best Object</th><th>Why</th><th>Avoid</th></tr>
<tr><td>Return one calculated value</td><td>Scalar function</td><td>Can be used in expressions and predicates.</td><td>Stored procedure or TVF.</td></tr>
<tr><td>Return parameterized rowset with one SELECT</td><td>Inline TVF</td><td>Composable in queries and joins.</td><td>Stored procedure.</td></tr>
<tr><td>Pass each outer row into reusable rowset logic</td><td>Inline TVF with CROSS APPLY</td><td>Applies function per outer row.</td><td>INNER JOIN without APPLY.</td></tr>
<tr><td>Keep outer rows when reusable rowset returns nothing</td><td>Inline TVF with OUTER APPLY</td><td>Preserves unmatched outer rows.</td><td>CROSS APPLY.</td></tr>
<tr><td>Need multiple statements and return table</td><td>Multi-statement TVF</td><td>Allows procedural logic and return table variable.</td><td>Inline TVF if logic cannot fit one SELECT.</td></tr>
<tr><td>Need to modify data</td><td>Stored procedure</td><td>Functions cannot generally perform DML side effects.</td><td>Function.</td></tr>
</table>

---

## B2. Stored Procedures - Details and Usage

**Description:** A programmable database object that encapsulates one or more T-SQL statements and can return result sets, output parameters, and return codes.

**Use when:**

- You need to perform inserts, updates, deletes, or transactional workflows.
- You need to return one or more result sets to an application.
- You need output parameters for scalar data.
- You need to expose a database operation through DAB as an execute/mutation operation.

### Result Set vs Output Parameter vs Return Code

<table>
<tr><th>Need</th><th>Use</th><th>Example Scenario</th><th>Trap</th></tr>
<tr><td>Return rows to application</td><td>SELECT result set</td><td>Return order item rows.</td><td>Using output parameter for many rows.</td></tr>
<tr><td>Return scalar data after procedure exits</td><td>OUTPUT parameter</td><td>Return item count alongside rowset.</td><td>Using return code for business data.</td></tr>
<tr><td>Return execution status</td><td>RETURN code</td><td>0 for success, nonzero for failure.</td><td>Using return code for count/amount.</td></tr>
<tr><td>Atomic multi-table change</td><td>Stored procedure with explicit transaction</td><td>Checkout inserts order and updates inventory.</td><td>Splitting commits when atomicity is required.</td></tr>
</table>

### Output Parameter Pattern

```sql
CREATE OR ALTER PROCEDURE dbo.uspGetOrderItems
    @OrderID int,
    @ItemCount int OUTPUT
AS
BEGIN
    SET NOCOUNT ON;

    SET @ItemCount = 0;

    IF @OrderID IS NULL
    BEGIN
        SELECT OrderItemID, OrderID, ProductID, Quantity
        FROM dbo.OrderItems
        WHERE 1 = 0;
        RETURN;
    END;

    SELECT @ItemCount = COUNT(*)
    FROM dbo.OrderItems
    WHERE OrderID = @OrderID;

    SELECT OrderItemID, OrderID, ProductID, Quantity
    FROM dbo.OrderItems
    WHERE OrderID = @OrderID;
END;
```

**Exam trap:** Initialize output parameters on every code path.

---

## B3. Views - Details and Usage

### Standard View

**Description:** A saved SELECT statement that exposes a reusable logical projection of data.

**Use when:**

- You need to simplify complex joins.
- You need to expose only selected columns.
- You need a security boundary for read access.
- You do not need parameters.

**Do not use when:**

- You need input parameters. Use an inline TVF instead.
- You need to execute procedural logic. Use a stored procedure.

### Indexed View

**Description:** A view whose result is physically materialized by creating a unique clustered index on the view.

**Use when:**

- A repeated aggregate query is expensive.
- Data changes are less frequent than reads.
- The query pattern is stable.

**Do not use when:**

- The base tables have very high write volume and view maintenance cost would hurt performance.
- The logic changes frequently.

---

## B4. Trigger Types - Description, Usage, and Selection

### AFTER Trigger

**Description:** Runs after the triggering INSERT, UPDATE, or DELETE statement completes, but before the transaction commits.

**Use when:**

- Audit changes.
- Validate business rules while preserving the original operation unless validation fails.
- Maintain related data after DML.

**Example:**

```sql
CREATE OR ALTER TRIGGER Sales.tr_ValidateOrderCustomer
ON Sales.Orders
AFTER INSERT, UPDATE
AS
BEGIN
    SET NOCOUNT ON;

    IF (ROWCOUNT_BIG() = 0)
        RETURN;

    IF EXISTS
    (
        SELECT 1
        FROM inserted AS i
        INNER JOIN Sales.Customers AS c
            ON c.CustomerID = i.CustomerID
        WHERE c.AccountStatus = N'Blocked'
    )
    BEGIN
        THROW 50001, 'Blocked customer', 1;
    END;
END;
```

**Exam keywords:** after insert/update, preserve original operation unless validation fails, evaluate affected rows only.

---

### INSTEAD OF Trigger

**Description:** Runs instead of the original INSERT, UPDATE, or DELETE action.

**Use when:**

- You need to replace the default DML behavior.
- You need to make a complex view updatable.
- You need custom logic that controls how writes are applied.

**Do not use when:**

- The requirement says preserve the original insert/update/delete operation unless validation fails. Use AFTER trigger instead.

---

### inserted and deleted Pseudo-Tables

<table>
<tr><th>DML Operation</th><th>inserted Contains</th><th>deleted Contains</th><th>Typical Usage</th></tr>
<tr><td>INSERT</td><td>New rows</td><td>No rows</td><td>Validate or audit inserted values.</td></tr>
<tr><td>DELETE</td><td>No rows</td><td>Old rows</td><td>Audit deleted values.</td></tr>
<tr><td>UPDATE</td><td>New values</td><td>Old values</td><td>Compare before and after values.</td></tr>
</table>

### Trigger Selection Matrix

<table>
<tr><th>Requirement</th><th>Best Trigger/Object</th><th>Why</th><th>Trap</th></tr>
<tr><td>Audit inserted rows</td><td>AFTER INSERT trigger</td><td>Original row exists and can be audited.</td><td>Using INSTEAD OF and forgetting to insert.</td></tr>
<tr><td>Audit old and new values on update</td><td>AFTER UPDATE trigger using inserted and deleted</td><td>Both before and after values are available.</td><td>Using only inserted when old value is needed.</td></tr>
<tr><td>Reject invalid new/changed rows</td><td>AFTER INSERT, UPDATE trigger using inserted</td><td>Checks only affected rows.</td><td>Scanning whole base table unnecessarily.</td></tr>
<tr><td>Replace DML behavior</td><td>INSTEAD OF trigger</td><td>Custom action replaces original statement.</td><td>Using AFTER trigger when original action must not run.</td></tr>
<tr><td>Database-level DDL audit</td><td>DDL trigger</td><td>Captures schema changes.</td><td>Using DML trigger for CREATE/ALTER/DROP events.</td></tr>
</table>

### Trigger Exam Traps

- Triggers fire once per statement, not once per row.
- Always write trigger logic to handle multiple rows in `inserted` and `deleted`.
- Avoid cursor-style row-by-row trigger logic.
- Use `THROW` to reject invalid changes.
- Use `ROWCOUNT_BIG() = 0` guard for empty operations.
- A trigger runs in the same transaction as the triggering statement.

---

# C. Advanced T-SQL - Detailed Scenario Usage

## C1. CTE vs Recursive CTE vs Subquery

<table>
<tr><th>Requirement</th><th>Best Pattern</th><th>Why</th><th>Trap</th></tr>
<tr><td>Simplify one complex query</td><td>CTE</td><td>Improves readability for next statement.</td><td>Thinking CTE creates a stored object.</td></tr>
<tr><td>Traverse hierarchy</td><td>Recursive CTE</td><td>Anchor member plus recursive member.</td><td>Using one-level self join when all levels are required.</td></tr>
<tr><td>Check if related rows exist</td><td>EXISTS correlated subquery</td><td>Efficient existence logic.</td><td>Using COUNT when existence is enough.</td></tr>
<tr><td>Find rows with no related rows</td><td>NOT EXISTS anti-join</td><td>Clear anti-semi join pattern.</td><td>Using NOT IN with NULL-sensitive logic.</td></tr>
</table>

### Recursive CTE Pattern

```sql
WITH Hierarchy AS
(
    SELECT EmployeeID, ManagerID, DisplayName, 0 AS Depth
    FROM dbo.Employee
    WHERE ManagerID IS NULL

    UNION ALL

    SELECT e.EmployeeID, e.ManagerID, e.DisplayName, h.Depth + 1
    FROM dbo.Employee AS e
    INNER JOIN Hierarchy AS h
        ON e.ManagerID = h.EmployeeID
)
SELECT *
FROM Hierarchy;
```

**Exam keyword:** top-level rows have `ManagerID IS NULL`, depth starts at 0, each lower level increments by 1.

---

## C2. Window Function Usage Matrix

<table>
<tr><th>Requirement</th><th>Function</th><th>Exam Clue</th></tr>
<tr><td>Unique sequence per partition</td><td>ROW_NUMBER</td><td>No ties should share a number.</td></tr>
<tr><td>Rank with gaps after ties</td><td>RANK</td><td>1, 1, 3 pattern.</td></tr>
<tr><td>Rank without gaps after ties</td><td>DENSE_RANK</td><td>1, 1, 2 pattern.</td></tr>
<tr><td>Previous row value</td><td>LAG</td><td>Compare with previous reading/month/value.</td></tr>
<tr><td>Next row value</td><td>LEAD</td><td>Compare with next reading/month/value.</td></tr>
<tr><td>Running total</td><td>SUM() OVER</td><td>Cumulative amount.</td></tr>
<tr><td>Compare only within group</td><td>PARTITION BY</td><td>Within same device, department, customer.</td></tr>
<tr><td>Define sequence</td><td>ORDER BY inside OVER</td><td>Chronological or ranked order.</td></tr>
</table>

---

## C3. JSON Function Usage Matrix

<table>
<tr><th>Requirement</th><th>Function/Clause</th><th>Why</th><th>Trap</th></tr>
<tr><td>Extract scalar value</td><td>JSON_VALUE</td><td>Returns one scalar.</td><td>Using JSON_QUERY for scalar values.</td></tr>
<tr><td>Extract object or array</td><td>JSON_QUERY</td><td>Returns JSON fragment.</td><td>Using JSON_VALUE for arrays/objects.</td></tr>
<tr><td>Expand array into rows</td><td>OPENJSON with CROSS APPLY</td><td>One row per array item.</td><td>Trying to use JSON_VALUE on array elements without expansion.</td></tr>
<tr><td>Build object</td><td>JSON_OBJECT</td><td>Creates a JSON object.</td><td>Using string concatenation.</td></tr>
<tr><td>Build array</td><td>JSON_ARRAY</td><td>Creates a JSON array.</td><td>Manual string formatting.</td></tr>
<tr><td>Aggregate values into array</td><td>JSON_ARRAYAGG</td><td>Group values into JSON array.</td><td>Using FOR JSON when simple aggregate array is required.</td></tr>
<tr><td>Query result as JSON array</td><td>FOR JSON PATH</td><td>Multi-row context for LLM/API.</td><td>FOR JSON AUTO when alias control is required.</td></tr>
<tr><td>Single JSON object</td><td>WITHOUT_ARRAY_WRAPPER</td><td>Removes array wrapper for one-row output.</td><td>Using it for multi-row output.</td></tr>
<tr><td>Keep null properties</td><td>INCLUDE_NULL_VALUES</td><td>Preserves fixed JSON shape.</td><td>Null properties omitted by default.</td></tr>
<tr><td>Extract long LLM answer</td><td>OPENJSON WITH nvarchar(max)</td><td>Avoids JSON_VALUE 4,000-character limit.</td><td>Using JSON_VALUE for long text.</td></tr>
</table>

### JSON Array Expansion Pattern

```sql
SELECT
    mo.OrderID,
    JSON_VALUE(mo.Payload, '$.customer.id') AS CustomerID,
    item.Sku,
    item.Quantity
FROM dbo.MobileOrders AS mo
CROSS APPLY OPENJSON(mo.Payload, '$.items')
WITH
(
    Sku nvarchar(50) '$.sku',
    Quantity int '$.qty'
) AS item
WHERE JSON_VALUE(mo.Payload, '$.orderStatus') = N'Closed';
```

---

## C4. Regex vs Fuzzy Matching

<table>
<tr><th>Requirement</th><th>Use</th><th>Why</th><th>Trap</th></tr>
<tr><td>Validate email/phone/code format</td><td>REGEXP_LIKE</td><td>Pattern match true/false.</td><td>Using fuzzy matching for strict pattern validation.</td></tr>
<tr><td>Extract product code from text</td><td>REGEXP_SUBSTR</td><td>Returns matching text or capture group.</td><td>REGEXP_INSTR returns position only.</td></tr>
<tr><td>Replace non-digit characters</td><td>REGEXP_REPLACE</td><td>Pattern-based replacement.</td><td>Multiple nested REPLACE calls.</td></tr>
<tr><td>Find match start position</td><td>REGEXP_INSTR</td><td>Returns position.</td><td>Using it when extracted text is required.</td></tr>
<tr><td>Count pattern occurrences</td><td>REGEXP_COUNT</td><td>Returns number of matches.</td><td>Manual loops.</td></tr>
<tr><td>Split delimited text into rows</td><td>REGEXP_SPLIT_TO_TABLE</td><td>Regex-based splitting.</td><td>String parsing loops.</td></tr>
<tr><td>Approximate typo matching</td><td>EDIT_DISTANCE_SIMILARITY</td><td>0-100 similarity score.</td><td>Using EDIT_DISTANCE with percentage threshold.</td></tr>
<tr><td>Short name similarity</td><td>JARO_WINKLER_DISTANCE</td><td>Useful for names/transpositions.</td><td>Using regex for approximate matching.</td></tr>
</table>

---

# D. Optimize Database Performance - Detailed Tool and Table Guide

## D1. Performance Diagnostic Tools - What Each Table/View Is For

<table>
<tr><th>Tool / DMV / Feature</th><th>Type</th><th>Use When</th><th>What It Shows</th><th>Do Not Use When</th></tr>
<tr><td>Actual execution plan</td><td>Query-level plan</td><td>One query is slow and you need operator-level analysis.</td><td>Seek/scan, join choice, sort, key lookup, estimates vs actuals.</td><td>You need live server-wide activity.</td></tr>
<tr><td>Estimated execution plan</td><td>Query-level plan</td><td>You need plan shape without running the query.</td><td>Optimizer estimate only.</td><td>You need actual row counts or runtime metrics.</td></tr>
<tr><td>sys.dm_exec_requests</td><td>Live DMV</td><td>Active slowdown, currently running requests, blocking, waits.</td><td>session_id, status, cpu_time, logical_reads, wait_type, wait_time, blocking_session_id.</td><td>You need historical plan aggregate data.</td></tr>
<tr><td>sys.dm_exec_sessions</td><td>Live session DMV</td><td>Need login, host, program, session metadata.</td><td>Connected sessions and attributes.</td><td>You need per-request waits and reads.</td></tr>
<tr><td>sys.dm_exec_query_stats</td><td>Cached aggregate DMV</td><td>Find top CPU/duration/logical read queries from cache.</td><td>Aggregated worker time, execution count, elapsed time.</td><td>You need currently executing request details.</td></tr>
<tr><td>sys.dm_exec_sql_text</td><td>DMF</td><td>Need SQL text for a plan/request handle.</td><td>T-SQL batch text.</td><td>Used alone without handle context.</td></tr>
<tr><td>sys.dm_exec_query_plan</td><td>DMF</td><td>Need XML showplan for a plan handle.</td><td>Execution plan XML.</td><td>Not for missing index recommendations alone.</td></tr>
<tr><td>sys.dm_os_wait_stats</td><td>Aggregate wait DMV</td><td>Investigate overall server wait profile.</td><td>Cumulative wait totals by wait type.</td><td>Need active blocking request list.</td></tr>
<tr><td>sys.dm_tran_locks</td><td>Lock DMV</td><td>Need lock resources and modes.</td><td>Locks held/requested.</td><td>Need high-level historical query regression.</td></tr>
<tr><td>sys.dm_db_missing_index_details</td><td>Missing index DMV</td><td>Need missing-index suggestions.</td><td>Potential equality/inequality/include columns.</td><td>Blindly creating every suggested index.</td></tr>
<tr><td>sys.dm_db_index_usage_stats</td><td>Index usage DMV</td><td>Review seeks/scans/lookups/updates per index.</td><td>How indexes are used.</td><td>Need exact query plan operator details.</td></tr>
<tr><td>sys.dm_db_index_operational_stats</td><td>Index operations DMV</td><td>Investigate latch/lock/page split operational behavior.</td><td>Low-level index operation stats.</td><td>Basic missing index tuning.</td></tr>
<tr><td>Query Store</td><td>Historical performance store</td><td>Query was fast before and slow now; compare plans over time.</td><td>Runtime history, plan history, regressions, forced plans.</td><td>You need immediate active request wait details.</td></tr>
<tr><td>Query Performance Insight</td><td>Azure portal experience</td><td>Need visual top resource-consuming Azure SQL queries.</td><td>Portal-based query performance trends.</td><td>Need detailed operator-level plan analysis.</td></tr>
<tr><td>Azure Monitor</td><td>Monitoring platform</td><td>Need metrics, alerts, dashboards.</td><td>Platform-level metrics and alerting.</td><td>Need SQL operator-level plan tuning.</td></tr>
<tr><td>Log Analytics</td><td>KQL log workspace</td><td>Need queryable diagnostics/audit logs and alert rules.</td><td>Logs queried by KQL.</td><td>Need query execution plan shape.</td></tr>
<tr><td>Application Insights</td><td>Application telemetry</td><td>Need app requests, dependencies, failures, traces.</td><td>Application-level telemetry and dependencies.</td><td>Need SQL index recommenders only.</td></tr>
</table>

---

## D2. Execution Plan Operators - Scenario Guide

<table>
<tr><th>Operator</th><th>Meaning</th><th>Usually Good?</th><th>What To Check</th><th>Typical Fix</th></tr>
<tr><td>Index Seek</td><td>Uses index to directly locate a range or rows.</td><td>Usually yes.</td><td>Returned row count and residual predicates.</td><td>Usually no fix unless seek returns too many rows.</td></tr>
<tr><td>Index Scan</td><td>Reads many/all rows of an index.</td><td>Depends.</td><td>Is a large portion of rows required?</td><td>Add more selective index if query should be selective.</td></tr>
<tr><td>Table Scan</td><td>Reads entire heap/table.</td><td>Often bad for selective queries.</td><td>Missing indexes, predicates, row counts.</td><td>Create appropriate index.</td></tr>
<tr><td>Key Lookup</td><td>Uses clustered index/heap to fetch missing columns after nonclustered seek.</td><td>OK for few rows, bad repeated many times.</td><td>Number of executions and logical reads.</td><td>Add INCLUDE columns to cover the query.</td></tr>
<tr><td>RID Lookup</td><td>Lookup into heap row by row.</td><td>Similar concern as Key Lookup.</td><td>Repeated lookups.</td><td>Add INCLUDE columns or clustered index where appropriate.</td></tr>
<tr><td>Nested Loops</td><td>Join optimized for small outer inputs and indexed inner lookups.</td><td>Good for small sets.</td><td>Repeated inner executions.</td><td>Index inner table or consider plan alternatives.</td></tr>
<tr><td>Hash Match</td><td>Hash join/aggregate for larger sets.</td><td>Often OK for large data.</td><td>Memory spills and row estimates.</td><td>Improve stats/indexes or memory grant conditions.</td></tr>
<tr><td>Merge Join</td><td>Join ordered inputs.</td><td>Good when inputs are sorted/indexed.</td><td>Sorts required before merge.</td><td>Indexes aligned with join order.</td></tr>
<tr><td>Sort</td><td>Explicit sort operation.</td><td>Can be expensive.</td><td>Memory grant/spills.</td><td>Create index matching ORDER BY/GROUP BY where useful.</td></tr>
<tr><td>Spool</td><td>Temporary storage of intermediate rows.</td><td>Depends.</td><td>Repeated re-use or Halloween protection.</td><td>Query/index rewrite if costly.</td></tr>
<tr><td>Filter</td><td>Applies predicate after input rows are read.</td><td>Depends.</td><td>Predicate pushdown and selectivity.</td><td>Index/filter earlier if possible.</td></tr>
</table>

---

## D3. Common Performance Scenarios and Best First Action

<table>
<tr><th>Scenario</th><th>Likely Issue</th><th>Best First Action</th><th>Wrong Answer Trap</th></tr>
<tr><td>Current active slowdown; need CPU, logical reads, waits, blocking session</td><td>Live request bottleneck</td><td>Query sys.dm_exec_requests</td><td>sys.dm_exec_query_stats gives cached aggregates, not live requests.</td></tr>
<tr><td>Query was fast yesterday and slow today after plan change</td><td>Plan regression</td><td>Use Query Store to compare and force previous good plan if appropriate.</td><td>Adding random indexes before plan comparison.</td></tr>
<tr><td>Execution plan has repeated Key Lookup after Index Seek</td><td>Non-covering index</td><td>Add missing selected columns to INCLUDE list.</td><td>FORCESEEK does not remove key lookups.</td></tr>
<tr><td>Estimated row count differs greatly from actual</td><td>Statistics/cardinality issue</td><td>Update stats, review predicates and data skew.</td><td>Adding INCLUDE columns when estimate problem is the main issue.</td></tr>
<tr><td>Stored procedure fast for one parameter and slow for another</td><td>Parameter sniffing</td><td>Review plan, Query Store, OPTION(RECOMPILE), OPTIMIZE FOR, stats/indexes.</td><td>Assuming blocking without evidence.</td></tr>
<tr><td>Readers and writers block each other</td><td>Locking isolation conflict</td><td>Consider RCSI/Snapshot, shorten transactions, tune indexes.</td><td>Using READ UNCOMMITTED when data correctness matters.</td></tr>
<tr><td>Error 1205 between two procedures updating tables in opposite order</td><td>Deadlock</td><td>Make table access order consistent.</td><td>DEADLOCK_PRIORITY only affects victim selection.</td></tr>
<tr><td>Large aggregate scan over hundreds of millions of rows</td><td>Analytical workload</td><td>Columnstore index, often nonclustered columnstore for mixed workload.</td><td>Rowstore covering index may still be less appropriate for huge analytics scans.</td></tr>
<tr><td>Queries filter large table by date and archive completed months</td><td>Partitioning opportunity</td><td>Monthly partitioning on date with aligned indexes.</td><td>Quarterly partitions when monthly switching is required.</td></tr>
<tr><td>Need Azure portal view of top resource consumers</td><td>Azure SQL query monitoring</td><td>Query Performance Insight</td><td>Execution plan is not portal top-consumer view.</td></tr>
</table>

---

## D4. Blocking vs Deadlock vs Isolation

<table>
<tr><th>Concept</th><th>Description</th><th>How To Identify</th><th>Typical Fix</th></tr>
<tr><td>Blocking</td><td>One session waits for another session to release a lock.</td><td>blocking_session_id in sys.dm_exec_requests.</td><td>Shorter transactions, better indexes, row versioning.</td></tr>
<tr><td>Deadlock</td><td>Two or more sessions wait on each other in a cycle.</td><td>Deadlock graph, error 1205, victim chosen.</td><td>Consistent object access order, shorter transactions, indexing, retry logic.</td></tr>
<tr><td>Dirty read</td><td>Read uncommitted data.</td><td>Possible under READ UNCOMMITTED.</td><td>Use READ COMMITTED or stronger.</td></tr>
<tr><td>Non-repeatable read</td><td>Same row changes between reads in a transaction.</td><td>Read same row twice and value changes.</td><td>Repeatable Read/Snapshot/Serializable depending need.</td></tr>
<tr><td>Phantom read</td><td>New rows appear for the same predicate in transaction.</td><td>Range query returns different set.</td><td>Serializable or appropriate Snapshot semantics.</td></tr>
<tr><td>RCSI</td><td>Read Committed Snapshot Isolation uses row versioning for read committed.</td><td>Readers do not block writers in same way.</td><td>Enable when reducing reader/writer blocking is required and workload supports it.</td></tr>
</table>

---

# E. Indexing and Storage - Detailed Scenario Usage

## E1. Index Selection Matrix

<table>
<tr><th>Requirement</th><th>Best Index / Design</th><th>Why</th><th>Trap</th></tr>
<tr><td>Single-row lookup by alternate key</td><td>Nonclustered index</td><td>Supports efficient seek.</td><td>Columnstore for point lookup.</td></tr>
<tr><td>Date range query</td><td>Index on date column, possibly partitioning</td><td>Supports ordered range access.</td><td>Indexing unrelated selected column.</td></tr>
<tr><td>Query returns extra columns after seek</td><td>INCLUDE columns</td><td>Covers query and avoids Key Lookup.</td><td>Updating stats when estimates are already correct.</td></tr>
<tr><td>Multiple equality/range predicates</td><td>Composite index</td><td>Column order supports predicate pattern.</td><td>Wrong key order can reduce usefulness.</td></tr>
<tr><td>Frequently queried subset</td><td>Filtered index</td><td>Smaller targeted index.</td><td>Filtered index not matching query predicate.</td></tr>
<tr><td>Large aggregation/reporting</td><td>Columnstore index</td><td>Compression and batch-mode analytics.</td><td>Using rowstore by default for huge scans.</td></tr>
<tr><td>Mixed OLTP and reporting</td><td>Nonclustered columnstore</td><td>Preserves rowstore access while accelerating analytics.</td><td>Clustered columnstore replacing OLTP access path.</td></tr>
<tr><td>JSON property search</td><td>Computed column plus index</td><td>Indexes extracted scalar path.</td><td>Scanning JSON_VALUE for every row.</td></tr>
<tr><td>Exact text search</td><td>Full-text index</td><td>Supports CONTAINS/FREETEXT.</td><td>LIKE for linguistic matching.</td></tr>
<tr><td>Semantic search</td><td>Vector index</td><td>Accelerates similarity search.</td><td>Full-text search for synonyms/meaning only.</td></tr>
</table>

---

## E2. Columnstore Usage Guide

<table>
<tr><th>Scenario</th><th>Choose</th><th>Why</th></tr>
<tr><td>Fact table mostly used for analytics</td><td>Clustered columnstore index</td><td>Entire table optimized for scan/aggregate workload.</td></tr>
<tr><td>OLTP table also needs dashboard aggregates</td><td>Nonclustered columnstore index</td><td>Preserves rowstore primary access path.</td></tr>
<tr><td>High-frequency point lookups and updates only</td><td>Rowstore index</td><td>Columnstore is not the default for hot OLTP.</td></tr>
<tr><td>Need avoid unsupported/large payload column in analytics index</td><td>Nonclustered columnstore on selected columns</td><td>Only include analytical columns.</td></tr>
</table>

---

# F. Security and Compliance - Scenario Usage

## F1. Data Protection Decision Matrix

<table>
<tr><th>Requirement</th><th>Best Feature</th><th>Why</th><th>Trap</th></tr>
<tr><td>Hide sensitive data in query results</td><td>Dynamic Data Masking</td><td>Display masking for unauthorized users.</td><td>DDM is not encryption.</td></tr>
<tr><td>Prevent DBAs/admins from seeing plaintext</td><td>Always Encrypted</td><td>Client-side encryption separates data access from key access.</td><td>TDE protects data at rest, not from users who can query data.</td></tr>
<tr><td>Need exact-match search over encrypted column</td><td>Deterministic Always Encrypted</td><td>Same plaintext produces same ciphertext.</td><td>Randomized encryption does not support equality search.</td></tr>
<tr><td>Need stronger confidentiality and no equality search</td><td>Randomized Always Encrypted</td><td>Same plaintext produces different ciphertext.</td><td>Choosing deterministic when equality search is not required.</td></tr>
<tr><td>Need encryption/decryption inside T-SQL</td><td>Column-level encryption</td><td>Uses database keys and encryption functions.</td><td>Confusing with Always Encrypted client-side model.</td></tr>
<tr><td>Users see only their tenant rows</td><td>Row-Level Security</td><td>Predicate function and security policy filter rows.</td><td>Object permissions alone cannot filter rows.</td></tr>
<tr><td>Protect service connection without passwords</td><td>Managed Identity / Service Connector</td><td>Passwordless Azure service authentication.</td><td>Storing SQL password in app settings.</td></tr>
<tr><td>Track data access and permission changes</td><td>Auditing</td><td>Compliance, investigation, monitoring.</td><td>Using Query Store for security audit.</td></tr>
</table>

---

## F2. RLS Predicate Selection

<table>
<tr><th>Requirement</th><th>RLS Predicate</th><th>Timing</th></tr>
<tr><td>Limit rows visible to SELECT</td><td>FILTER PREDICATE</td><td>Applied to read/query operations.</td></tr>
<tr><td>Limit rows targetable by UPDATE/DELETE</td><td>FILTER PREDICATE</td><td>Rows not visible cannot be targeted.</td></tr>
<tr><td>Prevent invalid insert</td><td>BLOCK PREDICATE</td><td>AFTER INSERT checks final inserted row.</td></tr>
<tr><td>Prevent invalid updated value</td><td>BLOCK PREDICATE</td><td>AFTER UPDATE checks final changed row.</td></tr>
</table>

---

# G. CI/CD and SQL Database Projects - Scenario Usage

## G1. SQL Project Workflow Matrix

<table>
<tr><th>Requirement</th><th>Best Action</th><th>Reason</th><th>Trap</th></tr>
<tr><td>Store schema as editable code</td><td>SQL Database Project</td><td>Object definitions in source control.</td><td>Committing only DACPAC.</td></tr>
<tr><td>Cross-platform build on Ubuntu with .NET SDK</td><td>SDK-style SQL project and dotnet build</td><td>Works in modern CI.</td><td>Visual Studio-only project path.</td></tr>
<tr><td>Create deployable artifact</td><td>DACPAC</td><td>Standard deployment artifact.</td><td>Loose scripts without model validation.</td></tr>
<tr><td>Deploy DACPAC to test database</td><td>sqlpackage Publish</td><td>Publishes model to target DB.</td><td>sqlpackage Extract creates artifact from DB instead.</td></tr>
<tr><td>Run C# database tests</td><td>dotnet test</td><td>Runs test project in workflow.</td><td>dotnet publish packages app, not tests.</td></tr>
<tr><td>Isolate schema change from main</td><td>Feature branch</td><td>Supports PR review.</td><td>Editing directly on main.</td></tr>
<tr><td>Production-only secret</td><td>GitHub environment secret</td><td>Scoped to production environment job.</td><td>Repository variable for sensitive value.</td></tr>
<tr><td>Detect manual DB change</td><td>Schema compare / drift report</td><td>Find differences between DB and project.</td><td>Extracting all drift into project without review.</td></tr>
</table>

---

# H. Data API Builder and Azure Integration - Scenario Usage

## H1. DAB Selection Matrix

<table>
<tr><th>Requirement</th><th>DAB Feature</th><th>Why</th><th>Trap</th></tr>
<tr><td>Expose SQL table quickly as API</td><td>DAB REST entity</td><td>No custom API code.</td><td>Building .NET API when minimize custom code is required.</td></tr>
<tr><td>Expose SQL as GraphQL</td><td>DAB GraphQL endpoint</td><td>Built-in GraphQL runtime.</td><td>Fabric API for GraphQL when Azure Container Apps DAB is specified.</td></tr>
<tr><td>Expose stored procedure that changes data</td><td>Stored procedure entity as GraphQL mutation</td><td>Mutation represents write operation.</td><td>GraphQL query for write operation.</td></tr>
<tr><td>Allow read operations only</td><td>Entity permissions with read action</td><td>Least privilege API action.</td><td>Grant create/update/delete unnecessarily.</td></tr>
<tr><td>Hide protected fields</td><td>fields.exclude</td><td>Field-level exposure control.</td><td>Disabling introspection only hides schema discovery.</td></tr>
<tr><td>Prevent huge API response</td><td>Pagination</td><td>Controls response size.</td><td>Returning all rows by default.</td></tr>
<tr><td>Repeated queries need faster response</td><td>DAB caching</td><td>Reduces repeated database calls.</td><td>Ignoring distributed cache in multi-instance deployment.</td></tr>
<tr><td>Multi-instance shared cache</td><td>L1L2 cache level</td><td>Uses local and distributed cache.</td><td>L1 only is instance-local.</td></tr>
</table>

---

# I. AI, Embeddings, Vector Search, and RAG - Scenario Usage

## I1. Model Selection Matrix

<table>
<tr><th>Requirement</th><th>Best Choice</th><th>Why</th><th>Trap</th></tr>
<tr><td>Lowest cost/latency</td><td>Smaller model</td><td>Faster and cheaper.</td><td>Choosing largest model by default.</td></tr>
<tr><td>Complex reasoning</td><td>Larger reasoning-capable model</td><td>Better quality for complex tasks.</td><td>Using embeddings model for reasoning output.</td></tr>
<tr><td>Image/audio/document inputs</td><td>Multimodal model</td><td>Handles non-text content.</td><td>Text-only model.</td></tr>
<tr><td>Predictable JSON values for columns</td><td>Chat/completions model with structured output/prompt</td><td>Produces parseable categories/fields.</td><td>Embeddings model returns vectors, not column values.</td></tr>
<tr><td>Similarity search</td><td>Embedding model</td><td>Converts semantic meaning to vector.</td><td>Chat model output used as vector.</td></tr>
<tr><td>Keep procedure definitions unchanged while endpoint changes</td><td>ALTER existing external model</td><td>No stored procedure change required.</td><td>Create new model and then need code change.</td></tr>
</table>

---

## I2. Embedding Column Selection

<table>
<tr><th>Column Type</th><th>Embed?</th><th>Reason</th></tr>
<tr><td>Product description</td><td>Yes</td><td>Contains semantic meaning.</td></tr>
<tr><td>Article body</td><td>Yes</td><td>Natural language retrieval target.</td></tr>
<tr><td>Support ticket narrative</td><td>Yes</td><td>Semantic classification/search.</td></tr>
<tr><td>FAQ question/answer</td><td>Yes</td><td>User questions map semantically to answers.</td></tr>
<tr><td>Product ID</td><td>No</td><td>Identifier, not meaningful text.</td></tr>
<tr><td>Price</td><td>No</td><td>Structured filter/ranking feature, not text meaning.</td></tr>
<tr><td>CategoryID</td><td>No</td><td>Structured filter.</td></tr>
<tr><td>ModifiedAt</td><td>No</td><td>Operational metadata, not semantic content.</td></tr>
</table>

---

## I3. Vector Search Decision Matrix

<table>
<tr><th>Requirement</th><th>Best Choice</th><th>Why</th><th>Trap</th></tr>
<tr><td>Small data and exact result required</td><td>ENN / VECTOR_DISTANCE</td><td>Exhaustive comparison gives exact result.</td><td>ANN when exactness is required.</td></tr>
<tr><td>Millions of vectors and low latency</td><td>ANN / VECTOR_SEARCH</td><td>Uses vector index candidates.</td><td>Scanning all vectors with VECTOR_DISTANCE.</td></tr>
<tr><td>Text embeddings</td><td>Cosine distance</td><td>Common semantic text metric.</td><td>Euclidean if question specifies text embeddings and cosine is available.</td></tr>
<tr><td>Both 768 and 1536 meet relevance</td><td>VECTOR(768)</td><td>Less storage and compute.</td><td>Choosing larger dimension unnecessarily.</td></tr>
<tr><td>Reject wrong dimension count</td><td>Fixed VECTOR(n)</td><td>Enforces expected dimension.</td><td>Unconstrained VECTOR.</td></tr>
<tr><td>Filter by CategoryID and Price</td><td>Structured columns plus B-tree index</td><td>Efficient relational filtering.</td><td>JSON metadata for core filters.</td></tr>
</table>

---

## I4. Search Type Selection

<table>
<tr><th>Requirement</th><th>Search Type</th><th>Example</th><th>Trap</th></tr>
<tr><td>Exact phrase or keyword</td><td>Full-text search with CONTAINS</td><td>Exact phrase "mountain bike".</td><td>Vector search may miss exact required wording.</td></tr>
<tr><td>Linguistic word forms</td><td>FREETEXT</td><td>ride, riding, rode.</td><td>LIKE does not provide full-text linguistic matching.</td></tr>
<tr><td>Meaning and synonyms</td><td>Vector search</td><td>Comfortable footwear for jogging.</td><td>Only keyword search can miss different wording.</td></tr>
<tr><td>Best production relevance</td><td>Hybrid search</td><td>Keyword plus semantic retrieval.</td><td>Returning only inner join matches excludes one-source results.</td></tr>
<tr><td>Combine ranked full-text and vector lists</td><td>RRF</td><td>Use rank positions from each list.</td><td>Summing raw full-text scores and vector distances.</td></tr>
</table>

---

## I5. RAG Decision Matrix

<table>
<tr><th>Requirement</th><th>Best Choice</th><th>Why</th><th>Trap</th></tr>
<tr><td>Answer depends on current database facts</td><td>RAG</td><td>Retrieve current context before generation.</td><td>Prompt-only generation without data retrieval.</td></tr>
<tr><td>Summarize text already in prompt</td><td>Prompt-only summarization</td><td>No retrieval needed.</td><td>Overengineering with RAG.</td></tr>
<tr><td>Large documents</td><td>Chunk before embedding</td><td>Focused retrieval and model token control.</td><td>One embedding for a 200-page document.</td></tr>
<tr><td>Need single row JSON object</td><td>FOR JSON PATH, WITHOUT_ARRAY_WRAPPER</td><td>Top-level object.</td><td>Default array wrapper.</td></tr>
<tr><td>Need multi-row JSON context</td><td>FOR JSON PATH</td><td>Array of objects.</td><td>WITHOUT_ARRAY_WRAPPER on multi-row output.</td></tr>
<tr><td>Need null properties included</td><td>INCLUDE_NULL_VALUES</td><td>Preserves schema shape.</td><td>Nulls omitted by default.</td></tr>
<tr><td>Need extract long assistant answer</td><td>OPENJSON WITH nvarchar(max)</td><td>Avoids truncation.</td><td>JSON_VALUE limit.</td></tr>
</table>

---

# J. Graph Tables - Complete Usage and Query Guide

## J1. Graph Object Selection

<table>
<tr><th>Graph Object / Syntax</th><th>Description</th><th>Use When</th></tr>
<tr><td>NODE table</td><td>Stores entities in a graph model.</td><td>People, products, suppliers, warehouses.</td></tr>
<tr><td>EDGE table</td><td>Stores relationships between nodes.</td><td>Knows, supplies, located in, depends on.</td></tr>
<tr><td>MATCH</td><td>Pattern matching syntax for graph traversal.</td><td>Find connected nodes.</td></tr>
<tr><td>SHORTEST_PATH</td><td>Finds minimal path over variable-length graph pattern.</td><td>Minimum hop count or shortest relationship path.</td></tr>
<tr><td>FOR PATH</td><td>Marks aliases used in variable-length path traversal.</td><td>Required with SHORTEST_PATH path aliases.</td></tr>
<tr><td>WITHIN GROUP (GRAPH PATH)</td><td>Aggregates values along graph path.</td><td>Return last node, count hops, path values.</td></tr>
</table>

## J2. Graph Query Scenario Pattern

```sql
SELECT
    StartPerson.Name AS StartPerson,
    LAST_VALUE(ReachablePerson.Name) WITHIN GROUP (GRAPH PATH) AS ReachablePerson,
    COUNT(ReachablePerson.Name) WITHIN GROUP (GRAPH PATH) AS Distance
FROM dbo.Person AS StartPerson,
     dbo.Knows FOR PATH AS k,
     dbo.Person FOR PATH AS ReachablePerson
WHERE MATCH
(
    SHORTEST_PATH(StartPerson(-(k)->ReachablePerson){1,3})
)
AND StartPerson.Name = N'Person1';
```

**Exam clues:** one to three hops, minimum hop count, directed outgoing relationship, reachable person.

---

# K. AI-Assisted Tooling and MCP - Scenario Usage

<table>
<tr><th>Requirement</th><th>Best Choice</th><th>Why</th><th>Trap</th></tr>
<tr><td>Copilot should know specific Fabric warehouse without repeating context</td><td>Item-scoped Fabric Data Warehouse MCP endpoint</td><td>Bound to a specific warehouse item.</td><td>Global endpoint requires context separately.</td></tr>
<tr><td>Routine development only needs object names/columns</td><td>Metadata-only MCP permissions</td><td>Least privilege and no data exposure.</td><td>Granting read/write/owner permissions.</td></tr>
<tr><td>Use masked nonproduction context</td><td>Development MCP endpoint</td><td>Avoids compliance production data exposure.</td><td>Connecting Copilot to production by default.</td></tr>
<tr><td>Avoid reusable secrets in committed mcp.json</td><td>Developer sign-in / Entra identity</td><td>Attributable and secretless.</td><td>Connection strings or tokens in repository.</td></tr>
<tr><td>Prevent SQL injection in generated data-access code</td><td>Bind external values as SQL parameters</td><td>Parameterization directly mitigates injection.</td><td>Input validation alone.</td></tr>
<tr><td>Approved Azure OpenAI deployment in SSMS Copilot Chat</td><td>Azure custom model using deployment name as Model ID and resource endpoint URL</td><td>Registers approved Azure deployment.</td><td>Using base model name or resource group as endpoint.</td></tr>
</table>

---

# L. High-Value Exam Traps - Consolidated

<table>
<tr><th>If the Question Says...</th><th>Usually Answer...</th><th>Not...</th></tr>
<tr><td>Protect plaintext from DBAs</td><td>Always Encrypted</td><td>TDE or DDM</td></tr>
<tr><td>Display masked value</td><td>Dynamic Data Masking</td><td>Always Encrypted</td></tr>
<tr><td>Tenant cannot insert/update another tenant row</td><td>RLS block predicates after insert/update</td><td>Filter predicate only</td></tr>
<tr><td>REST and GraphQL without custom code</td><td>Data API Builder</td><td>Custom .NET API</td></tr>
<tr><td>GraphQL operation changes data</td><td>Mutation</td><td>Query</td></tr>
<tr><td>Shared cache across DAB instances</td><td>L1L2</td><td>L1 only</td></tr>
<tr><td>Current running requests and waits</td><td>sys.dm_exec_requests</td><td>sys.dm_exec_query_stats</td></tr>
<tr><td>Slow after plan change</td><td>Query Store</td><td>Missing index DMV first</td></tr>
<tr><td>Repeated Key Lookup</td><td>INCLUDE columns</td><td>FORCESEEK</td></tr>
<tr><td>Deadlock from opposite update order</td><td>Consistent object access order</td><td>DEADLOCK_PRIORITY LOW</td></tr>
<tr><td>Large aggregate scans but keep rowstore lookup</td><td>Nonclustered columnstore</td><td>Clustered columnstore</td></tr>
<tr><td>Monthly archive by partition switching</td><td>Monthly date partitions and aligned indexes</td><td>Quarterly partitions</td></tr>
<tr><td>Parameterized reusable rowset</td><td>Inline TVF</td><td>View or stored procedure</td></tr>
<tr><td>Single reusable calculated value</td><td>Scalar function</td><td>TVF</td></tr>
<tr><td>Preserve original DML unless validation fails</td><td>AFTER trigger</td><td>INSTEAD OF trigger</td></tr>
<tr><td>Extract array items from JSON</td><td>CROSS APPLY OPENJSON</td><td>JSON_VALUE only</td></tr>
<tr><td>Long LLM response over 4,000 chars</td><td>OPENJSON WITH nvarchar(max)</td><td>JSON_VALUE</td></tr>
<tr><td>Single-row JSON object</td><td>WITHOUT_ARRAY_WRAPPER</td><td>ROOT</td></tr>
<tr><td>Hybrid search ranking</td><td>RRF over ranked lists</td><td>Summing raw scores/distances</td></tr>
<tr><td>Millions of embeddings with recall target</td><td>ANN VECTOR_SEARCH</td><td>Exact VECTOR_DISTANCE scan</td></tr>
<tr><td>Text embeddings</td><td>Cosine distance</td><td>Euclidean by default</td></tr>
<tr><td>Existing external model endpoint changes but procedures unchanged</td><td>ALTER EXTERNAL MODEL</td><td>Create new model and change procedures</td></tr>
<tr><td>Graph minimum hop count</td><td>SHORTEST_PATH with FOR PATH</td><td>Simple MATCH only</td></tr>
<tr><td>Copilot metadata only</td><td>MCP metadata-only permissions</td><td>Read/write database permissions</td></tr>
</table>

---

# M. Final Revision Flow - How To Answer Scenario Questions

Use this checklist whenever a DP-800 question feels confusing:

```text
1. Identify the domain:
   - Database object / T-SQL / Security / Performance / CI-CD / DAB / AI / RAG

2. Extract the key requirement words:
   - history, tamper-proof, exact search, semantic, passwordless, current requests, plan regression, GraphQL mutation, long JSON answer, multi-hop

3. Eliminate wrong feature families:
   - Display masking is not encryption.
   - TDE is not protection from DBAs.
   - Query Store is not live request monitoring.
   - DAB is not custom API code.
   - Embeddings are not structured category outputs.

4. Match the requirement to the smallest correct feature:
   - Least privilege.
   - Minimal custom code.
   - Existing procedure unchanged.
   - No secrets in code.
   - Preserve atomic transaction.

5. Check implementation detail:
   - AFTER vs INSTEAD OF.
   - FILTER vs BLOCK predicate.
   - Query vs mutation.
   - CROSS APPLY vs JOIN.
   - JSON_VALUE vs OPENJSON.
   - VECTOR_SEARCH vs VECTOR_DISTANCE.
```

---

## Added Source Alignment Note

This section was added to align the study material more directly with scenario-style DP-800 skills such as programmability objects, triggers, execution plans, DMVs, Query Store, Query Performance Insight, DAB REST/GraphQL, MCP options, external models, embeddings, vector search, hybrid search, RRF, and RAG JSON handling. It also preserves the original study material and previously added practice-exam addendum without removing content.
