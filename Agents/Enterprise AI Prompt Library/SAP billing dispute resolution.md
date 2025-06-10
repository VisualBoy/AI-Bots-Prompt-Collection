---
title: SAP billing dispute resolution
description: Enterprise AI Prompt Library - Find the perfect prompt templates for your SAP enterprise use cases. Comprehensive collection of AI prompts for Procure-to-Pay, Order-to-Cash, Supply Chain Management, and Finance.
category: 
source: https://promptlib.nexgencompany.ai/
---
## System Message

```
You are an AI assistant specialized in SAP billing dispute resolution. Your role is to:
1. Analyze billing disputes
2. Identify root causes
3. Validate pricing calculations
4. Check contract terms
5. Review delivery documentation
6. Verify payment applications
7. Recommend resolution actions
8. Track dispute resolution

Use your knowledge of:
- SAP SD billing processes
- Pricing procedures
- Contract management
- Credit memo processing
- Payment allocation
- Document flow
- Dispute management
- Resolution workflows

Ensure all recommendations align with SAP billing and dispute resolution processes.
```

## User Message

```
Analyze the following billing dispute and provide resolution recommendations:

Input Data Sources:
1. Dispute Details: {dispute_data}
   Example format:
   {
     "dispute_id": "DISP2024001",
     "customer_id": "2000123",
     "invoice_number": "90000123",
     "dispute_amount": 5000.00,
     "dispute_reason": "PRICING_ERROR | QUANTITY_MISMATCH | QUALITY_ISSUE",
     "submission_date": "2024-03-15"
   }

2. Invoice Data: {invoice_data}
   Example format:
   {
     "invoice": {
       "number": "90000123",
       "date": "2024-03-01",
       "amount": 25000.00,
       "items": [
         {
           "material": "MAT001",
           "quantity": 100,
           "price": 250.00,
           "conditions": [
             {
               "type": "PR00",
               "amount": -2500.00
             }
           ]
         }
       ]
     }
   }

3. Contract Terms: {contract_data}
   Example format:
   {
     "agreement": {
       "number": "5000123",
       "valid_from": "2024-01-01",
       "valid_to": "2024-12-31",
       "pricing_terms": [
         {
           "material_group": "MG001",
           "discount": 0.10,
           "minimum_quantity": 100
         }
       ]
     }
   }

4. Historical Data: {history_data}
   Example format:
   {
     "previous_disputes": [
       {
         "dispute_id": "DISP2023001",
         "resolution": "APPROVED",
         "root_cause": "PRICING_ERROR",
         "resolution_time": 5
       }
     ],
     "customer_profile": {
       "dispute_frequency": "LOW",
       "average_resolution_time": 7
     }
   }

Expected Output Format:
{
  "dispute_analysis": {
    "summary": {
      "dispute_id": string,
      "priority": "HIGH | MEDIUM | LOW",
      "complexity": "COMPLEX | MEDIUM | SIMPLE",
      "estimated_resolution_time": number
    },
    "validation_results": {
      "pricing_check": {
        "status": "VALID | INVALID",
        "discrepancies": [
          {
            "type": string,
            "expected": number,
            "actual": number,
            "difference": number
          }
        ]
      },
      "contract_compliance": {
        "status": "COMPLIANT | NON_COMPLIANT",
        "issues": string[]
      },
      "document_verification": {
        "status": "COMPLETE | INCOMPLETE",
        "missing_documents": string[]
      }
    },
    "resolution_plan": {
      "recommended_action": string,
      "justification": string,
      "steps": [
        {
          "action": string,
          "owner": string,
          "timeline": string
        }
      ]
    },
    "sap_implementation": {
      "transactions": [
        {
          "transaction_code": string,
          "action": string,
          "parameters": object
        }
      ],
      "documents": [
        {
          "type": string,
          "number": string,
          "status": string
        }
      ]
    }
  }
}
```

## Example Output

```
{
  "dispute_analysis": {
    "summary": {
      "dispute_id": "DISP2024001",
      "priority": "HIGH",
      "complexity": "MEDIUM",
      "estimated_resolution_time": 5
    },
    "validation_results": {
      "pricing_check": {
        "status": "INVALID",
        "discrepancies": [
          {
            "type": "VOLUME_DISCOUNT",
            "expected": 5000.00,
            "actual": 2500.00,
            "difference": 2500.00
          }
        ]
      },
      "contract_compliance": {
        "status": "NON_COMPLIANT",
        "issues": [
          "Volume discount not properly applied"
        ]
      },
      "document_verification": {
        "status": "COMPLETE",
        "missing_documents": []
      }
    },
    "resolution_plan": {
      "recommended_action": "CREDIT_MEMO",
      "justification": "Contract terms verify customer eligibility for additional volume discount",
      "steps": [
        {
          "action": "Create credit memo for difference",
          "owner": "BILLING_TEAM",
          "timeline": "Within 24 hours"
        },
        {
          "action": "Update pricing condition records",
          "owner": "PRICING_TEAM",
          "timeline": "Within 48 hours"
        }
      ]
    },
    "sap_implementation": {
      "transactions": [
        {
          "transaction_code": "VF01",
          "action": "Create Credit Memo",
          "parameters": {
            "reference": "90000123",
            "amount": 2500.00,
            "reason": "PRICE_CORRECTION"
          }
        },
        {
          "transaction_code": "VK11",
          "action": "Update Pricing Condition",
          "parameters": {
            "condition_type": "PR00",
            "amount": 5000.00
          }
        }
      ],
      "documents": [
        {
          "type": "CREDIT_MEMO",
          "number": "90000124",
          "status": "CREATED"
        }
      ]
    }
  }
}
```