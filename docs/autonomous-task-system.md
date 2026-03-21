# 🤖 自主任务执行系统配置指南

**配置时间：** 2026-03-21 12:50 CST  
**系统：** Task Orchestrator v1.0

---

## 🎯 系统概述

**功能：** 24 小时自主执行任务 + 定期汇报  
**检查频率：** 每 10 分钟  
**汇报频率：** 每小时 + 每日  
**推送渠道：** 飞书

---

## 📋 核心功能

### 1. Backlog 管理
- 任务文件：`backlog/YYYY-MM-DD.md`
- 优先级：P0(紧急) → P1(高) → P2(中) → P3(低)
- 状态：backlog → in_progress → done/failed

### 2. 自主执行
- 每 10 分钟自动检查 backlog
- 自动获取最高优先级任务
- 自主执行或分配给子 Agent

### 3. 定期汇报
- **小时报：** 每小时整点
- **日报：** 每日 18:00
- **推送：** 飞书自动通知

---

## 📁 目录结构

```
~/.openclaw/workspace/
├── backlog/
│   ├── 2026-03-21.md          # 今日任务
│   ├── src/
│   │   └── task_orchestrator.py  # 主程序
│   └── reports/
│       ├── hourly/            # 小时报
│       └── daily/             # 日报
└── skills/
    └── task-orchestrator/
        └── SKILL.md           # 技能定义
```

---

## 🔧 配置步骤

### Step 1: 初始化 Backlog

```bash
cd ~/.openclaw/workspace
python3 backlog/src/task_orchestrator.py --init
```

**输出：**
```
✅ 已创建今日 backlog: backlog/2026-03-21.md
```

### Step 2: 添加定时任务

编辑 crontab：
```bash
crontab -e
```

添加以下任务：
```bash
# 每 10 分钟检查并执行任务
*/10 * * * * cd ~/.openclaw/workspace && python3 backlog/src/task_orchestrator.py --cycle >> ~/.openclaw/logs/task-orchestrator.log 2>&1

# 每小时生成小时报
0 * * * * cd ~/.openclaw/workspace && python3 backlog/src/task_orchestrator.py --report hourly >> ~/.openclaw/logs/task-orchestrator.log 2>&1

# 每日 18:00 生成日报
0 18 * * * cd ~/.openclaw/workspace && python3 backlog/src/task_orchestrator.py --report daily >> ~/.openclaw/logs/task-orchestrator.log 2>&1
```

### Step 3: 验证配置

```bash
# 查看 crontab
crontab -l

# 手动测试
python3 backlog/src/task_orchestrator.py --cycle
python3 backlog/src/task_orchestrator.py --report hourly
```

---

## 📊 任务格式

### Backlog 示例

```markdown
# Backlog - 2026-03-21

## P1 - 高优先级

- [ ] 验证定时任务自动执行
  - status: backlog
  - assignee: pending
  - deadline: 2026-03-22 09:00
  - estimate: 30m

## P2 - 中优先级

- [ ] 编写 OpenClaw 最佳实践文档
  - status: backlog
  - assignee: pending
  - deadline: 2026-03-31
  - estimate: 8h

## P3 - 低优先级

- [ ] Twitter L2/L3 账号添加
  - status: backlog
  - assignee: pending
  - estimate: 2h
```

### 小时报示例

```markdown
# 小时报 - 2026-03-21 13:00

## 本小时完成

✅ 飞书推送配置
   - 用时：10 分钟

✅ GitHub 星标修复
   - 用时：1 小时

## 进行中

⏳ 定时任务配置
   - 进度：75%

## 待执行 (Top 5)

⏳ 交互式调试模式
   - 预计：4 小时

## 统计

- 已完成：2 个
- 进行中：1 个
- 待执行：5 个

---

**下次汇报：** 1 小时后
```

---

## 🎯 自主执行流程

```
每 10 分钟循环:
├─ 1. 加载 backlog
├─ 2. 优先级排序
├─ 3. 获取最高优先级任务
├─ 4. 执行任务 (或分配给子 Agent)
├─ 5. 更新任务状态
└─ 6. 等待 10 分钟
```

每小时整点:
```
├─ 生成小时报
├─ 推送到飞书
└─ 保存到 reports/hourly/
```

每日 18:00:
```
├─ 生成日报
├─ 推送到飞书
├─ 保存到 reports/daily/
└─ 规划明日 backlog
```

---

## 📤 汇报渠道

### 飞书推送

**配置：** 已配置飞书推送  
**触发条件：**
- 每小时整点（小时报）
- 每日 18:00（日报）
- P0 任务完成（立即通知）

### 文件保存

**位置：** `backlog/reports/`

```
reports/
├── hourly/
│   ├── hourly-20260321-13.md
│   └── hourly-20260321-14.md
└── daily/
    └── daily-20260321.md
```

---

## 🔍 监控方法

### 查看当前任务

```bash
cat backlog/2026-03-21.md
```

### 查看执行日志

```bash
tail -f ~/.openclaw/logs/task-orchestrator.log
```

### 查看最新报告

```bash
# 最新小时报
ls -lt backlog/reports/hourly/ | head -3

# 最新日报
ls -lt backlog/reports/daily/ | head -3
```

### 手动触发汇报

```bash
# 生成小时报
python3 backlog/src/task_orchestrator.py --report hourly

# 生成日报
python3 backlog/src/task_orchestrator.py --report daily
```

---

## 📋 今日任务（已初始化）

### P1 - 高优先级

1. **验证定时任务自动执行** (30m)
   - 截止时间：明日 09:00
   - 状态：backlog

### P2 - 中优先级

2. **编写 OpenClaw 最佳实践文档** (8h)
   - 截止时间：3 月 31 日
   - 状态：backlog

3. **多 Agent 协作流程设计** (12h)
   - 截止时间：3 月 31 日
   - 状态：backlog

4. **context 自动压缩 hook** (6h)
   - 截止时间：3 月 31 日
   - 状态：backlog

### P3 - 低优先级

5. **Twitter L2/L3 账号添加** (2h)
   - 截止时间：3 月 31 日
   - 状态：backlog

6. **语音输入集成** (8h)
   - 截止时间：3 月 31 日
   - 状态：backlog

---

## 🚀 下一步

### 立即执行

1. **配置 crontab**
   ```bash
   crontab -e
   # 添加 3 个定时任务
   ```

2. **验证执行**
   ```bash
   python3 backlog/src/task_orchestrator.py --cycle
   ```

3. **等待首次汇报**
   - 下次小时报：整点自动发送
   - 下次日报：今日 18:00

### 明日验证

- **09:00** - 检查定时任务是否自动执行
- **10:00** - 收到第一份小时报
- **18:00** - 收到第一份日报

---

## 🔗 相关资源

**参考项目:**
- [openclaw-skill-backlog](https://github.com/mopga/openclaw-skill-backlog)
- [self-improving-agent](~/.openclaw/workspace/skills/self-improving-agent/)

**技能文档:**
- `skills/task-orchestrator/SKILL.md`

---

**配置完成！系统开始自主运行！** 🎉  
**下次汇报：** 整点自动发送  
**文档位置：** `memory/autonomous-task-system.md`
