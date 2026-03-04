# 🧠 Shared Context Layer

**Cross-Agent Memory for the NeuroFamily Ecosystem**

---

## Purpose

This folder contains the **shared brain** that all agents can access. When one agent learns something important, it gets stored here so other agents can find it.

---

## How It Works

### What Gets Shared

| Category | Examples | Agents That Might Add |
|----------|----------|---------------------|
| **Child Triggers** | New sensory triggers, meltdown causes | Behaviour Advisor, Emotional Coach |
| **School Updates** | New IEP goals, accommodations added | Education Advocate |
| **Health Changes** | Medication changes, diagnoses | Family Navigator |
| **Food Updates** | New safe foods, ARFID changes | Food Support Coach |
| **Routine Changes** | New schedules, what works/doesn't | Routine Architect |
| **Family Updates** | Parent burnout level, sibling issues | Parent Companion, Sibling Support |

### What STAYS Private

| Category | Where It Stays |
|----------|---------------|
| Detailed therapy notes | Individual agent memory |
| Session specifics between child and one agent | That agent's memory |
| Sensitive family financial details | Family Navigator only |

---

## Shared Memory Files

### 1. CHILD_SUMMARY.md
Quick reference for each child — key facts all agents need:

```markdown
# Child: [Name]

## Quick Facts
- Age: 
- Diagnoses: 
- Communication: 
- Key Triggers: 
- Top 3 Regulators: 

## Current Priorities
1. 
2. 

## What Works
- 
- 

## What Doesn't Work
- 
- 

## Last Updated: [DATE]
```

### 2. ACTIVE_CONCERNS.md
Things multiple agents might need to know about:

```markdown
# Active Concerns

## 🚨 Urgent
| Concern | Who Noticed | Date | Action Needed |
|---------|-------------|------|---------------|
| | | | |

## ⚠️ Important
| Concern | Who Noticed | Date | Notes |
|---------|-------------|------|-------|
| | | | |

## 📝 Watch List
| Concern | Who Noticed | Date | Monitor |
|---------|-------------|------|---------|
| | | | |
```

### 3. SHARED_NOTES.md
Free-form notes that any agent can add to:

```markdown
# Cross-Agent Notes

## [DATE] - [Agent Name]
**Topic:** 

**Key Info:**

**Implications for other agents:**
- [Agent] should know: 
- [Agent] should consider: 

---

## [DATE] - [Agent Name]
...
```

### 4. AGENT_COORDINATION.md
Track what each agent is working on:

```markdown
# Agent Coordination Log

## Current Active Work

| Agent | Working On | Since | Status |
|-------|-----------|-------|--------|
| Family Navigator | | | |
| Education Advocate | | | |
| Emotional Coach | | | |
| ... | | | |

## Recent Handovers

| From | To | Topic | Date |
|------|----|-------|------|
| | | | |
```

### 5. FAMILY_CALENDAR.md
Key dates everyone should know:

```markdown
# Family Calendar

## Upcoming
| Date | Event | Who Needs to Know |
|------|-------|-------------------|
| | | |

## Past (Keep for 30 days)
| Date | Event | Outcome |
|------|-------|---------|
| | | |
```

---

## Agent Usage Instructions

### When an Agent Learns Something Important

1. **Assess:** Is this something other agents need to know?
2. **Record:** Add to the appropriate shared file
3. **Flag:** Mark in AGENT_COORDINATION.md if urgent
4. **Continue:** Carry on with your session

### When an Agent Needs Context

1. **Check:** Read CHILD_SUMMARY.md first
2. **Scan:** Check ACTIVE_CONCERNS.md
3. **Review:** Look at recent SHARED_NOTES.md
4. **Act:** Use the info to tailor your response

---

## Update Frequency

- **CHILD_SUMMARY.md** — Update when significant changes occur
- **ACTIVE_CONCERNS.md** — Review each session
- **SHARED_NOTES.md** — Add as needed
- **AGENT_COORDINATION.md** — Update when starting/finishing work
- **FAMILY_CALENDAR.md** — Update when events are scheduled

---

## Privacy Guidelines

✅ **Share:**
- Triggers and what helps
- School accommodations
- General health updates
- Routine changes
- Family priorities

❌ **Don't Share:**
- Detailed therapy notes
- Sensitive financial info
- Private family matters not relevant to support
- Anything the family has asked to keep private

---

## Integration with USER.md

The USER.md is the **authoritative source** for family details. The shared context layer supplements but doesn't replace it.

- USER.md = Everything the family has told us
- Shared Context = What agents have learned and need to share

When in doubt, defer to USER.md.

---

*This shared layer ensures that no agent works in isolation — the whole ecosystem knows what it needs to know.*
