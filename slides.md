---
theme: default
highlighter: shiki
title: Vibe Coding Done Right
author: Julien Deray
drawings:
  persist: false
transition: slide-left
mdc: true
---

# Vibe Coding Done Right

## Applying Product Development Practices to AI-Assisted Development

<br>

Sprint Accelerator / FinTech House Lisbon

**Julien Deray** - Engineering Manager

---

# Icebreaker

<v-click>

## Who here has been relying primarily on AI to build their product?

</v-click>

<v-click>

<br>

### What's been your experience?

- The magic moments
- The pain points

</v-click>

<!--
Let them surface "it's fast!" and "it deleted my database" stories naturally.
This sets up the problem we're solving.
-->

---

# About Me

<br>

- Engineering Manager, former developer
- Mentor at Sprint Accelerator
- "I've seen how great teams ship great products—and how AI changes the game"

---

# What a Product Team Looks Like

<br>

```mermaid {scale: 0.9}
flowchart LR
    PM[Product Manager]
    D[Designer]
    DEV[Developers]
    EM[Engineering Manager]

    PM <--> D
    D <--> DEV
    DEV <--> EM
    PM <--> EM
```

<br>

<v-click>

**Key point:** Each role has specific responsibilities. AI can assist with many—but someone still needs to **think**.

</v-click>

---
layout: section
---

# Part 2: Understanding AI

---

# How AI Actually Works
### The 30-Second Version

<br>

```mermaid {scale: 0.8}
flowchart LR
    subgraph Context["Current Conversation"]
        A[Your prompt]
        B[Previous messages]
        C[System instructions]
    end

    Context --> AI[AI Model]
    AI --> O[Predicted Response]
```

<br>

<v-clicks>

- AI predicts "what word comes next" based on everything it's seen
- It has **NO memory**—only what's in the current conversation
- It can write endlessly, but quality depends on what you give it

</v-clicks>

---

# The Divergence Problem

<br>

```mermaid {scale: 0.7}
flowchart TD
    Input["Write me a snake game"]
    Input --> L1[Python?]
    Input --> L2[JavaScript?]
    Input --> L3[C++?]
    L1 --> C1[Pygame?]
    L1 --> C2[Terminal?]
    L2 --> C3[Canvas?]
    L2 --> C4[DOM?]
    L3 --> C5[SDL?]
    C1 --> D1[WASD?]
    C1 --> D2[Arrows?]
    C3 --> D3[Click?]

    style Input fill:#f96,stroke:#333
```

<v-click>

**"It works, but it's not YOUR vision"**

</v-click>

---

# Quality In = Quality Out

<br>

```mermaid {scale: 0.8}
flowchart LR
    I[Your Instructions] --> AI[AI]
    AI --> O[Output]

    style I fill:#4a9,stroke:#333
    style O fill:#4a9,stroke:#333
```

<br>

| Vague | Precise |
|-------|---------|
| "Write a snake game" | "Write a snake game like Nokia 3310, arrow controls, wrap-around screen, pixel art style, score counter top-right" |
| Generic result | Exactly what you imagined |

<v-click>

**The AI is as precise as your instructions**

</v-click>

---

# AI Can't Imagine Something New

<br>

<v-clicks>

- AI was trained on what **already exists**
- You're building something **NEW**—that vision must come from **YOU**
- AI is a powerful executor, not a visionary

</v-clicks>

<br>

<v-click>

> "Spending 3 hours thinking before prompting beats spending 3 seconds"

</v-click>

---
layout: section
---

# Part 3: The Documentation-Centric Model

---

# The Problem with Conversations

<br>

<v-clicks>

- You can't have one infinite conversation with AI
- Context limits → AI starts **forgetting**
- Every new conversation = starting from zero

</v-clicks>

<br>

<v-click>

### "What if we could give AI perfect memory?"

</v-click>

---

# Documentation as the AI's Brain

<br>

```mermaid {scale: 0.6}
flowchart TD
    subgraph BRAIN["Documentation Hub"]
        V[Vision]
        A[Architecture]
        F[Features]
        G[Guidelines]
    end

    PM --> |Updates| BRAIN
    BRAIN --> |Reads| DEV
    DEV --> |Updates| BRAIN
    BRAIN --> |Reads| PM
```

<br>

<v-click>

**"Your docs ARE your product's brain"**

</v-click>

---

# Minimum Viable Documentation

<br>

What you need at MVP stage:

<v-clicks>

1. **Vision document** - What are we building? For whom? Why?
2. **User personas** - Who exactly uses this?
3. **Feature catalogue** - What exists, what's planned
4. **Architecture overview** - How the pieces fit together
5. **Development guidelines** - Conventions, patterns, constraints

</v-clicks>

<br>

<v-click>

**"Start simple. Update constantly."**

</v-click>

---

# The Double Diamond

<br>

