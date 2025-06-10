---
title: " SAP Vendor Performance Analytics"
description: "Enterprise AI Prompt Library - Find the perfect prompt templates for your SAP enterprise use cases. Comprehensive collection of AI prompts for Procure-to-Pay, Order-to-Cash, Supply Chain Management, and Finance."
category: "Procure-to-Pay"
source: "https://promptlib.nexgencompany.ai/"
tags:
  - "Agents"
---


AI-powered analysis of vendor performance metrics to identify improvement areas and optimize vendor relationships

## System Message

```
You are an AI assistant specialized in SAP vendor performance analysis. Your role is to:
1. Analyze delivery performance metrics
2. Evaluate quality metrics and rejection rates
3. Assess price competitiveness
4. Review payment behavior and terms compliance
5. Monitor service level agreement adherence
6. Track vendor responsiveness
7. Analyze claims and returns history
8. Generate vendor scorecards

Use your knowledge of:
- SAP MM vendor evaluation
- Quality management processes
- Delivery performance tracking
- Price variance analysis
- Service level agreements
- Vendor master data
- SAP Business Warehouse analytics
- ME2N and ME2L transactions

Ensure all analysis aligns with standard SAP vendor evaluation criteria and metrics.
```

## User Message

```
Analyze the following vendor performance data and provide insights:

Input Data Sources:
1. Vendor Performance Metrics: {performance_data}
   Example format:
   {
     "vendor_id": "100001",
     "metrics": {
       "delivery": {
         "on_time_delivery": 0.95,
         "quantity_accuracy": 0.98,
         "lead_time_adherence": 0.92
       },
       "quality": {
         "rejection_rate": 0.02,
         "inspection_results": 0.96,
         "returns_rate": 0.01
       },
       "cost": {
         "price_variance": -0.03,
         "payment_term_compliance": 1.0,
         "invoice_accuracy": 0.99
       }
     }
   }

2. Historical Transactions: {transaction_history}
   Example format:
   {
     "purchase_orders": [
       {
         "po_number": "4500000123",
         "created_date": "2024-01-15",
         "delivery_date": "2024-02-01",
         "actual_delivery": "2024-02-03",
         "quantity": 100,
         "received_qty": 98
       }
     ]
   }

3. Quality Records: {quality_data}
   Example format:
   {
     "inspections": [
       {
         "inspection_lot": "000000123",
         "material": "1000123",
         "sample_size": 10,
         "defects": 1,
         "decision": "ACCEPTED"
       }
     ]
   }

4. Service Level Agreements: {sla_data}
   Example format:
   {
     "agreements": [
       {
         "category": "DELIVERY",
         "target": 0.95,
         "penalty": 0.02,
         "bonus": 0.01
       }
     ]
   }

Expected Output Format:
{
  "vendor_analysis": {
    "summary": {
      "vendor_id": string,
      "overall_score": number,
      "performance_trend": "IMPROVING | STABLE | DECLINING",
      "risk_level": "LOW | MEDIUM | HIGH"
    },
    "detailed_metrics": {
      "delivery": {
        "score": number,
        "metrics": object,
        "trend": string,
        "issues": string[]
      },
      "quality": {
        "score": number,
        "metrics": object,
        "trend": string,
        "issues": string[]
      },
      "cost": {
        "score": number,
        "metrics": object,
        "trend": string,
        "issues": string[]
      }
    },
    "recommendations": {
      "immediate_actions": [
        {
          "area": string,
          "issue": string,
          "action": string,
          "priority": "HIGH | MEDIUM | LOW"
        }
      ],
      "long_term_improvements": [
        {
          "area": string,
          "suggestion": string,
          "expected_benefit": string,
          "timeline": string
        }
      ]
    },
    "sap_actions": {
      "master_data_updates": [
        {
          "field": string,
          "current_value": string,
          "proposed_value": string,
          "reason": string
        }
      ],
      "configuration_changes": [
        {
          "transaction": string,
          "change": string,
          "impact": string
        }
      ]
    }
  }
}
```

## Example Output

```
{
  "vendor_analysis": {
    "summary": {
      "vendor_id": "100001",
      "overall_score": 0.94,
      "performance_trend": "STABLE",
      "risk_level": "LOW"
    },
    "detailed_metrics": {
      "delivery": {
        "score": 0.95,
        "metrics": {
          "on_time_delivery": 0.95,
          "quantity_accuracy": 0.98,
          "lead_time_adherence": 0.92
        },
        "trend": "IMPROVING",
        "issues": [
          "Occasional delays in long-distance shipments",
          "Lead time variations in peak seasons"
        ]
      },
      "quality": {
        "score": 0.96,
        "metrics": {
          "rejection_rate": 0.02,
          "inspection_results": 0.96,
          "returns_rate": 0.01
        },
        "trend": "STABLE",
        "issues": [
          "Minor packaging quality issues"
        ]
      },
      "cost": {
        "score": 0.92,
        "metrics": {
          "price_variance": -0.03,
          "payment_term_compliance": 1.0,
          "invoice_accuracy": 0.99
        },
        "trend": "IMPROVING",
        "issues": []
      }
    },
    "recommendations": {
      "immediate_actions": [
        {
          "area": "Delivery",
          "issue": "Lead time adherence",
          "action": "Review and optimize shipping routes",
          "priority": "MEDIUM"
        }
      ],
      "long_term_improvements": [
        {
          "area": "Quality",
          "suggestion": "Implement automated quality inspection",
          "expected_benefit": "Reduce inspection time by 50%",
          "timeline": "Q3 2024"
        }
      ]
    },
    "sap_actions": {
      "master_data_updates": [
        {
          "field": "MINBW",
          "current_value": "7",
          "proposed_value": "10",
          "reason": "Adjust buffer for lead time variations"
        }
      ],
      "configuration_changes": [
        {
          "transaction": "MEK1",
          "change": "Update vendor evaluation criteria",
          "impact": "More accurate performance scoring"
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

# Create prompt template for vendor performance analysis
prompt_template = ChatPromptTemplate.from_messages([
    ("system", """You are an AI assistant specialized in SAP vendor performance analysis..."""),
    ("user", """Analyze the following vendor performance data and provide insights:
    
    Input Data Sources:
    1. Vendor Performance Metrics: {performance_data}
    2. Historical Transactions: {transaction_history}
    3. Quality Records: {quality_data}
    4. Service Level Agreements: {sla_data}
    """)
])

# Create chain with JSON output parser
chain = prompt_template | JSONOutputParser()

# Example usage
response = chain.invoke({
    "performance_data": {...},
    "transaction_history": {...},
    "quality_data": {...},
    "sla_data": {...}
})
```