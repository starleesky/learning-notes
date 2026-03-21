---
name: x-likes-to-notes
description: |
  自动汇总 X/Twitter 用户标记喜欢的文章到学习笔记。
  
  TRIGGER WHEN:
  - 每日 20:00 定时执行
  - 用户手动触发
  - 检测到新喜欢的推文
  
  功能:
  - 获取用户喜欢的推文列表
  - 识别文章链接（GitHub、博客、文档等）
  - 抓取文章内容
  - 整理成 Markdown 笔记
  - 保存到 learning-notes
  
  输出:
  - 每日收藏汇总
  - 分类笔记（AI/Agent、工具、教程等）
  - 自动提交 GitHub

metadata:
  pattern: pipeline
  steps: "5"
  requires: { anyBins: ["opencli", "curl"] }
  openclaw: { emoji: "❤️" }
  version: "1.0"
  created: "2026-03-21"
---

# ❤️ X 平台收藏自动汇总 v1.0

**版本：** v1.0  
**创建：** 2026-03-21  
**用途：** 自动汇总 X 平台喜欢的文章

---

## 🔧 执行流程

### Step 1: 获取喜欢的推文

```bash
# 使用 opencli 获取用户喜欢的推文
opencli twitter likes --limit 50 --since "24h"
```

**输出：**
```
推文 ID | 作者 | 内容 | 链接 | 时间
```

---

### Step 2: 识别文章链接

**过滤规则：**
- GitHub 链接：`github.com/*`
- 博客链接：`medium.com/*`, `substack.com/*`
- 文档链接：`docs.*`, `*documentation*`
- 技术文章：包含 "blog", "article", "tutorial"

**排除：**
- 纯图片/视频推文
- 短链接（t.co）无预览
- 重复链接

---

### Step 3: 抓取文章内容

```bash
# 使用 web_fetch 抓取文章
opencli web fetch <URL> --extractMode markdown --maxChars 10000
```

**输出：** Markdown 格式文章

---

### Step 4: 整理成笔记

**分类规则：**
| 关键词 | 分类目录 |
|--------|----------|
| AI, Agent, LLM | ai-agents/ |
| Tool, CLI, SDK | tools/ |
| Tutorial, Guide | tutorials/ |
| Design, UX | design/ |
| Other | misc/ |

**笔记模板：**
```markdown
# X 平台收藏 - 2026-03-21

**来源：** Twitter/X Likes  
**整理时间：** 20:00 CST  
**推文数：** N 条

---

## 📌 收藏 1

**原文：** [标题](URL)  
**作者：** @username  
**来源：** Twitter/X  
**日期：** 2026-03-21

### 摘要

文章内容摘要...

### 关键要点

1. 要点 1
2. 要点 2
3. 要点 3

### 原文链接

- [推文链接](https://x.com/status/xxx)
- [文章链接](https://...)

---

## 📊 统计

- 总推文数：N
- 文章数：N
- GitHub 项目：N
- 博客文章：N
```

---

### Step 5: 保存并提交

```bash
# 保存到 learning-notes
cd ~/github/learning-notes
mkdir -p x-likes
cp /tmp/x-likes-today.md x-likes/x-likes-2026-03-21.md

# 提交
git add x-likes/
git commit -m "likes: X 平台收藏汇总 2026-03-21"
git push origin main
```

---

## 📝 输出示例

```markdown
# X 平台收藏汇总 - 2026-03-21

**来源：** Twitter/X Likes  
**整理时间：** 20:00 CST  
**推文数：** 15 条

---

## 🤖 AI/Agent (5 篇)

### 1. Anthropic 发布新 Skills 系统

**原文：** [Introducing Agent Skills](https://anthropic.com/...)  
**作者：** @AnthropicAI  
**推文：** https://x.com/status/xxx

**摘要：**
Anthropic 发布新的 Agent Skills 系统，支持...

**关键要点：**
1. Skills 定义 Agent 能力
2. 支持自动触发
3. 可组合多个 Skills

---

## 🛠️ 工具 (3 篇)

### 1. gstack - Garry Tan 的开源软件工厂

**原文：** [gstack GitHub](https://github.com/garrytan/gstack)  
**作者：** @garrytan  
**推文：** https://x.com/status/xxx

**摘要：**
Garry Tan 分享他的 60 万行代码秘密武器...

---

## 📚 教程 (2 篇)

...

---

## 📊 统计

| 分类 | 数量 |
|------|------|
| AI/Agent | 5 |
| 工具 | 3 |
| 教程 | 2 |
| 设计 | 1 |
| 其他 | 4 |
| **总计** | **15** |
```

---

## 🔧 配置说明

### 定时任务

```yaml
# ~/.openclaw/cron/jobs.json
{
  "id": "x-likes-001",
  "name": "X 平台收藏汇总",
  "schedule": {"expr": "0 20 * * *"},
  "enabled": true
}
```

### 分类配置

```yaml
# ~/.openclaw/config/x-likes-categories.yaml
categories:
  ai-agents:
    keywords: ["AI", "Agent", "LLM", "Claude", "GPT"]
  tools:
    keywords: ["Tool", "CLI", "SDK", "Library"]
  tutorials:
    keywords: ["Tutorial", "Guide", "How-to"]
  design:
    keywords: ["Design", "UX", "UI"]
  misc:
    keywords: []
```

---

## 📊 质量评估

### 汇总评分

| 评分 | 标准 |
|------|------|
| ⭐⭐⭐⭐⭐ | 100% 覆盖，分类准确，摘要清晰 |
| ⭐⭐⭐⭐ | 无明显遗漏，分类正确 |
| ⭐⭐⭐ | 基本文章都有 |
| ⭐⭐ | 有遗漏 |

---

## 🔗 相关资源

- [Twitter 监控技能](./twitter-monitor/SKILL.md)
- [link-to-notes 技能](../skills/link-to-notes/SKILL.md)

---

**维护：** 根据 X 平台 API 变化和用户反馈优化。
监控技能](./twitter-monitor/SKILL.md)
- [link-to-notes 技能](../skills/link-to-notes/SKILL.md)

---

**维护：** 根据 X 平台 API 变化和用户反馈优化。
