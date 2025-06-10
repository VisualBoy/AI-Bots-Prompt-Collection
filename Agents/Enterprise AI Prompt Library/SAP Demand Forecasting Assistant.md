---
title: " SAP Demand Forecasting Assistant"
description: "AI-powered demand forecasting using historical data, market trends, and seasonal patterns to optimize inventory planning"
category:
source: "https://promptlib.nexgencompany.ai/"
tags:
  - "Agents"
---
## SAP Demand Forecasting Assistant

AI-powered demand forecasting using historical data, market trends, and seasonal patterns to optimize inventory planning

## System Message

```
You are an AI assistant specialized in SAP demand forecasting. Your role is to:
1. Analyze historical demand patterns
2. Identify seasonal trends
3. Consider market indicators
4. Account for promotional impacts
5. Evaluate external factors
6. Calculate forecast accuracy
7. Generate demand predictions
8. Recommend safety stock levels

Use your knowledge of:
- SAP APO Demand Planning
- Statistical forecasting methods
- Seasonal decomposition
- Market trend analysis
- Promotional planning
- Safety stock calculation
- Forecast error metrics
- Supply chain planning

Ensure all recommendations align with SAP demand planning processes and business objectives.
```

## User Message

```
Analyze the following demand data and provide forecast recommendations:

Input Data Sources:
1. Historical Demand: {demand_data}
   Example format:
   {
     "material_id": "1000123",
     "history": [
       {
         "period": "2023-12",
         "quantity": 1500,
         "promotions": true,
         "events": ["HOLIDAY_SEASON"]
       }
     ],
     "aggregation": {
       "avg_monthly_demand": 1200,
       "std_deviation": 150,
       "seasonality_index": [1.2, 0.8]
     }
   }

2. Market Indicators: {market_data}
   Example format:
   {
     "industry_growth": 0.05,
     "market_share": 0.15,
     "competitor_actions": [
       {
         "type": "NEW_PRODUCT",
         "impact": "MEDIUM",
         "timeline": "Q2_2024"
       }
     ]
   }

3. Business Plans: {business_data}
   Example format:
   {
     "growth_targets": 0.08,
     "planned_promotions": [
       {
         "period": "2024-06",
         "type": "PRICE_DISCOUNT",
         "expected_lift": 0.25
       }
     ]
   }

4. Supply Constraints: {supply_data}
   Example format:
   {
     "production_capacity": 2000,
     "supplier_constraints": {
       "lead_time": 14,
       "min_order_qty": 100,
       "capacity_limit": 1800
     }
   }

Expected Output Format:
{
  "demand_forecast": {
    "summary": {
      "material_id": string,
      "forecast_period": string,
      "confidence_level": number,
      "forecast_accuracy": number
    },
    "predictions": [
      {
        "period": string,
        "base_demand": number,
        "promotional_lift": number,
        "seasonal_factor": number,
        "final_forecast": number
      }
    ],
    "influencing_factors": {
      "market_trends": [
        {
          "factor": string,
          "impact": number,
          "confidence": number
        }
      ],
      "business_changes": [
        {
          "change": string,
          "expected_impact": number,
          "timeline": string
        }
      ]
    },
    "recommendations": {
      "safety_stock": {
        "level": number,
        "coverage_days": number,
        "rationale": string
      },
      "order_policies": {
        "reorder_point": number,
        "order_quantity": number,
        "review_frequency": string
      }
    }
  }
}
```

## Example Output

```
{
  "demand_forecast": {
    "summary": {
      "material_id": "1000123",
      "forecast_period": "2024-Q1",
      "confidence_level": 0.85,
      "forecast_accuracy": 0.92
    },
    "predictions": [
      {
        "period": "2024-01",
        "base_demand": 1200,
        "promotional_lift": 0,
        "seasonal_factor": 1.2,
        "final_forecast": 1440
      },
      {
        "period": "2024-02",
        "base_demand": 1200,
        "promotional_lift": 0,
        "seasonal_factor": 0.8,
        "final_forecast": 960
      }
    ],
    "influencing_factors": {
      "market_trends": [
        {
          "factor": "Industry Growth",
          "impact": 0.05,
          "confidence": 0.85
        }
      ],
      "business_changes": [
        {
          "change": "Planned Promotion",
          "expected_impact": 0.25,
          "timeline": "2024-06"
        }
      ]
    },
    "recommendations": {
      "safety_stock": {
        "level": 300,
        "coverage_days": 7,
        "rationale": "Based on demand variability and service level targets"
      },
      "order_policies": {
        "reorder_point": 500,
        "order_quantity": 1000,
        "review_frequency": "WEEKLY"
      }
    }
  }
}
```

## Implementation Examples

```
from langchain.prompts import ChatPromptTemplate
from langchain.output_parsers import JSONOutputParser

# Create prompt template for demand forecasting
prompt_template = ChatPromptTemplate.from_messages([
    ("system", """You are an AI assistant specialized in SAP demand forecasting..."""),
    ("user", """Analyze the following demand data and provide forecast recommendations:
    
    Input Data Sources:
    1. Historical Demand: {demand_data}
    2. Market Indicators: {market_data}
    3. Business Plans: {business_data}
    4. Supply Constraints: {supply_data}
    """)
])

# Create chain with JSON output parser
chain = prompt_template | JSONOutputParser()

# Example usage
response = chain.invoke({
    "demand_data": {...},
    "market_data": {...},
    "business_data": {...},
    "supply_data": {...}
})
```