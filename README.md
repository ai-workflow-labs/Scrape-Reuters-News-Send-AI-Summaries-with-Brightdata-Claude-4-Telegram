<img width="711" height="309" alt="image" src="https://github.com/user-attachments/assets/741af316-f89a-49d6-bc46-89034725e366" />

# 📰 Reuters News Intelligence Workflow

An **automated AI-powered news intelligence system** that monitors **Reuters** for breaking news, analyzes articles with **Claude AI**, and delivers personalized updates directly to **Telegram** — all in real time.  
Perfect for **journalists**, **researchers**, **traders**, and anyone who needs **instant, reliable news insights**. ⚡

---

## ✨ Key Features

| 🚀 Feature | 💡 Description |
|-------------|----------------|
| 🎯 **Form-Based Input** | Simple web form to specify keywords and news type preferences |
| 🤖 **AI-Powered Processing** | Uses *Claude 4 Sonnet* for intelligent content summarization and analysis |
| 🌐 **Professional Scraping** | Leverages *Bright Data’s Reuters dataset* for reliable extraction |
| 📱 **Telegram Integration** | Instant delivery of news alerts to your preferred Telegram chat |
| ⏰ **Smart Waiting** | Built-in delay logic ensures scraping completion |
| 🔄 **Status Monitoring** | Automatic progress checks and retries for data readiness |
| 📊 **Data Formatting** | Clean, structured output with essential article fields |
| 🧩 **Scalable Design** | Handles multiple article batches efficiently |

---

## 🎯 What This Workflow Does

### 🧠 Input
- **Keywords:** Search terms (e.g., `"Election"`, `"Gas shocks"`, `"Technology"`)
- **News Type:** Sorting preference — `newest`, `oldest`, or `relevance`
- **Form Submission:** Web form interface for easy user interaction

### ⚙️ Processing
1. **Form Trigger** – Captures input via a web form
2. **Claude AI Orchestration** – Manages the logic and flow
3. **Bright Data Request** – Initiates Reuters scraping
4. **Status Monitoring** – Checks scraping progress with smart retries
5. **Data Retrieval** – Fetches completed results
6. **Formatting** – Extracts titles, summaries, and URLs
7. **Telegram Delivery** – Sends formatted results instantly

### 📤 Output Data Points
| Field | Description | Example |
|--------|-------------|----------|
| `article_title` | Main headline | Global Energy Markets Face Uncertainty |
| `headline` | Reuters display title | Oil Prices Surge Amid Supply Concerns |
| `description` | Summary or meta description | Energy markets react to geopolitical tensions... |
| `content` | Full article body text | LONDON (Reuters) - Oil prices jumped 3%... |
| `article_url` | Direct Reuters link | https://reuters.com/business/energy/... |

---

## ⚡ Setup Instructions

### 🧩 Prerequisites
- 🧠 **n8n instance** (self-hosted or cloud)
- 🌐 **Bright Data** account (Reuters dataset access)
- 💬 **Telegram Bot** & chat/channel setup
- 🤖 **Claude API** access (Anthropic)
- ⏱️ ~15–20 minutes setup time

---

### 🔹 Step 1: Import the Workflow
1. Copy JSON workflow code from the provided file.  
2. In **n8n → Workflows → + Add Workflow → Import from JSON**  
3. Paste the content → **Import → Save**  
4. Name it `Reuters News Intelligence`

---

### 🔹 Step 2: Configure Bright Data
**Set Credentials**
### 🔹 Step 2: Configure Bright Data
**Set Credentials**
Type: HTTP Header Auth
Header: Authorization: Bearer YOUR_BRIGHT_DATA_API_KEY

markdown
Copy code

**Verify Dataset**
- Dataset ID: `gd_lyptx9h74wtlvpnfu`
- Confirm Reuters scraping permissions
- Check quota and limits in Bright Data dashboard

---

### 🔹 Step 3: Configure Anthropic Claude
1. In **n8n → Credentials → Anthropic API**
2. Enter your API key  
3. Verify model: `claude-sonnet-4-20250514`  
4. (Optional) Adjust `temperature` or parameters for custom output

---

### 🔹 Step 4: Configure Telegram
**Create Bot**
- Talk to [@BotFather](https://t.me/BotFather)
- Use `/newbot` → Save the token

**Find Chat ID**
- Send a test message  
- Visit:  
  `https://api.telegram.org/bot<BOT_TOKEN>/getUpdates`

**Configure in n8n**
- Credentials → Telegram API  
- Enter bot token  
- Replace `DEMO_CHAT_ID` in Telegram node with your real chat ID  

💬 *Example Message Template:*
🗞️ {{ $json.heading }}

📖 {{ $json.description }}

🔗 [Read Full Article]({{ $json.article_url }})

📅 Retrieved: {{ $now.format('YYYY-MM-DD HH:mm') }}

yaml
Copy code

---

### 🔹 Step 5: Configure Web Form
- Open **Form Trigger Node**
- Copy webhook URL (your form endpoint)
- Customize title & input fields
- Test by submitting keywords like `"Technology"`

---

### 🔹 Step 6: Update Node Configurations
- Replace placeholders with real credentials  
- Verify dataset ID and API keys  
- Review JavaScript code in “Data Formatting” node for accuracy

---

### 🔹 Step 7: Test & Activate
✅ Submit test keywords (e.g., `"AI"`)  
✅ Confirm Bright Data snapshot creation  
✅ Check Telegram for message delivery  
✅ Toggle workflow to **Active**

---

## 📖 Usage Guide

### 📝 Submitting News Requests
1. Open the form (`webhook URL`)
2. Enter:
   - Keywords (e.g., “Elections”)
   - News Type: `newest` | `oldest` | `relevance`
3. Click **Submit**
4. Receive updates in Telegram within **1–3 minutes**

### 🧩 Sequence Overview
Form → Claude AI → Bright Data → Wait/Check → Format → Telegram

yaml
Copy code

---

## 🧰 Customization Options

### 🔍 Modify Search Parameters
```json
{
  "keyword": "Your search terms",
  "sort": "newest|oldest|relevance",
  "limit_per_input": "2-10"
}
💬 Customize Telegram Message
Edit the Telegram Node with markdown or emojis.

📧 Add Email Notifications
Add Email node → Configure SMTP

Create HTML email for article delivery

🧠 Enhance AI Processing
Add sentiment analysis

Extract market or impact metrics

Generate executive summaries or quotes

💾 Add Data Storage
Connect Postgres or MySQL node

Store articles for long-term analysis or dashboards
