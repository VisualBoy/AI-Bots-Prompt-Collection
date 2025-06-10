---
title: "SAP MRP Optimization Assistant"
description: "Enterprise AI Prompt Library - Find the perfect prompt templates for your SAP enterprise use cases. Comprehensive collection of AI prompts for Procure-to-Pay, Order-to-Cash, Supply Chain Management, and Finance."
category: " Supply Chain Management"
source: "https://promptlib.nexgencompany.ai/"
tags:
  - "Agents"
---


## SAP MRP Optimization Assistant

AI-powered optimization of material requirements planning to improve procurement efficiency and reduce inventory costs

## System Message

```
You are an AI assistant specialized in SAP material requirements planning. Your role is to:
1. Analyze material requirements
2. Optimize order quantities
3. Balance inventory levels
4. Evaluate lead times
5. Consider lot sizes
6. Assess safety stocks
7. Optimize reorder points
8. Manage dependencies

Use your knowledge of:
- SAP MM (Materials Management)
- SAP PP (Production Planning)
- MRP procedures
- Inventory management
- Procurement strategies
- Lead time analysis
- Lot size optimization
- Safety stock calculation

Ensure all recommendations align with SAP MRP processes and business objectives.
```

## User Message

```
Analyze the following material planning data and provide optimization recommendations:

Input Data Sources:
1. Material Requirements: {requirements_data}
   Example format:
   {
     "material_id": "MAT001",
     "requirements": [
       {
         "period": "2024-04",
         "quantity": 1000,
         "source": "SALES_ORDER | FORECAST",
         "priority": "HIGH"
       }
     ],
     "current_stock": {
       "on_hand": 500,
       "in_transit": 200,
       "reserved": 300
     }
   }

2. Planning Parameters: {planning_data}
   Example format:
   {
     "mrp_type": "PD",
     "lot_size": {
       "minimum": 100,
       "maximum": 1000,
       "rounding": 10
     },
     "safety_stock": 200,
     "reorder_point": 300
   }

3. Supply Sources: {supply_data}
   Example format:
   {
     "suppliers": [
       {
         "supplier_id": "SUP001",
         "lead_time": 14,
         "min_order_qty": 100,
         "price_breaks": [
           {
             "quantity": 500,
             "price": 95.00
           }
         ]
       }
     ]
   }

4. Cost Parameters: {cost_data}
   Example format:
   {
     "holding_cost": 0.02,
     "ordering_cost": 150.00,
     "stockout_cost": 500.00,
     "unit_cost": 100.00
   }

Expected Output Format:
{
  "mrp_optimization": {
    "summary": {
      "material_id": string,
      "planning_horizon": string,
      "critical_issues": string[],
      "optimization_potential": string
    },
    "requirements_analysis": {
      "total_demand": number,
      "net_requirements": number,
      "coverage_profile": {
        "periods": string[],
        "quantities": number[],
        "coverage_days": number[]
      }
    },
    "planning_recommendations": {
      "lot_sizing": {
        "current": object,
        "recommended": object,
        "justification": string
      },
      "safety_levels": {
        "safety_stock": number,
        "reorder_point": number,
        "max_stock": number
      }
    },
    "procurement_plan": {
      "planned_orders": [
        {
          "period": string,
          "quantity": number,
          "supplier": string,
          "cost": number
        }
      ],
      "schedule_adjustments": [
        {
          "order_number": string,
          "current_date": string,
          "proposed_date": string,
          "reason": string
        }
      ]
    }
  }
}
```

## Example Output

```
{
  "mrp_optimization": {
    "summary": {
      "material_id": "MAT001",
      "planning_horizon": "6 months",
      "critical_issues": [
        "Suboptimal lot sizes",
        "High safety stock"
      ],
      "optimization_potential": "15% cost reduction"
    },
    "requirements_analysis": {
      "total_demand": 6000,
      "net_requirements": 5600,
      "coverage_profile": {
        "periods": ["2024-04", "2024-05", "2024-06"],
        "quantities": [1000, 1200, 1100],
        "coverage_days": [25, 28, 26]
      }
    },
    "planning_recommendations": {
      "lot_sizing": {
        "current": {
          "size": 1000,
          "frequency": "MONTHLY"
        },
        "recommended": {
          "size": 800,
          "frequency": "BI-WEEKLY"
        },
        "justification": "Better balance between ordering and holding costs"
      },
      "safety_levels": {
        "safety_stock": 150,
        "reorder_point": 250,
        "max_stock": 1000
      }
    },
    "procurement_plan": {
      "planned_orders": [
        {
          "period": "2024-04-01",
          "quantity": 800,
          "supplier": "SUP001",
          "cost": 76000.00
        }
      ],
      "schedule_adjustments": [
        {
          "order_number": "PO2024001",
          "current_date": "2024-04-15",
          "proposed_date": "2024-04-01",
          "reason": "Align with optimal lot size"
        }
      ]
    }
  }
}
```

## Implementation Examples

```
from langchain.prompts import ChatPromptTemplate
from langchain.output_parsers import JSONOutputParser

# Create prompt template for material planning optimization
prompt_template = ChatPromptTemplate.from_messages([
    ("system", """You are an AI assistant specialized in SAP material requirements planning..."""),
    ("user", """Analyze the following material planning data and provide optimization recommendations:
    
    Input Data Sources:
    1. Material Requirements: {requirements_data}
    2. Planning Parameters: {planning_data}
    3. Supply Sources: {supply_data}
    4. Cost Parameters: {cost_data}
    """)
])

# Create chain with JSON output parser
chain = prompt_template | JSONOutputParser()

# Example usage
response = chain.invoke({
    "requirements_data": {...},
    "planning_data": {...},
    "supply_data": {...},
    "cost_data": {...}
})
```