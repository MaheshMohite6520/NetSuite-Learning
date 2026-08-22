# Week 27 – Saved Search Fundamentals in NetSuite

## Overview

This week focuses on **NetSuite Saved Search Fundamentals**.

The goal is to understand how NetSuite's search architecture transforms simple record filtering into reusable, shareable, schedulable, and script-accessible data-retrieval objects through:

- Simple Searches
- Advanced Searches
- Saved Searches
- Saved Search Definition Page
- Criteria
- Results
- Summary Types
- Available Filters
- Formulas
- Permissions
- Audience & Roles
- Email & Scheduling
- Sharing & Governance
- SuiteScript 2.1 / N/search

A Saved Search is not simply a filtered list. It is a persisted, nameable, shareable search object that can power KPIs, dashboard and list views, reminders, scheduled emails, and other processes.

At a high level:

> **Simple Search → Advanced Search → Saved Search → Reusable Business Data → KPI / View / Reminder / Email / Integration**

This week builds the foundation behind the Custom KPIs introduced in Week 26 and prepares the architecture for the advanced search and performance techniques covered in Week 28.

---

# 📚 Topics Covered

- Search Architecture
- Simple Search
- Advanced Search
- Saved Search
- Saved Search Definition Page
- Header Settings
- Criteria Subtab
- Standard Filters
- Summary Filters
- Results Subtab
- Columns
- Sorting
- Output Types
- Drill Down
- Summary Types
- Group
- Count
- Sum
- Minimum
- Maximum
- Average
- Highlighting
- Available Filters
- Audience
- Roles
- Email & Scheduling
- Saving & Running Searches
- Search Formulas
- NetSuite Formula Variables
- Formula Limitations
- Search Permissions
- Perform Search
- Publish Search
- Persist Search
- Export Lists
- Tableau Workbooks Export
- Sharing & Governance
- Public vs Audience-Scoped Searches
- Allow Audience to Edit
- SuiteScript 2.1
- N/search
- `search.load()`
- `search.create()`
- `search.run()`
- Architect's Decision Framework

---

# 🏗️ What You'll Learn

- Understand how NetSuite's search architecture is layered.
- Understand the difference between Simple, Advanced, and Saved Searches.
- Learn why a Saved Search is more than a filtered list.
- Understand the anatomy of the Saved Search Definition Page.
- Learn how Header settings affect how a Saved Search behaves.
- Understand how the Criteria subtab determines which records qualify.
- Learn the difference between Standard and Summary filters.
- Understand how the Results subtab controls search output.
- Learn how columns, sorting, output types, and drill-down behavior work.
- Understand how Summary Types roll up search results.
- Learn how Group, Count, Sum, Minimum, Maximum, and Average work.
- Understand how Available Filters allow users to dynamically filter results.
- Learn how Audience and Roles control search visibility and presentation.
- Understand how Email alerts and scheduled emails work.
- Learn how formulas can be used in Criteria and Results.
- Understand NetSuite formula variables such as `{today}` and `{me}`.
- Learn important formula limitations and common pitfalls.
- Understand the permissions governing Saved Search capabilities.
- Learn the difference between visibility and editability.
- Understand Public vs Audience-based sharing.
- Learn how ownership changes can affect scheduled searches.
- Understand how Saved Searches can be accessed through SuiteScript 2.1.
- Learn how `search.load()` and `search.run()` work with existing Saved Searches.
- Understand the architectural decision points for choosing between Simple, Advanced, and Saved Search.

---

# 🎯 Why This Matters

A strong understanding of Saved Search architecture helps organizations:

- Build reusable data-retrieval components.
- Create reliable business metrics.
- Power Custom KPIs.
- Provide data to dashboard and list views.
- Build reminders and scheduled email processes.
- Give users controlled access to business data.
- Separate search definition from presentation.
- Apply role-based search governance.
- Build formula-driven reporting logic.
- Reproduce Saved Search results through SuiteScript.
- Create more maintainable NetSuite reporting solutions.
- Establish a strong foundation for advanced search construction and performance optimization.

The key architectural insight is:

> **A Saved Search is a reusable architecture component, not just a query.**

---

# 🔎 Search Architecture

NetSuite search capability is layered:

