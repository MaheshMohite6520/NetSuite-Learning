# Week 28 – Advanced Saved Search & Performance in NetSuite

## Overview

This week moves beyond the **Saved Search fundamentals** covered in Week 27 and explores how advanced search construction, formulas, auditing, performance, and SuiteScript can be used to build more capable and scalable NetSuite search solutions.

The goal is to understand how NetSuite's Saved Search architecture can be extended through:

- Search Joins
- Filter Expressions
- AND / OR / NOT Logic
- Search Operators
- Advanced SQL Formulas
- Numeric Functions
- Character Functions
- Datetime Functions
- NULL Handling
- DECODE / CASE
- Analytic Functions
- Formula (HTML)
- System Note Search
- Deleted Record Search
- Saved Search Execution Log
- Audit Trail
- Persisting Search Results
- Search Performance Analysis
- APM SuiteApp
- SuiteScript 2.1 / N/search
- `search.create()`
- `search.load()`
- `getRange()`
- `runPaged()`
- Governance-aware Search Processing

A Saved Search is not limited to simple filtering and reporting. At an advanced level, it can become a powerful mechanism for accessing related records, expressing complex business logic, auditing changes, executing SQL-style formulas, processing large result sets, and integrating search logic with SuiteScript.

At a high level:

> **Saved Search Fundamentals → Advanced Search Logic → SQL Formulas → Audit Data → Performance Engineering → Programmatic Search**

This week builds directly on Week 27 and prepares the foundation for more advanced NetSuite analytics and reporting architectures.


# 📚 Topics Covered

- Advanced Saved Search Architecture
- Search Joins
- Related Record Fields
- Multi-Level Joins
- Filter Expressions
- Use Expressions
- Explicit AND / OR Logic
- Parenthetical Logic
- Search Operators
- Equality / List Operators
- Text Matching Operators
- Numeric Comparison Operators
- Date Comparison Operators
- Emptiness Operators
- Free-form Operators
- `search.Operator`
- SQL Formula Surface
- Numeric SQL Functions
- Character SQL Functions
- Datetime SQL Functions
- NULL Handling
- `COALESCE`
- `NVL`
- `NVL2`
- `NULLIF`
- `DECODE`
- `CASE`
- Analytic Functions
- `RANK`
- `DENSE_RANK`
- `KEEP`
- Formula Guardrails
- Formula (HTML)
- HTML Formula Permissions
- System Note Search
- System Note Fields
- Deleted Record Search
- Saved Search Execution Log
- Audit Trail
- Persisting Search Results
- Persist Search Permission
- Search Performance Analysis
- Application Performance Management (APM)
- Search Performance Details Dashboard
- Search Performance Monitoring
- SuiteScript 2.1
- `N/search`
- `search.create()`
- `search.load()`
- Scripted Filter Expressions
- Joined Columns
- Formula Columns
- Summary Columns
- `ResultSet.each()`
- `ResultSet.getRange()`
- `Search.runPaged()`
- `PagedData`
- `PageRange`
- `Page`
- `search.lookupFields()`
- `search.duplicates()`
- `search.global()`
- `Column.setWhenOrderedBy()`
- `Search.save()`
- Governance-aware Search Design
- Architect's Decision Framework


# 🏗️ What You'll Learn

