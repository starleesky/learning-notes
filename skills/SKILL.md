---
name: multi-agent-coordinator
description: |
  多 Agent 协作管理器 - 参考 gstack 的 15 个专家角色。
  
  TRIGGER WHEN:
  - 复杂任务需要多专家协作
  - 并行执行多个 sprint
  - 需要 CEO/Eng Manager/Designer/QA 等角色评审
  
  功能:
  - 15 个专家角色定义
  - Sprint 流程管理 (Think → Plan → Build → Review → Test → Ship)
  - 并行执行 10-15 个 sprint
  - 智能评审路由
  - Review Readiness Dashboard
  
  输出:
  - 专家角色分配
  - Sprint 进度追踪
  - 评审报告

metadata:
  pattern: pipeline
  steps: "7"
  requires: { anyBins: ["opencli", "tmux"] }
  openclaw: { emoji: "🎯" }
  version: "1.0"
  created: "2026-03-21"
  reference: "garrytan/gstack"
---

# 🎯 多 Agent 协作管理器 v1.0

**版本：** v1.0  
**创建：** 2026-03-21  
**参考：** Garry Tan gstack (15 个专家角色)

---

## 📋 专家角色系统

### 核心流程

**Think → Plan → Build → Review → Test → Ship → Reflect**

### 15 个专家角色

| 角色 | 技能 | 职责 | 触发条件 |
|------|------|------|---------|
| **CEO/Founder** | plan-ceo-review | 重新定义问题，找到 10 星产品 | 新任务/需求模糊 |
| **Eng Manager** | plan-eng-review | 锁定架构、数据流、测试计划 | 技术方案设计 |
| **Senior Designer** | plan-design-review | 设计评审，AI Slop 检测 | UI/UX 相关 |
| **Design Partner** | design-consultation | 从零构建完整设计系统 | 需要设计系统 |
| **Staff Engineer** | review | 查找生产环境 bug | 代码完成 |
| **Debugger** | investigate | 系统性根因调试 | 遇到 bug |
| **Designer Who Codes** | design-review | 设计审计并修复 | 设计问题 |
| **QA Lead** | qa | 真实浏览器测试 | 功能完成 |
| **QA Reporter** | qa-only | 纯 bug 报告 | 只需要报告 |
| **Release Engineer** | ship | 同步、测试、推送、PR | 准备发布 |
| **Technical Writer** | document-release | 更新文档匹配发布 | 新功能发布 |
| **Eng Manager (Retro)** | retro | 团队感知周回顾 | 每周回顾 |
| **QA Engineer** | browse | 真实浏览器操作 | 需要视觉验证 |
| **Session Manager** | setup-browser-cookies | 导入浏览器 Cookie | 需要登录 |
| **YC Office Hours** | office-hours | 重新定义问题 | 任务开始 |

---

## 🔧 执行流程

### Step 1: 任务接收与分类

```bash
# 接收新任务
任务：实现交互式 Agent 调试模式

# 分类
类型：开发任务
复杂度：高
需要角色：CEO, Eng Manager, Designer, Staff Engineer, QA
```

### Step 2: 专家角色分配

```yaml
sprint-001:
  task: 交互式 Agent 调试模式
  roles:
    - office-hours: "重新定义问题"
    - plan-ceo-review: "产品定位"
    - plan-eng-review: "架构设计"
    - design-consultation: "UI 设计"
    - review: "代码审查"
    - qa: "浏览器测试"
    - ship: "发布"
  status: in_progress
  progress: 62.5%
```

### Step 3: 并行 Sprint 管理

```bash
# 创建多个 sprint
sprint-001: 交互式 Agent 调试模式 (62.5%)
sprint-002: X 平台收藏技能 (0%)
sprint-003: 最佳实践文档 (0%)
sprint-004: 多 Agent 协作流程 (0%)
sprint-005: context 自动压缩 (0%)

# 并行执行
tmux new-session -d -s sprint-001
tmux new-session -d -s sprint-002
tmux new-session -d -s sprint-003
tmux new-session -d -s sprint-004
tmux new-session -d -s sprint-005
```

### Step 4: 智能评审路由

```python
# 根据任务类型自动选择评审
def select_reviews(task_type, changes):
    reviews = []
    
    if task_type == "feature":
        reviews.append("ceo-review")
        reviews.append("eng-review")
    
    if has_ui_changes(changes):
        reviews.append("design-review")
    
    if has_backend_changes(changes):
        reviews.append("review")  # Staff Engineer
    
    if has_deployment(changes):
        reviews.append("ship")
    
    return reviews
```

### Step 5: Review Readiness Dashboard

