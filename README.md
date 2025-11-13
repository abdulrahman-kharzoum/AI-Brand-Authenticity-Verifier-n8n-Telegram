# 🛡️ AI Brand Authenticity Verifier

<img width="813" height="525" alt="image" src="https://github.com/user-attachments/assets/08c56be9-9a1c-490f-9e4d-13f084b4b537" />

**An intelligent Telegram bot that helps users verify the authenticity of beauty and luxury products using advanced AI analysis, image recognition, and real-time web search.**

[![n8n](https://img.shields.io/badge/Built%20with-n8n-orange)](https://n8n.io)
[![Gemini](https://img.shields.io/badge/Powered%20by-Gemini%20Flash%202.5-blue)](https://deepmind.google/technologies/gemini/)
[![Supabase](https://img.shields.io/badge/Database-Supabase-green)](https://supabase.com)

---

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
│    User sends photo + details via Telegram                  │
└──────────────────┬──────────────────────────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────────────────────────┐
│ 2. IMAGE ANALYSIS (Gemini Flash 2.5 Vision)                │
│    • Forensic packaging inspection                          │
│    • Logo/typography verification                           │
│    • Material quality assessment                            │
│    • Batch code format check                                │
│    • Returns 0-10 quality score + findings                  │
└──────────────────┬──────────────────────────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────────────────────────┐
│ 3. DATA COLLECTION (AI Agent + Memory)                     │
│    • Extract brand/product from image                       │
│    • Ask for: price, purchase location                      │
│    • Use memory to track what's already known               │
└──────────────────┬──────────────────────────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────────────────────────┐
│ 4. PRODUCT RESEARCH (Google Search Tool)                   │
│    Triggered when needed:                                   │
│    • Search official MSRP                                   │
│    • Verify seller authorization                            │
│    • Find counterfeit indicators                            │
│    • Check product variant existence                        │
└──────────────────┬──────────────────────────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────────────────────────┐
│ 5. RISK ANALYSIS (Think Tool)                              │
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
│ 6. DATABASE LOGGING (Supabase)                             │
│    Save complete record:                                    │
│    • Query ID, username, chat ID                            │
│    • Product details, price, seller                         │
│    • Image link, search queries                             │
│    • Risk score, verdict, reasoning                         │
└──────────────────┬──────────────────────────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────────────────────────┐
│ 7. DELIVER VERDICT                                          │
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
             │                  │                  │
             └──────────────────┼──────────────────┘
                                ▼
                    ┌──────────────────────┐
                    │  SUPABASE POSTGRES   │
                    │  ──────────────────  │
                    │  • Query Logs        │
                    │  • User Data         │
                    │  • Conversation Hist │
                    │  • Analytics         │
                    └──────────────────────┘
                                │
                                ▼
                    ┌──────────────────────┐
                    │  WINDOW BUFFER MEMORY│
                    │  ──────────────────  │
                    │  • Short-term context│
                    │  • Conversation state│
                    │  • Prevent repeats   │
                    └──────────────────────┘
```

---

## 🛠️ Tools & Technologies

### 1. **AI Model: Google Gemini Flash 2.5**

**Purpose:** Primary intelligence engine

**Capabilities:**

- **Vision API:** Multi-modal image + text analysis
- **Conversational AI:** Context-aware dialogue management
- **Reasoning:** Complex decision-making and risk assessment
- **Fast inference:** Sub-second response times
- **Long context window:** Handles extended conversations

**Usage in workflow:**

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

**Tables:**

#### `authenticity_queries`

```sql
CREATE TABLE authenticity_queries (
  query_id VARCHAR(50) PRIMARY KEY,
  username VARCHAR(100),
  chat_id BIGINT,
  telegram_username VARCHAR(100),
  brand VARCHAR(100),
  product TEXT,
  seller_info TEXT,
  price DECIMAL(10,2),
  currency VARCHAR(10),
  image_link TEXT,
  image_quality_score INTEGER,
  search_performed BOOLEAN,
  search_queries JSONB,
  official_msrp DECIMAL(10,2),
  seller_authorized BOOLEAN,
  risk_score DECIMAL(3,2),
  verdict VARCHAR(50),
  reasons JSONB,
  key_findings TEXT,
  timestamp TIMESTAMP DEFAULT NOW(),
  conversation_turns INTEGER
);
```

**Indexes:**

```sql
CREATE INDEX idx_chat_id ON authenticity_queries(chat_id);
CREATE INDEX idx_brand ON authenticity_queries(brand);
CREATE INDEX idx_verdict ON authenticity_queries(verdict);
CREATE INDEX idx_timestamp ON authenticity_queries(timestamp DESC);
```

---

### 7. **Telegram Bot API**

**Integration:** n8n Telegram Trigger + Message nodes

**Supported inputs:**

- Text messages
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

### Step 2: Set Up Supabase Database

1. Create new project at [supabase.com](https://supabase.com)
2. Go to **SQL Editor**
3. Run this schema:

```sql
-- Create authenticity queries table
CREATE TABLE authenticity_queries (
  query_id VARCHAR(50) PRIMARY KEY,
  username VARCHAR(100),
  chat_id BIGINT NOT NULL,
  telegram_username VARCHAR(100),
  brand VARCHAR(100),
  product TEXT,
  seller_info TEXT,
  price DECIMAL(10,2),
  currency VARCHAR(10) DEFAULT 'USD',
  image_link TEXT,
  image_quality_score INTEGER CHECK (image_quality_score >= 0 AND image_quality_score <= 10),
  search_performed BOOLEAN DEFAULT FALSE,
  search_queries JSONB,
  official_msrp DECIMAL(10,2),
  seller_authorized BOOLEAN,
  risk_score DECIMAL(3,2) CHECK (risk_score >= 0 AND risk_score <= 1),
  verdict VARCHAR(50),
  reasons JSONB,
  key_findings TEXT,
  timestamp TIMESTAMP DEFAULT NOW(),
  conversation_turns INTEGER DEFAULT 1
);

-- Create indexes for performance
CREATE INDEX idx_chat_id ON authenticity_queries(chat_id);
CREATE INDEX idx_brand ON authenticity_queries(brand);
CREATE INDEX idx_verdict ON authenticity_queries(verdict);
CREATE INDEX idx_timestamp ON authenticity_queries(timestamp DESC);
CREATE INDEX idx_risk_score ON authenticity_queries(risk_score DESC);

-- Create memory table (for Window Buffer)
CREATE TABLE chat_memory (
  id SERIAL PRIMARY KEY,
  session_id VARCHAR(100) NOT NULL,
  message_type VARCHAR(20), -- 'human' or 'ai'
  content TEXT,
  timestamp TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_session_id ON chat_memory(session_id, timestamp DESC);
```

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

- Model: `gemini-2.0-flash-exp` or `gemini-1.5-flash-002`
- Temperature: `0.3` (for consistent analysis)
- Max tokens: `2048`
- System prompt: [Use the optimized prompt from above]

**3. Image Analyzer Node:**

- Model: `gemini-2.0-flash-exp` (supports vision)
- Input: Image URL from Telegram
- Prompt: [Use forensic image analysis prompt]

**4. Memory Node:**

- Type: `Window Buffer Memory`
- Max messages: `20`
- Session ID: `{{ $json.message.from.id }}`
- Supabase connection configured

**5. Supabase Insert Node:**

- Table: `authenticity_queries`
- Columns: Map according to schema

---

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

### Step 8: Monitor & Optimize

**Check Supabase:**

```sql
-- View recent queries
SELECT * FROM authenticity_queries
ORDER BY timestamp DESC
LIMIT 10;

-- Analytics: Most queried brands
SELECT brand, COUNT(*) as queries
FROM authenticity_queries
GROUP BY brand
ORDER BY queries DESC;

-- Average risk scores by brand
SELECT brand, AVG(risk_score) as avg_risk
FROM authenticity_queries
WHERE risk_score IS NOT NULL
GROUP BY brand;
```

**n8n Execution Logs:**

- Monitor for errors
- Check execution times
- Verify tool calls

---

## 📱 Usage

### For End Users

#### **Starting a Verification**

1. **Find your bot on Telegram**

   - Search for `@YourBotName`
   - Send `/start`

2. **Send a product photo**

   - Take clear, well-lit photos of:
     - Front of product
     - Batch code / serial number
     - Box (if available)
     - Any labels or stickers

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

**Scenario: User bought perfume from eBay**

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

## 📊 Database Schema

### Complete Table Structure

```sql
-- Main queries table
CREATE TABLE authenticity_queries (
  -- Identification
  query_id VARCHAR(50) PRIMARY KEY,
  username VARCHAR(100),
  chat_id BIGINT NOT NULL,
  telegram_username VARCHAR(100),

  -- Product details
  brand VARCHAR(100),
  product TEXT,
  seller_info TEXT,
  price DECIMAL(10,2),
  currency VARCHAR(10) DEFAULT 'USD',

  -- Image data
  image_link TEXT,
  image_quality_score INTEGER CHECK (image_quality_score >= 0 AND image_quality_score <= 10),

  -- Search intelligence
  search_performed BOOLEAN DEFAULT FALSE,
  search_queries JSONB,
  official_msrp DECIMAL(10,2),
  seller_authorized BOOLEAN,

  -- Analysis results
  risk_score DECIMAL(3,2) CHECK (risk_score >= 0 AND risk_score <= 1),
  verdict VARCHAR(50) CHECK (verdict IN ('Likely Genuine', 'Likely Counterfeit', 'Unclear', 'Incomplete')),
  reasons JSONB,
  key_findings TEXT,

  -- Metadata
  timestamp TIMESTAMP DEFAULT NOW(),
  conversation_turns INTEGER DEFAULT 1
);

-- Memory for conversation context
CREATE TABLE chat_memory (
  id SERIAL PRIMARY KEY,
  session_id VARCHAR(100) NOT NULL,
  message_type VARCHAR(20) CHECK (message_type IN ('human', 'ai')),
  content TEXT,
  timestamp TIMESTAMP DEFAULT NOW()
);

-- Optional: User profiles
CREATE TABLE user_profiles (
  chat_id BIGINT PRIMARY KEY,
  username VARCHAR(100),
  first_name VARCHAR(100),
  telegram_username VARCHAR(100),
  total_queries INTEGER DEFAULT 0,
  first_interaction TIMESTAMP DEFAULT NOW(),
  last_interaction TIMESTAMP DEFAULT NOW()
);
```

### Sample Queries

```sql
-- Get user's verification history
SELECT query_id, brand, product, verdict, risk_score, timestamp
FROM authenticity_queries
WHERE chat_id = 123456789
ORDER BY timestamp DESC;

-- Find most counterfeited brands
SELECT brand,
       COUNT(*) as total_checks,
       SUM(CASE WHEN verdict = 'Likely Counterfeit' THEN 1 ELSE 0 END) as fake_count,
       ROUND(AVG(risk_score), 2) as avg_risk
FROM authenticity_queries
WHERE verdict IN ('Likely Genuine', 'Likely Counterfeit')
GROUP BY brand
ORDER BY fake_count DESC;

-- Risky sellers
SELECT seller_info,
       COUNT(*) as checks,
       AVG(risk_score) as avg_risk,
       SUM(CASE WHEN verdict = 'Likely Counterfeit' THEN 1 ELSE 0 END) as fakes
FROM authenticity_queries
WHERE seller_info IS NOT NULL
GROUP BY seller_info
HAVING AVG(risk_score) > 0.5
ORDER BY avg_risk DESC;

-- Daily analytics
SELECT DATE(timestamp) as date,
       COUNT(*) as total_queries,
       AVG(risk_score) as avg_risk,
       AVG(conversation_turns) as avg_turns
FROM authenticity_queries
GROUP BY DATE(timestamp)
ORDER BY date DESC;
```

---

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

---

#### ❌ Database insert fails

**Check:**

1. Supabase credentials correct
2. Table schema matches
3. Data types compatible
4. Network connection stable

**Fix:**

```sql
-- Test connection
SELECT NOW();

-- Check table exists
SELECT * FROM authenticity_queries LIMIT 1;

-- Verify column names
\d authenticity_queries
```

---

#### ❌ Memory not working

**Check:**

1. Window Buffer Memory configured
2. Session ID uses chat_id
3. Supabase backend connected
4. chat_memory table exists

**Fix:**

- Clear old memory: `DELETE FROM chat_memory WHERE session_id = '123456789';`
- Restart workflow
- Check memory node configuration

---

## 🔌 API & Integration

### Webhook Endpoints

**Telegram Webhook:**

```
POST https://your-n8n-instance.com/webhook/telegram-bot
```

**Query API (optional, if you expose it):**

```
GET  /api/authenticity/query/:queryId
POST /api/authenticity/check
GET  /api/authenticity/user/:chatId/history
```

---

### Programmatic Access

**Example: Query database directly**

```javascript
const { createClient } = require("@supabase/supabase-js");

const supabase = createClient(
  "https://your-project.supabase.co",
  "your-anon-key"
);

// Get user's verification history
const { data, error } = await supabase
  .from("authenticity_queries")
  .select("*")
  .eq("chat_id", 123456789)
  .order("timestamp", { ascending: false });

console.log(data);
```

---

### Extending the System

**Add new tool:**

```javascript
// In AI Agent node, add to tools array
{
  "name": "price_comparison",
  "description": "Compare prices across multiple retailers",
  "parameters": {
    "brand": "string",
    "product": "string"
  }
}
```

**Add new verification factor:**

```sql
-- Extend database schema
ALTER TABLE authenticity_queries
ADD COLUMN receipt_verified BOOLEAN,
ADD COLUMN packaging_weight DECIMAL(5,2);
```

---

## 📈 Performance Metrics

### Expected Performance

| Metric             | Target      | Notes                          |
| ------------------ | ----------- | ------------------------------ |
| **Response Time**  | <5 seconds  | For simple queries (text only) |
| **Image Analysis** | <8 seconds  | Including upload + processing  |
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

## 🔒 Security & Privacy

### Data Protection

- **Encryption:** All data in Supabase encrypted at rest
- **API Keys:** Store in n8n credentials (never in code)
- **User Privacy:** No personal data shared with third parties
- **Image Storage:** Optional - can delete after analysis
- **GDPR Compliant:** Users can request data deletion

### Best Practices

```javascript
// Sanitize user input
function sanitize(input) {
  return input
    .replace(/<script>/gi, '')
    .substring(0, 500); // Limit length
}

// Rate limiting (in n8n)
// Add "Limit" node: 10 requests per user per minute

// Anonymize data for analytics
SELECT
  brand,
  verdict,
  risk_score
FROM authenticity_queries
-- Exclude: username, chat_id, telegram_username
```

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

---

## 📞 Support

**For technical issues:**

- Check troubleshooting section
- Review n8n execution logs
- Verify API quotas
- Test each component individually

**For questions:**

- Open GitHub issue
- Join n8n community
- Contact via Telegram: @YourSupportUsername
