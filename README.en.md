<div align="center">

[中文](./README.md) · **English**

# 🏗️ Skill Architect

#### Strategy layer for Skill creation — research and reason before you write a single line

[![License](https://img.shields.io/badge/License-MIT-3B82F6?style=for-the-badge)](./LICENSE)
[![AgentSkills](https://img.shields.io/badge/AgentSkills-Standard-8B5CF6?style=for-the-badge)](https://agentskills.io)

![Claude Code](https://img.shields.io/badge/Claude_Code-Skill-D97706?style=flat-square&logo=anthropic&logoColor=white)

</div>

---

## ✨ Skill Architect

> *"Not every idea needs a Skill. Take a step back first: should we even build this? What already exists? Which path do we take?"*

Most people jump straight into writing a Skill the moment they have an idea — only to find out later that someone already built a better one, or that the whole thing could've been a two-line prompt template. **Skill Architect stops you at the gate and makes you think first.**

It handles the **strategy phase** of Skill creation: necessity reflection → competitive research → three-way approach comparison. Once the analysis is done, it hands off to [skill-creator](https://github.com/YeYueXingl/skill-creator) for implementation.

### Division of labor with skill-creator

```
skill-architect (you're here)            skill-creator
┌─────────────────────────┐           ┌──────────────────────┐
│ ① Necessity Reflection   │           │ Draft → Test →       │
│ ② Competitive Research   │ ──handoff─→│ Review → Iterate    │
│ ③ Approach Comparison    │           │ → Package            │
└─────────────────────────┘           └──────────────────────┘
    "Should we build it?                  "How to build it?
    What's already out there?              How to prove it works?"
    Which approach to take?"
```

### Three-phase workflow

| Phase | What it does | Output |
|-------|-------------|--------|
| ① **Necessity Reflection** | Pause and ask: does this really need a Skill? Would a prompt template / hook / script suffice? | Verdict: ✅ Build / ❌ Simpler solution |
| ② **Competitive Research** | Search 2–5 direct competitors in-domain + 1–2 cross-domain Skills; analyze strengths, gaps, and transferable patterns | Comparison table + research summary |
| ③ **Approach Comparison** | Three paths: A — adapt an existing Skill / B — fuse ideas from multiple Skills / C — design from scratch. Matrix comparison to pick the winner | Recommended approach + architecture decision |

### How to trigger

```
Create a skill for X
Build a skill that does Y
Research what existing skills cover X
Is this worth making into a skill?
先调研一下再写
分析一下这个需求适不适合做成 Skill
```

**⚠️ Note**: If the requirement is trivial (single step, < 30 lines, no dependencies), Skill Architect will tell you straight up — don't bother. That saves you time.

### Good for

- You want to write a new Skill but aren't sure how to approach it
- You're unsure if the idea even warrants a Skill
- You want competitive research before building
- You're torn between multiple design approaches

### Not good for

- You already know exactly what to build and don't need research → use [skill-creator](https://github.com/YeYueXingl/skill-creator) directly
- Quick tweaks, extremely simple needs → just write it

**🌐 Cross-platform**: Claude Code

---

## 📦 Install

In any agent that supports Skills, just say:

```
Install this skill: https://github.com/YeYueXingl/skill-architect
```

Or install via CLI:

```bash
npx skills add YeYueXingl/skill-architect
```

---

## 📁 File structure

```
skill-architect/
├── SKILL.md                              # Main skill definition
├── README.md                             # 中文 readme
├── README.en.md                          # English readme (you're reading it)
├── LICENSE                               # MIT
└── references/
    ├── research-methodology.md           # Search strategy & evaluation criteria
    └── comparison-template.md            # Three-way approach comparison template
```

→ [SKILL.md](./SKILL.md)

---

<div align="center">

[MIT License](./LICENSE) · Free to use, modify, and redistribute

Made by [@YeYueXingl](https://github.com/YeYueXingl)

</div>