```mermaid {scale: 0.7}
flowchart LR
    subgraph D1["Discover"]
        A1[Research]
        A2[Explore]
    end
    subgraph D2["Define"]
        B1[Synthesize]
        B2[Focus]
    end
    subgraph D3["Develop"]
        C1[Ideate]
        C2[Prototype]
    end
    subgraph D4["Deliver"]
        E1[Test]
        E2[Implement]
    end

    D1 --> D2
    D2 --> D3
    D3 --> D4

    style D1 fill:#e6f3ff
    style D2 fill:#cce6ff
    style D3 fill:#e6f3ff
    style D4 fill:#cce6ff
```

<br>

**Product development is about diverging (exploring) then converging (deciding)**

---

# The PM-Doc-Dev Loop

<br>

```mermaid {scale: 0.7}
flowchart LR
    subgraph PM["PM (Human + AI)"]
        P1[Think]
        P2[Validate]
    end

    subgraph DOCS["Documentation"]
        D1[PRD]
        D2[Architecture]
        D3[Features]
    end

    subgraph DEV["Dev (Human + AI)"]
        E1[Read]
        E2[Implement]
        E3[Update]
    end

    PM -->|writes PRD| DOCS
    DOCS -->|reads docs| DEV
    DEV -->|updates docs| DOCS
    DOCS -->|reads updates| PM
```

<br>

<v-click>

**Humans are ALWAYS in the loop—reading, validating, testing, deciding**

</v-click>

---

# The PRD is Everything

<br>

**"The PRD is your contract with the AI developer"**

<div class="grid grid-cols-2 gap-4">

<v-clicks>

1. Problem statement (why?)
2. Context (what exists?)
3. Proposed solution (high-level)
4. User workflow (step by step)
5. Acceptance criteria (how do we know it's done?)
6. Technical context (constraints)
7. Goals and non-goals (scope)
8. Open questions (unclear items)

</v-clicks>

</div>

<br>

<v-click>

*"I'll show you a real example in the demo"*

</v-click>

---

# The Feedback Loop

<br>

After AI implements:

<v-clicks>

1. Human **tests** the result
2. Human **validates** against PRD
3. Dev (or AI) **updates documentation** with decisions made
4. PM **reads** updated docs before next PRD

</v-clicks>

<br>

<v-click>

**"This loop is what keeps quality high"**

</v-click>

---
layout: section
---

# Part 4: Practical Considerations

---

# Environments Matter

<br>

```mermaid {scale: 0.9}
flowchart LR
    DEV[DEV] --> STAGING[STAGING] --> PROD[PRODUCTION]

    style DEV fill:#4a9,stroke:#333
    style STAGING fill:#fa4,stroke:#333
    style PROD fill:#f44,stroke:#333
```

<br>

<v-clicks>

- "AI has a tendency to delete databases"
- **Never let AI touch production directly**
- Always have a place to experiment safely

</v-clicks>

---

# Testing (Work in Progress)

<br>

Honest take: **"I'm still refining this myself"**

<br>

<v-clicks>

But even imperfect testing is better than none:

- Make AI write tests for every feature
- Run tests before every deployment
- When you find a bug manually, make AI write a test for it

</v-clicks>

<br>

<v-click>

**"The goal: catch regressions before your users do"**

</v-click>

---
layout: section
---

# Part 5: Live Demo

---

# Demo Introduction

<br>

"Let me show you this in action"

<v-clicks>

- Wealth management app context
- Documentation structure walkthrough
- Watch how much context the AI receives

</v-clicks>

<br>

<v-click>

### Demo Flow:
1. Show existing documentation
2. PRD for a small feature
3. Feed PRD + docs to AI
4. AI generates implementation plan
5. AI implements (questions welcome!)
6. Review output together
7. Update docs with what was built

</v-click>

---

# What You Just Saw

<br>

<v-clicks>

- The **amount of context** that went in
- The **precision** of the output
- The **human checkpoints** throughout

</v-clicks>

<br>

<v-click>

**"This is vibe coding with discipline"**

</v-click>

---
layout: section
---

# Part 6: Key Takeaways

---

# Key Takeaways

<br>

<v-clicks>

1. **Quality input = Quality output**
   - The fundamental truth

2. **AI replaces typing, not thinking**
   - You still need product discipline

3. **Documentation is your AI's brain**
   - Keep it fresh, keep it precise

4. **Humans stay in the loop**
   - Test, validate, decide

</v-clicks>

---

# Your Monday Action

<br>

## "Document your work"

<br>

<v-click>

Start with:

- Vision
- Persona
- Current State
- Next Feature

</v-click>

<br>

<v-click>

**"If you can explain it clearly in writing, AI can help you build it"**

</v-click>

---

# Office Hours

<br>

## I'm available for 1:1 guidance on your specific setup

<br>

<v-click>

**Let's make this work for YOUR product**

</v-click>

---
layout: center
class: text-center
---

# Q&A

<br>

## What questions do you have?