```text
Simple Search
      │
      ▼
Advanced Search
      │
      ▼
Saved Search
      │
      ├── KPIs
      ├── Dashboard Views
      ├── List Views
      ├── Reminders
      ├── Scheduled Emails
      └── Integrations
```

## Simple Search

A Simple Search provides basic field-based filtering.

It is useful when the requirement is simply to narrow down a list of records without complex search logic.

## Advanced Search

An Advanced Search adds capabilities such as:

- Multiple Criteria filters
- Results configuration
- Formulas
- Joins
- Expressions
- Sorting
- Summary calculations

## Saved Search

A Saved Search provides everything available in an Advanced Search while adding persistence and reusable configuration.

It can additionally provide:

- An owner
- Public or Audience-based sharing
- Available Filters
- Highlighting
- Email alerts
- Scheduled emails
- Dashboard and list views
- Reminder support
- Custom KPI eligibility

In practice:

> **Saved Search = Advanced Search + Persistence + Sharing + Reusability + Additional Automation**

---

# 📄 Saved Search Definition Page

A Saved Search definition page contains a header and multiple configuration subtabs.

The major areas include:

```text
Saved Search
│
├── Header
├── Criteria
├── Results
├── Available Filters
├── Highlighting
├── Audience
├── Roles
└── Email
```

The definition page controls not only which records are returned, but also how the search can be viewed, shared, scheduled, and reused.

---

# ⚙️ Header Settings

Important Header settings include:

- Title
- Owner
- Public
- Available as List View
- Available as Dashboard View
- Available as Sublist View
- Available for Reminders
- Show in Menu

The Title should be meaningful because it can surface as:

- A menu link
- A dashboard portlet header
- A Custom KPI name

Ownership is also important for scheduled searches.

Changing ownership of a scheduled Saved Search can silently stop the scheduled email if the new owner has never scheduled a Saved Search before. The new owner must log in and resave the search.

---

# 🔍 Criteria Subtab

The Criteria subtab determines which records qualify for the search.

It contains:

- Standard filters
- Summary filters

Standard filters can reference:

- Fields from the current record
- Related record fields
- Formula fields
- File-attachment fields

Multiple filters can also be combined using expressions.

For example:

```text
Condition A
      AND
Condition B
      OR
Condition C
```

The Criteria subtab is therefore the primary filtering layer of a Saved Search.

---

# 📅 Date Filters

Date filtering requires special attention.

If multiple date filters are configured on the Criteria subtab, the most recent date filter is used to calculate exchange rates.

For Saved Searches intended to work as Custom KPIs across multiple date ranges:

> **Do not place the date field as a Criteria filter.**

Instead, date scoping belongs on the:

```text
Available Filters
```

subtab.

This is the same structural concept used by the Custom KPIs discussed in Week 26.

---

# 📊 Results Subtab

The Results subtab controls what the search displays and how the results behave.

Important settings include:

- Sort By
- Output Type
- Show Totals
- Run Unrestricted
- Disallow Drill Down
- Max Results
- Columns
- Summary Types

A Saved Search requires a sort order. If no explicit Sort By is configured, the first Results column is used.

The Columns sublist controls:

- Displayed fields
- Custom labels
- Summary types
- Functions
- Column order

---

# 🧮 Summary Types

Summary Types allow Saved Searches to roll up groups of records.

The primary Summary Types are:

| Summary Type | Purpose |
|---|---|
| Group | Groups results by a field |
| Count | Counts results within a group |
| Sum | Adds numeric values |
| Minimum | Returns the smallest value or earliest date |
| Maximum | Returns the largest value or most recent date |
| Average | Calculates the average value |

The important relationship is:

```text
Group
  │
  ├── Count
  ├── Sum
  ├── Minimum
  ├── Maximum
  └── Average
```

`Group` provides the grouping structure that allows the other summary types to produce meaningful rollups.

---

# 📌 Custom KPI Connection

The Summary Type structure is directly connected to the Custom KPI architecture introduced in Week 26.

A Custom KPI-compatible Saved Search requires:

```text
No Date Criteria Filter
        +
Exactly One Summarized Results Field
        +
Date Available Filter
        =
Custom KPI-Compatible Search
```

