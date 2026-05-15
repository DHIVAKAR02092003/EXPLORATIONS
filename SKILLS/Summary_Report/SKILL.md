---
name: summary_report
description: Generates a formatted executive summary report of supply chain KPIs including inventory health, order fulfillment status, supplier performance, and critical alerts. Use this skill when the user asks for a summary, report, overview, dashboard, or KPI snapshot of the supply chain.
---

# Supply Chain Summary Report Skill

You generate a structured executive summary report of supply chain health and KPIs.

## Data Sources
- **SUPPLY_CHAIN_NETWORK_OPTIMIZATION_DB.ENTITIES.MFG_INVENTORY** - Inventory levels, safety stock, forward coverage
- **SUPPLY_CHAIN_NETWORK_OPTIMIZATION_DB.ENTITIES.ORDERS** - Customer orders and fulfillment status
- **SUPPLY_CHAIN_NETWORK_OPTIMIZATION_DB.ENTITIES.PRODUCT** - Product catalog and categories
- **SUPPLY_CHAIN_NETWORK_OPTIMIZATION_DB.ENTITIES.SUPPLIERS** - Supplier details and preferred status
- **SUPPLY_CHAIN_NETWORK_OPTIMIZATION_DB.ENTITIES.SHIPMENT** - Shipment tracking and delivery
- **SUPPLY_CHAIN_NETWORK_OPTIMIZATION_DB.ENTITIES.MFG_PLANT** - Plant capacity and locations

## Report Structure
Generate the report in this format:

### 1. INVENTORY HEALTH
- Total items tracked
- Items below safety stock (QUANTITY_ON_HAND < SAFETY_STOCK_LEVEL)
- Items with critical forward coverage (DAYS_FORWARD_COVERAGE < 7)
- Average days of forward coverage across all items

### 2. ORDER STATUS
- Total orders by status (Placed, In Production, Shipped, Delivered, Cancelled)
- Total order value
- Orders at risk (in production with inventory shortages)

### 3. SUPPLIER OVERVIEW
- Total active suppliers
- Preferred vs non-preferred supplier count
- Suppliers by business line breakdown

### 4. CRITICAL ALERTS
- List top 5 most urgent items (lowest DAYS_FORWARD_COVERAGE)
- Flag any items where QUANTITY_ON_HAND = 0
- Highlight items where lead time exceeds forward coverage

### 5. RECOMMENDATIONS
- Immediate actions needed
- Items to prioritize for replenishment
- Suggested supplier engagement

## Formatting Rules
- Use markdown tables for data
- Bold critical numbers
- Use emoji indicators: 🔴 critical, 🟡 warning, 🟢 healthy
- Keep the report concise (under 500 words)
