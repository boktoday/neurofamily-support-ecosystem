# 🚀 NeuroFamily Setup Guide

This guide walks you through setting up the NeuroFamily Support Ecosystem with OpenClaw.

---

## Prerequisites

- A machine to run OpenClaw (local computer, VPS, Raspberry Pi)
- An OpenRouter account (for free AI models) OR MiniMax account
- Basic comfort with command line (we'll keep it simple)

---

## Part 1: Choose Your AI Provider

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

### 3. Set Up Channels (Optional)

You can connect Telegram, WhatsApp, Discord, etc. See [OpenClaw Docs](https://docs.openclaw.ai).

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