The summarized Results field can use:

- `COUNT`
- `GROUP`
- `SUM`

Other Results fields should not have a summary type.

This makes Saved Search fundamentals the underlying foundation of the Custom KPI architecture.

---

# 🎛️ Available Filters

The Available Filters subtab provides additional filters that users can apply dynamically.

Unlike Criteria filters, Available Filters allow users to change the search scope without modifying the underlying Saved Search definition.

Available Filters can be presented as:

- Single-select filters
- Multi-select filters

The `Show in Filter Region` option determines whether the filter appears directly on the results page.

Date fields placed here are particularly important for searches that need to support multiple date ranges, including Custom KPI use cases.

---

# 👥 Audience & Roles

The Audience subtab controls who can run and view a Saved Search.

Audience can be defined using:

- Internal / External Roles
- Departments
- Subsidiaries
- Groups
- Employees
- Partners

The Roles subtab controls where search results can appear as default views.

This can include:

- Lists
- Sublists
- Dashboard list portlets
- Forms
- Quick Search results

---

# 📧 Email & Scheduling

The Email subtab supports:

- Record-based alert emails
- Scheduled emails
- Recurring email delivery
- Specific recipients
- Public subscription options

Scheduled email functionality is permission-gated through Publish Search.

This means a user may be able to run a Saved Search without necessarily being able to share or schedule it.

---

# ▶️ Saving & Running Searches

NetSuite provides several actions for executing a Saved Search:

```text
Preview
   │
   ├── Run without saving
   │
Save
   │
   ├── Persist the definition
   │
Save & Run
   │
   ├── Save and immediately display results
   │
Save & Email
   │
   └── Save and email configured recipients
```

`Save & Email` requires the appropriate Publish Search permission.

---

# 🧮 Formulas in Searches

Formulas can be used in several places:

- Custom formula-driven fields
- Criteria filters
- Results columns

Formula definitions can reference:

- NetSuite field IDs
- SQL functions
- Mathematical operators
- Built-in NetSuite variables

Formulas are dynamically recalculated when the search runs.

---

# 🔤 Built-in Formula Variables

Important variables include:

| Variable | Meaning |
|---|---|
| `{today}` | Current date |
| `{now}` | Current date/time context |
| `{me}` | Current user's internal ID |
| `{user.id}` | Current user's internal ID |
| `{userrole}` | Current user's role |
| `{userrole.id}` | Current user's role ID |
| `{user.department}` | Current user's department |
| `{user.location}` | Current user's location |
| `{user.subsidiary}` | Current user's subsidiary |
| `{user.class}` | Current user's class |
| `{usercurrency}` | Current user's currency |

For example:

```text
{today} - {startdate}
```

can calculate the number of days between the current date and a start date.

---

# ⚠️ Formula Pitfalls

Important formula considerations include:

- Aggregate and non-aggregate SQL functions cannot be mixed in a single formula definition.
- Formulas should reference internal field IDs rather than translated display values.
- Encrypted fields cannot be used in formulas.
- Formula (Text) results render as plain text for security.
- Formula (HTML) requires the appropriate feature and permission.

Using internal field IDs helps prevent formulas from behaving differently for users with different language preferences.

---

# 🔐 Permissions Governing Saved Searches

Five Lists-type permissions are particularly important:

| Permission | Primary Capability |
|---|---|
| Perform Search | Run and, at appropriate level, create/save searches |
| Publish Search | Share, alert, and schedule Saved Searches |
| Persist Search | Persist search results as CSV |
| Export Lists | Export/email search results |
| Tableau Workbooks Export | Export results to Tableau Workbooks |

These permissions operate independently.

Therefore:

> **A user may be able to run a Saved Search without being able to save, share, schedule, or export it.**

---

# 🛡️ Sharing & Governance

Saved Search visibility and editability are separate concepts.

There are two primary visibility approaches:

```text
Public
  │
  └── Available to all users

Audience
  │
  └── Available only to defined users/groups
```

Editability is controlled separately through:

```text
Allow Audience to Edit
```

Therefore:

> **Visibility ≠ Editability**

For sensitive data, Audience-based sharing is preferable to simply making a Saved Search Public.

---

