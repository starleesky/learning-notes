# 📂 GitHub 提交 vs 本地执行分类指南

**创建时间：** 2026-03-21 13:50 CST  
**用途：** 明确哪些内容提交 GitHub，哪些本地执行

---

## 📊 分类总览

| 类型 | 提交 GitHub | 本地执行 | 说明 |
|------|------------|---------|------|
| **技能定义** | ✅ SKILL.md | ❌ | 技能配置文件 |
| **学习笔记** | ✅ | ❌ | learning-notes 项目 |
| **文档** | ✅ | ❌ | docs/*.md |
| **脚本** | ✅ | ✅ | 可执行脚本 |
| **记忆文件** | ❌ | ✅ | memory/*.md |
| **日志** | ❌ | ✅ | *.log |
| **配置** | ⚠️ 部分 | ✅ | 敏感信息不提交 |
| **临时文件** | ❌ | ✅ | /tmp/* |

---

## ✅ 必须提交 GitHub 的内容

### 1. 技能定义文件

**位置：** `~/.openclaw/workspace/skills/*/SKILL.md`

**示例：**
```
skills/daily-briefing/SKILL.md          ✅ 提交
skills/twitter-monitor/SKILL.md         ✅ 提交
skills/github-trending/SKILL.md         ✅ 提交
```

**原因：** 技能是核心资产，需要版本控制和分享

---

### 2. 学习笔记

**位置：** `~/github/learning-notes/`

**分类：**
```
learning-notes/
├── ai-agents/                    # AI Agent 相关笔记
│   ├── anthropic-agent-skills.md
│   ├── andrewyng-context-hub.md
│   └── e2b-awesome-ai-agents.md
├── tools/                        # 工具使用笔记
│   └── opencli-install-practice.md
├── claude-code/                  # Claude Code 笔记
│   └── khazix0918-claude-code-tips.md
├── daily-briefings/              # 每日简报归档
│   └── daily-briefing-2026-03-21.md
├── twitter-digests/              # Twitter 摘要
│   └── twitter-digest-2026-03-21.md
├── github-trending/              # GitHub Trending
│   └── github-trending-2026-03-21.md
└── docs/                         # 文档
    ├── todo-list-2026-03-21.md
    ├── cron-config-final.md
    └── autonomous-execution-plan.md
