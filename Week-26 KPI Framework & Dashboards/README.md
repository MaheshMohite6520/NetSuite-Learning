# Week 26 – KPI Framework & Executive Dashboards in NetSuite

## Overview

This week focuses on **NetSuite KPI Framework and Executive Dashboard Architecture**.

The goal is to understand how NetSuite transforms financial and operational data into real-time, role-based decision-making surfaces through:

- Key Performance Indicators
- Standard KPIs
- Custom KPIs
- KPI Meters
- Trend Graphs
- KPI Scorecards
- Dashboard Publishing
- SuiteScript 2.1
- SuiteCloud Development Framework (SDF)

KPIs and dashboards are not simply reports with a different visual appearance. They form a presentation and decision-making layer on top of NetSuite's underlying financial, sales, support, ecommerce, HR, and operational data.

At a high level:

> **Business Data → KPI → Dashboard Portlet → Executive Insight → Role-Based Decision Making**


# 📚 Topics Covered

- Dashboard Architecture
- Centers
- Dashboards
- Dashboard Portlets
- Key Performance Indicators
- Standard KPIs
- Custom KPIs
- Custom KPI Saved Search Structure
- KPI Date Ranges
- KPI Employee Scope
- KPI Highlighting
- KPI Thresholds
- KPI Comparisons
- KPI Meters
- Trend Graphs
- KPI Scorecards
- Scorecard Date Ranges
- Scorecard Periods
- Scorecard Formulas
- Multi-KPI Comparisons
- Dashboard Publishing
- Publish Dashboards Permission
- Role-Based Dashboards
- SuiteScript 2.1
- N/search
- N/query / SuiteQL
- SDF
- KPI Scorecard Deployment
- Dashboard Deployment Limitations
- Enterprise KPI Architecture
- Architect Decision Framework


# 🏗️ What You'll Learn

- Understand how NetSuite's dashboard layer is structured.
- Learn how Centers, Dashboards, Portlets, and KPIs relate to each other.
- Understand the difference between Standard KPIs and Custom KPIs.
- Learn how Standard KPIs are based on NetSuite's standard reports.
- Understand how a Saved Search can become a Custom KPI.
- Learn the structural requirements for a Saved Search to work as a Custom KPI.
- Understand how KPI date ranges and employee scope affect results.
- Learn how KPI thresholds and highlighting work.
- Understand KPI comparisons and comparison ranges.
- Learn how KPI Meters visualize individual KPIs.
- Understand how Trend Graphs visualize KPI changes over time.
- Learn how KPI Scorecards support multi-KPI and multi-period analysis.
- Understand Scorecard formulas and comparison behavior.
- Learn how dashboards can be published across roles.
- Understand dashboard publishing permissions and Center restrictions.
- Learn what KPI-related objects can be accessed through SuiteScript.
- Understand how to reproduce Custom KPI values through their underlying Saved Searches.
- Learn how KPI Scorecards can be represented using SDF.
- Understand why dashboard layout and publishing are not general-purpose SDF objects.
- Learn how to design scalable KPI and dashboard architectures.


# 🎯 Why This Matters

A strong understanding of KPI and dashboard architecture helps organizations:

- Turn operational data into actionable business metrics.
- Provide executives with real-time visibility.
- Create role-based decision-making dashboards.
- Standardize KPI definitions across teams.
- Compare current performance with previous periods.
- Identify important threshold conditions quickly.
- Analyze multiple KPIs together.
- Build structured executive scorecards.
- Reduce manual reporting effort.
- Provide consistent dashboards across teams.
- Build reliable reporting and integration solutions.
- Separate data architecture from presentation-layer configuration.
- Improve enterprise reporting governance.
- Create scalable NetSuite dashboard architectures.


# 🏢 Dashboard Architecture

NetSuite's dashboard layer can be viewed as:

                         Center
                           │
                           ▼
                       Dashboard
                           │
                           ▼
                        Portlets
                           │
          ┌────────────────┼────────────────┐
          ▼                ▼                ▼
         KPI              Meter         Trend Graph
          │                                  │
          └────────────────┬─────────────────┘
                           ▼
                      KPI Scorecard
                           │
                           ▼
                          KPI
                           │
                 ┌─────────┴─────────┐
                 ▼                   ▼
          Standard KPI          Custom KPI
                 │                   │
          Standard Report        Saved Search


A simplified architecture is:

> **Center → Dashboard → Portlet → KPI → Underlying Report / Saved Search**

A **Center** represents the role-based set of tabbed pages a user sees.

