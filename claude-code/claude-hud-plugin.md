# Claude HUD - Claude Code 实时状态监控插件

**原文：** Claude HUD: A Claude Code plugin that shows what's happening  
**作者：** Jarrod Watts (@jarrodwatts)  
**来源：** https://github.com/jarrodwatts/claude-hud  
**翻译整理：** 2026-03-19  
**阅读时间：** 约 10 分钟  
**分类：** Claude Code / 工具插件

---

## 📌 核心摘要

> Claude HUD 是一个 Claude Code 插件，实时显示会话状态：上下文使用情况、活跃工具、运行中的子代理、待办任务进度。所有信息始终显示在输入框下方，无需额外窗口或 tmux。

**关键要点：**
1. **实时监控** - 原生 token 数据（非估算），每 300ms 更新
2. **多维度信息** - 项目路径、Git 状态、上下文健康度、工具活动、代理追踪、待办进度
3. **高度可定制** - 3 种预设模式（Full/Essential/Minimal），支持深度配置
4. **零依赖** - 使用 Claude Code 原生 statusline API，任何终端都可用

---

## 🚀 快速开始

### 3 步安装

**Step 1: 添加插件市场**
```bash
/plugin marketplace add jarrodwatts/claude-hud
```

**Step 2: 安装插件**
```bash
/plugin install claude-hud
```

> **⚠️ Linux 用户注意：** Linux 上 `/tmp` 通常是独立文件系统（tmpfs），会导致插件安装失败：
> ```
> EXDEV: cross-device link not permitted
> ```
> 
> **解决方案：**
> ```bash
> mkdir -p ~/.cache/tmp && TMPDIR=~/.cache/tmp claude
> # 然后在该会话中运行安装命令
> ```

**Step 3: 配置状态栏**
```bash
/claude-hud:setup
```

**完成！** HUD 立即显示，无需重启。

---

## 📊 功能详解

### 显示内容

| 信息 | 说明 | 价值 |
|------|------|------|
| **项目路径** | 当前项目目录（可配置 1-3 级） | 知道自己在哪个项目工作 |
| **上下文健康度** | 上下文窗口使用百分比 | 在超限前精确掌握剩余空间 |
| **工具活动** | 实时显示 Claude 读取、编辑、搜索文件 | 了解 Claude 正在做什么 |
| **代理追踪** | 显示运行中的子代理及其任务 | 多代理协作时特别有用 |
| **待办进度** | 实时追踪任务完成情况 | 保持对进度的掌控 |

---

### 显示示例

```
[Opus | Max] │ my-project git:(main*)
Context █████░░░░░ 45% │ Usage ██░░░░░░░░ 25% (1h 30m / 5h)

◐ Edit: auth.ts | ✓ Read ×3 | ✓ Grep ×2 ← 工具活动
◐ explore [haiku]: Finding auth code (2m 15s) ← 代理状态
▸ Fix authentication bug (2/5) ← 待办进度
```

**第 1 行：** 模型名称、计划名称、项目路径、Git 分支  
**第 2 行：** 上下文进度条（绿→黄→红）和使用率限制

---

## 🔧 技术架构

### 工作原理

```
Claude Code → stdin JSON → claude-hud → stdout → 显示在终端
             ↘ transcript JSONL (工具、代理、待办)
```

**核心特性：**
- ✅ 来自 Claude Code 的原生 token 数据（非估算）
- ✅ 随 Claude Code 报告的上下文窗口大小自动缩放（包括 1M 上下文）
- ✅ 解析 transcript 获取工具/代理活动
- ✅ 每 300ms 更新一次

---

## ⚙️ 配置选项

### 3 种预设模式

| 预设 | 显示内容 | 适用场景 |
|------|---------|---------|
| **Full** | 全部启用 - 工具、代理、待办、Git、使用量、时长 | 需要完整信息 |
| **Essential** | 活动行 + Git 状态，最小化信息干扰 | 日常开发 |
| **Minimal** | 核心 only - 仅模型名称和上下文进度条 | 简洁优先 |

