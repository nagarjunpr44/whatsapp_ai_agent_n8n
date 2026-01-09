<img width="1469" height="792" alt="Screenshot 2026-01-08 at 20 07 27" src="https://github.com/user-attachments/assets/5382624b-ce39-414b-ba46-45af68586592" />

# WhatsApp AI Customer Support Agent - N8N Workflow

This repository contains an N8N workflow for building an intelligent WhatsApp customer support agent powered by AI and Airtable as the database.

## 🎯 Workflow Overview

This automation creates a complete customer support system using:
- **WhatsApp Business API** - Customer communication channel
- **OpenAI/LLM** - AI-powered response generation
- **Airtable** - Database for storing conversations, customer data, and ticket history
- **N8N** - Workflow automation platform

## 📊 Workflow Architecture

```
WhatsApp Message → Webhook Trigger → Airtable Lookup → AI Processing → Airtable Update → WhatsApp Response
```

## 🔧 Workflow Steps

### 1. **Webhook Trigger**
- Receives incoming WhatsApp messages via webhook
- Extracts message content, sender phone number, and metadata

### 2. **Airtable Customer Lookup**
- Checks if customer exists in Airtable database
- Retrieves conversation history and customer details
- Tables used:
  - `Customers` - Customer profiles and contact info
  - `Conversations` - Message history and context
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

## 📋 Airtable Database Structure

### Customers Table
| Field | Type | Description |
|-------|------|-------------|
| Customer ID | Auto Number | Unique identifier |
| Phone Number | Phone | WhatsApp number |
| Name | Single Line Text | Customer name |
| Email | Email | Contact email |
| First Contact | Date | First interaction date |
| Last Contact | Date | Most recent interaction |
| Total Messages | Number | Message count |
| Status | Single Select | Active/Inactive |

### Conversations Table
| Field | Type | Description |
|-------|------|-------------|
| Message ID | Auto Number | Unique message ID |
| Customer | Link to Customers | Customer reference |
| Timestamp | Date/Time | Message timestamp |
| Message | Long Text | Customer message |
| Response | Long Text | Agent/AI response |
| Intent | Single Select | Message intent |
| Sentiment | Single Select | Positive/Neutral/Negative |
| Handled By | Single Select | AI/Human |

### Tickets Table
| Field | Type | Description |
|-------|------|-------------|
| Ticket ID | Auto Number | Unique ticket ID |
| Customer | Link to Customers | Customer reference |
| Status | Single Select | Open/In Progress/Resolved |
| Priority | Single Select | Low/Medium/High/Urgent |
| Category | Single Select | Issue category |
| Created | Date/Time | Ticket creation time |
| Resolved | Date/Time | Resolution time |
| Description | Long Text | Issue description |
| Resolution | Long Text | Solution provided |

## 🚀 Key Features

- ✅ **24/7 Automated Support** - AI handles queries round the clock
- ✅ **Context-Aware Responses** - Remembers conversation history from Airtable
- ✅ **Smart Escalation** - Routes complex issues to human agents
- ✅ **Multi-Language Support** - Can respond in customer's language
- ✅ **Sentiment Analysis** - Detects frustrated customers and prioritizes
- ✅ **Ticket Management** - Automatic support ticket creation in Airtable
- ✅ **Analytics Ready** - All data stored in Airtable for reporting

## 🛠️ Setup Instructions

### Prerequisites
1. N8N instance (cloud or self-hosted)
2. WhatsApp Business API account
3. OpenAI API key or other LLM provider
4. Airtable account with API access

### Installation Steps

1. **Clone this repository**
   ```bash
   git clone https://github.com/nagarjunpr44/whatsapp_ai_agent_n8n.git
   ```

2. **Import workflow to N8N**
   - Open N8N dashboard
   - Go to Workflows → Import
   - Upload the workflow JSON file

3. **Set up Airtable**
   - Create a new base or use existing one
   - Create the three tables: Customers, Conversations, Tickets
   - Copy your Airtable API key and Base ID

4. **Configure credentials in N8N**
   - Add WhatsApp Business API credentials
   - Add OpenAI API credentials
   - Add Airtable credentials (API key)

5. **Set environment variables**
   ```
   WHATSAPP_API_TOKEN=your_whatsapp_token
   WHATSAPP_PHONE_NUMBER_ID=your_phone_number_id
   OPENAI_API_KEY=your_openai_key
   AIRTABLE_API_KEY=your_airtable_key
   AIRTABLE_BASE_ID=your_base_id
   ```

6. **Configure webhook URL**
   - Copy the webhook URL from N8N
   - Set it in WhatsApp Business API settings

7. **Test the workflow**
   - Send a test message to your WhatsApp number
   - Verify data is being stored in Airtable
   - Check AI responses

## 🎨 Customization Options

### AI Prompt Engineering
Modify the AI prompt in the OpenAI node to:
- Match your brand voice
- Include specific product information
- Add custom business rules

### Airtable Automation
- Add Airtable automations to send email notifications
- Create views for filtering high-priority tickets
- Set up dashboard for support metrics

### Escalation Rules
Customize when to escalate to humans:
- Low AI confidence threshold
- Specific keywords detected
- Customer sentiment is negative
- Multiple unresolved messages

### Response Templates
Store common responses in Airtable:
- FAQs
- Product information
- Business hours
- Return policies

## 📈 Advanced Features

### Add-ons you can integrate:
- **Sentiment Analysis** - Detect customer emotions
- **Product Catalog Integration** - Show products from Airtable
- **Order Tracking** - Link to order management systems
- **Appointment Booking** - Schedule calls with agents
- **Multi-Agent Support** - Route to specialized departments
- **Analytics Dashboard** - Visualize Airtable data with charts

## 📊 Monitoring & Analytics

Use Airtable's built-in features:
- Create views to track open tickets
- Monitor response times
- Analyze customer sentiment trends
- Generate reports on common issues
- Track AI vs human handling rates

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📝 License

This project is open source and available under the MIT License.

## 🆘 Support

For issues and questions:
- Open an issue in this repository
- Check N8N community forums
- Review Airtable API documentation

## 🔗 Useful Links

- [N8N Documentation](https://docs.n8n.io)
- [WhatsApp Business API](https://developers.facebook.com/docs/whatsapp)
- [OpenAI API](https://platform.openai.com/docs)
- [Airtable API](https://airtable.com/developers/web/api/introduction)

---

Built with ❤️ using N8N, WhatsApp, OpenAI, and Airtable