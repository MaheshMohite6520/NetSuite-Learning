# Week 02 – NetSuite Master Data Architecture

## Overview

This week focuses on understanding **Master Data Architecture in NetSuite**.

Master data is the structural backbone of the system. Every transaction, workflow, financial report, and automation depends on properly designed and governed master records.

Without strong master data architecture:
- Reporting becomes inconsistent  
- Automation becomes unstable  
- Customization turns into technical debt  

This week organizes master data into a layered architecture model to ensure scalability, financial accuracy, and governance control.


## Topics Covered

- Core Transactional Masters (Customer, Vendor, Item, Employee)
- Financial Architecture Masters (Chart of Accounts, Subsidiary, Accounting Period, Currency)
- Control & Classification Masters (Department, Class, Location, Payment Terms, Price Levels, Tax Codes)
- Custom Records as Master Data
- Governance Controls and Configuration Risks
- Developer Considerations for Performance & Scalability
- Multi-Subsidiary and Multi-Currency Impact
- Financial Posting Dependencies


## Architectural Layers

### 1️⃣ Core Transactional Masters
Entities directly referenced in operational transactions.

These drive:
- Revenue
- Expense
- Inventory movement
- Approval workflows


### 2️⃣ Financial Architecture Masters
Records that control accounting structure and financial reporting integrity.

These define:
- GL structure
- Legal entity segregation
- Period control
- Currency behavior


### 3️⃣ Control & Classification Masters
Records used for segmentation, pricing logic, and policy enforcement.

These enable:
- Profitability analysis
- Cash flow forecasting
- Pricing consistency
- Tax compliance


### 4️⃣ Advanced & Custom Master Strategy
User-defined master records supporting business-specific automation and scalability.

These influence:
- Workflow routing
- Approval matrices
- Reporting logic
- Script performance


## Why This Matters for Developers

As NetSuite developers, understanding master data architecture is critical before writing scripts or building customizations.

### Key Developer Takeaways

- Avoid hardcoding internal IDs
- Design scalable data relationships
- Optimize saved search joins
- Respect subsidiary and currency restrictions
- Validate period locks before posting
- Prevent governance-heavy loops
- Maintain referential integrity across records

Strong architecture reduces rework, improves performance, and minimizes long-term technical debt.


## Real-World Data Flow Example

Customer configured with:
- Subsidiary  
- Currency  
- Terms  
- Price Level  


Sales Order created  
→ Item determines income & COGS accounts  
→ Department / Class segments reporting  
→ Tax Code calculates tax  
→ Invoice posts to Chart of Accounts  
→ Accounting Period controls posting  
→ Subsidiary controls consolidation  
→ Management views segmented P&L  

Every step depends on master data accuracy.


## Common Risks Identified

- Duplicate master creation
- Incorrect GL mapping
- Poor subsidiary hierarchy design
- Improper period locking
- Over-segmentation
- Excessive custom record creation
- Performance degradation due to inefficient joins


## Next Topic

**Week 03 – Items Foundation**