**切换预设：**
```bash
/claude-hud:configure
```

---

### 高级配置

**配置文件：** `~/.claude/plugins/claude-hud/config.json`

**关键选项：**

| 选项 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `lineLayout` | string | expanded | 布局：expanded（多行）或 compact（单行） |
| `pathLevels` | 1-3 | 1 | 项目路径显示的目录层级 |
| `gitStatus.enabled` | boolean | true | 显示 Git 分支 |
| `gitStatus.showDirty` | boolean | true | 显示 * 表示未提交更改 |
| `display.showTools` | boolean | false | 显示工具活动行 |
| `display.showAgents` | boolean | false | 显示代理活动行 |
| `display.showTodos` | boolean | false | 显示待办进度行 |
| `colors.context` | color | green | 上下文进度条颜色 |

**完整配置示例：**
```json
{
  "lineLayout": "expanded",
  "pathLevels": 2,
  "elementOrder": ["project", "tools", "context", "usage", "environment", "agents", "todos"],
  "gitStatus": {
    "enabled": true,
    "showDirty": true,
    "showAheadBehind": true,
    "showFileStats": true
  },
  "display": {
    "showTools": true,
    "showAgents": true,
    "showTodos": true,
    "showConfigCounts": true,
    "showDuration": true
  },
  "colors": {
    "context": "cyan",
    "usage": "cyan",
    "warning": "yellow",
    "usageWarning": "magenta",
    "critical": "red"
  }
}
```

---

### Git 状态显示

**1 级目录（默认）：**
```
[Opus] │ my-project git:(main)
```

**2 级目录：**
```
[Opus] │ apps/my-project git:(main)
```

**3 级目录：**
```
[Opus] │ dev/apps/my-project git:(main)
```

**脏状态指示器：**
```
[Opus] │ my-project git:(main*)  # * 表示未提交更改
```

**领先/落后远程：**
```
[Opus] │ my-project git:(main ↑2 ↓1)  # 领先 2 个提交，落后 1 个
```

**文件统计：**
```
[Opus] │ my-project git:(main* !3 +1 ✘2 ?4)
# ! = 修改文件，+ = 新增/暂存，✘ = 删除，? = 未追踪
```

---

## 📈 使用量显示

**适用订阅：** Claude Pro、Max、Team（API 用户不可用）

**显示内容：**
```
Context █████░░░░░ 45% │ Usage ██░░░░░░░░ 25% (1h 30m / 5h) | ██████████ 85% (2d / 7d)
```

**7 天使用率：** 当超过阈值（默认 80%）时显示

**故障排查：**
- ✅ 确保使用 Pro/Max/Team 账号登录（非 API key）
- ✅ 检查 `display.showUsage` 未设置为 false
- ✅ API 用户无使用量显示（按 token 付费，无速率限制）
- ✅ AWS Bedrock 模型显示 "Bedrock" 并隐藏使用量限制

---

## 🎨 颜色自定义

**支持的颜色：**
- red, green, yellow, magenta, cyan
- brightBlue, brightMagenta

**配置示例：**
```json
{
  "colors": {
    "context": "cyan",      # 上下文进度条
    "usage": "cyan",        # 使用量进度条
    "warning": "yellow",    # 警告颜色
    "usageWarning": "magenta",  # 使用量警告
    "critical": "red"       # 临界状态
  }
}
```

---

## 🛠️ 故障排查

### 常见问题

**Q: 配置不生效？**

**A:** 
- 检查 JSON 语法错误（无效 JSON 会静默回退到默认值）
- 确保值有效：`pathLevels` 必须是 1/2/3，`lineLayout` 必须是 expanded/compact
- 删除 config.json 并运行 `/claude-hud:configure` 重新生成

---

**Q: Git 状态缺失？**

**A:**
- 验证你在 git 仓库中
- 检查 `gitStatus.enabled` 未设置为 false

