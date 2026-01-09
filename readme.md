
# WhatsApp AI Customer Support Agent - N8N Workflow

Built an N8N workflow for an intelligent WhatsApp customer support agent powered by AI and Airtable as the database.

## 🎯 Workflow Overview

This automation creates a complete customer support system using:
- **Twillio** - Customer communication channel
- **Groq LLM** - AI-powered response generation
- **Airtable** - Database for storing conversations, customer data, and ticket history
- **N8N** - Workflow automation platform

## 📊 Workflow Architecture

<img width="1469" height="792" alt="Screenshot 2026-01-08 at 20 07 27" src="https://github.com/user-attachments/assets/5382624b-ce39-414b-ba46-45af68586592" />


## 🔧 Workflow Steps

### 1. **Webhook Trigger**
- Receives incoming WhatsApp messages(twillio) via webhook
- Extracts message content, sender phone number, and metadata

### 2. **Airtable Customer Lookup**
- Checks if customer exists in Airtable database
- Retrieves conversation history and customer details
- Tables used:
  - `Customers` - Customer profiles and contact info
  - `Inventory` - Message history and context
  - `Tickets` - Support ticket tracking

### 3. **Context Building**
- Compiles previous conversation history from Airtable
- Prepares context for AI model
- Includes customer preferences and past issues

### 4. **AI Processing (OpenAI/LLM)**
- Sends message with context to AI model
- AI analyzes the query and generates appropriate response
- Determines intent (info request, complaint, order status, etc.)

### 5. **Response Logic**
- Evaluates AI confidence score
- Routes to appropriate response path:
  - **High confidence**: Send AI-generated response
  - **Low confidence**: Escalate to human agent
  - **Specific intents**: Trigger specialized workflows

### 6. **Airtable Update**
- Logs the conversation in Conversations table
- Updates customer record with latest interaction
- Creates/updates support ticket if needed
- Stores sentiment and intent analysis

### 7. **WhatsApp Response**
- Sends formatted response back to customer
- Includes relevant images, documents, or quick reply buttons
- Confirms ticket creation if escalated


## 🚀 Key Features

- ✅ **24/7 Automated Support** - AI handles queries round the clock
- ✅ **Context-Aware Responses** - Remembers conversation history from Airtable
- ✅ **Smart Escalation** - Routes complex issues to human agents
- ✅ **Multi-Language Support** - Can respond in customer's language
- ✅ **Sentiment Analysis** - Detects frustrated customers and prioritizes
- ✅ **Ticket Management** - Automatic support ticket creation in Airtable
- ✅ **Analytics Ready** - All data stored in Airtable for reporting


- [Airtable API](https://airtable.com/developers/web/api/introduction)

---

Built with ❤️ using N8N, WhatsApp, OpenAI, and Airtable
