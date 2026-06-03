---
name: skill-architect
description: Skill creation strategist — research, reflection, and approach comparison BEFORE writing any skill. Use when the user wants to create a skill but needs to first determine: (1) whether a skill is even the right solution, (2) what existing skills already cover this space, and (3) which architectural approach to take. Triggers on phrases like "create a skill for X", "build a skill that does X", "I want a skill to handle X", especially when the user hasn't yet determined the best approach or when the task is complex enough to warrant research. After strategy is complete, hands off to skill-creator for implementation. Do NOT use for quick/simple skill creation where the approach is already obvious — use skill-creator directly instead. Also trigger when the user explicitly says "skill-architect", "先调研一下", or asks to research skills before building.
---

# Skill Architect

Skill 创建的**策略层**——在写任何代码之前，先回答三个问题：

1. **该不该做？** — 这个需求真的需要 Skill 吗？
2. **别人怎么做的？** — 市面上已有哪些同类型 Skill？有什么可借鉴的？
3. **我们走哪条路？** — 拿来改、融合创新、还是从零设计？

完成策略分析后，**移交 skill-creator** 进入执行（Draft → Test → Review → Iterate）。

## 与 skill-creator 的分工

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

**关键边界**：skill-architect 不做测试、不跑 eval、不写最终 Skill 草稿。它的产出是一个**经过调研论证的架构决策**，然后交给 skill-creator 落地。

---

## 三阶段工作流

### 阶段 ①：需求反思（Necessity Reflection）

用户表达「想做一个 Skill」时，不直接开始设计。先退一步问：**这真的需要 Skill 吗？**

#### 反思检查清单

按优先级依次考虑：

| 优先级 | 替代方案 | 什么时候够用 |
|--------|----------|--------------|
| 1 | **Prompt 模板 / alias** | 任务固定、无需多步骤决策、可复用一段指令即可 |
| 2 | **Claude Code Hook** | 需要在特定时机自动触发（如保存后格式化、提交前检查） |
| 3 | **独立脚本 + 简短说明** | 核心逻辑是确定性代码，Claude 只需知道怎么调用 |
| 4 | **已有 Skill 微调** | 市面上有接近的 Skill，改几行就能用 |
| 5 | **确实需要新 Skill** | 以上都不够，任务需要复杂工作流 + 领域知识 + 多文件资源 |

#### 用网络搜索验证

对于方案 4 和 5，**用 WebSearch 搜索**该问题域的最佳实践：
- 「how to do X efficiently」
- 「best approach for X automation」
- 该领域的常用工具链是什么？

如果搜索结果指向某个成熟工具/方法而非 Skill，将其作为替代方案列出。

#### 输出格式

```markdown
## 需求反思

**原始需求**：[用户的一句话描述]

**反思结论**：✅ 需要新建 Skill / ❌ 有更简单方案

**如果不需要 Skill**：
- 推荐替代方案：[具体方案]
- 理由：[为什么这样就够了]

**如果需要 Skill**：
- 核心理由：[为什么简单方案不够]
- 关键挑战：[这个 Skill 最难做对的是什么]
```

---

### 阶段 ②：竞品调研（Competitive Landscape Research）

确认需要 Skill 后，搜索市面上已有的同类 Skill。

#### 搜索工具

按优先级使用：

| 工具 | 命令 | 特点 |
|------|------|------|
| `npx skills` | `npx skills find "<关键词>"` | 按安装量排序 |
| `findskill` | `findskill search "<关键词>"` | 按 GitHub star 排序 |
| WebSearch | 搜索 `claude skill <关键词> site:skills.sh` | 兜底方案 |
| GitHub 搜索 | 搜索 `claude-skill-<关键词>` 仓库 | 找未上架的 |

参考 skill-discovery.md 中的场景词表确定搜索关键词。

#### 调研范围：两级搜索

| 轮次 | 目标 | 数量 | 目的 |
|------|------|------|------|
| **同领域** | 直接竞品 | 2-5 个（弹性） | 了解同行的做法、模式、取舍 |
| **跨领域** | 思维破圈 | 1-2 个 | 完全不同领域但有可迁移的设计模式 |

**跨领域选取标准**：
- 不看功能是否相似，看**设计模式是否可迁移**
- 例 1：做「代码审查 Skill」→ 跨领域看「医疗诊断 Skill」→ 借鉴「检查清单 + 严重等级 + 处方建议」模式
- 例 2：做「PDF 处理 Skill」→ 跨领域看「图像处理管线 Skill」→ 借鉴「多阶段管线 + 降级策略」模式

#### 每个 Skill 的分析维度

对搜索到的每个 Skill，按以下维度分析（详细信息见 `references/research-methodology.md`）：

```
┌──────────────┬─────────────────────────────────────────┐
│ 基本信息      │ 名称、来源 URL、安装量/star、最后更新    │
│ 核心工作流    │ 分几步？每步做什么？输入/输出？          │
│ 架构设计      │ 文件结构？脚本/参考/资产怎么组织的？     │
│ 亮点/优势     │ 什么做法值得借鉴？                       │
│ 不足/缺陷     │ 缺了什么？哪里做得不好？                 │
│ 可迁移思路    │ 对我们有什么启发？（最重要的维度）        │
└──────────────┴─────────────────────────────────────────┘
```