A **Dashboard** is a personalized collection of portlets.

A **Portlet** provides the presentation container.

A **KPI** represents the underlying business metric.


# 📊 Key Performance Indicators

The **Key Performance Indicators portlet** is the primary KPI presentation surface.

It can display:

- Standard KPIs
- Custom KPIs
- KPI ranges
- Employee scope
- Threshold highlighting
- Comparisons
- Headline KPIs
- Popup Trend Graphs

The KPI portlet can display up to **8 KPIs as headline KPIs**.

It can also contain up to **10 Custom KPIs**.

A KPI can provide a click-through path to its underlying report or Saved Search.


# 📦 Standard KPIs

NetSuite provides **75+ Standard KPIs**.

Standard KPIs are based on NetSuite's standard reports and underlying business data.

They provide predefined metrics across areas such as:

### Financial

- Revenue
- Expenses
- Profit
- COGS
- Receivables
- Payables
- Cash-related metrics

### Sales

- Sales
- Orders
- Forecast
- Quota
- Pipeline
- New Business

### CRM

- Leads
- Opportunities
- Open Opportunities
- Estimates
- Quotes

### Support

- Cases
- Open Cases
- Closed Cases
- Issues

### Ecommerce

- Web Orders
- Web Revenue
- Website Activity
- Cart Abandonment

The Standard KPI framework provides a predefined reporting layer without requiring a Saved Search for every common business metric.


# 🧩 Custom KPIs

Standard KPIs cannot cover every business requirement.

A **Custom KPI** allows a Saved Search to become a KPI data source.

For example:

                 Business Requirement
                         │
                         ▼
                 Metric not available
                  as Standard KPI
                         │
                         ▼
                  Saved Search
                         │
                         ▼
              Validate KPI Structure
                         │
                         ▼
                    Custom KPI
                         │
             ┌───────────┼────────────┐
             ▼           ▼            ▼
         KPI Portlet   KPI Meter   Trend Graph
                         │
                         ▼
                   KPI Scorecard


Custom KPIs can be useful for:

- Department-specific metrics
- Custom transaction rollups
- Custom record metrics
- Operational counts
- Specialized business calculations

A Custom KPI is therefore not simply another type of report.

It is a way of turning a properly structured Saved Search into a reusable KPI metric.


# ⚠️ Custom KPI Structural Requirement

A Saved Search must satisfy a specific structure before NetSuite can use it reliably as a Custom KPI.

The search must satisfy all three conditions:

### 1. No Date Criteria Filter

The Saved Search must **not include a date field as a filter on the Criteria subtab**.

### 2. Exactly One Summarized Results Field

The Results subtab must contain:

- Exactly one field with a summary type.
- The summary type can be:
  - `COUNT`
  - `GROUP`
  - `SUM`

Other Results fields must not have a summary type.

### 3. Date Available Filter

A date field must be defined as an **Available Filter**.

Therefore:

> **No Date Criteria Filter + One Summarized Results Field + Date Available Filter = Custom KPI-Compatible Search**

This is a critical structural rule for Custom KPIs.

A search that violates one of these requirements may:

- Not appear as an eligible Custom KPI.
- Produce blank results.
- Produce incorrect comparison data.
- Produce incorrect trend data.


# 🔄 One Metric, Multiple Surfaces

A single Saved Search can provide the underlying data for different KPI surfaces.

However, the KPI configuration is not automatically shared between every surface.

Conceptually:

                       Saved Search
                            │
             ┌──────────────┼──────────────┐
             ▼              ▼              ▼
        KPI Portlet      KPI Meter     Trend Graph
             │
             ▼
        KPI Scorecard


The important architectural point is:

> **The same Saved Search does not mean one shared KPI configuration.**

Custom KPI definitions can be configured independently for:

- KPI Portlet
- KPI Meter
- Trend Graph
- KPI Scorecard

For example:

> Changing the Saved Search assigned to a Custom KPI slot in the KPI Portlet does not automatically change the Custom KPI mapping inside a KPI Scorecard.

Each surface must be checked independently when troubleshooting.


# 🎯 KPI Highlighting & Thresholds

The KPI Portlet can highlight a KPI when its value crosses a configured threshold.

For example:

                    KPI
                     │
                     ▼
                Threshold
                     │
              ┌──────┴──────┐
              ▼             ▼
           Below          Above
           Target         Target
              │             │
              ▼             ▼
           Normal        Highlighted


A KPI can be configured to highlight when it is:

- Greater than a threshold.
- Less than a threshold.

Thresholds can therefore be used to make important KPI conditions visible immediately.

Up to **8 KPIs** can be displayed as headline KPIs.


# 🔄 KPI Comparisons

KPI comparisons allow a KPI's current range to be compared against another range.

For example:

                  Current Period
                       │
                       ▼
                     Sales
                       │
                ┌──────┴──────┐
                ▼             ▼
          Current Range   Compare Range
             $2.45M          $2.18M
                │             │
                └──────┬──────┘
                       ▼
                    Variance
                    +12.5%


KPI comparisons can provide:

- Current KPI value
- Comparison KPI value
- Percentage change
- Time-based analysis

A time-based comparison can also enable the KPI's popup Trend Graph.


# 📏 KPI Meters

A **KPI Meter** visually represents one KPI as a semi-circular gauge.

For example:

                    KPI Meter

                ┌───────────────┐
              /                   \
             /       85%           \
            /         ▲             \
           /           │             \
          └───────────────────────────┘
                     Target


Important characteristics:

- Represents one KPI.
- Uses a visual gauge.
- Supports KPI comparisons.
- Supports threshold settings.
- Up to **3 KPI Meter portlets** can be added to a dashboard.
- KPI choices are based on KPIs available in the Key Performance Indicators portlet.

Special ratio KPI options include:

- Actual vs. Forecast
- Actual vs. Quota
- Forecast vs. Quota
- Forecast vs. Quota (Alt. Sales)

For ratio-based meters, the required underlying KPIs must already be available in the KPI Portlet.


# 📈 Trend Graphs

Trend Graphs illustrate how KPIs change over time.

Supported chart types include:

- Area
- Line
- Bar
- Column

A Trend Graph can display up to **3 KPIs**.

Trend Graphs can appear in two forms:

### Popup Trend Graphs

Popup Trend Graphs can be launched from the Trend Graph icon in:

- KPI Portlets
- KPI Scorecards

A KPI generally needs a time-based comparison configured before the popup Trend Graph becomes available.

### Trend Graph Portlets

Trend Graph Portlets can be added directly to a dashboard.

Up to **5 Trend Graph portlets** can be added to a dashboard.

Trend Graphs support:

- Printing
- PNG download
- JPG download
- PDF download
- SVG download
- CSV export of underlying data

For Custom KPIs, the underlying Saved Search must satisfy the Custom KPI structural requirements.


# 📋 KPI Scorecards

KPI Scorecards provide a more advanced KPI comparison framework.

They support:

- Multiple KPIs
- Multiple date ranges
- Multiple periods
- KPI comparisons
- Custom KPIs
- Formula-based calculations

Conceptually:

                    KPI Scorecard
                         │
          ┌──────────────┼──────────────┐
          ▼              ▼              ▼
       Revenue         Profit         Orders
          │              │              │
     ┌────┼────┐    ┌────┼────┐    ┌────┼────┐
     ▼    ▼    ▼    ▼    ▼    ▼    ▼    ▼    ▼
   Current Prior YoY Current Prior YoY Current Prior YoY


KPI Scorecards therefore provide a structured way to analyze multiple KPIs across multiple time dimensions.


# 📅 KPI Scorecard Date Ranges & Periods

KPI Scorecards can work with:

- Date Ranges
- Accounting Periods

When **Use Periods** is enabled, the Date Ranges configuration is replaced by Periods.

This allows the scorecard to organize KPI comparisons around NetSuite accounting periods.

When Periods are used, Custom KPIs configured within the Scorecard require the appropriate Period Available Filter rather than the standard Date Available Filter structure.


# 🧮 KPI Scorecard Formulas

KPI Scorecards support Excel-like formulas.

Formula types include:

- Formula (Percent)
- Formula (Absolute)
- Formula (Currency)

Examples include:

### Percentage Variance

100 × (Current - Previous) / Previous

## Next Week

**Week 27 – Saved Search Fundamentals**, where we'll explore the foundation behind one of NetSuite's most important reporting and customization capabilities: **Saved Searches**.

Week 27 will move one layer deeper into the architecture explored this week:

Week 27

Saved Search Fundamentals
        │
        ├── Saved Search Architecture
        ├── Search Types
        ├── Criteria & Filters
        ├── Available Filters
        ├── Results
        ├── Summary & Grouping
        ├── Formulas
        ├── Joins
        ├── Sorting
        ├── Search Execution
        ├── Permissions
        ├── Performance
        └── SuiteScript / SuiteQL