```
┌─────────────────────────────────────────────┐
│  Review Readiness Dashboard - sprint-001   │
├─────────────────────────────────────────────┤
│  ✅ CEO Review      (14:00 - Completed)     │
│  ✅ Eng Review      (14:30 - Completed)     │
│  ✅ Design Review   (15:00 - Completed)     │
│  🔄 Code Review     (16:00 - In Progress)   │
│  ⏳ QA              (17:00 - Pending)       │
│  ⏳ Ship            (18:00 - Pending)       │
├─────────────────────────────────────────────┤
│  Status: Ready for Code Review              │
│  Blockers: None                             │
└─────────────────────────────────────────────┘
```

### Step 6: Sprint 进度追踪

```yaml
sprints:
  sprint-001:
    task: 交互式 Agent 调试模式
    status: in_progress
    progress: 62.5%
    current_role: review
    time_elapsed: 2.5h
    estimated_total: 4h
    
  sprint-002:
    task: X 平台收藏技能
    status: planning
    progress: 10%
    current_role: plan-ceo-review
    time_elapsed: 0.5h
    estimated_total: 3h
```

### Step 7: 每日回顾

```bash
# 18:00 自动执行 retro
/retro

# 输出
今日完成 sprint: 2
并行 sprint 数：5
总代码量：2,400 行
测试覆盖率：85%
Bug 发现/修复：3/3
```

---

## 📊 tmux 并行执行布局

```
┌─────────────────────────────────────────────────────────┐
│                    Main Dashboard                        │
├─────────────┬─────────────┬─────────────┬───────────────┤
│  sprint-001 │  sprint-002 │  sprint-003 │  sprint-004   │
│  (62.5%)    │  (10%)      │  (0%)       │  (0%)         │
│  review     │  plan-ceo   │  office     │  office       │
├─────────────┴─────────────┴─────────────┴───────────────┤
│                     Global Logs                          │
├─────────────────────────────────────────────────────────┤
│                    Control Panel                         │
└─────────────────────────────────────────────────────────┘
```

---

## 🎯 效率提升

### 传统单 Agent 模式

```
任务 1: 4 小时 (串行)
任务 2: 3 小时 (串行)
任务 3: 2 小时 (串行)
总计：9 小时
```

### 多 Agent 并行模式

```
sprint-001: 4 小时 ─┐
sprint-002: 3 小时 ─┼─ 并行执行
sprint-003: 2 小时 ─┘
总计：4 小时 (10-15 个 sprint 同时)
```

**效率提升：** 5-10 倍

---

## 📝 使用示例

### 示例 1: 新功能开发

```
You:    我想实现多 Agent 协作管理
You:    /office-hours
Agent:  [询问痛点 - 具体案例]

You:    任务太多，单个 Agent 执行太慢
Agent:  我理解。但你说"多 Agent 协作"，
        你实际需要的是一个虚拟工程团队。
        [提取 5 个能力]
        [挑战 3 个前提]
        [生成 3 种方案]
        建议：从 gstack 的 15 个专家角色开始

You:    /plan-ceo-review
        [重新定义产品]

You:    /plan-eng-review
        [架构设计，数据流图]

You:    批准计划，退出计划模式
        [开始执行]

You:    /review
        [代码审查]

You:    /qa
        [浏览器测试]

You:    /ship
        [发布]
```

### 示例 2: 并行 Sprint

```bash
# 创建 5 个 sprint
./create-sprint.sh sprint-001 "交互式调试模式"
./create-sprint.sh sprint-002 "X 收藏技能"
./create-sprint.sh sprint-003 "最佳实践文档"
./create-sprint.sh sprint-004 "多 Agent 管理"
./create-sprint.sh sprint-005 "context 压缩"

# 查看所有 sprint 状态
./sprint-dashboard.sh

# 输出
┌────────────┬──────────┬─────────┬──────────┐
│ Sprint     │ Task     │ Progress│ Status   │
├────────────┼──────────┼─────────┼──────────┤
│ sprint-001 │ 调试模式 │ 62.5%   │ review   │
│ sprint-002 │ X 收藏   │ 10%     │ planning │
│ sprint-003 │ 最佳实践 │ 0%      │ backlog  │
│ sprint-004 │ 多 Agent │ 0%      │ backlog  │
│ sprint-005 │ context  │ 0%      │ backlog  │
└────────────┴──────────┴─────────┴──────────┘
```

---

## 🔗 相关资源

- [gstack 原文](https://github.com/garrytan/gstack)
- [Sprint 流程文档](docs/sprint-workflow.md)
- [专家角色详解](docs/expert-roles.md)

---

**维护：** 根据实际执行情况优化角色定义和流程。
