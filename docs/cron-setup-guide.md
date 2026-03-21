# OpenClaw 定时任务配置说明

**配置日期：** 2026-03-21  
**配置方式：** OpenClaw 内置 cron 系统

---

## ✅ 已配置任务

| 任务名称 | 执行时间 | 状态 | 说明 |
|---------|---------|------|------|
| OpenClaw 每日安全检查 | 每日 09:00 | ⚠️ 飞书未配置 | 安全审计 + GitHub 更新检查 |
| OpenClaw 深度安全审计 | 每 3 天一次 | ⚠️ 飞书未配置 | 完整安全报告 |
| 每日学习 - 技术文档抓取 | 每日 09:00 | ⚠️ 执行错误 | 抓取技术文章 |
| 每日简报 - AI 动态汇总 | 每日 09:00 | ⚠️ 执行错误 | GitHub + X 平台动态 |

---

## ⚠️ 当前问题

### 问题 1: 飞书推送未配置

**错误信息：**
```
Error: Feishu account "default" not configured
```

**解决方案：**
```bash
# 配置飞书
openclaw configure --section feishu

# 或编辑配置文件
vim ~/.openclaw/config/feishu.yaml
```

**配置内容：**
```yaml
accounts:
  default:
    webhook_url: "https://open.feishu.cn/open-apis/bot/v2/hook/..."
    app_id: "cli_a..."
    app_secret: "..."
```

---

### 问题 2: 任务执行错误

**错误信息：**
```
TypeError: Cannot read properties of undefined (reading 'trim')
```

**可能原因：**
- 技能文件路径不正确
- 环境变量未设置
- OpenCLI 命令输出格式变化

**解决方案：**
1. 检查技能文件是否存在
2. 手动测试技能执行
3. 查看日志文件

---

## 📋 查看任务状态

### 查看已配置任务

```bash
# 查看任务列表
cat ~/.openclaw/cron/jobs.json | python3 -m json.tool | grep -A2 '"name"'

# 或使用一行命令
cat ~/.openclaw/cron/jobs.json | python3 -c "import sys,json; jobs=json.load(sys.stdin)['jobs']; [print(f\"- {j['name']}: {j['schedule'].get('expr','N/A')}\") for j in jobs]"
```

### 查看任务执行历史

```bash
# 查看执行记录
ls -la ~/.openclaw/cron/runs/

# 查看最近执行日志
tail -20 ~/.openclaw/cron/runs/*/output.log
```

### 查看 OpenClaw 日志

```bash
# 主日志
tail -f ~/.openclaw/logs/openclaw.log

# 技能执行日志
tail -f ~/.openclaw/logs/skills.log
```

---

## 🔧 手动测试任务

### 测试每日简报

```bash
cd ~/.openclaw/workspace
openclaw run daily-briefing
```

### 测试 Twitter 监控

```bash
cd ~/.openclaw/workspace
openclaw run twitter-monitor
```

### 测试每日学习

```bash
cd ~/.openclaw/workspace
openclaw run daily-learning
```

---

## 📝 添加新任务

### 方法 1: 使用 OpenClaw 命令

```bash
# 添加定时任务（待实现）
openclaw cron add --name "Twitter 监控" --schedule "0 9 * * *" --skill twitter-monitor
```

### 方法 2: 手动编辑 jobs.json

1. 备份现有配置
```bash
cp ~/.openclaw/cron/jobs.json ~/.openclaw/cron/jobs.json.bak
```

2. 编辑 jobs.json，添加新任务
```json
{
  "id": "twitter-monitor-001",
  "agentId": "main",
  "sessionKey": "agent:main:main",
  "name": "Twitter 监控 - 每日摘要",
  "enabled": true,
  "schedule": {
    "expr": "0 9 * * *",
    "kind": "cron",
    "tz": "Asia/Shanghai"
  },
  "sessionTarget": "main",
  "payload": {
    "kind": "systemEvent",
    "message": "🐦 执行 Twitter 每日监控\n\n请执行以下任务：\n1. 获取 L1 核心账号更新\n2. 搜索关键词\n3. 生成监控报告\n\n完成后通知用户。",
    "timeoutSeconds": 300
  },
  "delivery": { "mode": "announce" }
}
```

3. 重启 OpenClaw Gateway
```bash
openclaw gateway restart
```

---

## 🚀 下一步行动

### 立即执行

1. **配置飞书推送**
   ```bash
   openclaw configure --section feishu
   ```

2. **手动测试任务**
   ```bash
   openclaw run daily-briefing
   openclaw run twitter-monitor
   ```

3. **查看执行日志**
   ```bash
   tail -f ~/.openclaw/logs/openclaw.log
   ```

### 本周完成

- [ ] 修复飞书推送配置
- [ ] 修复任务执行错误
- [ ] 添加 Twitter 监控任务
- [ ] 验证所有定时任务正常执行

---

## 📊 任务执行时间表

| 时间 | 任务 |
|------|------|
| **09:00** | 每日安全检查 |
| **09:00** | 每日学习 |
| **09:00** | 每日简报 |
| **09:00** | Twitter 监控（待添加） |
| **18:00** | 进化日报（待添加） |
| **每 3 天** | 深度安全审计 |

---

## 🔗 相关资源

**配置文件：**
- `~/.openclaw/cron/jobs.json` - 定时任务配置
- `~/.openclaw/config/feishu.yaml` - 飞书配置
- `~/.openclaw/logs/` - 日志目录

**文档：**
- [OpenClaw 定时任务文档](https://docs.openclaw.ai/features/cron)
- [技能开发指南](https://docs.openclaw.ai/skills/developing)

---

**最后更新：** 2026-03-21  
**维护：** 根据任务执行情况更新配置
