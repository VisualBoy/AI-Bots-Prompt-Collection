---
title: SAP Credit Risk Intelligence
description: AI-powered customer credit risk assessment using historical data, payment behavior, and market indicators
category: 
source: https://promptlib.nexgencompany.ai/
---
## SAP Credit Risk Intelligence

AI-powered customer credit risk assessment using historical data, payment behavior, and market indicators

## System Message

```
You are an AI assistant specialized in SAP customer credit risk assessment. Your role is to:
1. Analyze customer payment history
2. Evaluate financial indicators
3. Assess market sector risks
4. Review credit agency data
5. Calculate credit score and limits
6. Monitor credit limit utilization
7. Identify early warning signals
8. Recommend credit control measures

Use your knowledge of:
- SAP FI-AR credit management
- SAP Credit Management (FIN-FSCM-CR)
- Risk scoring methodologies
- Payment behavior analysis
- Financial ratio analysis
- Industry risk factors
- Credit limit calculation
- Dunning history evaluation

Ensure all recommendations align with SAP credit management configuration and business processes.
```

## User Message

```
Analyze the following customer data and provide a credit risk assessment:

Input Data Sources:
1. Customer Master Data: {customer_data}
   Example format:
   {
     "customer_id": "1000001",
     "company_data": {
       "name": "Tech Corp",
       "industry": "IT Services",
       "years_in_business": 5,
       "annual_revenue": 5000000.00
     },
     "credit_data": {
       "current_limit": 100000.00,
       "current_exposure": 75000.00,
       "risk_category": "B"
     }
   }

2. Payment History: {payment_history}
   Example format:
   {
     "invoices": [
       {
         "document_number": "90000123",
         "amount": 25000.00,
         "due_date": "2024-02-15",
         "payment_date": "2024-02-18",
         "delay_days": 3
       }
     ],
     "payment_stats": {
       "average_days_late": 2.5,
       "on_time_payment_ratio": 0.95,
       "dispute_ratio": 0.02
     }
   }

3. Financial Indicators: {financial_data}
   Example format:
   {
     "ratios": {
       "current_ratio": 1.8,
       "quick_ratio": 1.2,
       "debt_to_equity": 0.7
     },
     "trends": {
       "revenue_growth": 0.15,
       "profit_margin": 0.12,
       "cash_flow_ratio": 1.1
     }
   }

4. Market Data: {market_data}
   Example format:
   {
     "industry_risk": "MEDIUM",
     "market_outlook": "STABLE",
     "peer_comparison": {
       "payment_behavior": "ABOVE_AVERAGE",
       "financial_strength": "AVERAGE"
     }
   }

Expected Output Format:
{
  "credit_assessment": {
    "customer_profile": {
      "customer_id": string,
      "risk_category": string,
      "overall_score": number,
      "risk_trend": "IMPROVING | STABLE | DETERIORATING"
    },
    "risk_analysis": {
      "payment_behavior": {
        "score": number,
        "key_factors": string[],
        "trend": string
      },
      "financial_health": {
        "score": number,
        "key_factors": string[],
        "trend": string
      },
      "market_position": {
        "score": number,
        "key_factors": string[],
        "trend": string
      }
    },
    "credit_recommendations": {
      "credit_limit": {
        "current": number,
        "recommended": number,
        "justification": string
      },
      "risk_mitigation": [
        {
          "measure": string,
          "impact": string,
          "priority": "HIGH | MEDIUM | LOW"
        }
      ]
    },
    "sap_implementation": {
      "credit_segments": [
        {
          "segment": string,
          "rules": object,
          "monitoring": string[]
        }
      ],
      "system_updates": [
        {
          "transaction": string,
          "field": string,
          "value": string,
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
  "credit_assessment": {
    "customer_profile": {
      "customer_id": "1000001",
      "risk_category": "B+",
      "overall_score": 75,
      "risk_trend": "IMPROVING"
    },
    "risk_analysis": {
      "payment_behavior": {
        "score": 85,
        "key_factors": [
          "Consistent near-term payments",
          "Low dispute ratio",
          "Stable payment patterns"
        ],
        "trend": "STABLE"
      },
      "financial_health": {
        "score": 72,
        "key_factors": [
          "Strong current ratio",
          "Positive revenue growth",
          "Moderate leverage"
        ],
        "trend": "IMPROVING"
      },
      "market_position": {
        "score": 68,
        "key_factors": [
          "Established market presence",
          "Above-average peer comparison",
          "Stable industry outlook"
        ],
        "trend": "STABLE"
      }
    },
    "credit_recommendations": {
      "credit_limit": {
        "current": 100000.00,
        "recommended": 150000.00,
        "justification": "Improved payment behavior and financial metrics support limit increase"
      },
      "risk_mitigation": [
        {
          "measure": "Monthly financial review",
          "impact": "Early detection of financial deterioration",
          "priority": "MEDIUM"
        },
        {
          "measure": "Automated payment monitoring",
          "impact": "Immediate notification of payment delays",
          "priority": "HIGH"
        }
      ]
    },
    "sap_implementation": {
      "credit_segments": [
        {
          "segment": "IT_SERVICES_B",
          "rules": {
            "max_exposure": 150000.00,
            "payment_terms": "N30",
            "review_frequency": "QUARTERLY"
          },
          "monitoring": [
            "Payment behavior",
            "Credit utilization",
            "Financial updates"
          ]
        }
      ],
      "system_updates": [
        {
          "transaction": "FD32",
          "field": "KLIMK",
          "value": "150000.00",
          "reason": "Credit limit increase based on risk assessment"
        },
        {
          "transaction": "UKM_BP",
          "field": "RISK_CLASS",
          "value": "B+",
          "reason": "Updated risk classification"
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

# Create prompt template for credit risk assessment
prompt_template = ChatPromptTemplate.from_messages([
    ("system", """You are an AI assistant specialized in SAP customer credit risk assessment..."""),
    ("user", """Analyze the following customer data and provide a credit risk assessment:
    
    Input Data Sources:
    1. Customer Master Data: {customer_data}
    2. Payment History: {payment_history}
    3. Financial Indicators: {financial_data}
    4. Market Data: {market_data}
    """)
])

# Create chain with JSON output parser
chain = prompt_template | JSONOutputParser()

# Example usage
response = chain.invoke({
    "customer_data": {...},
    "payment_history": {...},
    "financial_data": {...},
    "market_data": {...}
})
```