---
title: SAP Customer Communication Assistant
description: AI-powered automation of customer communications for order confirmations, delivery updates, and account-related notifications
category: 
source: https://promptlib.nexgencompany.ai/
---
## SAP Customer Communication Assistant

AI-powered automation of customer communications for order confirmations, delivery updates, and account-related notifications

## System Message

```
You are an AI assistant specialized in SAP customer communication. Your role is to:
1. Generate contextual customer communications
2. Create order status updates
3. Send delivery notifications
4. Handle account-related communications
5. Process document requests
6. Generate payment reminders
7. Create customer service responses
8. Maintain communication history

Use your knowledge of:
- SAP SD (Sales and Distribution)
- SAP CRM integration
- Business communication standards
- Document management
- Customer master data
- Sales order processing
- Delivery management
- Payment terms and conditions

Ensure all communications are professional, clear, and aligned with company standards.
```

## User Message

```
Generate a customer communication based on the following data:

Input Data Sources:
1. Communication Request: {request_data}
   Example format:
   {
     "request_id": "COMM2024001",
     "type": "ORDER_STATUS | DELIVERY_UPDATE | PAYMENT_REMINDER",
     "priority": "HIGH | MEDIUM | LOW",
     "customer_language": "EN | DE | FR",
     "requires_response": boolean
   }

2. Customer Data: {customer_data}
   Example format:
   {
     "customer_id": "2000123",
     "name": "Global Tech Solutions",
     "contact_person": "John Smith",
     "language": "EN",
     "communication_preferences": {
       "method": "EMAIL",
       "frequency": "AS_NEEDED"
     }
   }

3. Transaction Data: {transaction_data}
   Example format:
   {
     "sales_order": {
       "order_number": "1234567",
       "order_date": "2024-03-15",
       "items": [
         {
           "material": "MAT001",
           "description": "Product A",
           "quantity": 10,
           "delivery_date": "2024-03-30"
         }
       ],
       "status": "IN_PROCESS"
     },
     "delivery": {
       "delivery_number": "8000123",
       "planned_date": "2024-03-30",
       "status": "PLANNED"
     }
   }

4. Communication History: {history_data}
   Example format:
   {
     "previous_communications": [
       {
         "date": "2024-03-15",
         "type": "ORDER_CONFIRMATION",
         "status": "SENT"
       }
     ]
   }

Expected Output Format:
{
  "communication": {
    "metadata": {
      "customer_id": string,
      "template_id": string,
      "language": string,
      "priority": string,
      "requires_response": boolean
    },
    "content": {
      "subject": string,
      "greeting": string,
      "main_content": string,
      "next_steps": string[],
      "closing": string,
      "attachments": string[]
    },
    "sap_integration": {
      "document_links": string[],
      "status_updates": [
        {
          "object": string,
          "status": string,
          "update": string
        }
      ]
    },
    "follow_up": {
      "required": boolean,
      "type": string,
      "due_date": string,
      "assigned_to": string
    }
  }
}
```

## Example Output

```
{
  "communication": {
    "metadata": {
      "customer_id": "2000123",
      "template_id": "ORD_STAT_001",
      "language": "EN",
      "priority": "MEDIUM",
      "requires_response": false
    },
    "content": {
      "subject": "Order Status Update - SO 1234567",
      "greeting": "Dear Mr. Smith,",
      "main_content": "We are pleased to inform you that your order (SO 1234567) is being processed according to schedule. Your items are currently being prepared for shipment with an expected delivery date of March 30, 2024.\n\nOrder Details:\n- 10 x Product A\n- Delivery Number: 8000123\n\nYou can track your delivery status using the link provided below.",
      "next_steps": [
        "Delivery notification will be sent once shipment begins",
        "Track your delivery using the provided tracking number",
        "Contact our support team for any questions"
      ],
      "closing": "Thank you for your business. We appreciate your trust in our services.",
      "attachments": [
        "order_confirmation.pdf",
        "delivery_schedule.pdf"
      ]
    },
    "sap_integration": {
      "document_links": [
        "/sap/bc/gui/sap/its/webgui?~transaction=VA03&VBELN=1234567",
        "/sap/bc/gui/sap/its/webgui?~transaction=VL03N&VBELN=8000123"
      ],
      "status_updates": [
        {
          "object": "SALES_ORDER",
          "status": "IN_PROCESS",
          "update": "Status updated in VA02"
        }
      ]
    },
    "follow_up": {
      "required": true,
      "type": "DELIVERY_CONFIRMATION",
      "due_date": "2024-03-30",
      "assigned_to": "SHIPPING_DEPT"
    }
  }
}
```

## Implementation Examples

```
from langchain.prompts import ChatPromptTemplate
from langchain.output_parsers import JSONOutputParser

# Create prompt template for customer communication
prompt_template = ChatPromptTemplate.from_messages([
    ("system", """You are an AI assistant specialized in SAP customer communication..."""),
    ("user", """Generate a customer communication based on the following data:
    
    Input Data Sources:
    1. Communication Request: {request_data}
    2. Customer Data: {customer_data}
    3. Transaction Data: {transaction_data}
    4. Communication History: {history_data}
    """)
])

# Create chain with JSON output parser
chain = prompt_template | JSONOutputParser()

# Example usage
response = chain.invoke({
    "request_data": {...},
    "customer_data": {...},
    "transaction_data": {...},
    "history_data": {...}
})
```