# Andrew Ng Context Hub - AI Agent 上下文管理中心

**原文：** andrewyng/context-hub  
**作者：** Andrew Ng 团队  
**来源：** https://github.com/andrewyng/context-hub  
**npm：** @aisuite/chub  
**整理日期：** 2026-03-21  
**分类：** AI/Agent

---

## 📌 核心摘要

> Context Hub 解决 Coding Agent 的两大痛点：**API 幻觉**和**会话遗忘**。它提供经过策划、版本化的 API 文档，让 Agent 能够随着每次任务变得更聪明。所有内容以 Markdown 形式开放维护在 GitHub 仓库中，可以精确检查 Agent 读取的内容并贡献反馈。

**关键要点：**
1. **解决 API 幻觉** - 提供 curated、versioned 的官方文档，减少 Agent 编造 API
2. **会话记忆持久化** - Annotations 功能让 Agent 的经验跨会话保存
3. **多语言支持** - 同一 API 可提供 Python/JavaScript 等不同语言版本
4. **反馈闭环** - up/down vote 机制让文档质量持续改进
5. **开源透明** - 所有内容在 GitHub 可审查，无黑盒

---

## 📦 快速安装

```bash
npm install -g @aisuite/chub
```

---

## 🔧 核心命令

| 命令 | 用途 | 示例 |
|------|------|------|
| `chub search [query]` | 搜索文档和技能 | `chub search "stripe payments"` |
| `chub get <id> [--lang]` | 获取文档 | `chub get openai/chat --lang py` |
| `chub annotate <id> <note>` | 添加本地注释 | `chub annotate stripe/api "Needs raw body"` |
| `chub annotate --list` | 列出所有注释 | - |
| `chub annotate <id> --clear` | 清除注释 | - |
| `chub feedback <id> <up|down>` | 投票反馈 | `chub feedback stripe/api up` |

---

## 📖 使用流程

### 标准工作流

```bash
# 1. 搜索相关文档
chub search "stripe payments"

# 2. 获取文档（指定语言）
chub get stripe/api --lang js

# 3. Agent 读取文档，编写正确代码
# Done.
```

### 发现知识缺口时

```bash
# Agent 发现文档不足，添加本地注释
chub annotate stripe/api "Needs raw body for webhook verification"

# 下次获取时，注释自动出现
chub get stripe/api
# → 包含之前的注释
```

### 反馈给文档作者

```bash
# 文档好用，点赞
chub feedback stripe/api up

# 文档有问题，点踩
chub feedback stripe/api down
```

---

## 💡 核心设计理念

### 1. 为 Agent 设计（而非人类）

> "Chub is designed for your coding agent to use (not for you to use!)"

**集成方式：**
- 直接 prompt Agent 使用 CLI
- 创建 Agent Skill（SKILL.md）
- Claude Code 用户：`~/.claude/skills/get-api-docs/`

### 2. 会话记忆持久化

**问题：** Agent 每次会话从零开始，重复犯错

**解决：** Annotations 机制
```
Session 1: Agent 发现 webhook 需要 raw body
         → chub annotate stripe/api "Needs raw body"
         
Session 2: chub get stripe/api
         → 自动包含注释
         → Agent 不再犯同样错误
```

### 3. 反馈闭环

```
Agent 使用文档
    ↓
发现问题/成功经验
    ↓
Annotation (本地持久化) + Feedback (反馈给作者)
    ↓
作者改进文档
    ↓
所有用户受益
```

### 4. 多语言版本化

```bash
chub get openai/chat --lang py  # Python 版本
chub get openai/chat --lang js  # JavaScript 版本
```

---

## 🔄 与传统方式对比

| 维度 | 无 Context Hub | 有 Context Hub |
|------|---------------|----------------|
| **文档来源** | 网络搜索 | 策划文档库 |
| **结果质量** | 噪音多 | 准确率高 |
| **代码稳定性** | 经常出错 | 更可靠 |
| **知识发现** | 手动记录 | 自动注释 |
| **跨会话记忆** | 遗忘 | 持久化 |
| **改进方向** | 单向 | 反馈闭环 |

---

## 📁 内容结构

**内容类型：**
- API 文档（当前主要类型）
- Agent Skills（路线图）
- 更多类型计划中

**文件格式：**
- Markdown + YAML frontmatter
- 通过 Pull Request 贡献
- 开源透明，可审查

---

## 🔗 OpenClaw 可借鉴

### 1. 技能记忆持久化

**当前状态：** OpenClaw 技能无本地注释机制

**改进方向：**
```bash
# 为技能添加本地注释
openclaw annotate coding-agent "复杂任务需要 5 分钟以上"

# 下次使用技能时自动显示注释
```

### 2. 技能反馈机制

**当前状态：** 无用户反馈渠道

**改进方向：**
```bash
# 技能好用，点赞
openclaw feedback daily-briefing up

# 技能有问题，点踩
openclaw feedback rss-monitor down
```

### 3. 技能版本化文档

**当前状态：** SKILL.md 分散在仓库

**改进方向：**
- 统一技能注册表
- 版本化技能文档
- 多语言技能描述

### 4. 技能贡献流程

**当前状态：** 手动创建技能

**改进方向：**
- 标准化技能模板
- Pull Request 贡献机制
- 社区维护技能库

### 5. 为 Agent 设计的 CLI

**当前状态：** OpenClaw CLI 面向人类

**改进方向：**
- YAML/JSON 输出格式
- Agent Skill 自动发现
- `openclaw search <skill>` 命令

---

## 📝 下一步行动

### 立即实践

- [ ] 安装 `@aisuite/chub`
- [ ] 测试 `chub search openai`
- [ ] 获取 OpenAI 文档 `chub get openai/chat --lang py`
- [ ] 研究 SKILL.md 格式

### OpenClaw 改进计划

- [ ] 设计技能注释机制（本地持久化）
- [ ] 实现技能反馈系统（up/down vote）
- [ ] 建立技能注册表（类似 chub search）
- [ ] 标准化技能贡献流程（PR 机制）
- [ ] 优化 CLI 输出格式（Agent 可读）

---

## 🔗 相关资源

**官方资源：**
- GitHub: https://github.com/andrewyng/context-hub
- npm: https://www.npmjs.com/package/@aisuite/chub
- CLI 文档：`docs/cli-reference.md`
- 内容指南：`docs/content-guide.md`
- 反馈机制：`docs/feedback-and-annotations.md`

**延伸阅读：**
- [Anthropic Agent Skills](./anthropic-introduction-to-agent-skills.md)
- [OpenCLI 项目](../tools/opencli-install-and-practice.md)

---

**最后更新：** 2026-03-21  
**分类：** ai-agents  
**标签：** #AgentSkills #ContextHub #AndrewNg #AIEngineering #知识管理  
**原文版权：** MIT License