---

**Q: 工具/代理/待办行缺失？**

**A:**
- 这些默认隐藏 - 在 config 中启用 `showTools`、`showAgents`、`showTodos`
- 它们只在有活动时显示

---

### 性能优化

**高延迟环境：**
```bash
# 增加使用量 API 超时时间（毫秒）
export CLAUDE_HUD_USAGE_TIMEOUT_MS=5000
```

**缓存优化：**
```json
{
  "usage": {
    "cacheTtlSeconds": 120,        # 成功响应缓存时间
    "failureCacheTtlSeconds": 30   # 失败响应缓存时间
  }
}
```

---

## 💡 关键洞察

### 洞察 1: 上下文管理是核心痛点

**问题：** Claude Code 用户经常遇到上下文超限，导致会话重置。

**解决：** Claude HUD 实时显示上下文使用率，颜色从绿→黄→红，在超限前预警。

**价值：** 避免意外丢失会话上下文，提升长会话可靠性。

---

### 洞察 2: 可观测性提升信任

**问题：** 用户不知道 Claude 在做什么，感觉像黑盒。

**解决：** 实时显示工具活动（读取、编辑、搜索）、代理状态、待办进度。

**价值：** 增强用户对 AI 工作的理解和信任，便于及时干预。

---

### 洞察 3: 原生集成优于外部工具

**对比：**
- ❌ 外部监控工具 - 需要额外窗口、tmux 配置
- ✅ Claude HUD - 使用原生 statusline API，零配置

**价值：** 降低使用门槛，任何终端都能用。

---

## 🔗 相关资源

**官方资源：**
- [GitHub 仓库](https://github.com/jarrodwatts/claude-hud)
- [安装视频预览](https://github.com/jarrodwatts/claude-hud/blob/main/claude-hud-preview-5-2.png)
- [贡献指南](https://github.com/jarrodwatts/claude-hud/blob/main/CONTRIBUTING.md)

**相关链接：**
- [Claude Code 插件系统](https://docs.anthropic.com/claude-code/plugins)
- [Linux 安装问题讨论](https://github.com/anthropics/claude-code/issues/14799)

---

## 📝 译者思考

### 与当前项目的关联

**1. ai-skill-bench 项目**

可以借鉴 Claude HUD 的设计理念：
- **实时反馈** - 测试执行时显示进度和状态
- **多维度监控** - token 消耗、响应时间、成功率
- **可视化进度条** - 使用 ████░░░░░░ 格式

**应用示例：**
```
[Qwen3.5-Plus] │ ai-skill-bench git:(main)
Progress ████████░░ 80% │ Tokens 15.2k │ Time 2m 30s
✓ Code: 5/5 | ◐ Logic: 2/3 | ▸ Longtext: 0/2
```

---

**2. agent-skills 项目**

可以创建类似的监控技能：
- **技能名称：** `status-monitor`
- **功能：** 实时监控 Agent 执行状态
- **显示：** 上下文使用、工具活动、子代理状态

---

**3. OpenClaw 工作区**

可以为 OpenClaw 开发类似的状态栏：
- **显示：** 当前技能、执行进度、资源消耗
- **配置：** 支持自定义显示元素
- **集成：** 与飞书消息联动

---

### 下一步行动

- [ ] 为 ai-skill-bench 添加实时进度显示
- [ ] 创建 agent-skills/status-monitor 技能
- [ ] 调研 OpenClaw 状态栏实现方案
- [ ] 安装 Claude HUD 体验实际效果

---

## 📊 项目统计

**Star 增长：** 快速增长中（见 Star History 图表）  
**许可证：** MIT  
**最低要求：** 
- Claude Code v1.0.80+
- Node.js 18+ 或 Bun

---

**最后更新：** 2026-03-19  
**分类：** Claude Code / 工具插件  
**标签：** #ClaudeCode #插件 #状态监控 #HUD #开发者工具  
**原文版权：** MIT License