- Understand how advanced Saved Searches extend the fundamentals introduced in Week 27.
- Learn how Search Joins allow filters and Results columns to reach related records.
- Understand how joins can be chained across multiple relationships.
- Learn how to deliberately combine fields from different related records.
- Understand how NetSuite evaluates Standard filters by default.
- Learn how **Use Expressions** enables explicit AND / OR logic.
- Understand how parentheses control filter evaluation order.
- Learn how Summary filters differ from Standard filter expressions.
- Understand the major categories of NetSuite Search Operators.
- Learn how the same operator vocabulary applies across the UI and SuiteScript.
- Understand how `search.Operator` is used programmatically.
- Learn how NetSuite exposes a defined subset of Oracle SQL functions to Saved Search formulas.
- Understand Numeric, Character, and Datetime SQL functions.
- Learn how NULL-handling functions behave.
- Understand when to use `DECODE` and when `CASE` is more maintainable.
- Learn how analytic functions such as `RANK` and `DENSE_RANK` work.
- Understand how `KEEP()` can return values associated with ordered aggregate results.
- Learn the guardrails that apply to advanced formulas.
- Understand the difference between Formula (Text) and Formula (HTML).
- Learn how Formula (HTML) is enabled and permission-gated.
- Understand how System Note searches can be used as an audit mechanism.
- Learn how System Note fields can be incorporated into other record searches.
- Understand how Deleted Record searches expose deletion history.
- Learn how the Saved Search Execution Log differs from the Audit Trail.
- Understand how Persisting Search Results handles searches that are too large to render normally.
- Learn how the Search Performance Analysis dashboard helps identify performance issues.
- Understand when to use Persist (CSV) versus ongoing performance monitoring.
- Learn how `search.create()` builds searches programmatically.
- Understand when `search.create()` is preferable to `search.load()`.
- Learn how scripted filter expressions mirror the UI's Use Expressions syntax.
- Understand how joins and formulas are represented in scripted columns.
- Learn how `getRange()` and `runPaged()` retrieve large result sets.
- Understand why `runPaged()` is generally preferred for very large result sets.
- Learn how `search.lookupFields()` can avoid unnecessary full-search execution.
- Understand additional N/search methods such as `search.global()`, `search.duplicates()`, and `Search.save()`.
- Learn how governance considerations influence search design.
- Apply an architect-level decision framework to advanced Saved Search requirements.


# 🎯 Why This Matters

Advanced Saved Search knowledge helps organizations:

- Build more precise reporting logic.
- Query related records without duplicating data structures.
- Express complex business rules through filter expressions.
- Create SQL-driven reporting calculations.
- Rank and compare records within groups.
- Investigate historical changes through System Notes.
- Investigate deleted records.
- Diagnose who ran a search and when.
- Prevent large searches from timing out in the browser.
- Monitor search performance over time.
- Process large result sets efficiently through SuiteScript.
- Keep governance usage proportional to the amount of data actually processed.
- Separate one-time large exports from ongoing performance monitoring.
- Build reusable programmatic search components.
- Create more maintainable SuiteScript search implementations.
- Reduce unnecessary search execution when only a few fields are required.

The key architectural insight is:

> **An advanced Saved Search is not just about finding more records. It is about controlling how data is reached, filtered, calculated, audited, monitored, and processed.**

# 🧠 Key Architectural Insight

Advanced Saved Search should be viewed as a complete data-processing architecture:

                       Saved Search
                            │
          ┌─────────────────┼─────────────────┐
          ▼                 ▼                 ▼
       Joins          Filter Logic        Formulas
          │                 │                 │
          └─────────────────┼─────────────────┘
                            ▼
                      Search Results
                            │
          ┌─────────────────┼─────────────────┐
          ▼                 ▼                 ▼
       Auditing        Performance          SuiteScript
          │                 │                 │
          ▼                 ▼                 ▼
   System Notes        Persist / APM       N/search
   Deleted Records                         Paging
   

The same search architecture can therefore support:

Business Reporting
        +
Audit Investigation
        +
Performance Engineering
        +
Programmatic Processing

The key lesson is:

> **Advanced search design is not only about writing a more complicated query. It is about designing a reliable data-retrieval component that remains correct, auditable, performant, and maintainable as usage grows.**

# 🚀 Next Week

**Week 29 – SuiteAnalytics & Workbooks**

Week 29 will move beyond the Saved Search architecture and into NetSuite's analytics and workbook capabilities.

The progression is:

Week 26
KPI Framework & Executive Dashboards
        │
        ▼
Week 27
Saved Search Fundamentals
        │
        ▼
Week 28
Advanced Saved Search & Performance
        │
        ▼
Week 29
SuiteAnalytics & Workbooks

The learning progression is:

> **Search Fundamentals → Advanced Search Engineering → Analytics & Workbooks**

---

> **Strong search architecture → Better performance → Better analytics → Better NetSuite solutions**

```

The README deliberately preserves the Week 27 structure, while the Week 28 content is grounded in the document's actual sections and final learning summary, including joins/filter expressions, SQL formulas, auditing, persistence/APM, and `N/search` paging. :contentReference[oaicite:1]{index=1}
```