# 👤 Ownership & Scheduled Searches

Ownership is important for scheduled searches.

When ownership changes:

```text
Scheduled Saved Search
        │
        ▼
   Owner Changed
        │
        ▼
New Owner Has Never Scheduled Search?
        │
        ▼
Scheduled Email Can Stop
```

The new owner must log in with the appropriate role and resave the search to reinstate the schedule.

---

# 💻 SuiteScript 2.1 — N/search

Saved Search definitions can be accessed through SuiteScript 2.1.

Two important approaches are:

```javascript
search.load()
```

and:

```javascript
search.create()
```

`search.load()` retrieves an existing Saved Search by its script ID.

Example:

```javascript
define(['N/search', 'N/log'], function (search, log) {

    function execute(context) {

        var savedSearch = search.load({
            id: 'customsearch_open_support_cases'
        });

        var openCount = 0;

        savedSearch.run().each(function (result) {

            openCount++;

            return true;
        });

        log.audit('Open Cases', openCount);
    }

    return {
        execute: execute
    };
});
```

The important architectural relationship is:

```text
Saved Search Definition
        │
        ▼
search.load()
        │
        ▼
Search Object
        │
        ▼
.run()
        │
        ▼
Results
```

This provides a programmatic way to reproduce the numbers produced by an existing Saved Search.

---

# 🏛️ Architect's Decision Framework

A practical decision framework for choosing the appropriate search type:

| Requirement | Recommended Approach |
|---|---|
| Filter results without persistence | Simple or Advanced Search |
| Need reusable results | Saved Search |
| Need sharing | Saved Search |
| Need scheduled emails | Saved Search |
| Need a Custom KPI | Properly structured Saved Search |
| Need multiple date ranges | Available Filters for date scoping |
| Need sensitive-data sharing | Audience-based access |
| Need editable access for others | Allow Audience to Edit |
| Need grouped results | Group Summary Type |
| Need counts or totals | Count / Sum Summary Types |
| Need script access to existing search | `search.load()` |
| Need programmatic search construction | `search.create()` |

---

# 🧠 Key Architectural Insight

A Saved Search should be viewed as a reusable NetSuite architecture component:

```text
                 Saved Search
                      │
        ┌─────────────┼─────────────┐
        ▼             ▼             ▼
    Criteria       Results       Formulas
        │             │             │
        └─────────────┼─────────────┘
                      ▼
                 Search Data
                      │
        ┌─────────────┼──────────────┐
        ▼             ▼              ▼
      KPI           Views          Email
        │             │              │
        ▼             ▼              ▼
    Dashboard      Lists         Scheduling
```

The same underlying Saved Search architecture can support multiple NetSuite capabilities.

This is why understanding Saved Searches properly is essential before moving into advanced search construction and performance optimization.

---

# 📚 Week 27 Learning Summary

- NetSuite search is layered: **Simple Search → Advanced Search → Saved Search**.
- A Saved Search is a persisted, ownable, shareable superset of an Advanced Search.
- Saved Searches can support KPIs, views, reminders, scheduled emails, and integrations.
- The Criteria subtab controls which records qualify.
- The Results subtab controls displayed fields, sorting, summaries, and output.
- Summary Types provide grouped and aggregated results.
- Available Filters allow users to dynamically scope search results.
- Formulas can use NetSuite field IDs, SQL functions, and built-in variables.
- Search permissions independently control running, saving, sharing, scheduling, and exporting.
- Public visibility and Audience-based access are separate governance mechanisms.
- Editability is controlled independently through Allow Audience to Edit.
- SuiteScript can load and execute Saved Searches through `search.load()` and `.run()`.
- Advanced search construction, joins, efficient result paging, and performance considerations are reserved for Week 28.

---

# 🚀 Next Week

**Week 28 – Advanced Saved Search & Performance**

Week 28 will move beyond the fundamentals covered here and explore:

- Advanced search construction
- Programmatic filters and columns
- Search joins
- `search.create()`
- Efficient result paging
- `getRange()`
- Search execution considerations
- Governance and performance
- Advanced N/search techniques

The progression is:

```text
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
```

> **Strong search fundamentals → Better reporting architecture → Better NetSuite solutions**