```

**原因：** 知识沉淀，可追溯，可分享

---

### 3. 脚本文件

**位置：** `~/.openclaw/workspace/scripts/`

**示例：**
```
scripts/github-trending.py          ✅ 提交（工具脚本）
scripts/interactive-agent-tmux.sh   ✅ 提交（工具脚本）
scripts/setup-cron.sh               ✅ 提交（配置脚本）
```

**原因：** 可复用工具，帮助文档

---

### 4. 文档

**位置：** `~/.openclaw/workspace/docs/`

**示例：**
```
docs/cron-config-final.md           ✅ 提交（配置文档）
docs/autonomous-execution-plan.md   ✅ 提交（方案文档）
docs/github-trending-setup.md       ✅ 提交（技术文档）
docs/interactive-agent-debug-plan.md ✅ 提交（设计文档）
```

**原因：** 技术沉淀，团队协作

---

### 5. 记忆系统（精选）

**位置：** `~/.openclaw/workspace/memory/`

**提交 GitHub 的：**
```
memory/capabilities-and-goals-*.md     ✅ 提交（能力报告）
memory/capabilities-summary.md         ✅ 提交（速览）
memory/autonomous-execution-plan.md    ✅ 提交（方案）
memory/todo-list-*.md                  ✅ 提交（待办清单）
```

**不提交的：**
```
memory/heartbeat-state.json            ❌ 不提交（实时状态）
memory/daily-learning-*.md             ❌ 不提交（原始学习记录）
memory/task-progress-*.md              ❌ 不提交（临时进度）
```

**原因：** 精选重要文档，避免冗余

---

## ❌ 不提交 GitHub 的内容

### 1. 实时状态文件

```
memory/heartbeat-state.json       ❌ 实时状态，每秒变化
memory/task-execution-start.md    ❌ 临时通知
memory/task-progress-*.md         ❌ 中期汇报
```

---

### 2. 日志文件

```
~/.openclaw/logs/*.log            ❌ 体积大，无价值
~/.openclaw/cron/runs/*/output.log ❌ 执行日志
/tmp/*.md                         ❌ 临时文件
```

---

### 3. 敏感配置

```
~/.openclaw/openclaw.json         ❌ 含 API Key
~/.openclaw/config/feishu.yaml    ❌ 含 webhook URL
~/.openclaw/credentials/*          ❌ 凭证文件
```

---

### 4. 原始学习记录

```
memory/daily-learning-2026-03-21.md   ❌ 原始草稿
memory/daily-briefing-2026-03-21.md   ❌ 原始草稿（提交整理版）
```

**原因：** 只提交整理后的精编版

---

## ⚠️ 选择性提交的内容

### 1. 脚本文件

**提交的：**
```
scripts/github-trending.py        ✅ 通用工具
scripts/setup-cron.sh             ✅ 配置工具
```

**不提交的：**
```
scripts/temp-*.py                 ❌ 临时脚本
scripts/test-*.sh                 ❌ 测试脚本
```

---

### 2. 配置文件

**提交的：**
```
docs/cron-schedules.md            ✅ 配置说明文档
```

**不提交的：**
```
~/.openclaw/cron/jobs.json        ❌ 含运行时状态
~/.openclaw/config/*.yaml         ❌ 含敏感信息
```

---

## 📁 完整文件结构示例

```
~/.openclaw/workspace/
├── skills/                       # ✅ 全部提交
│   ├── daily-briefing/SKILL.md
│   ├── twitter-monitor/SKILL.md
│   └── github-trending/SKILL.md
│
├── scripts/                      # ⚠️ 选择性提交
│   ├── github-trending.py        ✅
│   ├── setup-cron.sh             ✅
│   └── temp-test.py              ❌
│
├── docs/                         # ✅ 全部提交
│   ├── cron-config-final.md
│   ├── autonomous-execution-plan.md
│   └── github-trending-setup.md
│
├── memory/                       # ⚠️ 精选提交
│   ├── capabilities-and-goals.md ✅
│   ├── todo-list-*.md            ✅
│   ├── heartbeat-state.json      ❌
│   └── task-progress-*.md        ❌
│
└── logs/                         # ❌ 全部不提交
    ├── openclaw.log
    └── skills.log

~/github/learning-notes/          # ✅ 全部提交
├── ai-agents/
├── tools/
├── daily-briefings/
└── docs/
```

---

## 🔄 提交流程

### 每日提交流程

```bash
# 1. 整理今日笔记
cd ~/github/learning-notes

# 2. 添加新文件
git add -A

# 3. 提交
git commit -m "docs: 2026-03-21 每日更新

- 学习笔记：3 篇
- 技能文档：1 个
- 进度报告：1 份"

# 4. 推送
git push origin main
```

### 技能提交流程

```bash
# 1. 复制技能文档
cp ~/.openclaw/workspace/skills/twitter-monitor/SKILL.md \
   ~/github/learning-notes/skills/twitter-monitor.md

# 2. 提交
cd ~/github/learning-notes
git add -A
git commit -m "skills: 添加 twitter-monitor 技能"
git push
```

---

## 📊 提交流水线

```
创建/修改文件
    ↓
判断类型
    ↓
┌─────────────────┬─────────────────┬─────────────────┐
│  必须提交 GitHub  │  选择性提交     │  不提交         │
│  - 技能定义     │  - 脚本         │  - 日志         │
│  - 学习笔记     │  - 配置文档     │  - 状态文件     │
│  - 文档         │  - 精选记忆     │  - 敏感配置     │
│                 │                 │  - 临时文件     │
└─────────────────┴─────────────────┴─────────────────┘
    ↓
git add + commit + push
    ↓
完成
```

---

## 🎯 最佳实践

### 1. 提交频率

- **学习笔记：** 每日提交（当日整理）
- **技能文档：** 完成即提交
- **进度报告：** 每日/每周提交
- **配置文件：** 变更即提交

### 2. 提交信息规范

```
<类型>: <简短描述>

- 详情 1
- 详情 2
- 详情 3
```

**示例：**
```
docs: 添加自主执行方案

- task-executor 技能
- progress-tracker 技能
- auto-reporter 技能
- 定时任务配置说明
```

### 3. 敏感信息处理

**❌ 错误：**
```yaml
# feishu.yaml
webhook_url: "https://open.feishu.cn/xxx"  # 直接提交
```

**✅ 正确：**
```yaml
# feishu.yaml.example
webhook_url: "YOUR_WEBHOOK_URL"  # 占位符

# .gitignore
feishu.yaml  # 忽略真实配置
```

---

## 📝 检查清单

### 提交前检查

- [ ] 是否包含敏感信息（API Key、webhook URL）
- [ ] 是否是精选内容（非原始草稿）
- [ ] 是否有价值（可复用、可参考）
- [ ] 是否符合分类规则

### 提交后验证

- [ ] GitHub 仓库可见
- [ ] 提交信息清晰
- [ ] 文件分类正确
- [ ] 无敏感信息泄露

---

**指南完成！** 📂  
**文档位置：** `docs/github-vs-local-guide.md`
