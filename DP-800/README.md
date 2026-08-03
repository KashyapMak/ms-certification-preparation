# DP-800 Complete Study Guide - README Version 3

**Exam:** DP-800: Developing AI-Enabled Database Solutions  
**Certification:** Microsoft Certified: SQL AI Developer Associate  
**Generated:** 3 August 2026  
**Purpose:** Single Markdown study pack with concepts, syntax, decision trees, examples, and last-mile missing topics so you do not need to jump back to Microsoft Learn at the last moment.

---

## Table of Contents

  - [How This Version Was Cleaned Up](#how-this-version-was-cleaned-up)
- [0. DP-800 Exam Blueprint and Mindset](#0-dp-800-exam-blueprint-and-mindset)
  - [0.1 Exam Domains](#01-exam-domains)
  - [0.2 Scenario Question Method](#02-scenario-question-method)
- [1. Database Design and Database Objects](#1-database-design-and-database-objects)
  - [1.1 Data Types](#11-data-types)
    - [What to Know](#what-to-know)
    - [Selection Matrix](#selection-matrix)
    - [Syntax Examples](#syntax-examples)
    - [Must Memorize](#must-memorize)
  - [1.2 Constraints, Identity, and Sequences](#12-constraints-identity-and-sequences)
    - [What to Know](#what-to-know)
    - [Exam Traps](#exam-traps)
  - [1.3 Index Design](#13-index-design)
    - [What to Know](#what-to-know)
    - [Index Selection Matrix](#index-selection-matrix)
    - [Rowstore Examples](#rowstore-examples)
    - [Composite Index Rule](#composite-index-rule)
    - [Columnstore Examples](#columnstore-examples)
    - [Key Lookup Scenario](#key-lookup-scenario)
    - [Exam Traps](#exam-traps)
  - [1.4 Partitioning](#14-partitioning)
    - [What to Know](#what-to-know)
    - [Use When](#use-when)
    - [Syntax Pattern](#syntax-pattern)
    - [Exam Traps](#exam-traps)
  - [1.5 Specialized Tables](#15-specialized-tables)
    - [Selection Matrix](#selection-matrix)
    - [Memory-Optimized Tables](#memory-optimized-tables)
    - [Temporal Tables](#temporal-tables)
    - [Ledger Tables](#ledger-tables)
    - [External Tables](#external-tables)
    - [Graph Tables](#graph-tables)
    - [Shortest Path Graph Pattern](#shortest-path-graph-pattern)
    - [Complete Graph Query Example Pack](#complete-graph-query-example-pack)
    - [Exam Traps](#exam-traps)
  - [1.6 JSON and Semi-Structured Data](#16-json-and-semi-structured-data)
    - [What to Know](#what-to-know)
    - [JSON Function Matrix](#json-function-matrix)
    - [JSON Property Indexing](#json-property-indexing)
    - [JSON Array Expansion](#json-array-expansion)
    - [JSON for RAG Context](#json-for-rag-context)
    - [Single-Row Object Instead of Array](#single-row-object-instead-of-array)
    - [Complete JSON Example Pack](#complete-json-example-pack)
    - [JSON Decision Tree](#json-decision-tree)
    - [Exam Traps](#exam-traps)
- [2. Programmability Objects](#2-programmability-objects)
  - [2.1 Object Selection Matrix](#21-object-selection-matrix)
  - [2.2 Views and Indexed Views](#22-views-and-indexed-views)
    - [Exam Traps](#exam-traps)
  - [2.3 Scalar Functions](#23-scalar-functions)
  - [2.4 Inline Table-Valued Functions](#24-inline-table-valued-functions)
    - [CROSS APPLY vs OUTER APPLY](#cross-apply-vs-outer-apply)
  - [2.5 Stored Procedures](#25-stored-procedures)
    - [Exam Traps](#exam-traps)
  - [2.6 Triggers](#26-triggers)
    - [AFTER Trigger](#after-trigger)
    - [Trigger Rules](#trigger-rules)
- [3. Advanced T-SQL](#3-advanced-t-sql)
  - [3.1 CTE and Recursive CTE](#31-cte-and-recursive-cte)
    - [Overview](#overview)
    - [Purpose](#purpose)
    - [Syntax](#syntax)
    - [Example 1 - Plain CTE for Aggregation](#example-1-plain-cte-for-aggregation)
    - [Example 2 - Multiple CTEs in One Query](#example-2-multiple-ctes-in-one-query)
    - [Example 3 - CTE with Window Function](#example-3-cte-with-window-function)
    - [Example 4 - Recursive CTE for Hierarchy](#example-4-recursive-cte-for-hierarchy)
    - [Example 5 - Recursive CTE with MAXRECURSION](#example-5-recursive-cte-with-maxrecursion)
    - [CTE vs Derived Table vs Temp Table](#cte-vs-derived-table-vs-temp-table)
    - [When to Use](#when-to-use)
    - [When NOT to Use](#when-not-to-use)
    - [Common Mistakes](#common-mistakes)
    - [DP-800 Exam Scenarios](#dp-800-exam-scenarios)
    - [DP-800 Exam Traps](#dp-800-exam-traps)
    - [Quick Revision](#quick-revision)
  - [3.2 Window Functions](#32-window-functions)
    - [Overview](#overview)
    - [Architecture / Working](#architecture-working)
    - [Function Matrix](#function-matrix)
    - [Example 1 - Ranking Functions Together](#example-1-ranking-functions-together)
    - [Example 2 - Top N per Group](#example-2-top-n-per-group)
    - [Example 3 - Running Total](#example-3-running-total)
    - [Example 4 - Partition Total and Percentage of Total](#example-4-partition-total-and-percentage-of-total)
    - [Example 5 - LAG and LEAD with Defaults](#example-5-lag-and-lead-with-defaults)
    - [Example 6 - FIRST_VALUE and LAST_VALUE with Correct Frame](#example-6-firstvalue-and-lastvalue-with-correct-frame)
    - [Example 7 - NTILE for Quartiles](#example-7-ntile-for-quartiles)
    - [Example 8 - Named Window Clause](#example-8-named-window-clause)
    - [When to Use](#when-to-use)
    - [When NOT to Use](#when-not-to-use)
    - [Common Mistakes](#common-mistakes)
    - [DP-800 Exam Scenarios](#dp-800-exam-scenarios)
    - [Quick Revision](#quick-revision)
  - [3.3 Correlated Queries](#33-correlated-queries)
    - [NOT EXISTS Anti-Join Pattern](#not-exists-anti-join-pattern)
  - [3.4 TRY/CATCH and Transactions](#34-trycatch-and-transactions)
  - [3.5 Regex and Fuzzy Matching](#35-regex-and-fuzzy-matching)
    - [Regex Function Matrix](#regex-function-matrix)
    - [Fuzzy Matching](#fuzzy-matching)
    - [Exam Traps](#exam-traps)
- [4. AI-Assisted Development, Copilot, and MCP](#4-ai-assisted-development-copilot-and-mcp)
  - [4.1 Safe Copilot Usage](#41-safe-copilot-usage)
  - [4.2 GitHub Copilot Instructions](#42-github-copilot-instructions)
- [Repository Copilot Instructions](#repository-copilot-instructions)
  - [4.3 MCP Scenario Selection](#43-mcp-scenario-selection)
    - [Exam Traps](#exam-traps)
- [5. Security and Compliance](#5-security-and-compliance)
  - [5.0 Security Comparison Tables](#50-security-comparison-tables)
    - [Always Encrypted vs TDE vs Dynamic Data Masking vs Column-Level Encryption](#always-encrypted-vs-tde-vs-dynamic-data-masking-vs-column-level-encryption)
    - [Deterministic vs Randomized Always Encrypted](#deterministic-vs-randomized-always-encrypted)
    - [Managed Identity vs Service Principal](#managed-identity-vs-service-principal)
    - [GRANT vs DENY vs REVOKE](#grant-vs-deny-vs-revoke)
    - [RLS Filter Predicate vs Block Predicate](#rls-filter-predicate-vs-block-predicate)
  - [5.1 Data Protection Feature Matrix](#51-data-protection-feature-matrix)
  - [5.2 Always Encrypted](#52-always-encrypted)
  - [5.3 Column-Level Encryption](#53-column-level-encryption)
  - [5.4 Dynamic Data Masking](#54-dynamic-data-masking)
  - [5.5 Row-Level Security](#55-row-level-security)
    - [Basic Filter Predicate](#basic-filter-predicate)
    - [Filter Plus Block Predicates](#filter-plus-block-predicates)
    - [Exam Traps](#exam-traps)
  - [5.6 Permissions](#56-permissions)
  - [5.7 Passwordless Authentication and Service Connector](#57-passwordless-authentication-and-service-connector)
    - [Exam Traps](#exam-traps)
  - [5.8 Auditing](#58-auditing)
  - [5.9 Endpoint Security](#59-endpoint-security)
- [6. Performance Optimization](#6-performance-optimization)
  - [6.0 Complete Performance Diagnostic Examples](#60-complete-performance-diagnostic-examples)
    - [Example 1 - Current Requests, Waits, and Blocking](#example-1-current-requests-waits-and-blocking)
    - [Example 2 - Top CPU Queries from Query Stats](#example-2-top-cpu-queries-from-query-stats)
    - [Example 3 - Index Usage Stats](#example-3-index-usage-stats)
    - [Example 4 - Wait Stats Review](#example-4-wait-stats-review)
    - [Example 5 - Blocking Chain Focus](#example-5-blocking-chain-focus)
    - [Example 6 - Query Store Regression Investigation Pattern](#example-6-query-store-regression-investigation-pattern)
    - [Query Store vs DMVs vs Execution Plans](#query-store-vs-dmvs-vs-execution-plans)
  - [6.1 Workload Design](#61-workload-design)
  - [6.2 Diagnostic Tool Matrix](#62-diagnostic-tool-matrix)
    - [Missing Index DMV Pattern](#missing-index-dmv-pattern)
  - [6.3 Execution Plan Operators](#63-execution-plan-operators)
    - [Estimated vs Actual Execution Plan](#estimated-vs-actual-execution-plan)
  - [6.4 Query Store](#64-query-store)
  - [6.5 Blocking, Deadlocks, and Isolation](#65-blocking-deadlocks-and-isolation)
    - [Isolation Level Comparison Table](#isolation-level-comparison-table)
    - [Isolation Level Syntax](#isolation-level-syntax)
    - [Isolation Exam Traps](#isolation-exam-traps)
    - [Deadlock Pattern](#deadlock-pattern)
  - [6.6 Parameter Sniffing](#66-parameter-sniffing)
  - [6.7 Performance Exam Traps](#67-performance-exam-traps)
- [7. CI/CD with SQL Database Projects](#7-cicd-with-sql-database-projects)
  - [7.1 SQL Project Concepts](#71-sql-project-concepts)
  - [7.2 SQL Project Testing Strategy](#72-sql-project-testing-strategy)
    - [Testing Flow](#testing-flow)
    - [Exam Traps](#exam-traps)
  - [7.3 Project Structure](#73-project-structure)
  - [7.4 Static Reference Data](#74-static-reference-data)
  - [7.5 SqlPackage Commands](#75-sqlpackage-commands)
  - [7.6 Feature Branch and Deployment Flow](#76-feature-branch-and-deployment-flow)
  - [7.7 Drift Reconciliation](#77-drift-reconciliation)
  - [7.8 Secrets and Governance](#78-secrets-and-governance)
- [8. Data API Builder and Azure Integration](#8-data-api-builder-and-azure-integration)
  - [8.1 DAB Concepts](#81-dab-concepts)
  - [8.2 DAB Selection Matrix](#82-dab-selection-matrix)
  - [8.3 DAB CLI](#83-dab-cli)
  - [8.4 Basic DAB Config](#84-basic-dab-config)
  - [8.5 DAB REST API Examples](#85-dab-rest-api-examples)
    - [Get All Customers](#get-all-customers)
    - [Get One Customer by Key](#get-one-customer-by-key)
    - [Filter Rows](#filter-rows)
    - [Limit Returned Rows with $top](#limit-returned-rows-with-top)
    - [Skip Rows for Paging](#skip-rows-for-paging)
    - [Select Specific Fields](#select-specific-fields)
    - [Sort Results](#sort-results)
    - [Combined REST Query](#combined-rest-query)
    - [REST Exam Traps](#rest-exam-traps)
  - [8.6 DAB GraphQL Field-Level Security](#86-dab-graphql-field-level-security)
  - [8.7 DAB GraphQL Query Examples](#87-dab-graphql-query-examples)
    - [Query Customers](#query-customers)
    - [Query with Filter and First N Rows](#query-with-filter-and-first-n-rows)
    - [Relationship Traversal Example](#relationship-traversal-example)
    - [Mutation Example for a Data-Changing Stored Procedure](#mutation-example-for-a-data-changing-stored-procedure)
    - [GraphQL Exam Traps](#graphql-exam-traps)
  - [8.8 Stored Procedure as GraphQL Mutation](#88-stored-procedure-as-graphql-mutation)
  - [8.9 DAB Caching](#89-dab-caching)
  - [8.10 Azure Monitor, Application Insights, and Log Analytics](#810-azure-monitor-application-insights-and-log-analytics)
  - [8.11 Change Handling](#811-change-handling)
- [9. Models, Embeddings, and External AI](#9-models-embeddings-and-external-ai)
  - [9.1 Model Selection](#91-model-selection)
    - [Model Evaluation Table](#model-evaluation-table)
    - [Model Evaluation Checklist](#model-evaluation-checklist)
  - [9.2 Embedding Column Selection](#92-embedding-column-selection)
  - [9.3 Chunking](#93-chunking)
  - [9.4 Embedding Table Design](#94-embedding-table-design)
    - [Exam Traps](#exam-traps)
  - [9.5 SQL AI Conceptual Functions - Platform-Dependent Syntax](#95-sql-ai-conceptual-functions-platform-dependent-syntax)
    - [AI_GENERATE_CHUNKS - Conceptual Pattern](#aigeneratechunks-conceptual-pattern)
    - [AI_GENERATE_EMBEDDINGS - Conceptual Pattern](#aigenerateembeddings-conceptual-pattern)
    - [Conceptual Flow](#conceptual-flow)
    - [Exam Traps](#exam-traps)
  - [9.6 Embedding Maintenance](#96-embedding-maintenance)
  - [9.7 External Models and Endpoint Credentials](#97-external-models-and-endpoint-credentials)
    - [Managed Identity Credential](#managed-identity-credential)
    - [API Key Credential Pattern](#api-key-credential-pattern)
    - [Alter Existing External Model](#alter-existing-external-model)
    - [Secure Model Invocation Scenario](#secure-model-invocation-scenario)
- [10. Intelligent Search](#10-intelligent-search)
  - [10.1 Search Type Selection](#101-search-type-selection)
    - [LIKE vs CONTAINS vs FREETEXT](#like-vs-contains-vs-freetext)
  - [10.2 Full-Text Search](#102-full-text-search)
    - [Exact Phrase Plus Linguistic Match](#exact-phrase-plus-linguistic-match)
    - [Complete Full-Text Example Pack](#complete-full-text-example-pack)
    - [Full-Text Exam Traps](#full-text-exam-traps)
  - [10.3 Vector Data Type and Search](#103-vector-data-type-and-search)
    - [Complete Vector Example Pack](#complete-vector-example-pack)
    - [Vector Exam Traps](#vector-exam-traps)
    - [Vector Function Matrix](#vector-function-matrix)
  - [10.4 Vector Metrics and Indexing](#104-vector-metrics-and-indexing)
    - [Exam Traps](#exam-traps)
  - [10.5 Hybrid Search and RRF](#105-hybrid-search-and-rrf)
    - [Exam Traps](#exam-traps)
  - [10.6 Search Evaluation Metrics](#106-search-evaluation-metrics)
- [11. Retrieval-Augmented Generation - RAG](#11-retrieval-augmented-generation-rag)
  - [11.1 RAG Architecture](#111-rag-architecture)
  - [11.2 RAG Decision Matrix](#112-rag-decision-matrix)
    - [Complete RAG Example Pack](#complete-rag-example-pack)
    - [RAG Common Mistakes](#rag-common-mistakes)
  - [11.3 Build Model Request Body](#113-build-model-request-body)
  - [11.4 Call Model Endpoint](#114-call-model-endpoint)
  - [11.5 Extract Long Assistant Answer](#115-extract-long-assistant-answer)
  - [11.6 RAG Security Checklist](#116-rag-security-checklist)
- [12. Consolidated Practice Questions](#12-consolidated-practice-questions)
  - [12.1 Domain 1](#121-domain-1)
  - [12.2 Domain 2](#122-domain-2)
  - [12.3 Domain 3](#123-domain-3)
- [13. Final Must-Memorize Facts](#13-final-must-memorize-facts)
  - [Database Design](#database-design)
  - [Programmability](#programmability)
  - [Security](#security)
  - [Performance](#performance)
  - [CI/CD and Integration](#cicd-and-integration)
  - [AI and RAG](#ai-and-rag)
- [14. Seven-Day Revision Plan](#14-seven-day-revision-plan)
- [15. Deduplication and Move Log](#15-deduplication-and-move-log)
- [16. Source Note](#16-source-note)
- [17. DP-800 Skills Coverage Matrix](#17-dp-800-skills-coverage-matrix)
- [18. Final Validation Report for V3](#18-final-validation-report-for-v3)
  - [18.1 Deduplication Validation](#181-deduplication-validation)
  - [18.2 Content Preservation Validation](#182-content-preservation-validation)
  - [18.3 Maintainability Guidance](#183-maintainability-guidance)
  - [18.4 Final Quality Checklist](#184-final-quality-checklist)

---

## How This Version Was Cleaned Up

The uploaded README had grown through multiple additions: original guide, expanded scenario cheat sheets, syntax pack, top facts, practice questions, practice exam gap addendum, and later scenario decision packs. That made the content correct but scattered.

In this version:

- Repeated **RLS** content is merged under **Security > Row-Level Security**.
- Repeated **DAB** content is merged under **Data API Builder**.
- Repeated **JSON** examples are merged under **JSON and Semi-Structured Data**.
- Repeated **Query Store, DMVs, blocking, deadlocks, Key Lookups, parameter sniffing** are merged under **Performance**.
- Repeated **Vector, ANN/ENN, hybrid search, RRF, RAG** content is merged under **AI Capabilities**.
- Repeated **decision trees, cheat sheets, traps, and must-memorize facts** are converted into topic-level scenario tables.
- Practice-exam gaps are moved into the exact topic where they belong instead of remaining as addendums.

---

# 0. DP-800 Exam Blueprint and Mindset

## 0.1 Exam Domains

| Domain | Weight | Master these areas |
|---|---:|---|
| Design and develop database solutions | 35-40% | Data types, tables, constraints, indexes, JSON, graph tables, temporal/ledger/external/memory-optimized tables, programmability, advanced T-SQL, Copilot/MCP |
| Secure, optimize, and deploy database solutions | 35-40% | Always Encrypted, Column-level encryption, Dynamic Data Masking, RLS, permissions, auditing, DMVs, Query Store, execution plans, CI/CD, SQL projects, DAB, Azure integration |
| Implement AI capabilities in database solutions | 25-30% | Models, external endpoints, embeddings, vector data type, vector search, ANN/ENN, full-text search, hybrid search, RRF, RAG, JSON prompt/response handling |

## 0.2 Scenario Question Method

When reading a DP-800 question, identify the action word:

| Requirement wording | Think |
|---|---|
| Historical row versions, point-in-time | Temporal table |
| Tamper-evident, cryptographic proof | Ledger table |
| Insert-only immutable audit records | Append-only ledger |
| Hide displayed values | Dynamic Data Masking |
| Protect from DBA/admin plaintext access | Always Encrypted |
| Tenant/user rows only | Row-Level Security |
| Stop invalid tenant writes | RLS block predicates |
| Currently executing requests, waits, blocker | `sys.dm_exec_requests` |
| Query was fast before, slow now | Query Store |
| API without custom code | Data API Builder |
| Exact phrase, keyword, word forms | Full-text search |
| Meaning, synonyms, semantic similarity | Vector search |
| Keyword plus semantic ranking | Hybrid search + RRF |
| Current enterprise data grounded answer | RAG |
| Long model response over 4,000 chars | `OPENJSON WITH nvarchar(max)` |

---

# 1. Database Design and Database Objects

## 1.1 Data Types

### What to Know

Choosing the correct data type affects correctness, storage, indexing, and query performance. DP-800 often tests whether you can match a business requirement to the smallest correct type.

### Selection Matrix

| Requirement | Best choice | Why | Exam trap |
|---|---|---|---|
| True/false flag | `bit` | Stores 0, 1, or NULL | Do not store flags as strings |
| Small numeric domain | `tinyint` / `smallint` | Saves space for small ranges | Check range before choosing |
| Standard key/counter | `int` | Common default integer | Not enough for very large counters |
| Huge fact table counter | `bigint` | Larger range | Bigger indexes and storage |
| Exact financial calculation | `decimal(p,s)` / `numeric(p,s)` | Exact precision | Avoid `float` for money |
| Approximate scientific value | `float` / `real` | Approximate numeric | Equality comparisons can be unreliable |
| Non-Unicode text | `varchar(n)` / `varchar(max)` | Smaller if Unicode not needed | Not suitable for multilingual data |
| Unicode or multilingual text | `nvarchar(n)` / `nvarchar(max)` | Supports Unicode | More storage than varchar |
| JSON text | `nvarchar(max)` | SQL JSON functions operate on text | Index searchable JSON paths using computed columns |
| Fixed binary | `binary(n)` | Fixed-size binary values | Not for large files |
| Variable binary or files | `varbinary(max)` | Images, files, encrypted payloads | Do not use text unless required |
| Date only | `date` | Stores date without time | No time component |
| Time only | `time` | Stores time without date | No date component |
| Date and time | `datetime2` | Preferred high precision | Legacy `datetime` is less precise |
| Time zone offset | `datetimeoffset` | Stores offset | Useful when offset matters |
| Distributed unique ID | `uniqueidentifier` | Globally unique | Random GUID as clustered key can fragment |
| XML document | `xml` | XML-specific operations | Use only when XML is required |
| Mixed type values | `sql_variant` | Stores different data types | Rare, avoid unless required |
| Embedding vector | `vector(n)` | Native vector storage | Dimension must match model output |

### Syntax Examples

```sql
CREATE TABLE dbo.CustomerProfile
(
    CustomerID int NOT NULL PRIMARY KEY,
    DisplayName nvarchar(100) NOT NULL,
    ProfileJson nvarchar(max) NULL,
    ProfilePhoto varbinary(max) NULL,
    CreatedAt datetime2(7) NOT NULL DEFAULT SYSUTCDATETIME()
);
```

```sql
CREATE TABLE dbo.ProductCatalog
(
    ProductID int NOT NULL PRIMARY KEY,
    ProductName nvarchar(200) NOT NULL,
    Description nvarchar(max) NOT NULL,
    ProductEmbedding vector(1536) NULL
);
```

### Must Memorize

- Use `decimal` or `numeric` for exact financial values.
- Use `nvarchar` for Unicode and JSON payloads.
- Use `datetime2` over legacy `datetime` where possible.
- Use `datetimeoffset` when time zone offset is part of the requirement.
- `vector(n)` dimension must match the embedding model output.

---

## 1.2 Constraints, Identity, and Sequences

### What to Know

Constraints enforce data quality at write time. Sequences and identity values generate numbers, but they serve different design needs.

| Requirement | Feature | Why |
|---|---|---|
| Unique row identifier | Primary key | Unique and not null |
| Parent-child relationship | Foreign key | Referential integrity |
| Unique non-primary attribute | Unique constraint | Prevents duplicates |
| Rule such as salary > 0 | Check constraint | Validates business rule |
| Default value when omitted | Default constraint | Supplies value at insert |
| Table-specific auto-number | Identity | Bound to one table |
| Shared number generator | Sequence | Independent object usable across tables |

```sql
CREATE TABLE dbo.Department
(
    DeptID int NOT NULL PRIMARY KEY,
    DeptName nvarchar(100) NOT NULL UNIQUE
);

CREATE TABLE dbo.Employee
(
    EmployeeID int IDENTITY(1,1) NOT NULL PRIMARY KEY,
    DeptID int NOT NULL,
    Email nvarchar(255) NULL UNIQUE,
    Salary decimal(12,2) NOT NULL CHECK (Salary > 0),
    Status varchar(20) NOT NULL DEFAULT 'Active',
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

### Exam Traps

- Choose **identity** when the value belongs only to one table.
- Choose **sequence** when multiple tables need a shared number source.
- A `DEFAULT` supplies missing values; a `CHECK` validates allowed values.

---

## 1.3 Index Design

### What to Know

Indexes support access patterns. DP-800 tests the ability to choose the right index from symptoms such as Key Lookup, large scans, OLTP analytics, JSON property search, or vector search.

### Index Selection Matrix

| Scenario | Best index/pattern | Why |
|---|---|---|
| One-row lookup by email/customer ID | Nonclustered index | Fast seek |
| Date range queries | Clustered or nonclustered index on date | Supports range access |
| Repeated Key Lookup | Add included columns | Covers returned columns |
| Multi-column filters | Composite index | Supports combined predicates |
| Equality plus range predicate | Equality column first, range later | Better seek pattern |
| Frequent subset e.g., open orders | Filtered index | Smaller targeted index |
| Analytics over millions of rows | Clustered columnstore | Compression and batch mode |
| OLTP table plus analytics dashboard | Nonclustered columnstore | Preserves rowstore lookup |
| JSON property filtering | Computed column + index | Indexes extracted value |
| Full-text keyword search | Full-text index | Enables CONTAINS/FREETEXT |
| Semantic vector search at scale | Vector/ANN index where supported | Accelerates nearest-neighbor search |

### Rowstore Examples

```sql
CREATE NONCLUSTERED INDEX IX_Orders_CustomerID
ON dbo.Orders(CustomerID)
INCLUDE (OrderDate, TotalAmount, ShippingAddress);
```

```sql
CREATE NONCLUSTERED INDEX IX_Orders_OpenOrders
ON dbo.Orders(CustomerID, OrderDate)
WHERE Status = 'Open';
```

### Composite Index Rule

```sql
CREATE NONCLUSTERED INDEX IX_Orders_Customer_Date
ON dbo.Orders(CustomerID, OrderDate DESC)
INCLUDE (TotalAmount, Status);
```

**Memory:** Equality predicates generally come before range predicates.

### Columnstore Examples

```sql
CREATE CLUSTERED COLUMNSTORE INDEX CCI_FactSales
ON dbo.FactSales;
```

```sql
CREATE NONCLUSTERED COLUMNSTORE INDEX NCCI_EventLog_Dashboard
ON dbo.EventLog(CreatedAt, CustomerID, Severity, DurationMs);
```

### Key Lookup Scenario

If a plan has an index seek followed by many Key Lookups, and estimated/actual rows are similar, the first fix is usually to add missing projected columns as `INCLUDE` columns.

### Exam Traps

- Updating statistics is not the first answer when row estimates are already accurate and Key Lookup dominates.
- Low-selectivity columns like `IsActive` are often weak standalone index keys, but can be useful in filtered indexes.
- Columnstore is not the default for high-frequency OLTP updates.
- Nonclustered columnstore can accelerate dashboard analytics while preserving clustered rowstore lookup.

---

## 1.4 Partitioning

### What to Know

Partitioning helps manage very large tables and can support partition elimination and fast archive/switch operations.

### Use When

- Large table, commonly filtered by date.
- Need to archive completed months/years quickly.
- Need easier maintenance of old partitions.
- Need partition elimination for queries.

### Syntax Pattern

```sql
CREATE PARTITION FUNCTION PF_Orders_OrderDate(date)
AS RANGE RIGHT FOR VALUES
(
    '2026-01-01', '2026-02-01', '2026-03-01'
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

### Exam Traps

- Monthly archive/switch requires monthly partitions, not quarterly.
- Aligned indexes use the same partition scheme as the table.
- The partition column should be part of the clustered key for aligned partitioned designs.

---

## 1.5 Specialized Tables

### Selection Matrix

| Requirement | Use | Description | Key syntax |
|---|---|---|---|
| Historical row versions | Temporal table | Maintains current and history tables | `SYSTEM_VERSIONING = ON` |
| Tamper evidence | Ledger table | Cryptographically verifiable changes | `LEDGER = ON` |
| Insert-only immutable log | Append-only ledger | Prevents update/delete | `LEDGER_TYPE = APPEND_ONLY` |
| Ultra-low-latency OLTP | Memory-optimized table | In-memory OLTP | `MEMORY_OPTIMIZED = ON` |
| Query data outside SQL | External table | Query files/lake data in place | `CREATE EXTERNAL TABLE` |
| Multi-hop relationships | Graph tables | Node/edge/MATCH patterns | `AS NODE`, `AS EDGE` |

### Memory-Optimized Tables

```sql
CREATE TABLE dbo.HighFreqTelemetry
(
    SessionID int NOT NULL PRIMARY KEY NONCLUSTERED,
    DeviceID int NOT NULL,
    Payload varchar(500) NOT NULL
)
WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA);
```

| Durability | Meaning | Use case |
|---|---|---|
| `SCHEMA_AND_DATA` | Schema and data persist | Critical low-latency OLTP |
| `SCHEMA_ONLY` | Data lost after restart | Session state, transient cache |

### Temporal Tables

```sql
CREATE TABLE dbo.Employee
(
    EmployeeID int PRIMARY KEY,
    Name nvarchar(100) NOT NULL,
    Salary decimal(18,2) NOT NULL,
    ValidFrom datetime2 GENERATED ALWAYS AS ROW START NOT NULL,
    ValidTo datetime2 GENERATED ALWAYS AS ROW END NOT NULL,
    PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
)
WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.EmployeeHistory));

SELECT *
FROM dbo.Employee
FOR SYSTEM_TIME AS OF '2026-06-01T10:00:00';
```

### Ledger Tables

```sql
CREATE TABLE dbo.FinancialAuditTrail
(
    TransactionID int IDENTITY PRIMARY KEY,
    AccountID int NOT NULL,
    Amount decimal(18,2) NOT NULL
)
WITH (LEDGER = ON (LEDGER_TYPE = APPEND_ONLY));
```

### External Tables

```sql
CREATE EXTERNAL TABLE dbo.ExternalSales
(
    SaleID int,
    Amount decimal(18,2)
)
WITH
(
    LOCATION = '/salesdata/*.parquet',
    DATA_SOURCE = MyAzureStorageSource,
    FILE_FORMAT = ParquetFormat
);
```

### Graph Tables

```sql
CREATE TABLE dbo.Person
(
    ID int PRIMARY KEY,
    Name nvarchar(100)
) AS NODE;

CREATE TABLE dbo.FriendOf AS EDGE;

SELECT p2.Name AS FriendName
FROM dbo.Person AS p1,
     dbo.FriendOf AS f,
     dbo.Person AS p2
WHERE MATCH(p1-(f)->p2)
  AND p1.Name = N'Alice';
```

### Shortest Path Graph Pattern

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

### Complete Graph Query Example Pack

#### Example 1 - Create Node and Edge Tables

```sql
CREATE TABLE dbo.Person
(
    PersonID int PRIMARY KEY,
    PersonName nvarchar(100) NOT NULL
) AS NODE;

CREATE TABLE dbo.Company
(
    CompanyID int PRIMARY KEY,
    CompanyName nvarchar(100) NOT NULL
) AS NODE;

CREATE TABLE dbo.WorksFor
(
    StartDate date NULL,
    JobTitle nvarchar(100) NULL
) AS EDGE;
```

#### Example 2 - Insert Nodes and Edges

```sql
INSERT INTO dbo.Person(PersonID, PersonName)
VALUES (1, N'Asha'), (2, N'Ravi');

INSERT INTO dbo.Company(CompanyID, CompanyName)
VALUES (10, N'Contoso');

INSERT INTO dbo.WorksFor($from_id, $to_id, StartDate, JobTitle)
SELECT p.$node_id, c.$node_id, '2024-01-01', N'Architect'
FROM dbo.Person AS p
CROSS JOIN dbo.Company AS c
WHERE p.PersonID = 1
  AND c.CompanyID = 10;
```

#### Example 3 - MATCH Query

```sql
SELECT
    p.PersonName,
    c.CompanyName,
    wf.JobTitle
FROM dbo.Person AS p,
     dbo.WorksFor AS wf,
     dbo.Company AS c
WHERE MATCH(p-(wf)->c);
```

#### Example 4 - Multi-Hop SHORTEST_PATH Query

```sql
SELECT
    StartPerson.PersonName AS StartPerson,
    LAST_VALUE(ConnectedPerson.PersonName) WITHIN GROUP (GRAPH PATH) AS ConnectedPerson,
    COUNT(ConnectedPerson.PersonName) WITHIN GROUP (GRAPH PATH) AS HopCount
FROM dbo.Person AS StartPerson,
     dbo.Knows FOR PATH AS k,
     dbo.Person FOR PATH AS ConnectedPerson
WHERE MATCH
(
    SHORTEST_PATH(StartPerson(-(k)->ConnectedPerson){1,3})
)
AND StartPerson.PersonName = N'Asha';
```

#### Graph Decision Tree

1. Relationship traversal is central to the problem? Consider graph tables.
2. Simple parent-child hierarchy only? Recursive CTE may be simpler.
3. Normal relational joins are enough? Use standard foreign keys and joins.
4. Need variable-length traversal? Use graph query pattern with `SHORTEST_PATH` where supported.

### Exam Traps

- Temporal = history; Ledger = tamper evidence.
- Append-only ledger is best for insert-only compliance trails.
- Graph is best when relationship traversal itself is the core query.
- External tables query data in place; they are not the same as importing data.

---

## 1.6 JSON and Semi-Structured Data

### What to Know

SQL stores JSON as text, commonly `nvarchar(max)`. The exam tests how to extract scalar values, objects, arrays, expand arrays into rows, index JSON properties, and create JSON for AI/RAG prompts.

### JSON Function Matrix

| Function | Purpose | Returns | Use case |
|---|---|---|---|
| `JSON_VALUE` | Extract scalar | Scalar text | Status, customer id, postcode |
| `JSON_QUERY` | Extract object/array | JSON fragment | Address object, tags array |
| `OPENJSON` | Convert JSON to rows | Rowset | Items array to relational rows |
| `JSON_OBJECT` | Build object | JSON | Model request object |
| `JSON_ARRAY` | Build array | JSON | Message array |
| `JSON_ARRAYAGG` | Aggregate values into array | JSON | IDs/tags array |
| `JSON_CONTAINS` | Test containment where supported | Predicate | Tag contains Premium |
| `FOR JSON PATH` | Convert SQL rows to JSON | JSON array/object | RAG context payload |

### JSON Property Indexing

```sql
CREATE TABLE dbo.Orders
(
    OrderID int PRIMARY KEY,
    OrderJson nvarchar(max) NOT NULL,
    CustomerCity AS JSON_VALUE(OrderJson, '$.customer.city')
);

CREATE INDEX IX_Orders_CustomerCity
ON dbo.Orders(CustomerCity);
```

### JSON Array Expansion

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

### JSON for RAG Context

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
```

### Single-Row Object Instead of Array

```sql
SELECT
    CustomerID AS customerId,
    CustomerName AS customerName,
    LoyaltyTier AS loyaltyTier
FROM dbo.Customer
WHERE CustomerID = @CustomerID
FOR JSON PATH, INCLUDE_NULL_VALUES, WITHOUT_ARRAY_WRAPPER;
```

### Complete JSON Example Pack

#### Example 1 - Extract Scalar Values with JSON_VALUE

```sql
SELECT
    OrderID,
    JSON_VALUE(OrderJson, '$.customer.id') AS CustomerID,
    JSON_VALUE(OrderJson, '$.customer.city') AS CustomerCity,
    JSON_VALUE(OrderJson, '$.status') AS OrderStatus
FROM dbo.JsonOrders
WHERE JSON_VALUE(OrderJson, '$.status') = N'Completed';
```

#### Example 2 - Extract Object or Array with JSON_QUERY

```sql
SELECT
    OrderID,
    JSON_QUERY(OrderJson, '$.customer.address') AS AddressObject,
    JSON_QUERY(OrderJson, '$.items') AS ItemsArray
FROM dbo.JsonOrders;
```

#### Example 3 - Expand JSON Array with OPENJSON

```sql
SELECT
    o.OrderID,
    item.Sku,
    item.Quantity,
    item.UnitPrice
FROM dbo.JsonOrders AS o
CROSS APPLY OPENJSON(o.OrderJson, '$.items')
WITH
(
    Sku nvarchar(50) '$.sku',
    Quantity int '$.quantity',
    UnitPrice decimal(18,2) '$.unitPrice'
) AS item;
```

#### Example 4 - Combine Root Scalar Extraction with Array Expansion

```sql
SELECT
    o.OrderID,
    JSON_VALUE(o.OrderJson, '$.customer.id') AS CustomerID,
    JSON_VALUE(o.OrderJson, '$.customer.tier') AS CustomerTier,
    item.Sku,
    item.Quantity
FROM dbo.JsonOrders AS o
CROSS APPLY OPENJSON(o.OrderJson, '$.items')
WITH
(
    Sku nvarchar(50) '$.sku',
    Quantity int '$.quantity'
) AS item
WHERE JSON_VALUE(o.OrderJson, '$.status') = N'Completed';
```

#### Example 5 - Build JSON Object and Array

```sql
SELECT JSON_OBJECT
(
    'customerId': CustomerID,
    'customerName': CustomerName,
    'tier': LoyaltyTier
) AS CustomerJson
FROM Sales.Customer
WHERE CustomerID = @CustomerID;
```

```sql
SELECT JSON_ARRAY(N'pending', N'completed', N'cancelled') AS StatusList;
```

#### Example 6 - Aggregate Rows into JSON Array

```sql
SELECT
    CustomerID,
    JSON_ARRAYAGG(OrderID) AS OrderIds
FROM Sales.Orders
GROUP BY CustomerID;
```

#### Example 7 - JSON_CONTAINS Pattern

Use this pattern when the platform supports `JSON_CONTAINS` and the requirement is containment testing inside a JSON document.

```sql
SELECT ProductID, ProductName
FROM dbo.Product
WHERE JSON_CONTAINS(ProductAttributes, JSON_OBJECT('tag':'Premium'), '$.tags') = 1;
```

#### Example 8 - FOR JSON PATH for AI/RAG Context

```sql
DECLARE @ContextJson nvarchar(max);

SELECT @ContextJson =
(
    SELECT
        ProductID AS productId,
        ProductName AS productName,
        Description AS description,
        Price AS price
    FROM dbo.Product
    WHERE CategoryID = @CategoryID
    FOR JSON PATH, INCLUDE_NULL_VALUES
);
```

#### Example 9 - Single JSON Object Without Array Wrapper

```sql
SELECT
    CustomerID AS customerId,
    CustomerName AS customerName,
    LoyaltyTier AS loyaltyTier
FROM Sales.Customer
WHERE CustomerID = @CustomerID
FOR JSON PATH, INCLUDE_NULL_VALUES, WITHOUT_ARRAY_WRAPPER;
```

### JSON Decision Tree

1. Need one scalar value? Use `JSON_VALUE`.
2. Need object or array fragment? Use `JSON_QUERY`.
3. Need JSON array values as relational rows? Use `OPENJSON`.
4. Need SQL rows converted to JSON for model input? Use `FOR JSON PATH`.
5. Need a single object instead of array? Add `WITHOUT_ARRAY_WRAPPER`.
6. Need null values retained? Add `INCLUDE_NULL_VALUES`.
7. Need to search a JSON property efficiently? Use computed column plus index.

### Exam Traps

- `JSON_VALUE` is for scalar values only.
- `JSON_QUERY` is for object/array fragments.
- `OPENJSON` is the answer when an array must become rows.
- `FOR JSON PATH` returns an array by default.
- Add `WITHOUT_ARRAY_WRAPPER` for a single top-level object.
- Add `INCLUDE_NULL_VALUES` when null properties must be preserved.

---

# 2. Programmability Objects

## 2.1 Object Selection Matrix

| Requirement | Use | Why |
|---|---|---|
| Reusable scalar calculation | Scalar function | Returns one value |
| Parameterized rowset used in joins | Inline TVF | Composable table expression |
| Multi-step table-returning function | Multi-statement TVF | Allows procedural logic and return table variable |
| Simplify/secure read projection | View | Saved SELECT, no parameters |
| Persist expensive aggregate | Indexed view | Materialized view with unique clustered index |
| Data-change workflow or transaction | Stored procedure | Supports DML, transactions, outputs |
| Validate/audit after DML | AFTER trigger | Runs after operation before commit |
| Replace DML behavior | INSTEAD OF trigger | Runs instead of operation |

## 2.2 Views and Indexed Views

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
GO

CREATE UNIQUE CLUSTERED INDEX CIX_vw_DailySales
ON dbo.vw_DailySales(OrderDate);
```

### Exam Traps

- Views do not accept parameters; use inline TVF for parameterized rowsets.
- Indexed views help repeated expensive reads but increase write maintenance cost.

## 2.3 Scalar Functions

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

Use when one value must be called directly in a `SELECT` list, `WHERE` predicate, or computed expression.

## 2.4 Inline Table-Valued Functions

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

### CROSS APPLY vs OUTER APPLY

| Pattern | Use when |
|---|---|
| `CROSS APPLY` | Return only outer rows where function returns rows |
| `OUTER APPLY` | Keep outer rows even when function returns no rows |

## 2.5 Stored Procedures

Stored procedures are best for reusable commands, workflows, DML, transactions, and returning result sets plus output parameters.

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

### Exam Traps

- Return codes are for execution status, not business data.
- Output parameters must be initialized on all code paths.
- Use stored procedures for transactional DML logic, not functions.

## 2.6 Triggers

### AFTER Trigger

```sql
CREATE OR ALTER TRIGGER Sales.tr_ValidateOrderCustomer
ON Sales.Orders
AFTER INSERT, UPDATE
AS
BEGIN
    SET NOCOUNT ON;
    IF (ROWCOUNT_BIG() = 0) RETURN;

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

### Trigger Rules

- Triggers fire once per statement, not once per row.
- Write set-based logic against `inserted` and `deleted`.
- Use `AFTER` to audit or validate after the original operation.
- Use `INSTEAD OF` to replace default write behavior, often for complex views.

---

# 3. Advanced T-SQL

## 3.1 CTE and Recursive CTE

### Overview

A Common Table Expression (CTE) is a named temporary result set defined within a single statement. It improves readability for complex queries, supports layered transformations, and enables recursive patterns such as employee hierarchy traversal.

### Purpose

Use CTEs when you need to:

- Break a complex query into readable logical steps.
- Reuse a derived result inside the same statement.
- Build hierarchical queries using recursion.
- Prepare ranked, filtered, or aggregated data before final selection.

### Syntax

```sql
WITH CteName AS
(
    SELECT column1, column2
    FROM dbo.TableName
)
SELECT column1, column2
FROM CteName;
```

### Example 1 - Plain CTE for Aggregation

This is the most basic exam pattern. The CTE calculates total sales per customer, and the outer query filters high-value customers.

```sql
WITH CustomerSales AS
(
    SELECT
        CustomerID,
        SUM(TotalAmount) AS TotalSales,
        COUNT(*) AS OrderCount
    FROM Sales.Orders
    GROUP BY CustomerID
)
SELECT
    CustomerID,
    TotalSales,
    OrderCount
FROM CustomerSales
WHERE TotalSales >= 10000
ORDER BY TotalSales DESC;
```

### Example 2 - Multiple CTEs in One Query

Use multiple CTEs when each step has a separate purpose. This keeps the query easy to review.

```sql
WITH MonthlySales AS
(
    SELECT
        CustomerID,
        DATEFROMPARTS(YEAR(OrderDate), MONTH(OrderDate), 1) AS SalesMonth,
        SUM(TotalAmount) AS MonthAmount
    FROM Sales.Orders
    GROUP BY CustomerID, DATEFROMPARTS(YEAR(OrderDate), MONTH(OrderDate), 1)
),
CustomerTotals AS
(
    SELECT
        CustomerID,
        SUM(MonthAmount) AS TotalAmount,
        COUNT(*) AS ActiveMonths
    FROM MonthlySales
    GROUP BY CustomerID
)
SELECT
    CustomerID,
    TotalAmount,
    ActiveMonths
FROM CustomerTotals
WHERE ActiveMonths >= 3;
```

### Example 3 - CTE with Window Function

A common exam pattern is to calculate rankings inside a CTE and filter from the outer query.

```sql
WITH RankedOrders AS
(
    SELECT
        OrderID,
        CustomerID,
        OrderDate,
        TotalAmount,
        ROW_NUMBER() OVER
        (
            PARTITION BY CustomerID
            ORDER BY OrderDate DESC, OrderID DESC
        ) AS OrderRank
    FROM Sales.Orders
)
SELECT
    OrderID,
    CustomerID,
    OrderDate,
    TotalAmount
FROM RankedOrders
WHERE OrderRank = 1;
```

### Example 4 - Recursive CTE for Hierarchy

Recursive CTEs contain an anchor member and a recursive member joined by `UNION ALL`.

```sql
WITH EmployeeHierarchy AS
(
    -- Anchor member: top-level employees
    SELECT
        EmployeeID,
        ManagerID,
        DisplayName,
        0 AS Depth,
        CAST(DisplayName AS nvarchar(max)) AS HierarchyPath
    FROM HumanResources.Employee
    WHERE ManagerID IS NULL

    UNION ALL

    -- Recursive member: employees reporting to previous level
    SELECT
        e.EmployeeID,
        e.ManagerID,
        e.DisplayName,
        h.Depth + 1 AS Depth,
        CONCAT(h.HierarchyPath, N' > ', e.DisplayName) AS HierarchyPath
    FROM HumanResources.Employee AS e
    INNER JOIN EmployeeHierarchy AS h
        ON e.ManagerID = h.EmployeeID
)
SELECT
    EmployeeID,
    ManagerID,
    DisplayName,
    Depth,
    HierarchyPath
FROM EmployeeHierarchy
ORDER BY HierarchyPath;
```

### Example 5 - Recursive CTE with MAXRECURSION

Use `MAXRECURSION` when you want to protect the query from accidental infinite recursion.

```sql
WITH NumberSeries AS
(
    SELECT 1 AS NumberValue
    UNION ALL
    SELECT NumberValue + 1
    FROM NumberSeries
    WHERE NumberValue < 100
)
SELECT NumberValue
FROM NumberSeries
OPTION (MAXRECURSION 100);
```

### CTE vs Derived Table vs Temp Table

| Feature | CTE | Derived table | Temp table |
|---|---|---|---|
| Scope | One statement | One statement | Session or procedure scope |
| Reusable across multiple statements | No | No | Yes |
| Indexable directly | No | No | Yes |
| Best for readability | Yes | Sometimes | Not primarily |
| Best for multi-step stored procedure logic | No | No | Yes |
| Supports recursion | Yes | No | No |

### When to Use

- You need readable one-statement transformations.
- You need recursion for hierarchy or number generation.
- You need to calculate rank then filter in an outer query.

### When NOT to Use

- You need to reuse the result across multiple statements.
- You need indexes on intermediate results.
- The logic is easier to manage with a temp table in a stored procedure.

### Common Mistakes

- Thinking a CTE is physically materialized like a temp table.
- Referencing a CTE in a second separate statement.
- Forgetting the anchor member in a recursive CTE.
- Reversing the parent-child join in hierarchy recursion.
- Forgetting `MAXRECURSION` protection in open-ended recursive logic.

### DP-800 Exam Scenarios

| Scenario | Best answer |
|---|---|
| Need readable query step before final filter | Plain CTE |
| Need latest order per customer | CTE with `ROW_NUMBER()` then filter `WHERE RowNum = 1` |
| Need employee hierarchy with levels | Recursive CTE |
| Need reusable intermediate results across multiple procedure statements | Temp table, not CTE |
| Need index on intermediate result | Temp table, not CTE |

### DP-800 Exam Traps

- Recursive CTE uses anchor + recursive member + `UNION ALL`.
- CTE exists only for the immediately following statement.
- Recursive join for employee hierarchy is child `ManagerID` to parent `EmployeeID`.
- `MAXRECURSION 0` means no recursion limit, so use carefully.

### Quick Revision

- Plain CTE = readability.
- Multiple CTEs = staged transformation.
- Recursive CTE = hierarchy, tree, graph-like traversal, number/date series.
- CTE is not a persisted or indexed object.

## 3.2 Window Functions

### Overview

Window functions calculate values across a set of rows related to the current row without collapsing rows like `GROUP BY`. They are heavily tested in SQL exams because they solve ranking, running totals, previous/next value, and partitioned aggregate problems.

### Architecture / Working

A window function commonly uses:

- `PARTITION BY` to split rows into groups.
- `ORDER BY` to define sequence within each partition.
- A frame such as `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` for running calculations.

### Function Matrix

| Function | Purpose | Tie behavior / note |
|---|---|---|
| `ROW_NUMBER()` | Unique sequence per partition | Always unique, no tie reuse |
| `RANK()` | Ranking with gaps | Ties share rank, gaps appear |
| `DENSE_RANK()` | Ranking without gaps | Ties share rank, no gaps |
| `NTILE(n)` | Divide ordered rows into buckets | Useful for quartiles/percentiles |
| `LAG()` | Previous row value | Can specify offset and default |
| `LEAD()` | Next row value | Can specify offset and default |
| `FIRST_VALUE()` | First value in ordered window | Frame matters |
| `LAST_VALUE()` | Last value in ordered window | Frame matters, common trap |
| `SUM() OVER` | Running or partition total | Aggregate without collapsing rows |
| `AVG() OVER` | Moving or partition average | Aggregate per row |
| `COUNT() OVER` | Count rows in partition | Useful for duplication checks |

### Example 1 - Ranking Functions Together

This example shows the difference between `ROW_NUMBER`, `RANK`, and `DENSE_RANK` when salaries tie.

```sql
SELECT
    EmployeeID,
    DepartmentID,
    Salary,
    ROW_NUMBER() OVER
    (
        PARTITION BY DepartmentID
        ORDER BY Salary DESC, EmployeeID
    ) AS RowNumberValue,
    RANK() OVER
    (
        PARTITION BY DepartmentID
        ORDER BY Salary DESC
    ) AS RankValue,
    DENSE_RANK() OVER
    (
        PARTITION BY DepartmentID
        ORDER BY Salary DESC
    ) AS DenseRankValue
FROM HumanResources.EmployeeSalary;
```

### Example 2 - Top N per Group

```sql
WITH RankedEmployees AS
(
    SELECT
        EmployeeID,
        DepartmentID,
        Salary,
        ROW_NUMBER() OVER
        (
            PARTITION BY DepartmentID
            ORDER BY Salary DESC, EmployeeID
        ) AS SalaryRank
    FROM HumanResources.EmployeeSalary
)
SELECT
    EmployeeID,
    DepartmentID,
    Salary
FROM RankedEmployees
WHERE SalaryRank <= 3;
```

### Example 3 - Running Total

```sql
SELECT
    OrderDate,
    OrderID,
    TotalAmount,
    SUM(TotalAmount) OVER
    (
        ORDER BY OrderDate, OrderID
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
    ) AS RunningTotal
FROM Sales.Orders
ORDER BY OrderDate, OrderID;
```

### Example 4 - Partition Total and Percentage of Total

```sql
SELECT
    OrderID,
    CustomerID,
    TotalAmount,
    SUM(TotalAmount) OVER
    (
        PARTITION BY CustomerID
    ) AS CustomerTotal,
    CAST
    (
        100.0 * TotalAmount /
        NULLIF(SUM(TotalAmount) OVER (PARTITION BY CustomerID), 0)
        AS decimal(5,2)
    ) AS PercentOfCustomerTotal
FROM Sales.Orders;
```

### Example 5 - LAG and LEAD with Defaults

```sql
SELECT
    DeviceID,
    ReadingTime,
    Temperature,
    LAG(Temperature, 1, Temperature) OVER
    (
        PARTITION BY DeviceID
        ORDER BY ReadingTime
    ) AS PreviousTemperature,
    LEAD(Temperature, 1, Temperature) OVER
    (
        PARTITION BY DeviceID
        ORDER BY ReadingTime
    ) AS NextTemperature,
    Temperature - LAG(Temperature, 1, Temperature) OVER
    (
        PARTITION BY DeviceID
        ORDER BY ReadingTime
    ) AS TemperatureChange
FROM dbo.SensorReadings;
```

### Example 6 - FIRST_VALUE and LAST_VALUE with Correct Frame

`LAST_VALUE` is a common trap. Without the correct frame, it may return the current row instead of the last row in the partition.

```sql
SELECT
    CustomerID,
    OrderID,
    OrderDate,
    FIRST_VALUE(OrderDate) OVER
    (
        PARTITION BY CustomerID
        ORDER BY OrderDate, OrderID
        ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING
    ) AS FirstOrderDate,
    LAST_VALUE(OrderDate) OVER
    (
        PARTITION BY CustomerID
        ORDER BY OrderDate, OrderID
        ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING
    ) AS LastOrderDate
FROM Sales.Orders;
```

### Example 7 - NTILE for Quartiles

```sql
SELECT
    CustomerID,
    TotalSpend,
    NTILE(4) OVER
    (
        ORDER BY TotalSpend DESC
    ) AS SpendQuartile
FROM Sales.CustomerSpend;
```

### Example 8 - Named Window Clause

```sql
SELECT
    DeviceID,
    ReadingID,
    ReadingTime,
    Temperature,
    LAG(Temperature, 1, Temperature) OVER SensorWindow AS PreviousTemperature,
    LEAD(Temperature, 1, Temperature) OVER SensorWindow AS NextTemperature
FROM dbo.SensorReadings
WINDOW SensorWindow AS
(
    PARTITION BY DeviceID
    ORDER BY ReadingTime, ReadingID
);
```

### When to Use

- You need rankings without reducing rows.
- You need running totals or moving averages.
- You need previous or next row comparisons.
- You need top N per group.

### When NOT to Use

- You only need one row per group; use `GROUP BY`.
- You need to persist calculated results; compute and store separately if required.

### Common Mistakes

- Using `GROUP BY` when the original rows must remain visible.
- Forgetting `PARTITION BY`, causing the whole table to be one partition.
- Using `LAST_VALUE` without an explicit full frame.
- Using `RANK` when the exam asks for no gaps; use `DENSE_RANK`.
- Using `ROW_NUMBER` when ties must share the same rank.

### DP-800 Exam Scenarios

| Scenario | Best function |
|---|---|
| Get latest row per customer | `ROW_NUMBER()` |
| Rank salespeople and allow ties with gaps | `RANK()` |
| Rank products and allow ties without gaps | `DENSE_RANK()` |
| Compare current telemetry with previous reading | `LAG()` |
| Compare current row with next row | `LEAD()` |
| Running total | `SUM() OVER (ORDER BY ...)` |
| Quartiles | `NTILE(4)` |
| First and last order date per customer | `FIRST_VALUE`, `LAST_VALUE` with full frame |

### Quick Revision

- Window functions preserve row detail.
- `PARTITION BY` defines the group.
- `ORDER BY` defines row order.
- Frame clause matters for running totals and `LAST_VALUE`.

## 3.3 Correlated Queries

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

**Memory:** A correlated subquery references columns from the outer query.

### NOT EXISTS Anti-Join Pattern

Use `NOT EXISTS` when the requirement is to return rows from one table that do not have matching rows in another table. It is a common exam pattern for "customers without orders", "products never sold", or "employees without assigned tasks".

```sql
SELECT
    c.CustomerID,
    c.CustomerName
FROM Sales.Customers AS c
WHERE NOT EXISTS
(
    SELECT 1
    FROM Sales.Orders AS o
    WHERE o.CustomerID = c.CustomerID
);
```

#### EXISTS vs NOT EXISTS

| Requirement | Pattern | Exam wording |
|---|---|---|
| Return parent rows that have at least one child row | `EXISTS` | Customers who placed orders |
| Return parent rows that have no child rows | `NOT EXISTS` | Customers who never placed orders |
| Return rows where a related condition is true | Correlated `EXISTS` | Products with active promotions |
| Return rows where a related condition is missing | Correlated `NOT EXISTS` | Products not assigned to any category |

#### Common Mistake

Do not use `NOT IN` when the subquery can return `NULL`, because null handling can produce unexpected results. `NOT EXISTS` is usually safer for anti-join scenarios.


## 3.4 TRY/CATCH and Transactions

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

## 3.5 Regex and Fuzzy Matching

### Regex Function Matrix

| Function | Purpose |
|---|---|
| `REGEXP_LIKE` | Boolean pattern test |
| `REGEXP_REPLACE` | Replace matching text |
| `REGEXP_SUBSTR` | Extract matching text |
| `REGEXP_INSTR` | Return match position |
| `REGEXP_COUNT` | Count matches |
| `REGEXP_MATCHES` | Return match details where supported |
| `REGEXP_SPLIT_TO_TABLE` | Split string into rows where supported |

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

### Fuzzy Matching

| Requirement | Function |
|---|---|
| Count edits between strings | `EDIT_DISTANCE` |
| 0-to-100 similarity score | `EDIT_DISTANCE_SIMILARITY` |
| Names and short strings | `JARO_WINKLER_DISTANCE` |

```sql
SELECT ProductID, Name
FROM dbo.Products
WHERE CategoryID = @CategoryID
  AND IsActive = 1
  AND EDIT_DISTANCE_SIMILARITY(Name, @SearchTerm) >= 70;
```

### Exam Traps

- Regex is for pattern matching and extraction.
- Fuzzy matching is for approximate similarity and typos.
- `REGEXP_INSTR` returns a position; `REGEXP_SUBSTR` returns text.
- Apply indexed filters before fuzzy functions to reduce evaluated rows.

---

# 4. AI-Assisted Development, Copilot, and MCP

## 4.1 Safe Copilot Usage

Never paste secrets, passwords, tokens, customer PII, or connection strings into prompts. Review generated SQL for schema names, missing filters, wrong table references, unsafe dynamic SQL, and performance issues.

## 4.2 GitHub Copilot Instructions

Path:

```text
.github/copilot-instructions.md
```

Recommended file:

```markdown
# Repository Copilot Instructions
- Generate T-SQL for SQL Server, Azure SQL, and Fabric SQL where compatible.
- Always use schema-qualified object names.
- Avoid SELECT * in production examples.
- Use parameterized queries and stored procedures.
- Do not concatenate user input into SQL command text.
- Add TRY/CATCH for transactional code.
- Never include secrets, credentials, tokens, or connection strings.
- Prefer set-based SQL over row-by-row cursors.
- Generated SQL changes must be reviewed through pull requests.
```

## 4.3 MCP Scenario Selection

| Scenario | Best answer |
|---|---|
| Copilot needs SQL metadata | Configure MCP endpoint |
| Fabric warehouse context should not be repeated | Item-scoped Fabric Data Warehouse MCP endpoint |
| Developers need object names/columns only | Metadata-only permissions |
| Avoid production data exposure | Use development endpoint with masked data |
| Repository has `.vscode/mcp.json` | Do not store reusable secrets in repo |
| Secure AI tool database access | Least privilege, Entra identity, read-only where possible |

### Exam Traps

- Input validation alone is not enough to prevent SQL injection; parameterization directly addresses injection risk.
- MCP should not be over-scoped to production data when metadata is enough.
- Use signed-in developer identity rather than committed secrets.

---

# 5. Security and Compliance

## 5.0 Security Comparison Tables

### Always Encrypted vs TDE vs Dynamic Data Masking vs Column-Level Encryption

| Feature | Protects at rest | Protects from DBA plaintext access | Masks query output | Supports equality search | Typical DP-800 scenario |
|---|---|---|---|---|---|
| Always Encrypted | Yes | Yes | No | Deterministic only | App must protect sensitive values from database admins |
| TDE | Yes | No | No | Yes, because data is decrypted by engine | Protect database files, backups, and storage |
| Dynamic Data Masking | No | No | Yes | Not a security boundary | Support users should see masked values |
| Column-level encryption | Yes | No, database can decrypt with keys | No | Depends on implementation | T-SQL encryption/decryption functions are required |

### Deterministic vs Randomized Always Encrypted

| Requirement | Deterministic | Randomized |
|---|---|---|
| Same plaintext gives same ciphertext | Yes | No |
| Equality lookup | Yes | No |
| Joins/grouping on encrypted column | Limited support | No |
| Stronger confidentiality | Lower than randomized | Higher |
| Best exam scenario | Search encrypted national ID | Store highly sensitive value not searched |

### Managed Identity vs Service Principal

| Feature | Managed Identity | Service Principal |
|---|---|---|
| Secret management | No credential stored by app | Requires certificate or secret unless federated |
| Best for Azure-hosted resource | Yes | Sometimes |
| Rotation burden | Lower | Higher if secrets are used |
| Typical use | Azure Function/App Service to Azure SQL or Azure OpenAI | Automation across tenants or non-Azure workloads |

### GRANT vs DENY vs REVOKE

| Command | Meaning | Exam tip |
|---|---|---|
| `GRANT` | Allows permission | Gives access |
| `DENY` | Explicitly blocks permission | Usually overrides grant |
| `REVOKE` | Removes grant or deny | Does not explicitly block |

### RLS Filter Predicate vs Block Predicate

| Predicate | Controls | Example scenario |
|---|---|---|
| Filter predicate | Which rows are visible for SELECT/UPDATE/DELETE | Tenant can only read own rows |
| Block predicate BEFORE | Prevents write before operation | Stop updates that would touch restricted rows |
| Block predicate AFTER INSERT | Checks inserted row after insert attempt | Stop inserting another tenant ID |
| Block predicate AFTER UPDATE | Checks updated row after update attempt | Stop changing row to another tenant ID |

## 5.1 Data Protection Feature Matrix

| Requirement | Best answer | Why | Trap |
|---|---|---|---|
| Hide displayed sensitive values | Dynamic Data Masking | Masks result values | Not encryption |
| Protect plaintext from admins/DBAs | Always Encrypted | Client-side encryption | TDE is not enough for this requirement |
| Need equality lookup on encrypted value | Deterministic Always Encrypted | Same plaintext gives same ciphertext | Lower confidentiality than randomized |
| Need strongest encrypted confidentiality | Randomized Always Encrypted | Same plaintext gives different ciphertext | No equality search |
| Need T-SQL encryption functions | Column-level encryption | Database-side keys/functions | Engine can access plaintext |
| Different users see different rows | Row-Level Security | Predicate function + security policy | Filter-only does not stop bad writes |
| Passwordless Azure service access | Managed Identity / Service Connector | Removes secrets | Azure RBAC is not SQL data permission |
| Track security/data access | Auditing | Compliance and investigation | Not full row versioning |

## 5.2 Always Encrypted

```sql
CREATE TABLE dbo.CustomerSecure
(
    CustomerID int NOT NULL PRIMARY KEY,
    SSN nvarchar(20) COLLATE Latin1_General_BIN2
    ENCRYPTED WITH
    (
        COLUMN_ENCRYPTION_KEY = CEK1,
        ENCRYPTION_TYPE = DETERMINISTIC,
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256'
    )
);
```

| Type | Same plaintext gives | Search support | Security |
|---|---|---|---|
| Deterministic | Same ciphertext | Equality | Good |
| Randomized | Different ciphertext | No equality | Stronger |

## 5.3 Column-Level Encryption

```sql
OPEN SYMMETRIC KEY SalesKey
DECRYPTION BY CERTIFICATE SalesCert;

SELECT EncryptByKey(Key_GUID('SalesKey'), N'Sensitive Data');
```

## 5.4 Dynamic Data Masking

```sql
ALTER TABLE dbo.Customers
ALTER COLUMN Email ADD MASKED WITH (FUNCTION = 'email()');

ALTER TABLE dbo.Customers
ALTER COLUMN CreditCard ADD MASKED WITH (FUNCTION = 'partial(2,"XXXX-XXXX-",4)');
```

**Memory:** DDM hides display values; it does not encrypt stored data.

## 5.5 Row-Level Security

### Basic Filter Predicate

```sql
CREATE SCHEMA Security;
GO

CREATE FUNCTION Security.fn_TenantAccessPredicate(@TenantID int)
RETURNS TABLE
WITH SCHEMABINDING
AS
RETURN
    SELECT 1 AS fn_securityPredicate_result
    WHERE @TenantID = CAST(SESSION_CONTEXT(N'TenantID') AS int);
GO

CREATE SECURITY POLICY Security.TenantIsolationPolicy
ADD FILTER PREDICATE Security.fn_TenantAccessPredicate(TenantID)
ON dbo.Orders
WITH (STATE = ON);
```

### Filter Plus Block Predicates

Use this when tenants must not read, update, delete, insert, or update rows for another tenant.

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

### Exam Traps

- Filter predicate controls row visibility.
- Block predicate controls whether writes are allowed.
- Filter-only RLS does not stop an insert with another tenant ID.
- Predicate functions require `WITH SCHEMABINDING`.

## 5.6 Permissions

```sql
GRANT SELECT, INSERT ON dbo.Orders TO SalesUsers;
DENY DELETE ON dbo.Orders TO SalesUsers;
REVOKE INSERT ON dbo.Orders FROM SalesUsers;
```

| Command | Meaning |
|---|---|
| `GRANT` | Gives permission |
| `DENY` | Explicitly blocks permission |
| `REVOKE` | Removes grant/deny |

**Memory:** `DENY` generally overrides `GRANT`.

## 5.7 Passwordless Authentication and Service Connector

```sql
CREATE USER [id-my-app-prod] FROM EXTERNAL PROVIDER;
GRANT SELECT, INSERT ON dbo.Orders TO [id-my-app-prod];
```

| Requirement | Best answer |
|---|---|
| Azure Function/App Service connects without password | Managed Identity |
| Minimize manual connection and identity setup | Service Connector with system-assigned managed identity |
| Avoid secrets in source control | Managed Identity and/or Key Vault |
| App connects using Entra identity | Microsoft Entra authentication |

### Exam Traps

- Azure RBAC controls Azure resource management, not SQL table permissions inside the database.
- The identity that calls the database/model endpoint must receive the required permission.

## 5.8 Auditing

Use auditing for compliance tracking, login monitoring, data-access investigation, permission-change tracking, and security review.

| Destination | Use when |
|---|---|
| Azure Storage | Retain audit logs |
| Log Analytics | KQL queries and alert rules |
| Event Hubs | Stream audit events |

**Memory:** Server-level Azure SQL auditing can cover future databases on the logical server.

## 5.9 Endpoint Security

| Endpoint | Controls |
|---|---|
| Model endpoint | Managed Identity, private endpoint, scoped credential, least privilege Azure role |
| REST endpoint | Authentication, authorization, throttling, least privilege |
| GraphQL endpoint | Entity permissions, field exclusions, restrict mutations |
| MCP endpoint | Scoped tools, metadata-only where possible, audit logs |

---

# 6. Performance Optimization

## 6.0 Complete Performance Diagnostic Examples

### Example 1 - Current Requests, Waits, and Blocking

```sql
SELECT
    r.session_id,
    r.status,
    r.command,
    r.cpu_time,
    r.logical_reads,
    r.wait_type,
    r.wait_time,
    r.blocking_session_id,
    s.login_name,
    s.host_name,
    t.text AS sql_text
FROM sys.dm_exec_requests AS r
INNER JOIN sys.dm_exec_sessions AS s
    ON r.session_id = s.session_id
CROSS APPLY sys.dm_exec_sql_text(r.sql_handle) AS t
WHERE r.session_id <> @@SPID;
```

### Example 2 - Top CPU Queries from Query Stats

```sql
SELECT TOP (20)
    qs.total_worker_time AS TotalCpu,
    qs.execution_count,
    qs.total_worker_time / NULLIF(qs.execution_count, 0) AS AvgCpu,
    qs.total_logical_reads AS TotalReads,
    SUBSTRING
    (
        st.text,
        (qs.statement_start_offset / 2) + 1,
        ((CASE qs.statement_end_offset
            WHEN -1 THEN DATALENGTH(st.text)
            ELSE qs.statement_end_offset
          END - qs.statement_start_offset) / 2) + 1
    ) AS StatementText
FROM sys.dm_exec_query_stats AS qs
CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS st
ORDER BY qs.total_worker_time DESC;
```

### Example 3 - Index Usage Stats

```sql
SELECT
    OBJECT_NAME(ius.object_id) AS TableName,
    i.name AS IndexName,
    ius.user_seeks,
    ius.user_scans,
    ius.user_lookups,
    ius.user_updates
FROM sys.dm_db_index_usage_stats AS ius
INNER JOIN sys.indexes AS i
    ON ius.object_id = i.object_id
   AND ius.index_id = i.index_id
WHERE ius.database_id = DB_ID()
ORDER BY ius.user_lookups DESC, ius.user_scans DESC;
```

### Example 4 - Wait Stats Review

```sql
SELECT TOP (20)
    wait_type,
    waiting_tasks_count,
    wait_time_ms,
    signal_wait_time_ms
FROM sys.dm_os_wait_stats
WHERE wait_type NOT LIKE 'SLEEP%'
ORDER BY wait_time_ms DESC;
```

### Example 5 - Blocking Chain Focus

```sql
SELECT
    blocked.session_id AS BlockedSession,
    blocked.blocking_session_id AS BlockingSession,
    blocked.wait_type,
    blocked.wait_time,
    blocked_sql.text AS BlockedSql,
    blocker_sql.text AS BlockingSql
FROM sys.dm_exec_requests AS blocked
OUTER APPLY sys.dm_exec_sql_text(blocked.sql_handle) AS blocked_sql
LEFT JOIN sys.dm_exec_requests AS blocker
    ON blocked.blocking_session_id = blocker.session_id
OUTER APPLY sys.dm_exec_sql_text(blocker.sql_handle) AS blocker_sql
WHERE blocked.blocking_session_id <> 0;
```

### Example 6 - Query Store Regression Investigation Pattern

```sql
SELECT TOP (20)
    qsq.query_id,
    qsp.plan_id,
    rs.avg_duration,
    rs.avg_cpu_time,
    rs.avg_logical_io_reads,
    rsi.start_time,
    qt.query_sql_text
FROM sys.query_store_query AS qsq
INNER JOIN sys.query_store_query_text AS qt
    ON qsq.query_text_id = qt.query_text_id
INNER JOIN sys.query_store_plan AS qsp
    ON qsq.query_id = qsp.query_id
INNER JOIN sys.query_store_runtime_stats AS rs
    ON qsp.plan_id = rs.plan_id
INNER JOIN sys.query_store_runtime_stats_interval AS rsi
    ON rs.runtime_stats_interval_id = rsi.runtime_stats_interval_id
ORDER BY rs.avg_duration DESC;
```

### Query Store vs DMVs vs Execution Plans

| Tool | Best for | Time scope | Exam wording |
|---|---|---|---|
| Actual execution plan | Operator-level query tuning | Single execution | Key Lookup, scan, sort, join operator |
| DMVs | Current requests and accumulated engine stats | Current or since last restart | Blocking session, wait type, top CPU |
| Query Store | Historical plan and runtime regression | Persisted history | Query was fast before and slow now |
| Query Performance Insight | Azure portal visual query monitoring | Azure SQL history | Top resource-consuming queries in portal |

## 6.1 Workload Design

| Workload | Recommended design |
|---|---|
| OLTP | Rowstore indexes, short transactions, normalized schema, memory-optimized where needed |
| Data warehouse | Columnstore, partitioning, star schema |
| Mixed HTAP | Rowstore plus nonclustered columnstore |

## 6.2 Diagnostic Tool Matrix

| Symptom | Use first | Why |
|---|---|---|
| One slow query | Actual execution plan | Operator-level analysis |
| Current waits/blocking | `sys.dm_exec_requests` | Live request DMV |
| Query regressed over time | Query Store | Historical plans and runtime stats |
| Azure portal top consumers | Query Performance Insight | Visual Azure SQL query resource view |
| Platform logs and alerts | Azure Monitor + Log Analytics | Metrics, diagnostics, KQL |
| Top CPU queries | `sys.dm_exec_query_stats` | Aggregated query stats |
| Index usage | `sys.dm_db_index_usage_stats` | Seeks, scans, lookups, updates |
| Missing index suggestions | `sys.dm_db_missing_index_details` | Candidate indexes considered by optimizer |

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

### Missing Index DMV Pattern

`sys.dm_db_missing_index_details` can help identify indexes the optimizer considered useful. Treat it as a starting point, not an automatic create-index instruction.

```sql
SELECT
    mid.database_id,
    OBJECT_NAME(mid.object_id, mid.database_id) AS TableName,
    mid.equality_columns,
    mid.inequality_columns,
    mid.included_columns,
    migs.user_seeks,
    migs.avg_total_user_cost,
    migs.avg_user_impact
FROM sys.dm_db_missing_index_details AS mid
INNER JOIN sys.dm_db_missing_index_groups AS mig
    ON mid.index_handle = mig.index_handle
INNER JOIN sys.dm_db_missing_index_group_stats AS migs
    ON mig.index_group_handle = migs.group_handle
WHERE mid.database_id = DB_ID()
ORDER BY migs.avg_user_impact DESC;
```

#### Missing Index DMV Exam Traps

- Missing index DMVs do not understand your full workload or write overhead.
- They may suggest overlapping indexes.
- Review existing indexes before creating a new one.
- Put equality columns before inequality/range columns when designing a composite index.


## 6.3 Execution Plan Operators

| Operator | Meaning | Common fix |
|---|---|---|
| Index Seek | Efficient targeted access | Usually good |
| Index Scan | Reads many index rows | May be okay for large result |
| Table Scan | Reads full table | Add selective index if appropriate |
| Key Lookup | Fetches missing columns | Add INCLUDE columns |
| Sort | Extra sort operation | Index matching `ORDER BY` |
| Hash Match | Large join/aggregate | Check predicates, memory, indexes |
| Nested Loops | Repeated inner access | Good for small outer input |
| Merge Join | Joins sorted inputs | Useful with ordered indexes |

### Estimated vs Actual Execution Plan

| Plan type | What it shows | Requires running query | Best use | Exam trap |
|---|---|---:|---|---|
| Estimated execution plan | Optimizer's predicted plan before execution | No | Review expected access strategy without executing expensive query | Does not include actual rows or runtime metrics |
| Actual execution plan | Plan plus runtime information after execution | Yes | Compare estimated vs actual rows, confirm operators and runtime behavior | Requires executing the query |

#### Why Estimated vs Actual Matters

If estimated rows are very different from actual rows, statistics or cardinality estimation may be part of the issue. If estimated and actual rows are close but the query still performs many Key Lookups, adding included columns may be the better fix.


## 6.4 Query Store

Use Query Store when a query worked well before but became slow after deployment, statistics change, or plan choice.

```sql
ALTER DATABASE CurrentDB SET QUERY_STORE = ON;

EXEC sp_query_store_force_plan
    @query_id = 101,
    @plan_id = 12;

EXEC sp_query_store_unforce_plan
    @query_id = 101,
    @plan_id = 12;
```

Workflow:

1. Identify query regression.
2. Compare historical runtime stats and plans.
3. Find previous good plan.
4. Force plan if appropriate.
5. Monitor after forcing.

## 6.5 Blocking, Deadlocks, and Isolation

| Problem | Description | Fix direction |
|---|---|---|
| Blocking | One session waits for another | Find blocker, shorten transaction, tune indexes |
| Deadlock | Circular wait; victim chosen | Consistent object access order, retry logic |
| Reader/writer blocking | Reads and writes block each other | RCSI or Snapshot isolation |

```sql
ALTER DATABASE CurrentDB SET READ_COMMITTED_SNAPSHOT ON;
```

### Isolation Level Comparison Table

| Isolation level | Dirty reads | Non-repeatable reads | Phantom reads | Concurrency | Typical DP-800 scenario |
|---|---:|---:|---:|---|---|
| Read Uncommitted | Possible | Possible | Possible | Highest, least consistent | Rarely correct; reporting query accepts dirty data |
| Read Committed | Prevented | Possible | Possible | Default balance | Default SQL Server behavior without RCSI |
| Repeatable Read | Prevented | Prevented | Possible | Lower | Rows read cannot change during transaction |
| Serializable | Prevented | Prevented | Prevented | Lowest | Strict range consistency required |
| Snapshot | Prevented | Prevented | Prevented for transaction view | Good reader/writer concurrency | Transaction sees versioned snapshot |
| Read Committed Snapshot (RCSI) | Prevented | Statement-level consistent reads | Possible across statements | Good reader/writer concurrency | Reduce read/write blocking under read committed semantics |

### Isolation Level Syntax

```sql
SET TRANSACTION ISOLATION LEVEL SNAPSHOT;

BEGIN TRANSACTION;
    SELECT *
    FROM Sales.Orders
    WHERE CustomerID = 10;
COMMIT TRANSACTION;
```

```sql
ALTER DATABASE CurrentDB
SET READ_COMMITTED_SNAPSHOT ON;
```

### Isolation Exam Traps

- `READ UNCOMMITTED` can read uncommitted data, also called dirty reads.
- `SERIALIZABLE` gives strongest consistency but can reduce concurrency.
- `SNAPSHOT` uses row versions and requires database configuration.
- RCSI changes `READ COMMITTED` behavior to use row versions for reads.
- Use RCSI/Snapshot to reduce reader-writer blocking, not to fix all deadlocks.


### Deadlock Pattern

If two procedures update the same two tables in opposite order and fail with error 1205, make both procedures access objects in the same order while keeping transactions short.

## 6.6 Parameter Sniffing

| Symptom | Likely issue | Possible fix |
|---|---|---|
| Same procedure fast for one parameter, slow for another | Parameter sniffing | Query Store, `OPTION(RECOMPILE)`, `OPTIMIZE FOR`, review stats/indexes |

```sql
CREATE PROCEDURE dbo.usp_GetOrders
    @CustomerID int
AS
BEGIN
    SELECT OrderID, CustomerID, OrderDate, TotalAmount
    FROM dbo.Orders
    WHERE CustomerID = @CustomerID
    OPTION (RECOMPILE);
END;
```

## 6.7 Performance Exam Traps

- Blocking is one-way waiting; deadlock is circular waiting.
- Query Store is for history/regression, not live requests.
- Key Lookup repeated many times usually points to INCLUDE columns.
- Similar estimated and actual row counts means statistics are likely not the first fix.
- RCSI helps with reader/writer blocking but does not remove all locking concerns.

---

# 7. CI/CD with SQL Database Projects

## 7.1 SQL Project Concepts

| Requirement | Best choice |
|---|---|
| Store schema as code | SQL Database Project |
| Cross-platform CI build | SDK-style SQL project |
| Build deployable artifact | DACPAC |
| Deploy artifact | SqlPackage Publish |
| Existing DB to model | Extract/schema compare |
| Validate project compiles | Build validation |
| Test stored procedure behavior | Unit tests |
| Test end-to-end DB flow | Integration tests |
| Manage reference data | Post-deployment MERGE |
| Detect out-of-band changes | Drift report/schema compare |

## 7.2 SQL Project Testing Strategy

Testing strategy is part of DP-800 CI/CD coverage. The goal is to validate schema, deployment behavior, and database logic before production deployment.

| Test type | Purpose | Example validation | When to run |
|---|---|---|---|
| Build validation | Confirm SQL project compiles into a DACPAC | No unresolved references or syntax errors | Every pull request |
| Unit tests | Validate individual stored procedures/functions | Procedure returns expected output for known input | Pull request and CI |
| Integration tests | Validate database objects working together | Insert order, update inventory, verify totals | CI against test database |
| Deployment validation | Confirm DACPAC deploys successfully | Deploy to disposable/test database | CI/CD pipeline |
| Static/reference data validation | Confirm lookup data exists and is correct | Status table contains approved values | After post-deployment script |
| Security validation | Confirm least privilege and access rules | App role can execute proc but cannot read sensitive table | Pre-production |
| Drift validation | Detect changes outside source control | Schema compare or deployment report | Before production deployment |

### Testing Flow

1. Build SQL project.
2. Deploy DACPAC to an empty or disposable test database.
3. Run post-deployment scripts.
4. Run unit and integration tests.
5. Validate permissions and reference data.
6. Generate deployment report for controlled environments.

### Exam Traps

- A successful build does not prove deployment will succeed against the target database.
- Unit tests validate object behavior; integration tests validate end-to-end database workflows.
- Reference/static data should be version controlled, commonly through post-deployment scripts.

## 7.3 Project Structure

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

## 7.4 Static Reference Data

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

## 7.5 SqlPackage Commands

```bash
SqlPackage /Action:Build /SourceFile:Database.sqlproj
```

```bash
SqlPackage /Action:DeployReport \
  /SourceFile:bin/Output.dacpac \
  /TargetConnectionString:"..." \
  /OutputPath:drift-report.xml
```

```bash
SqlPackage /Action:Publish \
  /SourceFile:bin/Output.dacpac \
  /TargetConnectionString:"..."
```

## 7.6 Feature Branch and Deployment Flow

```bash
git checkout -b feature/add-column1
git add .
git commit -m "Add Column1 to Customer"
git push origin feature/add-column1
```

Recommended flow:

1. Create feature branch.
2. Modify SQL object files.
3. Build SQL project.
4. Deploy DACPAC to test database.
5. Run tests.
6. Open pull request.
7. Require approvals and build validation.
8. Generate deployment script for review.
9. Publish after production approval.

## 7.7 Drift Reconciliation

If production has an approved hotfix plus an unwanted monitoring table:

1. Compare live database to SQL project.
2. Apply only the approved change to the project.
3. Do not import monitoring/vendor table.
4. Commit and build.
5. Generate deployment script for review.
6. Publish after approval.

## 7.8 Secrets and Governance

| Requirement | Best answer |
|---|---|
| Production-only connection string in GitHub Actions | GitHub environment secret in `production` environment |
| Keep secrets out of Git | Key Vault, secure variables, environment secrets |
| Require production approval | Environment approval gate |
| Require specific reviewers | CODEOWNERS |
| Prevent unreviewed changes | Branch policies and PR checks |

---

# 8. Data API Builder and Azure Integration

## 8.1 DAB Concepts

Data API Builder exposes SQL database objects as REST and GraphQL endpoints without writing custom API code.

## 8.2 DAB Selection Matrix

| Requirement | DAB answer |
|---|---|
| Expose table as REST | Entity with REST enabled |
| Expose SQL as GraphQL | GraphQL endpoint/entity |
| Expose view | Entity over view |
| Expose stored procedure | Stored procedure entity |
| Stored procedure changes data | GraphQL mutation with execute permission |
| Restrict read/write operations | Entity permissions |
| Hide sensitive fields | `fields.exclude` |
| Avoid huge responses | Pagination |
| Improve repeated read latency | Caching |
| Share cache across instances | L1L2 cache |

## 8.3 DAB CLI

```bash
dab init --database-type mssql --connection-string "@env('SQL_CONN_STR')"
dab add Customer --source dbo.Customers --permissions "authenticated:read"
dab add Order --source dbo.Orders --permissions "authenticated:read,create,update"
dab start
```

## 8.4 Basic DAB Config

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

## 8.5 DAB REST API Examples

These examples belong with Data API Builder because DP-800 can ask how the REST endpoint is consumed after an entity is configured.

### Get All Customers

```http
GET /api/Customer
```

### Get One Customer by Key

```http
GET /api/Customer/id/1
```

### Filter Rows

```http
GET /api/Customer?$filter=City eq 'London'
```

### Limit Returned Rows with $top

```http
GET /api/Customer?$top=10
```

### Skip Rows for Paging

```http
GET /api/Customer?$skip=20&$top=10
```

### Select Specific Fields

```http
GET /api/Customer?$select=CustomerID,CustomerName,City
```

### Sort Results

```http
GET /api/Customer?$orderby=CustomerName asc
```

### Combined REST Query

```http
GET /api/Order?$filter=Status eq 'Open'&$orderby=OrderDate desc&$top=25
```

### REST Exam Traps

- DAB REST endpoints expose configured entities, not every database object automatically.
- Filtering, paging, and sorting should be controlled to avoid large unbounded responses.
- Authentication and entity permissions still apply even when the endpoint exists.

## 8.6 DAB GraphQL Field-Level Security

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

**Trap:** Disabling GraphQL introspection reduces discovery but does not enforce field-level authorization.

## 8.7 DAB GraphQL Query Examples

These examples show how DAB GraphQL endpoints are consumed after entities and relationships are configured.

### Query Customers

```graphql
query GetCustomers {
  customers {
    items {
      CustomerID
      CustomerName
      City
    }
  }
}
```

### Query with Filter and First N Rows

```graphql
query GetOpenOrders {
  orders(
    first: 10
    filter: { Status: { eq: "Open" } }
    orderBy: { OrderDate: DESC }
  ) {
    items {
      OrderID
      OrderDate
      Status
      TotalAmount
    }
  }
}
```

### Relationship Traversal Example

```graphql
query GetCustomerWithOrders {
  customers(filter: { CustomerID: { eq: 1 } }) {
    items {
      CustomerID
      CustomerName
      orders {
        items {
          OrderID
          OrderDate
          TotalAmount
        }
      }
    }
  }
}
```

### Mutation Example for a Data-Changing Stored Procedure

```graphql
mutation Checkout($customerId: Int!, $productId: Int!, $quantity: Int!) {
  executeCheckout(
    CustomerID: $customerId
    ProductID: $productId
    Quantity: $quantity
  ) {
    result
  }
}
```

### GraphQL Exam Traps

- GraphQL relationship traversal requires relationships to be configured in DAB.
- A stored procedure that changes data should be exposed as a mutation, not a query.
- Field exclusion in DAB permissions is authorization. Disabling introspection is not a replacement for authorization.


## 8.8 Stored Procedure as GraphQL Mutation

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

## 8.9 DAB Caching

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

| Cache level | Meaning |
|---|---|
| L1 | Local in-memory cache |
| L1L2 | Local plus distributed cache, useful across multiple instances |

## 8.10 Azure Monitor, Application Insights, and Log Analytics

| Requirement | Tool |
|---|---|
| Application traces and dependencies | Application Insights |
| Query diagnostics with KQL | Log Analytics |
| Metrics and alerts | Azure Monitor |
| Stream audit/change events | Event Hubs |

```kql
AzureDiagnostics
| where ResourceProvider == "MICROSOFT.SQL"
| summarize Count = count() by Category, bin(TimeGenerated, 1h)
```

## 8.11 Change Handling

| Requirement | Feature |
|---|---|
| Lightweight changed row keys | Change Tracking |
| Detailed insert/update/delete changes | CDC |
| Streaming changes to downstream systems | CES |
| Serverless response to SQL row changes | Azure Functions SQL trigger |
| Low-code workflow integration | Logic Apps |
| Near-real-time multi-consumer embedding maintenance | Change Event Streaming |

---

# 9. Models, Embeddings, and External AI

## 9.1 Model Selection

| Requirement | Best model/pattern |
|---|---|
| Low latency/cost | Smaller model |
| Complex reasoning | Larger model |
| Images/documents/audio | Multimodal model |
| Multiple languages | Multilingual model |
| Category/Priority/RouteQueue values | Chat model with structured JSON output |
| Similarity search | Embedding model |

**Trap:** Embeddings are numeric meaning vectors. They are not the right output for structured business columns like category or route queue.

### Model Evaluation Table

| Model type | Strength | Trade-off | DP-800 scenario |
|---|---|---|---|
| Small model | Lower latency and lower cost | Lower reasoning depth | Simple classification, extraction, routing |
| Large model | Better reasoning and generation quality | Higher latency and cost | Complex natural language answer generation |
| Multimodal model | Handles images, documents, audio, or mixed input | More expensive and integration-heavy | AI-enabled app needs to process non-text inputs |
| Multilingual model | Works across multiple languages | Quality can vary by language | Global support knowledge base or customer tickets |
| Structured-output capable model | Returns predictable JSON/schema-like output | Requires prompt/schema discipline | Category, priority, route queue, or status extraction |
| Embedding model | Converts text to vectors for similarity search | Does not generate business labels directly | Semantic search and RAG retrieval |

### Model Evaluation Checklist

- Accuracy and relevance for the workload.
- Latency and throughput requirements.
- Cost per request and expected volume.
- Language and modality requirements.
- Structured output support.
- Security, privacy, and endpoint access model.
- Compatibility with SQL external model or REST invocation pattern.


## 9.2 Embedding Column Selection

| Column/data | Embed? | Why |
|---|---|---|
| Product description | Yes | Semantic meaning |
| Knowledge article body | Yes | Searchable language |
| FAQ answer | Yes | Maps user questions to answers |
| Support ticket text | Yes | Classification/search |
| Customer ID | No | Identifier |
| Invoice number | No | Identifier |
| Status code | No | Use filter/category |
| Foreign key | No | Relationship, not semantic text |
| CategoryID and Price | No | Use normal columns and B-tree indexes |

## 9.3 Chunking

| Strategy | Use when | Trade-off |
|---|---|---|
| Fixed-size | Quick/simple implementation | Can split meaning |
| Sentence-based | Need cleaner semantic boundaries | More parsing |
| Paragraph-based | Docs have clear paragraphs | Uneven sizes |
| Structural | Headings/sections matter | Requires document structure |
| Hierarchical | Need exact child chunks plus broader parent context | More storage/logic |
| Semantic | Free-form text with unclear boundaries | Higher cost/complexity |

## 9.4 Embedding Table Design

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

### Exam Traps

- Store one vector per chunk for multi-paragraph long text.
- Do not store vectors as JSON when SQL vector operations are required.
- Keep structured filters such as category and price as normal columns.
- Prefer smaller embedding dimension if relevance is equivalent.
- Fixed `vector(n)` rejects unexpected dimension counts.

## 9.5 SQL AI Conceptual Functions - Platform-Dependent Syntax

Some DP-800 learning material refers to SQL AI helper functions conceptually. Treat these as platform-dependent patterns. The exact syntax and availability can vary by SQL platform and preview/GA status, but the exam intent is to understand what each function is meant to do.

### AI_GENERATE_CHUNKS - Conceptual Pattern

Purpose: split long text into smaller chunks before generating embeddings.

```sql
SELECT
    ProductID,
    chunk_id,
    chunk_text
FROM AI_GENERATE_CHUNKS
(
    SOURCE =>
    (
        SELECT ProductID, Description
        FROM dbo.Product
    ),
    TEXT_COLUMN => 'Description',
    MAX_CHUNK_SIZE => 1000,
    OVERLAP_SIZE => 100
);
```

### AI_GENERATE_EMBEDDINGS - Conceptual Pattern

Purpose: generate vector embeddings from text chunks or natural language columns.

```sql
SELECT
    ProductID,
    ChunkID,
    ChunkText,
    AI_GENERATE_EMBEDDINGS
    (
        MODEL => 'text-embedding-model',
        INPUT => ChunkText
    ) AS ChunkEmbedding
FROM dbo.ProductChunk;
```

### Conceptual Flow

1. Select descriptive text columns.
2. Generate chunks for long content.
3. Generate embeddings for each chunk.
4. Store embeddings in a `vector(n)` column.
5. Use vector search, full-text search, or hybrid search for retrieval.

### Exam Traps

- Chunking and embedding generation are separate conceptual steps.
- Do not embed identifiers such as ProductID, InvoiceNumber, or StatusCode.
- Always verify platform support and exact syntax before implementing in production.

## 9.6 Embedding Maintenance

| Method | Latency | Best scenario | DP-800 guidance |
|---|---|---|---|
| Azure Functions SQL trigger | Near real time | Serverless embedding regeneration after row changes | First-class option when database changes should trigger serverless embedding updates |
| Change Tracking | Low/medium | Lightweight changed-key polling | Good when only changed primary keys are needed |
| CDC | Medium | Detailed insert/update/delete processing | Good for downstream ETL or detailed change capture |
| CES | Near real time | Decoupled streaming and multiple consumers | Best when multiple services need change events |
| Table trigger | Immediate | Small critical tables, write overhead acceptable | Use carefully because it adds write-path overhead |
| Azure Logic Apps | Workflow-oriented | Low-code business process | Good for business workflows and connectors |
| Microsoft Foundry | Enterprise AI lifecycle | Model/app orchestration | Use when AI lifecycle and orchestration are central |

## 9.7 External Models and Endpoint Credentials

### Managed Identity Credential

```sql
CREATE DATABASE SCOPED CREDENTIAL [https://my-openai-resource.openai.azure.com]
WITH IDENTITY = 'Managed Identity';
```

### API Key Credential Pattern

```sql
CREATE DATABASE SCOPED CREDENTIAL MyEmbeddingCredential
WITH IDENTITY = 'HTTPEndpointHeaders',
SECRET = '{"api-key":"<stored-securely>"}';
```

### Alter Existing External Model

Use this when stored procedures reference an existing model and definitions must remain unchanged.

```sql
ALTER EXTERNAL MODEL Model1
WITH
(
    LOCATION = 'https://my-openai-resource.openai.azure.com/openai/deployments/Deployment1/embeddings?api-version=2024-02-01',
    CREDENTIAL = MyEmbeddingCredential
);

GRANT EXECUTE ANY EXTERNAL ENDPOINT TO Role1;
```

### Secure Model Invocation Scenario

If SQL calls Azure OpenAI using `sp_invoke_external_rest_endpoint` and API keys must be removed:

1. Enable/use SQL logical server managed identity.
2. Grant the SQL server managed identity the required Azure OpenAI role, such as Cognitive Services User, at the Azure OpenAI resource scope.
3. Create database scoped credential with Managed Identity.
4. Grant only required stored procedure execute permissions to the application database role.

```sql
CREATE ROLE EmbeddingRequestExecutor;
ALTER ROLE EmbeddingRequestExecutor ADD MEMBER [app-service-identity];
GRANT EXECUTE ON dbo.GetEmbedding TO EmbeddingRequestExecutor;
```

**Trap:** If SQL is the caller to Azure OpenAI, grant the Azure OpenAI role to the SQL logical server identity, not the app identity.

---

# 10. Intelligent Search

## 10.1 Search Type Selection

| Requirement | Best choice | Why |
|---|---|---|
| Exact keyword, phrase, prefix, Boolean text | `CONTAINS` | Precise full-text search |
| Linguistic/natural language word forms | `FREETEXT` | Full-text meaning/inflection |
| Meaning/synonyms/concepts | Vector search | Semantic similarity |
| Exact plus semantic relevance | Hybrid search | Combines lexical and semantic |
| Combine rank lists | RRF | Uses positions, not raw scores |
| Small vector set, maximum accuracy | ENN | Exact exhaustive search |
| Large vector set, low latency | ANN | Approximate scalable search |

### LIKE vs CONTAINS vs FREETEXT

| Feature | Type of search | Requires full-text index | Best for | Avoid when |
|---|---|---:|---|---|
| `LIKE` | Basic pattern matching | No | Simple wildcard checks such as prefix/suffix patterns | Large linguistic search, ranking, word forms |
| `CONTAINS` | Full-text precise lexical search | Yes | Exact phrase, prefix term, Boolean-style full-text conditions | Semantic similarity or synonym-heavy search |
| `FREETEXT` | Full-text natural language search | Yes | Word forms and meaning-like linguistic matching | Exact phrase control is required |
| Vector search | Semantic similarity | Vector storage/index | Meaning, concepts, synonyms | Exact legal phrase or keyword-only matching |

#### LIKE Baseline Example

```sql
SELECT ProductID, ProductName
FROM dbo.Product
WHERE ProductName LIKE N'Mountain%';
```

#### Exam Tip

If the question mentions exact phrase, inflectional words, ranking, or full-text catalog/index, think `CONTAINS`, `FREETEXT`, `CONTAINSTABLE`, or `FREETEXTTABLE`. If it only mentions a simple wildcard pattern, `LIKE` may be enough.

## 10.2 Full-Text Search

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

```sql
SELECT ProductID, ProductName
FROM dbo.Product
WHERE CONTAINS(Description, '"running shoes"');
```

```sql
SELECT ProductID, ProductName
FROM dbo.Product
WHERE FREETEXT(Description, 'comfortable footwear for jogging');
```

### Exact Phrase Plus Linguistic Match

```sql
SELECT ProductID, Name
FROM dbo.Product
WHERE CONTAINS(Name, N'"mountain bike"')
  AND FREETEXT(Description, N'ride')
  AND IsActive = 1;
```

### Complete Full-Text Example Pack

#### Example 1 - CONTAINS Exact Phrase

```sql
SELECT ProductID, ProductName
FROM dbo.Product
WHERE CONTAINS(Description, '"running shoes"');
```

#### Example 2 - CONTAINS Prefix Term

```sql
SELECT ProductID, ProductName
FROM dbo.Product
WHERE CONTAINS(ProductName, '"mountain*"');
```

#### Example 3 - FREETEXT Natural Language Query

```sql
SELECT ProductID, ProductName
FROM dbo.Product
WHERE FREETEXT(Description, 'comfortable footwear for jogging');
```

#### Example 4 - CONTAINSTABLE with Rank

```sql
SELECT
    p.ProductID,
    p.ProductName,
    ft.[RANK] AS FullTextRank
FROM CONTAINSTABLE(dbo.Product, Description, '"running shoes"') AS ft
INNER JOIN dbo.Product AS p
    ON p.ProductID = ft.[KEY]
ORDER BY ft.[RANK] DESC;
```

#### Example 5 - FREETEXTTABLE with Rank

```sql
SELECT
    p.ProductID,
    p.ProductName,
    ft.[RANK] AS FreeTextRank
FROM FREETEXTTABLE(dbo.Product, Description, 'lightweight shoes for running') AS ft
INNER JOIN dbo.Product AS p
    ON p.ProductID = ft.[KEY]
ORDER BY ft.[RANK] DESC;
```

#### Example 6 - Exact Phrase plus Linguistic Match

```sql
SELECT ProductID, ProductName
FROM dbo.Product
WHERE CONTAINS(ProductName, N'"mountain bike"')
  AND FREETEXT(Description, N'ride')
  AND IsActive = 1;
```

### Full-Text Exam Traps

- `CONTAINS` is better for exact phrase, prefix, and Boolean-style search.
- `FREETEXT` is better for natural language meaning and inflectional forms.
- `CONTAINSTABLE` and `FREETEXTTABLE` return ranking metadata.
- Full-text search is lexical, not semantic vector search.

## 10.3 Vector Data Type and Search

```sql
CREATE TABLE dbo.ProductCatalog
(
    ProductID int PRIMARY KEY,
    ProductName nvarchar(200) NOT NULL,
    Description nvarchar(max) NOT NULL,
    ProductEmbedding vector(1536) NULL
);

DECLARE @QueryEmbedding vector(1536) = N'[0.012, -0.045, 0.231]';

SELECT TOP 5
    ProductID,
    ProductName,
    VECTOR_DISTANCE('cosine', @QueryEmbedding, ProductEmbedding) AS Distance
FROM dbo.ProductCatalog
ORDER BY Distance ASC;
```

### Complete Vector Example Pack

#### Example 1 - Store Vector Embeddings

```sql
CREATE TABLE dbo.ArticleEmbedding
(
    ArticleID int NOT NULL PRIMARY KEY,
    Title nvarchar(200) NOT NULL,
    Body nvarchar(max) NOT NULL,
    BodyEmbedding vector(1536) NOT NULL,
    CategoryID int NOT NULL,
    CreatedAt datetime2 NOT NULL DEFAULT SYSUTCDATETIME()
);
```

#### Example 2 - Inspect Vector Properties

```sql
SELECT
    ArticleID,
    VECTORPROPERTY(BodyEmbedding, 'Dimensions') AS VectorDimensions
FROM dbo.ArticleEmbedding;
```

#### Example 3 - Normalize a Vector

```sql
DECLARE @RawVector vector(3) = '[3, 4, 0]';
SELECT VECTOR_NORMALIZE(@RawVector) AS NormalizedVector;
```

#### Example 4 - Exact Vector Search with VECTOR_DISTANCE

```sql
DECLARE @QueryEmbedding vector(1536) = @GeneratedEmbedding;

SELECT TOP (10)
    ArticleID,
    Title,
    VECTOR_DISTANCE('cosine', @QueryEmbedding, BodyEmbedding) AS Distance
FROM dbo.ArticleEmbedding
WHERE CategoryID = @CategoryID
ORDER BY Distance ASC;
```

#### Example 5 - Vector Index Assisted Search with VECTOR_SEARCH

```sql
SELECT
    vs.ArticleID,
    a.Title,
    vs.distance
FROM VECTOR_SEARCH
(
    TABLE = dbo.ArticleEmbedding,
    COLUMN = BodyEmbedding,
    QUERY_VECTOR = @QueryEmbedding,
    METRIC = 'cosine',
    TOP_N = 20
) AS vs
INNER JOIN dbo.ArticleEmbedding AS a
    ON a.ArticleID = vs.ArticleID
WHERE a.CategoryID = @CategoryID
ORDER BY vs.distance ASC;
```

#### Example 6 - ANN vs ENN Decision

| Requirement | Choose | Reason |
|---|---|---|
| Small table and exact result required | ENN / `VECTOR_DISTANCE` ordered scan | Maximum accuracy |
| Millions of vectors and low latency required | ANN / vector index search | Faster approximate retrieval |
| Need recall tuning | ANN index configuration | Balance recall, memory, and latency |
| Need perfect nearest neighbors | ENN | No approximation |

#### Example 7 - Vector Search with Structured Filters

```sql
SELECT TOP (10)
    ProductID,
    ProductName,
    Price,
    VECTOR_DISTANCE('cosine', @QueryEmbedding, ProductEmbedding) AS Distance
FROM dbo.ProductCatalog
WHERE CategoryID = @CategoryID
  AND Price BETWEEN @MinPrice AND @MaxPrice
ORDER BY Distance ASC;
```

### Vector Exam Traps

- Do not embed IDs, status codes, or prices; keep them as structured filters.
- Vector dimension must match the embedding model output.
- `VECTOR_DISTANCE` ordered over rows is exact-style searching.
- `VECTOR_SEARCH` indicates vector index assisted retrieval where supported.
- Cosine distance is commonly used for text embeddings.

### Vector Function Matrix

| Function | Purpose |
|---|---|
| `VECTOR_DISTANCE` | Calculate vector distance/similarity metric |
| `VECTOR_NORMALIZE` | Normalize vector magnitude |
| `VECTORPROPERTY` | Inspect metadata such as dimension count |
| `VECTOR_SEARCH` | Vector-index-assisted nearest-neighbor retrieval where supported |

## 10.4 Vector Metrics and Indexing

| Metric | Best for | Exam note |
|---|---|---|
| Cosine | Text embeddings | Most common for semantic text |
| Euclidean / L2 | Geometric distance | Sensitive to magnitude |
| Dot product | Normalized vectors | Fast in many systems |

| Requirement | Recommendation |
|---|---|
| Small dataset, maximum accuracy | ENN |
| Millions of vectors, low latency | ANN |
| High recall and low latency | HNSW where available |
| Very large partitioned vector sets | IVF or platform-specific scalable ANN |
| Disk-friendly large vector workload | DiskANN where available |

### Exam Traps

- `VECTOR_DISTANCE` over all rows is exact scanning logic.
- `VECTOR_SEARCH` points to vector index candidate retrieval where supported.
- Use cosine distance for most text embedding scenarios.
- Structured filters should remain structured columns with indexes.

## 10.5 Hybrid Search and RRF

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

### Exam Traps

- Use `FULL OUTER JOIN` when results from either full-text or vector search must be included.
- RRF combines rank positions, not raw full-text scores and vector distances.
- Hybrid search improves relevance but can increase latency and complexity.

## 10.6 Search Evaluation Metrics

| Metric | Meaning |
|---|---|
| Precision | Of returned results, how many are relevant |
| Recall | Of all relevant results, how many were found |
| Recall@K | Relevant results found in top K |
| MRR | Mean reciprocal rank of first relevant result |
| NDCG | Ranking quality with graded relevance |
| Latency | Response time |
| Throughput | Queries per second |

---

# 11. Retrieval-Augmented Generation - RAG

## 11.1 RAG Architecture

1. User asks a question.
2. Generate query embedding.
3. Retrieve top chunks using vector search.
4. Optionally include full-text search.
5. Rerank/merge using RRF.
6. Apply RLS/security filters before prompt creation.
7. Convert retrieved rows to JSON.
8. Build grounded prompt.
9. Call model endpoint securely.
10. Parse assistant answer.
11. Return response with citations/source IDs.

## 11.2 RAG Decision Matrix

| Requirement | Best RAG pattern |
|---|---|
| Current DB facts in LLM answer | RAG |
| Long documents | Chunk before embedding |
| Semantic retrieval | Embeddings + vector search |
| Exact terms also matter | Hybrid search |
| Combine search methods | RRF |
| SQL rows to model | `FOR JSON PATH` |
| Secure SQL-to-model call | Scoped credential / Managed Identity |
| Long assistant answer extraction | `OPENJSON WITH nvarchar(max)` |

### Complete RAG Example Pack

#### Example 1 - Retrieve Candidate Chunks

```sql
DECLARE @QuestionEmbedding vector(1536) = @GeneratedQuestionEmbedding;

SELECT TOP (5)
    ChunkID,
    SourceDocumentID,
    ChunkText,
    VECTOR_DISTANCE('cosine', @QuestionEmbedding, ChunkEmbedding) AS Distance
FROM dbo.DocumentChunk
WHERE TenantID = CAST(SESSION_CONTEXT(N'TenantID') AS int)
ORDER BY Distance ASC;
```

#### Example 2 - Convert Retrieved Chunks to JSON Context

```sql
DECLARE @ContextJson nvarchar(max);

SELECT @ContextJson =
(
    SELECT TOP (5)
        SourceDocumentID AS sourceDocumentId,
        ChunkID AS chunkId,
        ChunkText AS chunkText
    FROM dbo.DocumentChunk
    WHERE TenantID = CAST(SESSION_CONTEXT(N'TenantID') AS int)
    ORDER BY VECTOR_DISTANCE('cosine', @QuestionEmbedding, ChunkEmbedding)
    FOR JSON PATH, INCLUDE_NULL_VALUES
);
```

#### Example 3 - Build Grounded Prompt

```sql
DECLARE @Prompt nvarchar(max) = CONCAT
(
    N'Answer only from the context. If missing, say you do not know.',
    NCHAR(10), N'Context: ', @ContextJson,
    NCHAR(10), N'Question: ', @UserQuestion
);
```

#### Example 4 - Extract Short Response with JSON_VALUE

```sql
SELECT JSON_VALUE(@Response, '$.result.choices[0].message.content') AS AnswerText;
```

#### Example 5 - Extract Long Response with OPENJSON

```sql
DECLARE @Answer nvarchar(max);

SELECT @Answer = GeneratedAnswer
FROM OPENJSON(@Response, '$.result.choices[0]')
WITH
(
    GeneratedAnswer nvarchar(max) '$.message.content'
);
```

### RAG Common Mistakes

- Sending all database rows to the model instead of retrieving relevant chunks.
- Not applying RLS or tenant filters before building prompt context.
- Using `JSON_VALUE` for long model responses.
- Embedding entire long documents without chunking.
- Treating RAG as model training. RAG retrieves context at query time; it does not retrain the model.

## 11.3 Build Model Request Body

```sql
DECLARE @RequestBody nvarchar(max) = JSON_OBJECT
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
```

## 11.4 Call Model Endpoint

```sql
DECLARE @Response nvarchar(max);

EXEC sp_invoke_external_rest_endpoint
    @url = N'https://my-openai-resource.openai.azure.com/openai/deployments/my-chat-model/chat/completions?api-version=2024-02-01',
    @method = N'POST',
    @payload = @RequestBody,
    @credential = [https://my-openai-resource.openai.azure.com],
    @response = @Response OUTPUT;
```

## 11.5 Extract Long Assistant Answer

```sql
DECLARE @answer nvarchar(max);

SELECT @answer = GeneratedAnswer
FROM OPENJSON(@Response, '$.result.choices[0]')
WITH
(
    GeneratedAnswer nvarchar(max) '$.message.content'
);

INSERT dbo.RagResponse(RequestId, AnswerText)
VALUES (@RequestId, @answer);
```

**Trap:** `JSON_VALUE` returns `nvarchar(4000)`, so it can truncate long assistant responses. Use `OPENJSON WITH nvarchar(max)`.

## 11.6 RAG Security Checklist

- Apply RLS/security filters before retrieving context.
- Use least privilege for database and model endpoint access.
- Do not send unnecessary PII to the model.
- Prefer Managed Identity and private networking where supported.
- Log prompts/responses only according to policy.
- Instruct model to answer only from provided context.
- Include source IDs/citations in context.

---

# 12. Consolidated Practice Questions

## 12.1 Domain 1

1. Product attributes differ by category and one JSON property must be searched efficiently.  
   **Answer:** Store JSON in `nvarchar(max)`, expose property with `JSON_VALUE` computed column, then index it.

2. Financial records must prove no tampering occurred.  
   **Answer:** Ledger table.

3. Employee salary history must support point-in-time query.  
   **Answer:** Temporal table.

4. Huge reporting table performs aggregations over hundreds of millions of rows.  
   **Answer:** Clustered columnstore index.

5. OLTP table retains rowstore lookup but dashboard aggregates many rows.  
   **Answer:** Nonclustered columnstore over analytical columns.

6. Query has repeated Key Lookups after a good seek.  
   **Answer:** Add returned columns as included columns.

7. Need many-to-many path traversal with one-to-three hops.  
   **Answer:** Graph tables with `SHORTEST_PATH`, `FOR PATH`, and `WITHIN GROUP (GRAPH PATH)`.

8. Need reusable parameterized rowset for each customer.  
   **Answer:** Inline TVF with `CROSS APPLY`.

9. Need one scalar calculation in SELECT and WHERE.  
   **Answer:** Scalar function.

10. Need one row per JSON array item plus scalar from root.  
    **Answer:** `JSON_VALUE` plus `CROSS APPLY OPENJSON`.

## 12.2 Domain 2

1. Support users should see masked credit card values.  
   **Answer:** Dynamic Data Masking.

2. DBAs must not see plaintext national ID values.  
   **Answer:** Always Encrypted.

3. Encrypted value must support equality lookup.  
   **Answer:** Deterministic Always Encrypted.

4. Tenant app must stop inserts for another tenant.  
   **Answer:** RLS filter predicate plus block predicates after insert and update.

5. Azure App Service must connect without SQL password and minimize manual setup.  
   **Answer:** Service Connector with system-assigned managed identity.

6. Query became slow after deployment due to a new plan.  
   **Answer:** Query Store.

7. Need current blocking session ID and wait type.  
   **Answer:** `sys.dm_exec_requests`.

8. Two procedures update objects in opposite order and deadlock.  
   **Answer:** Make object access order consistent.

9. Need REST and GraphQL over SQL without custom API code.  
   **Answer:** Data API Builder.

10. DAB GraphQL must hide `InternalNotes` and `CostPrice`.  
    **Answer:** Configure read action with `fields.exclude`.

## 12.3 Domain 3

1. Which should be embedded: product description or product ID?  
   **Answer:** Product description.

2. 200-page PDF/document must support semantic search.  
   **Answer:** Chunk first, then embed chunks.

3. Semantic search over millions of vectors must be low latency.  
   **Answer:** ANN with vector-index-assisted search.

4. Need exact keyword plus semantic meaning and one ranking.  
   **Answer:** Hybrid search with RRF.

5. Chat answer may exceed 4,000 characters.  
   **Answer:** Extract using `OPENJSON WITH nvarchar(max)`.

6. Need structured values like category and priority from AI.  
   **Answer:** Chat endpoint with structured/JSON output, not embeddings.

7. SQL rows must be sent to model as context.  
   **Answer:** `FOR JSON PATH`.

8. Single-row JSON must be top-level object.  
   **Answer:** `WITHOUT_ARRAY_WRAPPER`.

9. Multi-row JSON must include null properties.  
   **Answer:** `FOR JSON PATH, INCLUDE_NULL_VALUES`.

10. Multiple consumers need near-real-time decoupled embedding maintenance.  
    **Answer:** Change Event Streaming.

---

# 13. Final Must-Memorize Facts

## Database Design

- Clustered index: one per rowstore table.
- Nonclustered index: supports lookups, joins, filters.
- INCLUDE columns reduce Key Lookups.
- Columnstore is for analytics.
- Filtered indexes are for small frequently queried subsets.
- Temporal means history.
- Ledger means tamper evidence.
- Append-only ledger means insert-only immutable records.
- Graph uses node, edge, `MATCH`, and sometimes `SHORTEST_PATH`.
- JSON scalar = `JSON_VALUE`; object/array = `JSON_QUERY`; array to rows = `OPENJSON`.

## Programmability

- Scalar function returns one value.
- Inline TVF returns a composable parameterized rowset.
- Stored procedure supports data-change workflows and output parameters.
- AFTER trigger validates/audits after DML.
- INSTEAD OF trigger replaces DML behavior.
- Triggers must handle multi-row operations.

## Security

- Always Encrypted protects plaintext from DBAs/admins.
- Deterministic encryption supports equality search.
- Randomized encryption is stronger but less searchable.
- DDM masks output only; it is not encryption.
- RLS uses predicate function and security policy.
- RLS filter predicate controls visibility; block predicate controls writes.
- Managed Identity enables passwordless Azure access.
- DENY usually overrides GRANT.

## Performance

- Execution plans diagnose one query.
- DMVs show current activity and engine stats.
- Query Store shows historical runtime and plan regressions.
- Query Performance Insight is Azure portal view of top resource-consuming queries.
- Blocking is one-way waiting.
- Deadlock is circular waiting.
- Parameter sniffing causes different performance for different parameter values.

## CI/CD and Integration

- SQL Database Project stores schema as code.
- DACPAC is deployable artifact.
- SqlPackage Publish deploys DACPAC.
- Schema drift means target database differs from project.
- DAB exposes SQL as REST/GraphQL without custom API code.
- DAB mutation is for data-changing stored procedure operations.
- Change Tracking = changed keys.
- CDC = detailed changes.
- CES = streaming changes.

## AI and RAG

- Embeddings represent semantic meaning.
- Embed descriptive text, not IDs or codes.
- Chunk large documents before embedding.
- `vector(n)` dimension must match model output.
- Cosine distance is common for text embeddings.
- ENN is exact but slower.
- ANN is approximate but faster.
- Full-text search is lexical.
- Vector search is semantic.
- Hybrid search plus RRF is strongest relevance pattern.
- RAG retrieves context before generation.
- Use `OPENJSON WITH nvarchar(max)` for long LLM responses.

---

# 14. Seven-Day Revision Plan

| Day | Focus |
|---:|---|
| 1 | Data types, constraints, indexes, partitioning, JSON indexing |
| 2 | Specialized tables, graph, programmability, triggers, advanced T-SQL |
| 3 | Security: encryption, DDM, RLS, permissions, auditing, endpoint security |
| 4 | Performance: plans, DMVs, Query Store, blocking, deadlocks, parameter sniffing |
| 5 | SQL projects, DACPAC, drift, GitHub workflow, DAB, Azure Monitor |
| 6 | Models, embeddings, chunking, vector search, full-text, hybrid search, RRF |
| 7 | RAG, external model calls, JSON response handling, decision tables, weak areas |

---

# 15. Deduplication and Move Log

| Original repeated area | Final location |
|---|---|
| Data type tables and top facts | Section 1.1 Data Types |
| Constraints and sequence examples | Section 1.2 Constraints, Identity, and Sequences |
| Index overview, scenario cheat sheet, Key Lookup, columnstore addendum | Section 1.3 Index Design |
| Partitioning original and practice scenario | Section 1.4 Partitioning |
| Temporal, Ledger, Memory Optimized, External, Graph | Section 1.5 Specialized Tables |
| JSON overview, syntax pack, RAG JSON, OPENJSON practice gaps | Section 1.6 JSON and Section 11 RAG |
| Views, functions, stored procedures, triggers, later usage guide | Section 2 Programmability Objects |
| CTE, window functions, regex, fuzzy, correlated queries, TRY/CATCH | Section 3 Advanced T-SQL |
| Copilot instructions, MCP scenarios, SSMS custom model notes | Section 4 AI-Assisted Development |
| Always Encrypted, DDM, RLS, permissions, auditing, endpoint security | Section 5 Security |
| DMVs, Query Store, execution plans, blocking, deadlocks, parameter sniffing | Section 6 Performance |
| SQL projects, DACPAC, GitHub secrets, drift reconciliation | Section 7 CI/CD |
| DAB REST/GraphQL, field security, stored procedure mutation, caching | Section 8 DAB and Azure Integration |
| Embeddings, external models, structured output, maintenance methods | Section 9 Models and Embeddings |
| Full-text, vector, ANN/ENN, hybrid, RRF, metrics | Section 10 Intelligent Search |
| RAG architecture, scoped credentials, JSON response extraction | Section 11 RAG |
| Practice questions and must-memorize lists | Sections 12 and 13 |

---

# 16. Source Note

This file was created by consolidating the uploaded README.md into one topic-centric master guide. The goal is to make each topic self-contained so a reader can study one topic and find the description, when-to-use guidance, syntax, scenarios, exam traps, and practice points in the same place.

---

# 17. DP-800 Skills Coverage Matrix

This matrix is included as a final quality gate so the README can be maintained against the official DP-800 skills outline without creating duplicate topic chapters.

| Official DP-800 objective area | Covered in this README V2 | Coverage status |
|---|---|---|
| Design and implement tables, data types, columns, rowstore indexes, and columnstore indexes | [Database Design](#1-database-design-and-database-objects), [Index Design](#13-index-design) | Complete |
| Specialized tables: in-memory, temporal, external, ledger, and graph | [Specialized Tables](#15-specialized-tables) | Complete |
| JSON columns, JSON functions, and JSON indexing | [JSON and Semi-Structured Data](#16-json-and-semi-structured-data), [RAG](#11-retrieval-augmented-generation-rag) | Complete |
| Constraints and sequences | [Constraints, Identity, and Sequences](#12-constraints-identity-and-sequences) | Complete |
| Partitioning for tables and indexes | [Partitioning](#14-partitioning) | Complete |
| Views, scalar functions, TVFs, stored procedures, and triggers | [Programmability Objects](#2-programmability-objects) | Complete |
| CTEs, window functions, correlated queries, error handling, regex, fuzzy functions, and graph MATCH | [Advanced T-SQL](#3-advanced-t-sql), [Graph tables](#15-specialized-tables) | Complete |
| GitHub Copilot, Fabric Copilot, instruction files, MCP tool options, and MCP endpoints | [AI-Assisted Development, Copilot, and MCP](#4-ai-assisted-development-copilot-and-mcp) | Complete |
| Always Encrypted, column-level encryption, Dynamic Data Masking, RLS, permissions, passwordless access, auditing, and endpoint security | [Security and Compliance](#5-security-and-compliance) | Complete |
| Database configurations, isolation levels, concurrency, execution plans, DMVs, Query Store, Query Performance Insight, blocking, and deadlocks | [Performance Optimization](#6-performance-optimization) | Complete |
| SQL Database Projects, SDK-style models, tests, source control, branching, PRs, secrets, drift, and deployment controls | [CI/CD with SQL Database Projects](#7-cicd-with-sql-database-projects) | Complete |
| Data API Builder REST/GraphQL, DAB deployment, cache, pagination, filtering, searching, stored procedures, views, and relationships | [Data API Builder and Azure Integration](#8-data-api-builder-and-azure-integration) | Complete |
| Azure Monitor, Application Insights, Log Analytics, CDC, Change Tracking, CES, Azure Functions SQL trigger, and Logic Apps | [Data API Builder and Azure Integration](#8-data-api-builder-and-azure-integration) | Complete |
| External models, multimodal/multilanguage/model size/structured output, model management, embedding maintenance, columns, chunks, and embeddings | [Models, Embeddings, and External AI](#9-models-embeddings-and-external-ai) | Complete |
| Full-text search, vector search, vector data type, vector indexes, vector functions, ANN vs ENN, vector metrics, hybrid search, RRF, and search performance | [Intelligent Search](#10-intelligent-search) | Complete |
| RAG use cases, `sp_invoke_external_rest_endpoint`, SQL-to-JSON conversion, sending results to models, and extracting model responses | [Retrieval-Augmented Generation - RAG](#11-retrieval-augmented-generation-rag) | Complete |

---

# 18. Final Validation Report for V3

## 18.1 Deduplication Validation

- Duplicate topic explanations were consolidated into one source-of-truth chapter.
- Duplicate syntax samples were merged into single authoritative examples unless the same syntax is intentionally reused in a different context.
- Duplicate comparison tables, decision trees, scenario lists, top facts, and practice notes were normalized into the relevant topic or final revision sections.
- The README no longer uses scattered addendum sections as the primary learning material.

## 18.2 Content Preservation Validation

The following original README content families were preserved by consolidation:

- Original domain-wise study guide content.
- Expanded scenario cheat sheets.
- Decision trees.
- Syntax pack examples.
- Top facts and final revision notes.
- Practice questions.
- Practice exam gap addendum.
- Security, DAB, performance, CI/CD, vector, RAG, graph, and MCP missing-detail sections.

## 18.3 Maintainability Guidance

When adding future content:

1. Do not create a new addendum unless it is temporary.
2. Add new details directly into the relevant chapter.
3. If adding a new scenario, place it under the topic's exam scenario or practice question section.
4. If adding a new syntax pattern, place it under the topic's syntax section.
5. If adding a new comparison, place it near the topic it helps explain.
6. Keep each concept as one source of truth.

## 18.4 Final Quality Checklist

- [x] Markdown format preserved.
- [x] Clickable table of contents added.
- [x] Heading hierarchy normalized.
- [x] Duplicate topic sections removed.
- [x] Related content consolidated.
- [x] Missing explanations filled where relevant.
- [x] Missing examples added where relevant, including expanded CTE, window functions, correlated queries, JSON, graph, security, performance, DAB REST/GraphQL, SQL AI conceptual functions, full-text, vector, and RAG examples.
- [x] Missing exam scenarios added where relevant.
- [x] DP-800 skills outline cross-check added.
- [x] Final revision structure retained.
- [x] Document reads as a professional study guide rather than accumulated notes.

