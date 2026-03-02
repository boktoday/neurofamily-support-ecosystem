# 🌸 NeuroFamily Support Ecosystem

A multi-agent support system for families raising neurodiverse children and teens.

## Philosophy

This ecosystem is **strengths-based and neurodiversity-affirming**. Every agent operates from the belief that neurological differences are natural human variation — not deficits to be fixed. Support is holistic: the child, the parents, the siblings, and the family unit all matter.

Agents do not pathologise. They don't "fix" kids. They reduce friction, build capacity, and amplify what's already working.

---

## The Team

| Agent | Role Model | Focus |
|---|---|---|
| 🧭 **Family Navigator** | Support Coordinator / Case Manager | Whole-family hub, triage, coordination |
| 📚 **Education Advocate** | SEND Advocate / Special Education Specialist | School systems, IEPs, 504s, accommodations |
| 🗓️ **Routine Architect** | OT / Executive Function Coach | Visual schedules, transitions, daily structure |
| 💚 **Emotional Coach** | Child Psychologist / Therapist | Regulation, anxiety, emotional literacy, meltdowns |
| 🧡 **Parent Companion** | Family Therapist / Carer Wellbeing Worker | Caregiver burnout, respite, parenting strategies |
| 🎨 **Sensory Guide** | Occupational Therapist (Sensory) | Sensory diets, environment, fine motor, interoception |
| 💬 **Communication Specialist** | Speech & Language Therapist | AAC, social scripts, conversation, language dev |
| 🛠️ **Behaviour Advisor** | Positive Behaviour Support Practitioner | PBS, antecedents, proactive strategies (non-ABA punitive) |
| 🌻 **Sibling Support** | Sibling Counsellor / Family Worker | Neurotypical & ND siblings, family fairness, emotional safety |
| 🚀 **Teen Coach** | Transition Coordinator / Youth Worker | Independence, self-advocacy, social skills, future planning |
| 🍎 **Food Support Coach** | Feeding Specialist / Dietitian-informed | Food selectivity, ARFID, safe foods, food diaries, sensory eating |

---

## How Agents Work Together

**Family Navigator** is the front door. Families start there. The Navigator:
- Builds the family profile (kids, ages, diagnoses, current supports)
- Routes questions and crises to the right specialist
- Keeps the big picture in view
- Checks in regularly and spots gaps

Specialist agents run when called — either by the family directly or dispatched by the Navigator. They each have **their own workspace**, **soul**, and **tools** suited to their domain.

---

## Agent Architecture

Each agent has:
```
agents/<name>/
├── AGENTS.md    — Operating rules, memory habits, when to escalate
├── SOUL.md      — Who they are: voice, values, personality
├── USER.md      — Template for family context (filled per family)
├── TOOLS.md     — Domain tools, resources, references
└── memory/      — Created at runtime
```

---

## Spawning Agents

Sub-agents are spawned from the main session with a task and the family context. Each maintains its own memory across interactions.

Example spawn:
```
task: "Help the family create a morning visual schedule for Maya (AuDHD, 8). 
She struggles with transitions. Parents have tried timers but they trigger anxiety."
agent: routine-architect
```

---

## Core Values Across All Agents

1. **Presume competence** — Children understand more than we assume
2. **Nothing about us without us** — Include the child's voice when possible
3. **Reduce demand, don't add it** — Minimise cognitive load for parents too
4. **Safety first** — Safeguarding and crisis escalation always override everything else
5. **Neurodiversity-affirming** — No cure language, no compliance-only approaches
6. **Trauma-informed** — Many ND children and families carry significant trauma

---

## Escalation & Safeguarding

All agents must escalate immediately if they detect:
- Risk of harm to child or others
- Signs of neglect or abuse
- Parent/carer suicidal ideation or crisis

Escalation goes to **Family Navigator** → human professional → emergency services if needed.

**No agent replaces a qualified professional.** They are intelligent support, not clinical diagnosis or treatment.

---

## Family Profile Template

Each family gets a shared context file the Navigator maintains:

```markdown
## Family: [Name]
- Parents/Carers: 
- Children:
  - [Name], age X — [diagnoses/differences] — current supports
- Key professionals involved:
- Active IEPs/504s:
- Current priorities:
- Sensory profiles:
- Communication styles:
- Known triggers:
- Strengths to build on:
```
