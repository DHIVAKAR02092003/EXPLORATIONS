---
name: chart_generator
description: Generates visual charts and graphs from supply chain data including inventory levels, order trends, supplier distribution, and coverage analysis. Use this skill when the user asks for a chart, graph, plot, visualization, picture, or visual representation of supply chain data.
---

# Supply Chain Chart Generator Skill

You generate visual charts from supply chain data using Python code execution.

## When to Use
- User asks for a chart, graph, plot, or visualization
- User wants to "see" data visually
- User asks for trends over time
- User wants a picture or image of data

## Available Charts

### 1. Inventory Health Bar Chart
Show QUANTITY_ON_HAND vs SAFETY_STOCK_LEVEL for items, highlighting those below threshold in red.

### 2. Days Forward Coverage Distribution
Histogram showing distribution of DAYS_FORWARD_COVERAGE across all inventory items.

### 3. Order Status Pie Chart
Breakdown of orders by ORDER_STATUS (Placed, In Production, Shipped, Delivered, Cancelled).

### 4. Supplier Distribution by Business Line
Bar chart of supplier counts by BUSINESS_LINE.

### 5. Demand Trend Line Chart
Monthly order quantities over time from ORDERS table.

## Instructions for Code Execution
When generating charts, write Python code that:
1. Queries the relevant table using the Snowflake connection
2. Uses matplotlib or plotly to create the visualization
3. Saves the chart and returns it to the user

Example pattern:
```python
import matplotlib.pyplot as plt
import pandas as pd

# Query data
query = """
SELECT PRODUCT_ID, QUANTITY_ON_HAND, SAFETY_STOCK_LEVEL, DAYS_FORWARD_COVERAGE
FROM SUPPLY_CHAIN_NETWORK_OPTIMIZATION_DB.ENTITIES.MFG_INVENTORY
ORDER BY DAYS_FORWARD_COVERAGE ASC
LIMIT 20
"""

df = session.sql(query).to_pandas()

# Create chart
fig, ax = plt.subplots(figsize=(12, 6))
colors = ['red' if row['QUANTITY_ON_HAND'] < row['SAFETY_STOCK_LEVEL'] else 'green' for _, row in df.iterrows()]
ax.bar(df['PRODUCT_ID'].astype(str), df['QUANTITY_ON_HAND'], color=colors, label='On Hand')
ax.axhline(y=df['SAFETY_STOCK_LEVEL'].mean(), color='orange', linestyle='--', label='Avg Safety Stock')
ax.set_xlabel('Product ID')
ax.set_ylabel('Quantity')
ax.set_title('Inventory Health: Quantity on Hand vs Safety Stock')
ax.legend()
plt.tight_layout()
plt.show()
```

## IMPORTANT NOTE
This skill requires the `code_execution` tool to be enabled on the agent.
If code execution is not available, provide the data in a markdown table instead
and explain that chart generation requires the code_execution feature.
