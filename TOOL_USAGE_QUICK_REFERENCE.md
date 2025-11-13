# 🚀 AI Agent Tool Usage - Quick Reference Card

## ⚡ MANDATORY SEQUENCE (Every Message)

```
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃  📨 USER SENDS MESSAGE                      ┃
┗━━━━━━━━━━━━━━━━━━┯━━━━━━━━━━━━━━━━━━━━━━━━┛
                    ▼
    ┌───────────────────────────────┐
    │ 1️⃣ MEMORY TOOL               │
    │ Check conversation history    │
    │ ⚠️  ALWAYS DO THIS FIRST!     │
    └───────────┬───────────────────┘
                ▼
    ┌───────────────────────────────┐
    │ 2️⃣ GET DATABASE LOGGER        │
    │ Existing query?               │
    │ Load queryId & current data   │
    └───────────┬───────────────────┘
                ▼
    ┌───────────────────────────────┐
    │ 3️⃣ CREATE/PREPARE UPDATE      │
    │ New → Create entry            │
    │ Existing → Prepare update     │
    └───────────┬───────────────────┘
                ▼
    ┌───────────────────────────────┐
    │ 4️⃣ IMAGE ANALYZER (if photo)  │
    │ Extract brand, product, score │
    │ Optional - only if photo sent │
    └───────────┬───────────────────┘
                ▼
    ┌───────────────────────────────┐
    │ 5️⃣ SEARCH TOOL (if needed)    │
    │ MSRP, seller verification     │
    │ Optional - only when needed   │
    └───────────┬───────────────────┘
                ▼
    ┌───────────────────────────────┐
    │ 6️⃣ THINK TOOL ⚠️  MANDATORY!  │
    │ Plan response                 │
    │ Calculate risk (if ready)     │
    │ List reasons                  │
    │ 🚨 NEVER SKIP THIS!           │
    └───────────┬───────────────────┘
                ▼
    ┌───────────────────────────────┐
    │ 7️⃣ DATABASE UPDATE ⚠️  MANDATORY!│
    │ Save ALL new data             │
    │ Incomplete data OK!           │
    │ 🚨 THIS FIXES YOUR ISSUE!     │
    └───────────┬───────────────────┘
                ▼
    ┌───────────────────────────────┐
    │ 8️⃣ RESPOND TO USER            │
    │ Warm, conversational reply    │
    └───────────────────────────────┘
```

---

## 🎯 The 3 Non-Negotiable Steps

### 🧠 1. Memory Tool (Step 1)

**Why:** Prevents asking same question twice  
**When:** FIRST THING on every message  
**Result:** Know what user already told you

### 🎯 2. Think Tool (Step 6)

**Why:** Strategic planning + risk calculation  
**When:** BEFORE responding to user  
**Result:** Calculated risk score + specific reasons

### 💾 3. Database Update (Step 7)

**Why:** Logs every interaction  
**When:** AFTER Think Tool, BEFORE responding  
**Result:** Complete audit trail  
**⚠️ THIS IS YOUR FIX!**

---

## 📊 Risk Score Formula (Think Tool)

```
Price Factor (40%):
├─ 0-20% discount   → 0.0
├─ 20-40% discount  → 0.2
├─ 40-60% discount  → 0.5
└─ 60%+ discount    → 0.9

Seller Factor (30%):
├─ Authorized       → 0.0
├─ Major marketplace→ 0.4
└─ Unknown/social   → 0.8

Image Quality (20%):
├─ 9-10/10         → 0.0
├─ 7-8/10          → 0.2
├─ 5-6/10          → 0.5
└─ <5/10           → 0.8

Visual Red Flags (10%):
├─ None            → 0.0
├─ Minor concerns  → 0.3
└─ Major flags     → 0.9

────────────────────────────────
FINAL = Weighted average

0.00-0.30 → Likely Genuine ✅
0.31-0.69 → Unclear ⚠️
0.70-1.00 → Likely Counterfeit ❌
```

---

## 💾 Database Update Rules

### ✅ DO UPDATE:

- User sends ANY message (even "Hi")
- After image analysis
- After getting price
- After getting seller
- After Think Tool calculates risk
- After every conversation turn

### ✅ INCOMPLETE DATA IS OK:

```json
{
  "brand": "Dior",
  "product": null,        ← OK!
  "price": null,          ← OK!
  "seller": null,         ← OK!
  "riskScore": null,      ← OK!
  "verdict": "Incomplete" ← OK!
}
```

### ❌ DON'T:

- Wait for "complete" data
- Skip because "nothing new to add"
- Only log final verdict

---

## 🧠 Memory Tool Usage

### Check Memory For:

```
✓ Previous messages
✓ Data already collected
✓ Questions already answered
✓ User preferences
```

