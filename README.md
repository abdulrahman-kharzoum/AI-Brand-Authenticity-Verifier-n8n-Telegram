# 🛡️ AI Brand Authenticity Verifier

<img width="813" height="525" alt="image" src="https://github.com/user-attachments/assets/08c56be9-9a1c-490f-9e4d-13f084b4b537" />

**An intelligent Telegram bot that helps users verify the authenticity of beauty and luxury products using advanced AI analysis, voice recognition, image recognition, and real-time web search.**

[![n8n](https://img.shields.io/badge/Built%20with-n8n-orange)](https://n8n.io)
[![Gemini](https://img.shields.io/badge/Powered%20by-Gemini%20Flash%202.5-blue)](https://deepmind.google/technologies/gemini/)
[![Supabase](https://img.shields.io/badge/Database-Supabase-green)](https://supabase.com)

---
## n8n Version used:
+ Version 1.119.1 stable Cloud
+ Released in 11/12/2025
## Telegram ID 
+ @ai_brand_wonder_beauties_bot

## 📋 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [How It Works](#-how-it-works)
- [Architecture](#-architecture)
- [Tools & Technologies](#-tools--technologies)
- [Setup Guide](#-setup-guide)
- [Usage](#-usage)
- [Database Schema](#-database-schema)
- [Conversation Flow](#-conversation-flow)
- [Example Scenarios](#-example-scenarios)
- [Troubleshooting](#-troubleshooting)
- [API & Integration](#-api--integration)

---

## 📚 Additional Documentation

- **[TOOL_USAGE_QUICK_REFERENCE.md](./TOOL_USAGE_QUICK_REFERENCE.md)** - Quick reference card for AI agent tool usage sequence and best practices

---

## 🎯 Overview

The **AI Brand Authenticity Verifier** is a sophisticated counterfeit detection system that helps consumers identify fake beauty and luxury products. Built on n8n workflow automation, it combines:

- **Voice-to-text transcription** using Google Gemini Flash 2.5
- **Forensic image analysis** using Google Gemini Vision
- **Real-time product research** via Google Search
- **Intelligent conversation management** with memory
- **Risk scoring algorithm** based on multiple factors
- **Persistent data logging** in Supabase PostgreSQL

### 🎭 Use Cases

- Verify products purchased from third-party sellers (eBay, Amazon, Instagram)
- Check authenticity before opening sealed products
- Get expert assessment on suspicious packaging
- Learn about common counterfeit patterns
- Find authorized retailers for authentic purchases

---

## ✨ Features

### Core Capabilities

| Feature                      | Description                                                                            |
| ---------------------------- | -------------------------------------------------------------------------------------- |
| 🎤 **Voice Input**           | Voice message transcription and natural language understanding via Gemini Flash 2.5    |
| 🖼️ **Image Analysis**        | Deep forensic examination of product photos (packaging, logos, batch codes, materials) |
| 🔍 **Product Research**      | Real-time Google search for MSRP, authorized retailers, and counterfeit patterns       |
| 💬 **Smart Conversations**   | Context-aware dialogue with memory to avoid repetitive questions                       |
| 📊 **Risk Scoring**          | 0-1 scale authenticity score based on price, seller, visuals, and research             |
| 💾 **Query Logging**         | Every assessment saved to database with full audit trail                               |
| 🎯 **Multi-Factor Analysis** | Price verification, seller authorization, packaging inspection, batch code validation  |
| 🌍 **Regional Intelligence** | Understands packaging variations across US, EU, Asia markets                           |
| 🛡️ **Safety Warnings**       | Alerts users about health risks of counterfeit cosmetics                               |

### Supported Product Categories

- Skincare (serums, moisturizers, treatments)
- Fragrances (perfumes, colognes, eau de toilette)
- Makeup (foundations, lipsticks, eyeshadows)
- Luxury beauty (premium brands: Dior, Chanel, La Mer, Tom Ford, etc.)
- Haircare (high-end treatments and styling products)

---

## 🔧 How It Works

### Step-by-Step Process

```
┌─────────────────────────────────────────────────────────────┐
│ 1. USER INTERACTION                                         │
│    User sends text, voice, or photo via Telegram            │
└──────────────────┬──────────────────────────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────────────────────────┐
│ 2. INPUT PROCESSING                                         │
│    • Voice → Transcription (Gemini Flash 2.5)               │
│    • Image → Vision Analysis (Gemini Flash 2.5)             │
│    • Text → Direct processing                               │
└──────────────────┬──────────────────────────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────────────────────────┐
│ 3. IMAGE ANALYSIS (if applicable)                           │
│    • Forensic packaging inspection                          │
│    • Logo/typography verification                           │
│    • Material quality assessment                            │
│    • Batch code format check                                │
│    • Returns 0-10 quality score + findings                  │
└──────────────────┬──────────────────────────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────────────────────────┐
│ 4. DATA COLLECTION (AI Agent + Memory)                     │
│    • Extract brand/product from image/voice/text            │
│    • Ask for: price, purchase location                      │
│    • Use memory to track what's already known               │
└──────────────────┬──────────────────────────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────────────────────────┐
│ 5. PRODUCT RESEARCH (Google Search Tool)                   │
│    Triggered when needed:                                   │
│    • Search official MSRP                                   │
│    • Verify seller authorization                            │
│    • Find counterfeit indicators                            │
│    • Check product variant existence                        │
└──────────────────┬──────────────────────────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────────────────────────┐
│ 6. RISK ANALYSIS (Think Tool)                              │
│    Calculate risk score (0-1) based on:                     │
│    • Price vs MSRP (40%+ discount = red flag)              │
│    • Seller authorization status                            │
│    • Image quality score                                    │
│    • Packaging authenticity                                 │
│    • Known counterfeit patterns                             │
└──────────────────┬──────────────────────────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────────────────────────┐
│ 7. DATABASE LOGGING (Supabase)                             │
│    Save complete record:                                    │
│    • Query ID, username, chat ID                            │
│    • Product details, price, seller                         │
│    • Image link, search queries                             │
│    • Risk score, verdict, reasoning                         │
└──────────────────┬──────────────────────────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────────────────────────┐
│ 8. DELIVER VERDICT                                          │
│    User receives:                                           │
│    • Clear verdict (Genuine ✅ / Counterfeit ❌ / Unclear ⚠️)│
│    • Risk score with explanation                            │
│    • Specific reasons for assessment                        │
│    • Actionable recommendations                             │
│    • Authorized retailer suggestions                        │
└─────────────────────────────────────────────────────────────┘
```

---

## 🏗️ Architecture

### System Components

```
┌───────────────────────────────────────────────────────────────┐
│                    TELEGRAM BOT INTERFACE                     │
│              (User sends photos + text messages)              │
└────────────────────────┬──────────────────────────────────────┘
                         │
                         ▼
┌───────────────────────────────────────────────────────────────┐
│                    N8N WORKFLOW ENGINE                        │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │  Telegram Trigger → Message Router → Workflow Logic    │ │
│  └─────────────────────────────────────────────────────────┘ │
└────────────┬──────────────────┬──────────────────┬───────────┘
             │                  │                  │
             ▼                  ▼                  ▼
┌──────────────────┐  ┌──────────────────┐  ┌──────────────────┐
│  GEMINI FLASH 2.5│  │  AI AGENT NODE   │  │  GOOGLE SEARCH   │
│  ─────────────── │  │  ──────────────  │  │  ──────────────  │
│  • Vision API    │  │  • Conversation  │  │  • Product MSRP  │
│  • Image Analysis│  │  • Context Mgmt  │  │  • Seller Check  │
│  • OCR Text      │  │  • Think Tool    │  │  • Fake Patterns │
│  • Quality Score │  │  • Memory Access │  │  • Retail Lists  │
└──────────────────┘  └──────────────────┘  └──────────────────┘

```

---

## 🛠️ Tools & Technologies

### 1. **AI Model: Google Gemini Flash 2.5**

**Purpose:** Primary intelligence engine

**Capabilities:**

- **Voice Transcription:** Audio-to-text conversion with natural language understanding
- **Vision API:** Multi-modal image + text analysis
- **Conversational AI:** Context-aware dialogue management
- **Reasoning:** Complex decision-making and risk assessment
- **Fast inference:** Sub-second response times
- **Long context window:** Handles extended conversations

**Usage in workflow:**

- Voice transcription node (audio message processing)
- Image analysis node (forensic packaging inspection)
- AI Agent node (conversation orchestration)
- Tool integration (calls Search and Think tools)

---

### 2. **Image Analyzer Tool**

**Technology:** Gemini Vision API with custom forensic prompt

**What it detects:**

| Category           | Checkpoints                                                        |
| ------------------ | ------------------------------------------------------------------ |
| **Print Quality**  | Pixelation, blurred text, ink distribution, smudging               |
| **Typography**     | Font weight, kerning, family matching, alignment                   |
| **Logo Forensics** | Proportions, curves, trademark symbols, positioning                |
| **Color Accuracy** | Pantone standards, brand color matching, tone variations           |
| **Materials**      | Glass quality, plastic thickness, metallic finishes, texture       |
| **Micro-details**  | Batch codes, barcodes, seals, cellophane, cap mechanisms           |
| **Brand Elements** | Signature details (e.g., Chanel double-C overlap)                  |
| **Manipulation**   | Photoshop artifacts, stock photo indicators, inconsistent lighting |

**Output Format:**

```
Visual Quality Score: 8/10
✅ Authenticity Indicators: [list]
⚠️ Warning Signs: [list]
🚩 Critical Red Flags: [list]
Product Details Detected: [brand, batch codes, etc.]
Confidence Level: High/Medium/Low
```

---

### 3. **Search Tool (Google Search Integration)**

**Purpose:** Real-time product intelligence gathering

**When it's triggered:**

- Price seems suspicious (>30% discount)
- Unfamiliar product variant
- Unknown seller/platform
- Need MSRP verification
- Batch code format unclear

**Search query types:**

```javascript
// MSRP Verification
"[Brand] [Product] official price 2024";
"[Product] MSRP";

// Authentication Guides
"authentic [Brand] [Product] vs fake";
"how to spot fake [Brand] [Product]";

// Seller Verification
"[Brand] authorized retailers";
"[Seller] [Brand] authorized";

// Packaging Intelligence
"[Brand] [Product] packaging 2024";
"[Brand] batch code format";
```

**Data extraction:**

- Official retail prices from 3+ sources
- Authorized retailer lists
- Known counterfeit indicators
- Packaging variation info (regional, limited edition)

---

### 4. **Think Tool (Risk Assessment Engine)**

**Purpose:** Calculate authenticity risk score

**Input parameters:**

```json
{
  "brand": "string",
  "product": "string",
  "price": number,
  "seller": "string",
  "imageAnalysis": "findings from vision API",
  "searchFindings": "MSRP and retailer data"
}
```

**Risk calculation factors:**

| Factor                 | Weight | Red Flag Threshold   |
| ---------------------- | ------ | -------------------- |
| Price discount         | 30%    | >40% below MSRP      |
| Seller authorization   | 25%    | Not on official list |
| Image quality score    | 20%    | <6/10                |
| Packaging authenticity | 15%    | Mismatched elements  |
| Batch code format      | 10%    | Invalid format       |

**Output:**

```json
{
  "riskScore": 0.78, // 0 = authentic, 1 = fake
  "verdict": "Likely Counterfeit",
  "reasoning": [
    "Price 50% below MSRP",
    "Unauthorized seller",
    "Batch code irregular"
  ]
}
```

---

### 5. **Memory System: Window Buffer Memory**

**Technology:** n8n Window Buffer Memory (Supabase-backed)

**Purpose:** Maintain conversation context

**What it stores:**

- Previous messages (last 10-20 exchanges)
- Already collected data (price, seller, product name)
- User preferences
- Conversation state

**Benefits:**

- ✅ Prevents asking same question twice
- ✅ Natural conversation flow
- ✅ References previous details ("Based on the photo you sent earlier...")
- ✅ Efficient data collection

**Configuration:**

```javascript
Memory Type: Window Buffer
Max Messages: 20
Session ID: {{ $json.message.from.id }} // Telegram Chat ID
Backend: Supabase PostgreSQL
```

---

### 6. **Database: Supabase PostgreSQL**

**Purpose:** Persistent storage and analytics

### 7. **Telegram Bot API**

**Integration:** n8n Telegram Trigger + Message nodes

**Supported inputs:**

- Text messages
- Voice messages (transcribed via Gemini Flash 2.5)
- Photo uploads (up to 10MB)
- Document attachments
- Command triggers

**Message parsing:**

```javascript
// User data
{
  {
    $json.message.from.first_name;
  }
}
{
  {
    $json.message.from.id;
  }
}
{
  {
    $json.message.from.username;
  }
}

// Content
{
  {
    $json.message.text;
  }
}
{
  {
    $json.message.voice.file_id;
  }
}
{
  {
    $json.message.photo[0].file_id;
  }
}
```

---

## 📦 Setup Guide

### Prerequisites

- **n8n instance** (self-hosted or cloud)
- **Telegram Bot Token** ([Get from @BotFather](https://t.me/botfather))
- **Google AI API Key** (Gemini Flash 2.5) ([Get here](https://aistudio.google.com/app/apikey))
- **Supabase Account** ([Free tier available](https://supabase.com))
- **Google Custom Search API** (optional, for search tool)

---

### Step 1: Create Telegram Bot

1. Open Telegram and search for **@BotFather**
2. Send `/newbot` command
3. Follow prompts to name your bot
4. **Save the bot token** (looks like `123456789:ABCdefGhIJKlmNoPQRsTUVwxyZ`)
5. Send `/setprivacy` and disable privacy mode (allows bot to see messages)

---

### Step 2: Set Up Google Sheet Database
AI Brand  Authenticity Verifier File
query_id
	Telegram Username
  	chatID
    	product name
      	brand name
         	price that customer paid
          	seller_info
             	image_link
              	imageQualityScore
                	risk_score
                  	verdict
                    	reasons
                      	sellerAuthorized
                        	searchQueries
                          	searchPerformed
                            	officialMSRP
                              	timestamp									
AI Brand  Authenticity Verifier Images db :
query_id
	image_link																								

4. Go to **Settings → API** and copy:
   - Project URL
   - `anon/public` API key

---

### Step 3: Get Google AI API Key

1. Visit [Google AI Studio](https://aistudio.google.com/app/apikey)
2. Click **"Get API Key"**
3. Create new key or use existing project
4. **Save the API key** (starts with `AIza...`)

---

### Step 4: Configure Google Search API (Optional)

1. Go to [Google Custom Search](https://programmablesearchengine.google.com/)
2. Create new search engine
3. Enable "Search the entire web"
4. Get **Search Engine ID** (CX)
5. Enable **Custom Search API** in [Google Cloud Console](https://console.cloud.google.com/apis/library/customsearch.googleapis.com)
6. Create **API credentials** (same or different from AI key)

---

### Step 5: Import Workflow to n8n

1. Download the `AI_Brand_Authenticity_Verifier.json` workflow
2. Open n8n
3. Go to **Workflows → Import from File**
4. Upload the JSON file
5. Configure credentials:

#### Telegram Credentials

- **Name:** `Telegram Bot`
- **Access Token:** [Your bot token from Step 1]

#### Google AI Credentials

- **Name:** `Google Gemini`
- **API Key:** [Your Gemini API key from Step 3]

#### Supabase Credentials

- **Name:** `Supabase`
- **Host:** [Your Supabase project URL]
- **Database:** `postgres`
- **User:** `postgres`
- **Password:** [From Supabase settings]
- **API Key:** [Your anon key]

#### Google Custom Search Credentials (if using)

- **API Key:** [Your search API key]
- **CX:** [Your search engine ID]

---

### Step 6: Configure Workflow Variables

Open the workflow and update these node configurations:

**1. Telegram Trigger Node:**

- Set webhook URL (auto-generated by n8n)
- Test connection

**2. AI Agent Node:**

- Model: `gemini-2.5-flash` 
- Temperature: `0.8` (for consistent analysis)
- Top K: `40.0`
- Top P: `0.95`
- System prompt: [Use the optimized prompt ]

**3. Image Analyzer Node:**

- Model: `gemini-2.5-pro` (best supports vision)
- Input: Image URL from Telegram
- Prompt: [Use forensic image analysis prompt]

**4. Memory Node:**
Postgres Chat Memory
Stores the chat history in Postgres table.
- Type: `Postgres Chat Memory`
- Max messages: `10`
- key: `{{ $('Telegram Trigger').item.json.message.from.id }}`
- Supabase connection configured


### Step 7: Test the Workflow

1. **Activate** the workflow in n8n
2. Open Telegram and find your bot
3. Send `/start` command
4. Upload a product photo
5. Answer the bot's questions
6. Verify:
   - ✅ Image analyzed
   - ✅ Conversation flows naturally
   - ✅ Search triggered (check logs)
   - ✅ Verdict delivered
   - ✅ Data saved to Supabase

---

## 📱 Usage

### For End Users

#### **Starting a Verification**

1. **Find your bot on Telegram**

   - Search for `@YourBotName`
   - Send `/start`

2. **Provide product information**

   You can interact in multiple ways:

   - **📸 Send photos:** Take clear, well-lit pictures of:

     - Front of product
     - Batch code / serial number
     - Box (if available)
     - Any labels or stickers

   - **🎤 Send voice messages:** Simply describe the product:

     - "I bought a Chanel perfume from eBay for $50"
     - "Can you check this Dior lipstick I got?"

   - **💬 Type messages:** Provide details via text

3. **Answer questions**

   - Where did you buy it?
   - How much did you pay?
   - Do you have a receipt?

4. **Receive assessment**
   - Risk score (0-1)
   - Clear verdict
   - Detailed reasoning
   - Recommendations

---

### Example User Journey

**Scenario 1: User sends photo (Traditional Flow)**

```
User: [Sends photo of Dior Sauvage bottle]

Bot: Thanks for the photo! 📸

I can see this is **Dior Sauvage Eau de Toilette**.

From my visual analysis (Score: 8/10):
✅ Logo appears correctly proportioned
✅ Glass quality looks premium
⚠️ Batch code format needs verification

To complete my assessment:
• Where did you purchase this?
• How much did you pay?

─────────────────────────

User: eBay for $55

─────────────────────────

Bot: 🔍 **AUTHENTICITY ASSESSMENT**

**Product:** Dior Sauvage Eau de Toilette (100ml)
**Purchased From:** eBay third-party seller
**Price Paid:** $55 (Official retail: $110)

───

**🎯 VERDICT: Likely Counterfeit ❌**
**📊 Risk Score:** 0.78/1.00 (high risk)

───

**🔬 Analysis:**

**Visual Inspection (Score: 8/10):**
✅ Overall presentation looks decent
⚠️ Batch code font appears slightly irregular
⚠️ Cap finish quality uncertain from image

**Key Risk Factors:**
• **Price:** $55 is 50% below official retail of $110 — major red flag
• **Seller:** eBay third-party sellers are not authorized Dior retailers
• **Batch code:** Format doesn't match Dior's standard system
• **Discount:** Authentic Dior rarely discounted beyond 25%

───

**💡 RECOMMENDATION:**
I strongly advise against using this product. Counterfeit fragrances can contain harmful chemicals.

**Next steps:**
• Request full refund through eBay buyer protection
• Report seller for counterfeit goods

**Where to buy authentic Dior Sauvage:**
• Dior official website
• Sephora
• Nordstrom, Macy's, Bloomingdale's

Your safety matters! 🛡️

───

**Reference ID:** `AQ-20250121154523-K8P2`

Want me to check another product? 🛍️
```

---

**Scenario 2: User sends voice message (Voice Flow)**

```
User: [Sends voice message] "Hi, I just bought a Dior Sauvage perfume from eBay for $55. Can you check if it's real?"

Bot: [Transcribes voice message]

Thanks for reaching out! 👋

I heard you loud and clear! You mentioned:
• **Product:** Dior Sauvage perfume
• **Seller:** eBay
• **Price:** $55

That price is catching my attention already 👀 - the official retail for Dior Sauvage is around $110.

To give you a complete authentication, I'll need:
📸 A clear photo of the bottle (especially the batch code area)

Once I can see it, I'll run my full forensic analysis and give you a detailed verdict! 🔍

─────────────────────────

User: [Sends photo]

Bot: Perfect! Now I have everything I need. 🕵️‍♀️

🔍 **AUTHENTICITY ASSESSMENT**

**Product:** Dior Sauvage Eau de Toilette (100ml)
**Purchased From:** eBay third-party seller
**Price Paid:** $55 (Official retail: $110)

───

**🎯 VERDICT: Likely Counterfeit ❌**
**📊 Risk Score:** 0.78/1.00 (high risk)

───

**🔬 Analysis:**

**Visual Inspection (Score: 8/10):**
✅ Overall presentation looks decent
⚠️ Batch code font appears slightly irregular
⚠️ Cap finish quality uncertain from image

**Key Risk Factors:**
• **Price:** $55 is 50% below official retail of $110 — major red flag
• **Seller:** eBay third-party sellers are not authorized Dior retailers
• **Batch code:** Format doesn't match Dior's standard system
• **Discount:** Authentic Dior rarely discounted beyond 25%

───

**💡 RECOMMENDATION:**
I strongly advise against using this product. Counterfeit fragrances can contain harmful chemicals.

**Next steps:**
• Request full refund through eBay buyer protection
• Report seller for counterfeit goods

**Where to buy authentic Dior Sauvage:**
• Dior official website
• Sephora
• Nordstrom, Macy's, Bloomingdale's

Your safety matters! 🛡️

───

**Reference ID:** `AQ-20250113162315-V8X2`

Feel free to send another voice message or text if you have more questions! 🎤💬
```

---

## 📊 Database Schema

### Complete Table Structure

```sql
-- Memory for conversation context
create table public.n8n_chat_histories_aibrandauthenticity (
  id serial not null,
  session_id character varying(255) not null,
  message jsonb not null,
  constraint n8n_chat_histories_aibrandauthenticity_pkey primary key (id)
) TABLESPACE pg_default;

```

## 🔄 Conversation Flow

### State Machine

```
┌─────────────┐
│   START     │ User sends message/photo
└──────┬──────┘
       │
       ▼
┌─────────────────────┐
│ INTAKE              │ Extract available info from message/image
│ ─────────────       │ Check memory for existing data
│ • Parse image       │
│ • Extract text      │
│ • Check memory      │
└──────┬──────────────┘
       │
       ▼
┌─────────────────────┐
│ DATA COLLECTION     │ Ask for missing information
│ ─────────────       │ Max 3 questions per turn
│ Missing product? →  │
│ Missing price? →    │
│ Missing seller? →   │
│ Missing photo? →    │
└──────┬──────────────┘
       │
       │ [All critical data collected]
       ▼
┌─────────────────────┐
│ RESEARCH            │ Trigger if needed
│ ─────────────       │ • Price suspicious
│ • Search MSRP       │ • Unknown seller
│ • Check seller      │ • Unfamiliar product
│ • Find patterns     │
└──────┬──────────────┘
       │
       ▼
┌─────────────────────┐
│ ANALYSIS            │ Calculate risk score
│ ─────────────       │ Generate verdict
│ • Think Tool        │ Compile reasoning
│ • Risk scoring      │
│ • Reasoning         │
└──────┬──────────────┘
       │
       ▼
┌─────────────────────┐
│ LOGGING             │ Save to Supabase
│ ─────────────       │ Before responding
│ • Generate query_id │
│ • Insert record     │
│ • Update memory     │
└──────┬──────────────┘
       │
       ▼
┌─────────────────────┐
│ RESPONSE            │ Deliver formatted verdict
│ ─────────────       │ Offer next steps
│ • Format report     │
│ • Add recommends    │
│ • Ask for more      │
└──────┬──────────────┘
       │
       ▼
  [END or LOOP]
```

---

## 💡 Example Scenarios

### Scenario 1: Clear Counterfeit

**Input:**

- Photo: Chanel No. 5 bottle
- Seller: "Instagram seller @cheapfragrances"
- Price: $30

**Analysis:**

- MSRP: $135
- Discount: 78%
- Image quality: 4/10 (blurry logo, wrong font)
- Seller: Unauthorized

**Verdict:** `Likely Counterfeit ❌`  
**Risk Score:** `0.92`

---

### Scenario 2: Authentic Product

**Input:**

- Photo: La Mer cream jar
- Seller: "Nordstrom in-store"
- Price: $185

**Analysis:**

- MSRP: $180-$195
- Discount: 0%
- Image quality: 9/10 (all elements correct)
- Seller: Authorized retailer

**Verdict:** `Likely Genuine ✅`  
**Risk Score:** `0.08`

---

### Scenario 3: Unclear / Need More Info

**Input:**

- Photo: Blurry Fenty Beauty foundation
- Seller: "Friend gave it to me"
- Price: Unknown

**Analysis:**

- Image quality: 5/10 (can't verify details)
- No price data
- Unknown provenance

**Verdict:** `Unclear ⚠️`  
**Action:** Request clearer photo + more context

---

## 🐛 Troubleshooting

### Common Issues

#### ❌ Bot doesn't respond to photos

**Check:**

1. Telegram trigger is active
2. Privacy mode disabled in @BotFather
3. Webhook properly configured
4. n8n workflow is activated

**Fix:**

```
/setprivacy → disable
Restart workflow in n8n
Check execution logs
```

---

#### ❌ Image analysis fails

**Check:**

1. Gemini API key is valid
2. Image format supported (JPG, PNG)
3. File size under 10MB
4. API quota not exceeded

**Fix:**

- Test API key in Google AI Studio
- Check n8n error logs
- Verify image node configuration

---

#### ❌ Search tool not finding results

**Check:**

1. Google Custom Search API enabled
2. Search Engine ID (CX) correct
3. Query format is specific
4. API quota available

**Fix:**

```javascript
// Make queries more specific
"Dior Sauvage official price"
→ "Dior Sauvage EDT 100ml price 2024 USA"
```

## 📈 Performance Metrics

### Expected Performance

| Metric             | Target      | Notes                          |
| ------------------ | ----------- | ------------------------------ |
| **Response Time**  | <10 seconds  | For simple queries (text only) |
| **Image Analysis** | <60 seconds  | Including upload + processing  |
| **With Search**    | <12 seconds | Image + search + analysis      |
| **Accuracy**       | >85%        | Based on manual verification   |
| **Uptime**         | 99%+        | n8n workflow stability         |

### Optimization Tips

1. **Cache common searches** (save MSRP in database)
2. **Pre-load brand data** (authorized retailers list)
3. **Optimize image size** (compress before sending to API)
4. **Batch database inserts** (if high volume)
5. **Use CDN for images** (faster loading)

---

## 📚 Additional Resources

### Documentation Links

- [n8n Documentation](https://docs.n8n.io/)
- [Google Gemini API](https://ai.google.dev/docs)
- [Supabase Docs](https://supabase.com/docs)
- [Telegram Bot API](https://core.telegram.org/bots/api)

### Community & Support

- **Issues:** [GitHub Issues](https://github.com/your-repo/issues)
- **Discussions:** [Community Forum](https://community.n8n.io/)
- **Updates:** Follow development on Twitter

---

## 📄 License

MIT License - Free to use and modify

---

## 🙏 Credits

**Built with:**

- n8n workflow automation
- Google Gemini Flash 2.5
- Supabase PostgreSQL
- Telegram Bot API


**Created for:** Protecting consumers from counterfeit beauty and luxury products
**Created by:** Abdulrahman Kharzoum

---

## 📞 Support

**For technical issues:**

- Review n8n execution logs
- contact me: https://www.linkedin.com/in/abdulrahman-kharzoum-9040bb20a
- my Portfolio: https://abdulrahmankharzoum.zentraid.com
- another Ai project: https://nevermissai.zentraid.com

**For questions:**
- Open GitHub issue
- Contact via Telegram: @Abdulrahman_Kharzoum

Thank you ❤️
