# Garry Tan gstack - 开源软件工厂

**原文：** garrytan/gstack  
**作者：** Garry Tan (YC CEO)  
**来源：** https://github.com/garrytan/gstack  
**整理日期：** 2026-03-21  
**分类：** AI Agent/开发工具

---

## 📌 核心摘要

> gstack 是 Garry Tan 的开源软件工厂，将 Claude Code 变成虚拟工程团队。包含 15 个专家角色和 6 个权力工具，全部通过 slash 命令实现。Garry 在过去 60 天用 gstack 编写了**60 万行生产代码**（35% 测试），日均**1-2 万行可用代码**，同时担任 YC CEO。

**关键要点：**
1. **15 个专家角色** - CEO、Eng Manager、Designer、QA 等
2. **6 个权力工具** - /browse, /careful, /freeze, /guard 等
3. **完整 Sprint 流程** - Think → Plan → Build → Review → Test → Ship → Reflect
4. **并行执行** - 可同时运行 10-15 个 sprint
5. **MIT 开源** - 完全免费，支持 Claude Code/Codex/Gemini CLI/Cursor

---

## 🚀 核心成就

### Garry 的代码产出（2026）

| 指标 | 数值 |
|------|------|
| **60 天代码量** | 600,000+ 行 |
| **测试占比** | 35% |
| **日均产出** | 10,000 - 20,000 行 |
| **最近 7 天** | 140,751 行新增，362 commits |
| **2026 贡献** | 1,237 contributions |

**对比：** 2013 年构建 Bookface 时 772 contributions（同年）

---

## 🎯 15 个专家角色

### Sprint 流程

**Think → Plan → Build → Review → Test → Ship → Reflect**

| 技能 | 专家角色 | 功能 |
|------|---------|------|
| `/office-hours` | **YC Office Hours** | 重新定义问题，挑战前提，生成 3 种实现方案 |
| `/plan-ceo-review` | **CEO/Founder** | 重新思考问题，找到 10 星产品 |
| `/plan-eng-review` | **Eng Manager** | 锁定架构、数据流、测试计划 |
| `/plan-design-review` | **Senior Designer** | 设计评审，AI Slop 检测，0-10 评分 |
| `/design-consultation` | **Design Partner** | 从零构建完整设计系统 |
| `/review` | **Staff Engineer** | 查找通过 CI 但会在生产环境爆炸的 bug |
| `/investigate` | **Debugger** | 系统性根因调试，Iron Law: 无调查不修复 |
| `/design-review` | **Designer Who Codes** | 设计审计并修复 |
| `/qa` | **QA Lead** | 真实浏览器测试，发现并修复 bug |
| `/qa-only` | **QA Reporter** | 纯 bug 报告，不修改代码 |
| `/ship` | **Release Engineer** | 同步 main、运行测试、推送、开 PR |
| `/document-release` | **Technical Writer** | 更新所有文档匹配新发布 |
| `/retro` | **Eng Manager** | 团队感知周回顾，个人分解 |
| `/browse` | **QA Engineer** | 真实 Chromium 浏览器，真实点击 |
| `/setup-browser-cookies` | **Session Manager** | 导入真实浏览器 Cookie |

---

## 🔧 6 个权力工具

| 工具 | 功能 |
|------|------|
| `/codex` | **Second Opinion** - OpenAI Codex 独立代码审查 |
| `/careful` | **Safety Guardrails** - 破坏性命令警告 |
| `/freeze` | **Edit Lock** - 限制文件编辑到单一目录 |
| `/guard` | **Full Safety** - /careful + /freeze |
| `/unfreeze` | **Unlock** - 移除/freeze 边界 |
| `/gstack-upgrade` | **Self-Updater** - 自动升级到最新版 |

---

## 📖 使用示例

### 构建每日简报应用

```
You:    我想构建一个每日简报应用，用于日历管理。
You:    /office-hours
Claude: [询问痛点 - 具体案例，非假设]

You:    多个 Google 日历，活动信息过时，地点错误。
        准备工作耗时且结果不够好...

Claude: 我要挑战你的框架。你说"每日简报应用"，
        但你实际描述的是个人首席 AI 助理。
        [提取 5 个你未意识到的能力]
        [挑战 4 个前提 - 你同意/不同意/调整]
        [生成 3 种实现方案及工作量估算]
        建议：明日发布最窄楔形，从真实使用学习。
        [编写设计文档 → 自动输入下游技能]

You:    /plan-ceo-review
        [阅读设计文档，挑战范围，运行 10 部分评审]

You:    /plan-eng-review
        [数据流 ASCII 图、状态机、错误路径]
        [测试矩阵、失败模式、安全考虑]

You:    批准计划，退出计划模式。
        [编写 2,400 行代码，11 个文件，约 8 分钟]

You:    /review
        [自动修复] 2 个问题。[询问] 竞态条件 → 你批准修复。

You:    /qa https://staging.myapp.com
        [打开真实浏览器，点击流程，发现并修复 bug]

You:    /ship
        测试：42 → 51 (+9 新增)。PR: github.com/you/app/pull/42
```