### Use Memory To:

```
✓ Avoid: "What's the price?" (they told you!)
✓ Reference: "Based on the photo you sent..."
✓ Continue: "You mentioned eBay earlier..."
```

---

## 🔍 When to Use Search Tool

### Always Search:

- Price >30% below expected retail
- Unknown seller/platform
- User asks "what's the retail price?"
- Unfamiliar product variant

### Search Queries:

```
"[Brand] [Product] official price 2024"
"[Brand] authorized retailers"
"[Seller] [Brand] authorized dealer"
"authentic [Brand] [Product] vs fake"
```

---

## 📝 Think Tool Output Format

```json
{
  "nextAction": "ask for price | deliver verdict | request photo",
  "riskScore": 0.78,
  "verdict": "Likely Counterfeit",
  "reasons": [
    "Price 50% below MSRP ($55 vs $110)",
    "eBay seller not on authorized list",
    "Batch code format irregular",
    "Discount exceeds normal patterns"
  ],
  "missingData": ["none"],
  "confidenceLevel": "high"
}
```

### ⚠️ Reasons Must Be SPECIFIC:

```
❌ "Price is suspicious"
✅ "Price 50% below MSRP ($55 vs $110)"

❌ "Seller looks bad"
✅ "eBay seller not on Dior authorized list"

❌ "Packaging concerns"
✅ "Batch code format doesn't match Dior standard"
```

---

## 🎭 Example: Complete Message Flow

```
USER: [sends photo of perfume]

BOT INTERNAL PROCESS:
├─ 1. Memory Tool → No previous messages
├─ 2. Get DB → No existing query
├─ 3. Create DB → New query AQ-xxx
├─ 4. Image Analyzer → Dior Sauvage, 8/10
├─ 5. Search Tool → (skip, no price yet)
├─ 6. Think Tool → "ask for price and seller"
├─ 7. Update DB → Save brand, product, imageScore
└─ 8. Respond → "Great photo! I see it's Dior Sauvage..."

────────────────────────────────

USER: "I paid $55 from eBay"

BOT INTERNAL PROCESS:
├─ 1. Memory Tool → User sent photo, have brand/product
├─ 2. Get DB → Load AQ-xxx query
├─ 3. Prepare update → Add price, seller
├─ 4. Image Analyzer → (skip, no new photo)
├─ 5. Search Tool → Find MSRP=$110, eBay unauthorized
├─ 6. Think Tool → Calculate risk=0.78, verdict=Counterfeit
├─ 7. Update DB → Save price, seller, MSRP, risk, verdict, reasons
└─ 8. Respond → "I see some serious red flags here..."
```

---

## 🚨 Common Mistakes to Avoid

### ❌ Skipping Database Update

```
WRONG: User says "Hi" → Skip DB (nothing to log)
RIGHT: User says "Hi" → Create entry with username, chatId
```

### ❌ Waiting for Complete Data

```
WRONG: Only log when have brand+price+seller
RIGHT: Log immediately with whatever data available
```

### ❌ Not Using Think Tool

```
WRONG: Skip Think Tool, respond directly
RIGHT: Use Think Tool first → Plan → Respond
```

### ❌ Not Checking Memory

```
WRONG: Ask "What's the price?" (user told you already)
RIGHT: Check memory → See price=$55 → Use it
```

### ❌ Generic Reasons

```
WRONG: "Price is suspicious"
RIGHT: "Price 50% below MSRP ($55 vs $110)"
```

---

## ✅ Success Checklist (Before Responding)

```
☑ Checked Memory Tool?
☑ Checked Database Logger?
☑ Created/Updated Database?
☑ Used Think Tool?
☑ Updated Database with Think Tool results?
☑ Response is conversational/warm?
```

**If all ✅ → You're good to respond!**

---

## 🎯 Database Update = Your Primary Fix

### The Problem:

Agent was NOT recording data consistently

### The Solution:

Made Database Update **MANDATORY** (Step 7) with:

- Visual warnings: "⚠️ MANDATORY!", "🚨 NEVER SKIP!"
- Explicit permission for incomplete data
- Examples of logging at every stage
- Step 7 position (after Think Tool, before Response)

### Result:

Agent CANNOT respond without first updating database

---

## 📞 Quick Troubleshooting

**Agent not logging?**

1. Check if Database Update node is connected in n8n
2. Verify credentials (Google Sheets/Supabase)
3. Check execution log for tool calls
4. Ensure prompt is fully updated

**Agent asking twice?**

1. Verify Memory Tool is connected
2. Check session ID uses chatId
3. Confirm memory backend working

**Risk scores wrong?**

1. Verify Think Tool has access to formula
2. Check if all factors calculated
3. Ensure proper weighting applied

---

**Print this card and keep it handy when testing! 📋**