#### 输出格式

```markdown
## 竞品调研

### 同领域 Skill

| # | Skill 名称 | 来源 | 核心思路 | 亮点 | 不足 | 可迁移启发 |
|---|-----------|------|---------|------|------|-----------|
| 1 | ... | ... | ... | ... | ... | ... |
| 2 | ... | ... | ... | ... | ... | ... |
| ... | ... | ... | ... | ... | ... | ... |

### 跨领域 Skill

| # | Skill 名称 | 领域 | 为什么跨领域看它 | 可迁移模式 |
|---|-----------|------|-----------------|-----------|
| 1 | ... | ... | ... | ... |
| 2 | ... | ... | ... | ... |

### 调研总结

- **同领域共识做法**：[大家都这么做的事情]
- **同领域分歧点**：[各家做法不同的地方]
- **同领域盲区**：[大家都忽略的地方]
- **跨领域启发**：[从别的领域学到了什么]
```

---

### 阶段 ③：三路方案对比（Approach Comparison）

基于调研结果，产出三种架构方案的**摘要对比**（每种 5-10 行，不写完整 Skill）。

#### 三种方案

| 方案 | 代号 | 思路 | 适合场景 |
|------|------|------|----------|
| **A** | 拿来主义 | 以最好的已有 Skill 为基础，列出保留/修改/删除项 | 已有高质量 Skill，只需定制 |
| **B** | 融合创新 | 吸收 2+ 个 Skill 的优点（含跨领域启发），取长补短 | 多个 Skill 各有所长，融合产生新方案 |
| **C** | 原生设计 | 吸收所有调研洞察，但从零设计全新架构 | 现有方案都不够好，或需求非常特殊 |

#### 每个方案摘要的结构

```markdown
### 方案 X：[名称]

**核心思路**：[一句话概括]

**关键设计决策**：
- [决策 1 及理由]
- [决策 2 及理由]

**预计结构**：[简述文件组织]

**优势**：
- [优势 1]
- [优势 2]

**劣势**：
- [劣势 1]
- [劣势 2]

**预计工作量**：[小/中/大]
```

#### 完整对比矩阵

最后用一个矩阵表做总结：

```markdown
### 方案对比矩阵

| 维度 | 方案 A: 拿来 | 方案 B: 融合 | 方案 C: 原生 |
|------|:-----------:|:-----------:|:-----------:|
| 开发成本 | 低 | 中 | 高 |
| 可维护性 | 依赖上游 | 中 | 自主可控 |
| 创新程度 | 低 | 中 | 高 |
| 适配度 | 中 | 高 | 最高 |
| 风险 | 上游停更 | 整合复杂 | 从头造轮子 |
| **推荐场景** | 需求标准、已有好轮子 | 借鉴点多、取各家之长 | 需求特殊、现有方案不够好 |

**推荐**：[方案 X]，理由：[一句话]
```

使用 `references/comparison-template.md` 中的模板确保格式一致。

---

## 移交 skill-creator

完成三阶段分析后，**必须**向用户建议移交：

> 「方向已定。现在需要 skill-creator 来写草稿、跑测试、迭代改进了。要我切换到 skill-creator 继续，还是先在这个策略上讨论/调整？」

- 如果用户确认 → 建议用户调用 skill-creator，并传递本阶段的分析结论作为上下文
- 如果用户想调整 → 回到对应阶段修改
- 如果用户想直接在这里写 Skill → 可以写初稿，但**不要做测试**（那是 skill-creator 的领域）

---

## 沟通原则

与 skill-creator 一样，注意用户的背景差异：

1. **不要假设用户知道什么是「Skill 生态」**——如果用户看起来不熟悉，简要解释 `npx skills` 和 skills.sh 是什么
2. **调研结果要解释「为什么这个值得关注」**——不只列事实，给出判断
3. **尊重用户的领域知识**——用户可能比搜索结果更懂自己的需求。搜索到的 Skill 只是参考，不是标准答案
4. **控制节奏**——每个阶段完成后等用户确认，不要连续推完三个阶段

---

## 快速决策（跳过流程）

以下情况可以跳过部分或全部流程：

| 情况 | 处理方式 |
|------|----------|
| 需求极其简单（单步、无依赖、< 30 行） | 直接告诉用户「这不需要 skill-architect，用 skill-creator 即可」 |
| 用户已有明确设计思路 | 跳过阶段 ①，只做竞品验证（阶段 ②）看看有没有遗漏 |
| 用户赶时间 | 简化：需求反思减为 2 个问题（必须用 Skill？有没有现成的？），竞品搜 2 个即可，跳过跨领域 |
| 用户说「就按我說的做」 | 尊重用户判断，直接进入 skill-creator |

---

## 参考文件

- `references/research-methodology.md` — 搜索策略详解、评估维度、质量标准
- `references/comparison-template.md` — 三路方案对比输出模板
