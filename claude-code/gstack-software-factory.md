# gstack - Garry Tan 的 Claude Code 软件工程工厂

**原文：** gstack: Use Garry Tan's exact Claude Code setup  
**作者：** Garry Tan (@garrytan) - Y Combinator President & CEO  
**来源：** https://github.com/garrytan/gstack  
**翻译整理：** 2026-03-19  
**阅读时间：** 约 15 分钟  
**分类：** Claude Code / 工程效率 / AI 工具

---

## 📌 核心摘要

> gstack 是 Garry Tan 的开源软件工厂，将 Claude Code 变成你实际管理的虚拟工程团队——一个重新思考产品的 CEO、锁定架构的工程经理、发现 AI 垃圾的设计师、找出生产漏洞的偏执审查者、在真实浏览器中点击测试的 QA 主管，以及发布 PR 的发布工程师。15 个专家 + 6 个强大工具，全部作为斜杠命令，全部 Markdown，全部免费，MIT 许可。

**关键成就：**
- **60 天 60 万行代码** - 35% 是测试代码
- **日均 1-2 万行可用代码** - 作为 YC CEO 的兼职工作
- **1 人抵 20 人团队** - 同时运行 10-15 个并行冲刺

---

## 🚀 快速开始

### 30 秒安装

**要求：** [Claude Code](https://docs.anthropic.com/en/docs/claude-code), [Git](https://git-scm.com/), [Bun](https://bun.sh/) v1.0+

**安装命令：**
```bash
# 在 Claude Code 中粘贴
git clone https://github.com/garrytan/gstack.git ~/.claude/skills/gstack && cd ~/.claude/skills/gstack && ./setup
```

**添加 gstack 到当前项目：**
```bash
cp -Rf ~/.claude/skills/gstack .claude/skills/gstack && rm -rf .claude/skills/gstack/.git && cd .claude/skills/gstack && ./setup
```

**完成！** 然后添加 "gstack" 部分到 CLAUDE.md。

---

## 📊 15 个专家技能

### 思考阶段

| 技能 | 角色 | 职责 |
|------|------|------|
| **/office-hours** | YC Office Hours | 6 个强制问题，在写代码前重新定义产品 |
| **/plan-ceo-review** | CEO/创始人 | 重新思考问题，找到隐藏的 10 星产品 |
| **/plan-eng-review** | 工程经理 | 锁定架构、数据流、边界条件、测试 |
| **/plan-design-review** | 高级设计师 | 评分 0-10，编辑计划达到 10 分标准 |
| **/design-consultation** | 设计合作伙伴 | 从零构建完整设计系统 |

### 构建阶段

| 技能 | 角色 | 职责 |
|------|------|------|
| **/review** | 员工工程师 | 找出通过 CI 但在生产环境爆炸的漏洞 |
| **/investigate** | 调试器 | 系统性根因调试，铁律：无调查不修复 |
| **/design-review** | 会写代码的设计师 | 审计并修复设计问题 |
| **/qa** | QA 主管 | 在真实浏览器中测试、修复、生成回归测试 |
| **/qa-only** | QA 报告员 | 纯漏洞报告，不修改代码 |

### 发布阶段

| 技能 | 角色 | 职责 |
|------|------|------|
| **/ship** | 发布工程师 | 同步 main、运行测试、推送、开 PR |
| **/document-release** | 文档工程师 | 生成发布说明和文档 |
| **/retro** | 回顾分析 | 生成开发者统计数据和分析 |

### 辅助工具

| 技能 | 用途 |
|------|------|
| **/browse** | 网页浏览（替代 MCP Chrome 工具） |
| **/codex** | 代码探索和分析 |
| **/careful** | 谨慎模式，逐步确认 |
| **/freeze** | 冻结当前状态 |
| **/guard** | 添加保护检查 |
| **/unfreeze** | 解冻状态 |
| **/gstack-upgrade** | 升级 gstack |

---

## 💼 完整工作流示例

### 场景：构建每日简报应用

**你：** 我想为我的日历构建一个每日简报应用。

**你：** `/office-hours`

**Claude：**
```
[询问痛点 - 具体案例，而非假设]

你：多个 Google 日历、事件信息过时、地点错误。
    准备工作花很长时间，结果不够好...

Claude: 我要反驳你的框架。你说"每日简报应用"，
        但你实际描述的是个人首席助理 AI。
        
[提取 5 个你没意识到的能力]
[挑战 4 个前提 - 你同意、不同意或调整]
[生成 3 种实现方案，附带工作量估算]

推荐：明天发布最窄的切入点，从真实 usage 学习。
      完整愿景是 3 个月项目——从真正可用的每日简报开始。
      
[编写设计文档 → 自动流入下游技能]
```

**你：** `/plan-ceo-review`
```
[阅读设计文档，挑战范围，运行 10 节审查]
```

**你：** `/plan-eng-review`
```
[数据流的 ASCII 图、状态机、错误路径]
[测试矩阵、失败模式、安全考虑]
```

**你：** 批准计划，退出计划模式。
```
[编写 2400 行代码，跨越 11 个文件，约 8 分钟]
```

**你：** `/review`
```
[AUTO-FIXED] 2 个问题
[ASK] 竞争条件 → 你批准修复
```

**你：** `/qa https://staging.myapp.com`
```
[打开真实浏览器，点击流程，发现并修复漏洞]
```

**你：** `/ship`
```
测试：42 → 51 (+9 个新增)
PR: github.com/you/app/pull/42
```

---

## 🎯 核心洞察

### 洞察 1: 这不是 Copilot，这是团队

**你说：** "每日简报应用"  
**Agent 说：** "你在构建首席助理 AI"

**为什么？** 因为它倾听你的痛点，而非功能请求。然后：
- 挑战你的前提
- 生成 3 种方案
- 推荐最窄切入点
- 编写设计文档流入每个下游技能

**8 个命令完成一个完整冲刺。**

---

### 洞察 2: gstack 是流程，不是工具集合

**技能顺序遵循冲刺流程：**

```
思考 → 计划 → 构建 → 审查 → 测试 → 发布 → 反思
```

**每个技能流入下一个：**
- `/office-hours` 写的设计文档被 `/plan-ceo-review` 阅读
- `/plan-eng-review` 写的测试计划被 `/qa` 使用
- `/review` 发现的漏洞被 `/ship` 验证修复

**没有遗漏，因为每一步都知道前一步发生了什么。**

---

### 洞察 3: 并行冲刺是规模化的关键

**传统方式：**
```
1 个冲刺 → 30 分钟 → 1 个功能
```

**gstack 方式：**
```
10-15 个并行冲刺 → 30 分钟 → 10-15 个功能
```

**这就是 Garry Tan 作为 YC CEO 兼职工作，却能日均发布 1 万 + 行生产代码的秘诀。**

---

## 📋 详细技能说明

### /office-hours - YC 办公时间

**角色：** YC Office Hours

**做什么：**
- 6 个强制问题，在写代码前重新定义产品
- 反驳你的框架
- 挑战前提
- 生成实现替代方案
- 设计文档自动流入下游技能

**何时使用：** 任何新功能的起点

---

### /plan-ceo-review - CEO 审查

**角色：** CEO / 创始人

**做什么：**
- 重新思考问题
- 找到隐藏的 10 星产品
- 4 种模式：扩张、选择性扩张、保持范围、缩减

**何时使用：** 功能想法形成后

---

### /plan-eng-review - 工程审查

**角色：** 工程经理

**做什么：**
- 锁定架构
- 数据流图（ASCII）
- 状态机
- 边界条件
- 测试矩阵
- 失败模式
- 安全考虑

**何时使用：** CEO 审查批准后

---

### /review - 代码审查

**角色：** 员工工程师

**做什么：**
- 找出通过 CI 但在生产环境爆炸的漏洞
- 自动修复明显问题
- 标记完整性差距

**何时使用：** 代码编写完成后

---

### /qa - 质量保证

**角色：** QA 主管

**做什么：**
- 在真实浏览器中测试应用
- 发现并修复漏洞
- 原子提交
- 为每个修复生成回归测试

**何时使用：** 代码审查通过后

---

### /ship - 发布

**角色：** 发布工程师

**做什么：**
- 同步 main 分支
- 运行测试
- 审计覆盖率
- 推送代码
- 创建 PR

**何时使用：** QA 通过后

---

## 🛠️ 技术架构

### 文件结构

```
gstack/
├── skills/                 # 15 个专家技能
│   ├── office-hours/
│   ├── plan-ceo-review/
│   ├── plan-eng-review/
│   ├── plan-design-review/
│   ├── design-consultation/
│   ├── review/
│   ├── investigate/
│   ├── design-review/
│   ├── qa/
│   ├── qa-only/
│   ├── ship/
│   ├── document-release/
│   ├── retro/
│   ├── browse/
│   └── ...
├── tools/                  # 6 个强大工具
│   ├── codex/
│   ├── careful/
│   ├── freeze/
│   ├── guard/
│   ├── unfreeze/
│   └── gstack-upgrade/
├── setup                   # 安装脚本
└── CLAUDE.md.example       # 配置示例
```

### 工作原理

```
Claude Code → stdin JSON → gstack 技能 → stdout → 显示在终端
             ↘ transcript JSONL (工具、代理、待办)
```

**核心特性：**
- ✅ 所有技能都是 Markdown 文件
- ✅ 使用 Claude Code 原生技能 API
- ✅ 无需修改 PATH 或后台运行
- ✅ 真实文件提交到仓库（非 submodule）
- ✅ `git clone` 即可用

---

## 📊 Garry Tan 的成绩单

### 2026 年（60 天）

| 指标 | 数值 |
|------|------|
| **代码行数** | 600,000+ |
| **测试比例** | 35% |
| **日均产出** | 10,000-20,000 行可用代码 |
| **最近 7 天** | 140,751 行新增，362 次提交，~115k 净 LOC |
| **GitHub 贡献** | 1,237 次（持续增加） |

### 对比 2013 年

**2013 年：** 构建 Bookface（772 次贡献）  
**2026 年：** 1,237 次贡献并持续增长

**同一个人，不同时代。差异在于工具。**

---

## 💡 关键洞察

### 洞察 1: 工具改变生产力数量级

**Garry 的成就：**
- 作为 YC CEO 全职工作外的**兼职时间**
- 日均 1-2 万行**可用**代码（35% 测试）
- 同时运行 10-15 个并行冲刺

**核心：** 不是更努力工作，而是使用更好的工具。

---

### 洞察 2: 结构化角色 > 空白提示

**传统方式：**
```
"帮我写个功能..."
```

**gstack 方式：**
```
/office-hours → /plan-ceo-review → /plan-eng-review → 
/review → /qa → /ship
```

**每个角色都有明确职责和输出标准。**

---

### 洞察 3: 设计驱动开发

**gstack 的设计技能：**

| 技能 | 职责 |
|------|------|
| `/plan-design-review` | 评分 0-10，编辑计划达到 10 分 |
| `/design-consultation` | 从零构建完整设计系统 |
| `/design-review` | 审计并修复设计问题 |

**理念：** 设计不是事后添加，而是核心驱动力。

---

### 洞察 4: 铁律 - 无调查不修复

**/investigate 技能的核心原则：**

> "no fixes without investigation"

**调试流程：**
1. 追踪数据流
2. 测试假设
3. 3 次修复失败后停止

**避免：** 盲目修复、表面修复、引入新漏洞。

---

## 🔗 相关资源

**官方资源：**
- [GitHub 仓库](https://github.com/garrytan/gstack)
- [安装指南](https://github.com/garrytan/gstack#quick-start)
- [技能文档](https://github.com/garrytan/gstack/tree/main/skills)

**相关链接：**
- [Garry Tan X/Twitter](https://x.com/garrytan)
- [Y Combinator](https://www.ycombinator.com/)
- [Claude Code 文档](https://docs.anthropic.com/en/docs/claude-code)

---

## 📝 译者思考

### 与当前项目的关联

**1. ai-skill-bench 项目**

可以借鉴 gstack 的技能设计模式：
- **角色明确** - 每个技能有清晰职责
- **流程有序** - 思考→计划→构建→审查→测试→发布
- **质量保障** - 35% 测试代码，/qa 真实浏览器测试

**应用示例：**
```
ai-skill-bench 测试流程:
/office-hours → 定义测试目标
/plan-eng-review → 设计测试架构
/review → 审查测试代码
/qa → 实际运行测试
/ship → 发布测试结果
```

---

**2. agent-skills 项目**

可以直接学习 gstack 的 15 个专家角色：
- **思考类：** /office-hours, /plan-ceo-review
- **计划类：** /plan-eng-review, /plan-design-review
- **执行类：** /review, /investigate, /design-review
- **质量类：** /qa, /qa-only
- **发布类：** /ship, /document-release

**技能设计模板：**
```yaml
---
name: skill-name
description: 清晰描述角色和职责
metadata:
  pattern: expert-role
  domain: specific-domain
---

你是{角色}。你的职责是：
1. 职责 1
2. 职责 2
3. 职责 3

工作流程：
1. 步骤 1
2. 步骤 2
3. 步骤 3

输出标准：
- 标准 1
- 标准 2
```

---

**3. OpenClaw 工作区**

可以优化为类似 gstack 的工作流：
- **技能编排** - 按流程顺序组织技能
- **角色定义** - 每个技能有明确角色
- **质量保障** - 添加 /review 和 /qa 技能
- **发布流程** - 添加 /ship 技能

---

### 下一步行动

- [ ] 为 ai-skill-bench 添加 gstack 式工作流
- [ ] 创建 agent-skills/gstack-roles 技能包
- [ ] 学习 gstack 的技能设计模式
- [ ] 安装 gstack 体验实际效果
- [ ] 为 OpenClaw 设计类似的工作流编排

---

## 🎯 安装检查清单

**安装前：**
- [ ] 已安装 Claude Code
- [ ] 已安装 Git
- [ ] 已安装 Bun v1.0+

**安装步骤：**
- [ ] 运行安装命令
- [ ] 添加 gstack 到 CLAUDE.md
- [ ] 测试 /office-hours 技能
- [ ] 测试 /review 技能
- [ ] 测试 /qa 技能

**验收标准：**
- [ ] 5 分钟内完成首次运行
- [ ] 技能命令正常工作
- [ ] 理解工作流顺序

---

**最后更新：** 2026-03-19  
**分类：** Claude Code / 工程效率 / AI 工具  
**标签：** #gstack #ClaudeCode #工程效率 #AI 工具 #GarryTan  
**原文版权：** MIT License