**结果：** 8 个命令，30 分钟完成原本需要 20 人团队的工作。

---

## 💡 核心创新

### 1. /office-hours 重新定义产品

**传统方式：** 用户说功能 → Agent 写代码

**gstack 方式：**
1. 倾听真实痛点（非假设）
2. 挑战框架（你说 A，实际需要 B）
3. 挑战前提（为什么需要这个？）
4. 生成 3 种方案（窄/中/宽）
5. 推荐最窄楔形（明日可发布）
6. 编写设计文档（自动输入下游）

**价值：** 避免构建错误产品，节省数周时间

---

### 2. 设计为核心

**/design-consultation 不只是选字体：**
- 研究竞品
- 提出安全选择 + 创意风险
- 生成真实产品 mockup
- 编写 DESIGN.md
- 设计决策贯穿整个系统

---

### 3. /qa 是重大突破

**能力：**
- 打开真实浏览器
- 点击测试流程
- 发现并修复 bug
- 自动生成回归测试

**影响：** Garry 从 6 个并行 worker 提升到 12 个

---

### 4. 智能评审路由

**类似创业公司：**
- CEO 不看 infra bug 修复
- 设计评审不参与后端变更
- gstack 追踪已运行的评审
- 自动判断需要什么评审
- Review Readiness Dashboard 显示状态

---

### 5. 测试一切

**策略：**
- `/ship` 从零启动测试框架（如无）
- 每次`/ship` 生成覆盖率审计
- 每次`/qa` bug 修复生成回归测试
- **目标：100% 测试覆盖率**

**理念：** 测试让 vibe coding 安全，而非 yolo coding

---

## 🔗 OpenClaw 可借鉴

### 1. 专家角色系统

**当前状态：** 单 Agent 执行

**改进方向：**
```yaml
agents:
  - role: ceo
    skill: plan-ceo-review
    trigger: "重新思考问题"
  - role: eng-manager
    skill: plan-eng-review
    trigger: "架构设计"
  - role: designer
    skill: design-consultation
    trigger: "设计评审"
  - role: qa-lead
    skill: qa
    trigger: "测试验证"
```

### 2. Sprint 流程

**当前状态：** 无明确流程

**改进方向：**
```
Think (09:00) → Plan (09:30) → Build (10:00) → 
Review (14:00) → Test (15:00) → Ship (16:00) → 
Reflect (18:00)
```

### 3. Slash Commands

**当前状态：** 技能手动触发

**改进方向：**
```
/office-hours - 重新定义问题
/plan - 架构设计
/review - 代码审查
/qa - 测试验证
/ship - 发布
```

### 4. 并行执行

**当前状态：** 单任务执行

**改进方向：**
- 支持 10-15 个并行 sprint
- 不同功能、不同分支、不同 Agent
- 统一 Dashboard 管理

### 5. 设计文档驱动

**当前状态：** 直接编码

**改进方向：**
```
/office-hours → DESIGN.md
/design-consultation → DESIGN.md
/plan-eng-review → 读取 DESIGN.md
```

---

## 📝 下一步行动

### 立即实践

- [ ] 安装 gstack 到本地
- [ ] 测试/office-hours 命令
- [ ] 学习 15 个专家角色设计
- [ ] 研究 Sprint 流程实现

### OpenClaw 改进计划

- [ ] 设计专家角色系统
- [ ] 实现 Sprint 流程
- [ ] 创建 Slash Commands
- [ ] 支持并行执行
- [ ] 设计文档驱动开发

---

## 🔗 相关资源

**官方资源：**
- GitHub: https://github.com/garrytan/gstack
- 文档：https://github.com/garrytan/gstack/blob/main/docs/skills.md
- 安装指南：`git clone https://github.com/garrytan/gstack.git ~/.claude/skills/gstack`

**关键链接：**
- SKILL.md 标准：https://github.com/anthropics/claude-code
- Garry Tan Twitter: https://x.com/garrytan

**延伸阅读：**
- [Anthropic Agent Skills](./anthropic-introduction-to-agent-skills.md)
- [Andrew Ng ContextHub](./andrewyng-context-hub.md)
- [e2b Awesome AI Agents](./e2b-awesome-ai-agents.md)

---

**最后更新：** 2026-03-21  
**分类：** ai-agents  
**标签：** #gstack #ClaudeCode #AIAgents #GarryTan #YC #SoftwareFactory  
**原文版权：** MIT License
