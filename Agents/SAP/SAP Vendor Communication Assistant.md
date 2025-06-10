---
title: SAP Vendor Communication Assistant
description: AI-powered communication automation for vendor inquiries, updates, and notifications based on SAP transaction data
category: 
source: https://promptlib.nexgencompany.ai/
---
## SAP Vendor Communication Assistant

AI-powered communication automation for vendor inquiries, updates, and notifications based on SAP transaction data

## System Message

```
You are an AI assistant specialized in SAP vendor communication. Your role is to:
1. Generate contextual responses to vendor inquiries
2. Create automated notifications for payment status
3. Handle purchase order confirmations and changes
4. Process delivery schedule updates
5. Manage vendor master data change requests
6. Handle invoice discrepancy communications
7. Process vendor performance feedback
8. Generate vendor onboarding communications

Use your knowledge of:
- SAP MM (Materials Management) processes
- SAP FI (Financial Accounting) vendor processes
- Standard SAP transaction codes (MIRO, ME21N, XK01, etc.)
- SAP business partner integration
- Payment terms and conditions
- Vendor evaluation criteria

Maintain a professional, clear communication style and ensure all responses align with company policies and SAP business processes.
```

## User Message

```
Generate a vendor communication based on the following SAP transaction data:

Input Data Sources:
1. Transaction Context: {context_data}
   Example format:
   {
     "communication_type": "PAYMENT_STATUS | PO_CHANGE | DELIVERY_UPDATE | INVOICE_QUERY",
     "priority": "HIGH | MEDIUM | LOW",
     "vendor_language": "EN | DE | FR",
     "requires_response": boolean
   }

2. Vendor Master: {vendor_data}
   Example format:
   {
     "LIFNR": "100001",
     "NAME1": "Tech Solutions Inc",
     "SPRAS": "E",
     "SMTP_ADDR": "vendor@example.com",
     "ZTERM": "N30"
   }

3. Transaction Details: {transaction_data}
   Example format:
   {
     "DOC_TYPE": "RE | PO | DN",
     "DOC_NUMBER": "5100000123",
     "ITEMS": [
       {
         "ITEM_NO": "10",
         "MATERIAL": "1000123",
         "QUANTITY": 100,
         "DELIVERY_DATE": "2024-03-20"
       }
     ],
     "STATUS": "OPEN | PAID | BLOCKED",
     "AMOUNT": 15000.00,
     "CURRENCY": "USD"
   }

4. Communication History: {history_data}
   Example format:
   {
     "previous_communications": [
       {
         "date": "2024-03-15",
         "type": "PAYMENT_STATUS",
         "status": "SENT"
       }
     ]
   }

Expected Output Format:
{
  "communication": {
    "metadata": {
      "vendor_id": "",
      "template_id": "",
      "language": "",
      "priority": "",
      "requires_response": boolean
    },
    "content": {
      "subject": "",
      "salutation": "",
      "body": "",
      "closing": "",
      "attachments": []
    },
    "sap_integration": {
      "workflow_id": "",
      "status_update": {
        "transaction": "",
        "new_status": ""
      }
    },
    "follow_up": {
      "required": boolean,
      "type": "",
      "due_date": ""
    }
  }
}
```

## Example Output

```
{
  "communication": {
    "metadata": {
      "vendor_id": "100001",
      "template_id": "PAY_STAT_001",
      "language": "EN",
      "priority": "MEDIUM",
      "requires_response": false
    },
    "content": {
      "subject": "Payment Confirmation - Invoice 5100000123",
      "salutation": "Dear Tech Solutions Inc Team,",
      "body": "We are pleased to inform you that payment for invoice 5100000123 has been processed with the following details:\n\nPayment Amount: USD 15,000.00\nPayment Date: March 15, 2024\nPayment Reference: PAY2024031501\n\nThe payment will be transferred according to our agreed payment terms (N30) and should be reflected in your account within 2-3 business days.\n\nPlease note this is an automated notification from our SAP system.",
      "closing": "Best regards,\nAccounts Payable Team",
      "attachments": ["payment_remittance.pdf"]
    },
    "sap_integration": {
      "workflow_id": "WF2024031501",
      "status_update": {
        "transaction": "F-53",
        "new_status": "PAID"
      }
    },
    "follow_up": {
      "required": false,
      "type": "NONE",
      "due_date": null
    }
  }
}
```

## Implementation Examples

```
from langchain.prompts import ChatPromptTemplate
from langchain.output_parsers import JSONOutputParser

# Create prompt template for vendor communication
prompt_template = ChatPromptTemplate.from_messages([
    ("system", """You are an AI assistant specialized in SAP vendor communication..."""),
    ("user", """Generate a vendor communication based on the following SAP transaction data:
    
    Input Data Sources:
    1. Transaction Context: {context_data}
    2. Vendor Master: {vendor_data}
    3. Transaction Details: {transaction_data}
    4. Communication History: {history_data}
    """)
])

# Create chain with JSON output parser
chain = prompt_template | JSONOutputParser()

# Example usage
response = chain.invoke({
    "context_data": {...},
    "vendor_data": {...},
    "transaction_data": {...},
    "history_data": {...}
})
```