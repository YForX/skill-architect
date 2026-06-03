<div align="center">

[中文](#-skill-architect) · [English](./README.en.md)

# 🏗️ Skill Architect

#### Skill 创建的策略层 — 先调研论证，再动手写代码

[![License](https://img.shields.io/badge/License-MIT-3B82F6?style=for-the-badge)](./LICENSE)
[![AgentSkills](https://img.shields.io/badge/AgentSkills-Standard-8B5CF6?style=for-the-badge)](https://agentskills.io)

![Claude Code](https://img.shields.io/badge/Claude_Code-Skill-D97706?style=flat-square&logo=anthropic&logoColor=white)

</div>

---

## ✨ Skill Architect

> *"不是每个需求都值得写一个 Skill。先退一步问：该不该做？别人怎么做的？我们走哪条路？"*

很多人一有想法就扑进去写 Skill，写完才发现市面上已经有更好的、或者根本不需要 Skill 就能解决。**Skill Architect 就是拦住你，让你先想清楚再动手的那个角色。**

它负责 Skill 创建的**策略阶段**：需求反思 → 竞品调研 → 三路方案对比。分析完成后移交 [skill-creator](https://github.com/YeYueXingl/skill-creator) 进入实现。

### 与 skill-creator 的分工

```
skill-architect（你）                    skill-creator
┌─────────────────────────┐           ┌──────────────────────┐
│ ① 需求反思              │           │ Draft → Test →       │
│ ② 竞品调研（含跨领域）  │ ──移交──→ │ Review → Iterate     │
│ ③ 三路方案对比          │           │ → Package            │
└─────────────────────────┘           └──────────────────────┘
    「该不该做？                  「怎么做出来？
    别人怎么做的？                 怎么验证做好？」
    我们选哪条路？」
```

### 三阶段工作流

| 阶段 | 做什么 | 产出 |
|------|--------|------|
| ① **需求反思** | 退一步问：这真的需要 Skill 吗？Prompt 模板 / Hook / 脚本是不是就够了？ | 反思结论：✅ 需要 / ❌ 更简单方案 |
| ② **竞品调研** | 搜同领域 2-5 个直接竞品 + 1-2 个跨领域 Skill，分析亮点/不足/可迁移点 | 竞品对比表 + 调研总结 |
| ③ **方案对比** | 三条路：A 拿来改 / B 融合创新 / C 原生设计，对比矩阵选最优 | 推荐方案 + 架构决策 |

### 怎么触发

```
帮我创建一个 Skill 来做 X
我想写一个 Skill 来处理 Y
先调研一下 X 领域有没有现成的 Skill
分析一下这个需求适不适合做成 Skill
```

**⚠️ 注意**：如果需求很简单（单步、< 30 行、无依赖），Skill Architect 会直接告诉你「这不需要新建 Skill」，省你的时间。

### 适合

- 想写一个新 Skill，但不确定该怎么做
- 不确定这个需求适不适合做成 Skill
- 想做竞品调研，看看别人怎么做的
- 在多个方案之间纠结

### 不适合

- 已经想清楚要怎么写、不需要调研 → 直接用 [skill-creator](https://github.com/YeYueXingl/skill-creator)
- 快速小修改、需求极简单 → 直接写就行

**🌐 跨平台**：Claude Code

---

## 📦 安装

在 Claude Code 里直接说：

```
帮我安装这个 skill：https://github.com/YeYueXingl/skill-architect
```

或者用命令行：

```bash
npx skills add YeYueXingl/skill-architect
```

---

## 📁 文件结构

```
skill-architect/
├── SKILL.md                              # Skill 主文件
├── README.md                             # 就是你在看的这个
├── LICENSE                               # MIT
└── references/
    ├── research-methodology.md           # 搜索策略详解
    └── comparison-template.md            # 三路方案对比模板
```

→ [SKILL.md](./SKILL.md)

---

<div align="center">

[MIT License](./LICENSE) · 自由使用 / 修改 / 再分发

Made by [@YeYueXingl](https://github.com/YeYueXingl)

</div>
