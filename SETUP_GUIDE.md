# 🚀 NeuroFamily Setup Guide

This guide walks you through setting up the NeuroFamily Support Ecosystem with **OpenClaw**.

---

## What is OpenClaw?

**OpenClaw** is a personal AI assistant you run on your own devices. It answers you on the channels you already use:

- **Messaging:** WhatsApp, Telegram, Slack, Discord, Google Chat, Signal, iMessage, Microsoft Teams, WebChat
- **Extension Channels:** BlueBubbles, Matrix, Zalo, Zalo Personal
- **Voice:** Speaks and listens on macOS/iOS/Android
- **Canvas:** Renders a live, interactive Canvas you control

The Gateway is just the control plane — the product is the assistant itself.

NeuroFamily is designed as a drop-in agent system for **[OpenClaw](https://openclaw.ai/)**. Install it once, and your family has access to a complete support team through any channel you use.

---

## Prerequisites

- A machine to run OpenClaw (local computer, VPS, Raspberry Pi)
- An OpenRouter account (for free AI models) OR MiniMax account
- Basic comfort with command line (we'll keep it simple)

---

## Part 1b: Local AI with LMStudio (Advanced Option)

**Want to run AI completely offline on your own computer?** You can use LMStudio with local models instead of cloud APIs.

### What is LMStudio?

**LMStudio** is a free desktop app that lets you run large language models (LLMs) locally on your Mac or PC.

- **100% Private** — No data leaves your computer
- **No Internet Required** — Works offline
- **No API Costs** — One-time download
- **Free Models** — Many available

### Getting Started with LMStudio

#### 1. Download LMStudio

```bash
# Visit the website
https://lmstudio.ai/

# Download for your OS:
# - macOS (Apple Silicon or Intel)
# - Windows
# - Linux
```

#### 2. Download a Model

In LMStudio:

1. Click **🔍 Discover** in the sidebar
2. Search for recommended models (see below)
3. Click **Download**
4. Wait for download to complete

#### 3. Recommended Models

| Model | Size | RAM Needed | Best For |
|-------|------|------------|----------|
| **Qwen 2.5 9B** | ~18GB | 16GB+ RAM | 🌟 Best overall |
| **Qwen 2.5 14B** | ~28GB | 32GB+ RAM | More capable |
| **Llama 3.2 3B** | ~6GB | 8GB+ RAM | Fast, less RAM |
| **Mistral 7B** | ~14GB | 16GB+ RAM | Good balance |
| **Phi-3.5 4B** | ~8GB | 8GB+ RAM | Lightweight |

**🌟 Recommended: Qwen 2.5 9B**
- Excellent reasoning for multi-agent coordination
- Fits in 16GB RAM
- Good context window
- Free, open weights

#### 4. Run the Model

1. Click **💬 Chat** in sidebar
2. Select your downloaded model
3. Adjust settings:
   - **Context Length:** 8192 (or higher if supported)
   - **GPU Offload:** Max (uses your graphics card)
   - **Threads:** Match your CPU cores

### Connecting LMStudio to OpenClaw

#### Option A: Local API Server (Recommended)

1. In LMStudio, click **🧠 Server** in sidebar
2. Check **Enable Server**
3. Note the port (default: 1234)
4. Configure OpenClaw:

```bash
openclaw config edit
```

Add:

```json
{
  "model": "local/qwen-2.5-9b",
  "provider": "lmstudio",
  "baseUrl": "http://localhost:1234/v1"
}
```

#### Option B: Ollama (Alternative)

If LMStudio doesn't work for you, try **Ollama**:

```bash
# Install Ollama
brew install ollama  # macOS
# or
winget install ollama.ollama  # Windows

# Pull a model
ollama pull qwen2.5:9b

# It runs on port 11434 by default
```

Configure OpenClaw:

```json
{
  "model": "qwen2.5:9b",
  "provider": "ollama",
  "baseUrl": "http://localhost:11434"
}
```

### LMStudio vs Cloud: Which to Choose?

| Feature | LMStudio (Local) | OpenRouter (Cloud) |
|---------|------------------|---------------------|
| **Cost** | Free (after download) | Pay for API |
| **Privacy** | 100% private | Data goes to cloud |
| **Internet** | Works offline | Needs internet |
| **Setup** | More complex | Easy |
| **Speed** | Fast (your hardware) | Depends on connection |
| **Quality** | Good for size | Can use bigger models |

### System Requirements

| Model Size | Minimum RAM | Recommended |
|------------|-------------|-------------|
| 3B | 8GB | 12GB |
| 7B | 16GB | 24GB |
| 9B | 16GB | 32GB |
| 14B | 32GB | 64GB |

**Tip:** More RAM = bigger models = better performance

### Hardware Recommendations

| Use Case | Setup |
|----------|-------|
| **Light use** | 16GB RAM, any modern CPU |
| **Regular use** | 32GB RAM, modern CPU |
| **Power user** | 64GB+ RAM, discrete GPU (NVIDIA) |

### Troubleshooting LMStudio

**Model won't load:**
- Not enough RAM — try smaller model
- Close other apps to free RAM

**Slow responses:**
- Increase GPU offload in settings
- Reduce context length
- Try smaller model

**Can't connect:**
- Check port in LMStudio server settings
- Ensure firewall allows localhost
- Try http://127.0.0.1 instead of localhost

### Option A: OpenRouter (Free Models) 🌟 Recommended

OpenRouter offers free tiers for many models. Here's what's available:

| Model | Strengths | Best For |
|-------|-----------|----------|
| **Qwen QwQ 32B** | Excellent reasoning, large context | Complex tasks, multi-agent coordination |
| **DeepSeek Chat** | Fast, capable | General conversation, simple tasks |
| **Llama 3.2 90B** | Great all-rounder | Balanced performance |
| **Mistral 7B** | Fast, efficient | Quick simple responses |
| **Gemma 2 27B** | Google quality, free | Reasoning tasks |

**Setup:**
1. Go to [openrouter.ai](https://openrouter.ai)
2. Sign up (free)
3. Get your API key
4. Add credits (start with $5-10 for testing)

---

### Option B: MiniMax (Budget-Friendly)

MiniMax offers excellent pricing for high usage:

| Plan | Price | Tokens Included |
|------|-------|-----------------|
| **Pay-as-you-go** | ~$0.10-0.30/1M tokens | You choose |
| **MiniMax-Text-01** | ~$0.10/1M input | Latest model |

**Setup:**
1. Go to [minimax.io](https://minimax.io)
2. Sign up
3. Get API key from settings

---

### Token Budget Suggestion

For a family using ~10-20 conversations/day:

| Usage Level | Model Choice | Estimated Monthly Cost |
|-------------|--------------|----------------------|
| **Light** (5 chats/day) | DeepSeek/Mistral | $2-5/month |
| **Medium** (15 chats/day) | QwQ 32B | $10-15/month |
| **Heavy** (30+ chats/day) | MiniMax + fallback | $15-25/month |

**Pro Tip:** Set up model fallbacks. Use a free model for simple tasks, premium for complex ones.

---

## Part 2: Install OpenClaw

### Option A: Quick Install (Linux/Mac)

```bash
# Install OpenClaw
curl -sL https://get.openclaw.ai | bash

# Start the gateway
openclaw gateway start
```

### Option B: Docker Install (All Platforms)

```bash
# Install Docker first, then:
docker run -d \
  --name openclaw \
  -p 8080:8080 \
  -v openclaw-data:/data \
  openclaw/openclaw:latest
```

### Option C: Manual Install

```bash
# Clone OpenClaw
git clone https://github.com/openclaw/openclaw.git
cd openclaw

# Install dependencies
pip install -r requirements.txt

# Run
python -m openclaw gateway start
```

---

## Part 3: Configure OpenClaw

### 1. Edit the Config

```bash
# Find your config file
openclaw config edit
```

### 2. Add Your API Key

```json
{
  "model": "minimax/auto",
  "apiKey": "your-api-key-here",
  "provider": "openrouter"
}
```

### 3. Set Up Channels

You can connect NeuroFamily to Telegram, WhatsApp, Discord, and other messaging platforms. Here's how:

---

## Part 3b: Connect to Messaging Platforms

### Option A: Telegram 🌟 Most Popular

Telegram is the easiest platform to set up. You can use it in two ways:

#### Method 1: Individual Bot (One Family Member)

1. **Create a Telegram Bot**
   - Open Telegram and message @BotFather
   - Send `/newbot` and follow the prompts
   - Copy your **Bot API Token**

2. **Configure OpenClaw**
   ```bash
   openclaw channels add telegram
   ```
   - Enter your Bot API Token when prompted
   - Set as direct (not group)

3. **Start Chatting**
   - Search for your bot username
   - Send `/start` to begin

**Best for:** Private conversations between your family and NeuroFamily

---

#### Method 2: Group Chat (Whole Family)

1. **Create a Group**
   - Create a new Telegram group
   - Add your family members
   - Add the bot to the group

2. **Configure for Group**
   ```bash
   openclaw channels add telegram
   ```
   - Enter your Bot API Token
   - Set as **group** mode

3. **How It Works**
   - Everyone in the family can chat with NeuroFamily
   - Tag the bot: `@yourbot help`
   - Useful for family coordination

**Best for:** Family-wide communication, multiple caregivers

---

#### Method 3: Multiple Bots (Different Specialists)

You can set up different bots for different agents:

| Bot Name | Agent | Use Case |
|----------|-------|----------|
| @FamilyNavigatorBot | Family Navigator | General support, triage |
| @ParentSupportBot | Parent Companion | Caregiver wellbeing |
| @FoodCoachBot | Food Support Coach | Meal planning, ARFID |
| @EducationBot | Education Advocate | School support |

**Setup:**
- Create separate bots via @BotFather
- Configure each as a different agent in OpenClaw
- Assign each bot to a specific agent

---

### Option B: WhatsApp

WhatsApp is popular but requires more setup:

#### Method 1: WhatsApp Business API (Official)

1. **Create WhatsApp Business Account**
   - Go to [business.facebook.com](https://business.facebook.com)
   - Create a Meta App
   - Add WhatsApp product

2. **Get Credentials**
   - Phone Number ID
   - Access Token
   - Verify your phone number

3. **Configure OpenClaw**
   ```bash
   openclaw channels add whatsapp
   ```
   - Enter your credentials
   - Set up webhook URL

**Pros:** Official, reliable, supports rich messages  
**Cons:** Requires Meta developer account, phone verification

---

#### Method 2: WhatsApp QR Linking (Personal)

1. **Generate QR Code**
   ```bash
   openclaw whatsapp login
   ```

2. **Scan with Phone**
   - Open WhatsApp on your phone
   - Go to Settings → Linked Devices
   - Scan the QR code

3. **You're Connected!**
   - Your personal WhatsApp is now linked
   - Works like the Telegram individual bot

**Pros:** No business account needed, free  
**Cons:** Phone must stay online, personal number visible

**Best for:** Personal family use without business setup

---

### Option C: Discord (Best for Teens)

If your teen prefers Discord:

1. **Create a Discord Bot**
   - Go to [discord.com/developers](https://discord.com/developers)
   - Create Application → Bot
   - Copy the **Token**

2. **Invite the Bot**
   - Generate an invite link
   - Add to your server

3. **Configure OpenClaw**
   ```bash
   openclaw channels add discord
   ```
   - Enter your bot token
   - Set channel permissions

**Best for:** Teens who already live on Discord

---

### Option D: Other Platforms

| Platform | Setup Difficulty | Best For |
|----------|-----------------|----------|
| **Slack** | Medium | Work-from-home families |
| **Signal** | Hard | Privacy-focused families |
| **Microsoft Teams** | Medium | Business + family |
| **Google Chat** | Easy | Google ecosystem users |
| **iMessage** | Hard | Apple-only households |
| **Matrix** | Medium | Privacy, self-hosted |

See [OpenClaw Channels Docs](https://docs.openclaw.ai/channels) for full setup.

---

### Channel Comparison

| Feature | Telegram | WhatsApp | Discord |
|--------|----------|----------|---------|
| **Setup Ease** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐ |
| **Group Chat** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Privacy** | ⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ |
| **Rich UI** | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Bot Creation** | ⭐⭐⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐⭐ |
| **Voice** | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ |

---

### Recommended Setup for Families

**Single Parent / Small Family:**
- Telegram Individual Bot → Simple, private

**Two-Parent + Kids:**
- Telegram Group → Everyone included
- Or WhatsApp Personal → Already familiar

**Teen-Focused:**
- Discord Server → Natural for teens

**Extended Family / Care Team:**
- Multiple Telegram bots → Different agents for different needs

---

### Testing Your Connection

```bash
# Check channel status
openclaw channels status

# Send a test message
openclaw channels test telegram
```

Then start chatting:

> "Hi! This is our family. We have a child named [name] who is [age]. Our main challenge is [priority]."

NeuroFamily will read your USER.md and respond tailored to your family!

---

### ⚠️ Important: Privacy Considerations

- **Telegram:** Bot username is public, but chats are private
- **WhatsApp:** Personal number visible to the bot
- **Discord:** Messages visible to everyone in the server
- **Group chats:** Consider what family info is shared in groups

**Tip:** For sensitive discussions, use direct messages (individual bots), not group chats.

---

## Part 4: Clone the NeuroFamily Ecosystem

### Option A: Direct Clone (Recommended)

```bash
# Navigate to your OpenClaw agents directory
cd /root/.openclaw/agents

# Clone the repo
git clone https://github.com/boktoday/neurofamily-support-ecosystem.git neurofamily
```

### Option B: Manual Copy

```bash
# Download from GitHub
wget https://github.com/boktoday/neurofamily-support-ecosystem/archive/refs/heads/main.zip

# Unzip
unzip main.zip

# Move to agents folder
mv neurofamily-support-ecosystem-main ~/.openclaw/agents/neurofamily
```

---

## Part 5: Configure the Agents

### 1. Edit Family Navigator's USER.md

This is the MOST IMPORTANT file. Fill in:

```
/root/.openclaw/agents/neurofamily/family-navigator/USER.md
```

**See Section 6 below for details.**

### 2. Update Identities (Optional)

If you want to customize agent names/voices:

```
family-navigator/IDENTITY.md
```

### 3. Test It

```bash
# Restart OpenClaw to load new agents
openclaw gateway restart
```

---

## Part 6: Which Files to Customize

### 🔴 CRITICAL: Must Fill In

| File | Why | Time to Fill |
|------|-----|---------------|
| `family-navigator/USER.md` | Contains ALL family info | 30-60 min |
| ^ This is the main file I read before every response | | |

### 🟡 IMPORTANT: Should Review

| File | What It Contains | When to Update |
|------|------------------|----------------|
| `family-navigator/AGENTS.md` | How I work | Usually don't need to change |
| `family-navigator/TOOLS.md` | My resources | Add local resources if needed |
| `family-navigator/SOUL.md` | My personality | Usually don't change |

### 🟢 Optional: Per-Child Details

You can create additional profile files in:
```
family-navigator/memory/
```

---

## Part 7: USER.md Walkthrough

The USER.md is your family's profile. Here's what matters most:

### Quick Start (15 min)

Fill in these sections first:

1. **Parent names** — So I know who I'm talking to
2. **Child names & ages** — For personalization
3. **Diagnoses** — Autism? ADHD? AuDHD? Dyslexia?
4. **Current priorities** — What's the #1 thing you need help with?
5. **What triggers meltdowns** — So I can help avoid them

### Full Profile (30-60 min)

Add details for better support:

- **Sensory profile** — What overwhelms them? What helps?
- **Communication style** — Verbal? AAC? Non-verbal?
- **Safe foods / Food issues** — For Food Coach
- **School situation** — IEP? 504? For Education Advocate
- **What has NOT worked** — So I don't suggest it again

### Pro Tips

- **Be specific:** "mornings are hard" → "transitions between activities cause meltdowns"
- **Include strengths:** What is your child brilliant at?
- **Update as you learn:** Come back and add new information

---

## Part 8: First Conversation

Once everything is set up, start with:

> "Hi, this is our family. We have a child named [name] who is [age] and was diagnosed with [diagnosis]. Our main challenge right now is [top priority]."

I'll read your USER.md and tailor my responses to your family.

---

## Troubleshooting

### "Agent not found"

```bash
# Restart gateway
openclaw gateway restart

# Check agents are loaded
openclaw agents list
```

### "Model not available"

- Check your API key is valid
- Ensure you have credits/balance
- Try a different model

### "Conversation not remembering"

- The agent should maintain memory within a session
- For cross-session memory, the Navigator writes to memory files

---

## Getting Help

- **OpenClaw Docs:** [docs.openclaw.ai](https://docs.openclaw.ai)
- **NeuroFamily GitHub:** [github.com/boktoday/neurofamily-support-ecosystem](https://github.com/boktoday/neurofamily-support-ecosystem)
- **OpenClaw Discord:** [discord.gg/clawd](https://discord.com/invite/clawd)

---

## Summary Checklist

- [ ] Choose AI provider (OpenRouter or MiniMax)
- [ ] Get API key
- [ ] Install OpenClaw
- [ ] Configure model
- [ ] Clone neurofamily repo
- [ ] Fill in USER.md (CRITICAL)
- [ ] Restart OpenClaw
- [ ] Start first conversation

---

*Questions? Open an issue on GitHub or ask in the Discord!*

---

**Created by:** Brendan O'Keefe  
**Date:** February 2026  
**AI Orchestrator Training:** https://aiorchestrator.com.au

---

## ⚠️ Disclaimer & Terms of Use

**IMPORTANT: READ BEFORE USING**

### Disclaimer

The NeuroFamily Support Ecosystem is an **AI-powered support tool**, not a replacement for professional medical, therapeutic, or educational advice.

- **Not a medical device** — This system does not diagnose, treat, or cure any condition
- **Not a qualified professional** — AI assistants have limitations; always consult doctors, therapists, specialists, and educators for clinical decisions
- **Information only** — Content provided is for informational purposes only
- **Accuracy not guaranteed** — While we strive for accuracy, AI can make mistakes; verify critical information independently
- **Crisis support** — This system is not a crisis service. If you or someone you know is in crisis, contact emergency services or a crisis helpline immediately

### Terms of Use

- **Personal/family use only** — This system is designed for personal family use
- **Commercial use** — Contact the creator for commercial licensing
- **Modification allowed** — Feel free to adapt for your family's needs
- **No warranty** — This system is provided "as is" without warranties of any kind
- **Liability limitation** — The creator is not liable for any damages arising from use of this system

### Safety First

If at any time you or your family are in crisis, please contact:

- **Emergency:** 000 (Australia) / 911 (US/UK) / your local emergency number
- **Beyond Blue (AU):** 1300 22 4636
- **Samaritans (UK):** 116 123
- **Crisis Text Line (US):** Text HOME to 741741

---

*By using this system, you acknowledge that you have read, understood, and agree to this disclaimer and terms of use.*
