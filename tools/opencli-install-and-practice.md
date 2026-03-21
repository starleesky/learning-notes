# OpenCLI 安装与实践指南

**原文：** OpenCLI - Make any website your CLI  
**项目：** https://github.com/opencli/opencli  
**npm：** @jackwener/opencli  
**安装日期：** 2026-03-21  
**分类：** 开发工具

---

## 📦 快速安装

```bash
npm install -g @jackwener/opencli
```

**版本：** v1.1.0（2026-03-20 发布）

---

## 🔧 核心命令

### 发现与探索

| 命令 | 用途 |
|------|------|
| `opencli list` | 列出所有可用 CLI 命令 |
| `opencli explore <url>` | 探索网站：发现 API、存储，推荐策略 |
| `opencli synthesize <target>` | 从探索结果合成 CLI |
| `opencli generate <url>` | 一键完成：explore → synthesize → register |
| `opencli cascade <url>` | 策略级联：找到最简单的可用策略 |

### 验证与诊断

| 命令 | 用途 |
|------|------|
| `opencli validate [target]` | 验证 CLI 定义 |
| `opencli verify [target]` | 验证 + 冒烟测试 |
| `opencli doctor` | 诊断浏览器桥接连接性 |
| `opencli setup` | 交互式设置：验证浏览器桥接 |

### 外部 CLI 管理

| 命令 | 用途 |
|------|
| `opencli install <name>` | 安装外部 CLI |
| `opencli register <name>` | 注册外部 CLI |

---

## 📋 预置 CLI 列表

### AI 与开发工具
- `codex` - OpenAI Codex
- `cursor` - Cursor IDE
- `chatgpt` - ChatGPT
- `grok` - Grok AI
- `discord-app` - Discord
- `feishu` - 飞书
- `notion` - Notion

### 内容平台
- `bilibili` - B 站（下载、动态、收藏、历史等）
- `xiaohongshu` - 小红书
- `zhihu` - 知乎
- `weibo` - 微博
- `wechat` - 微信
- `youtube` - YouTube
- `reddit` - Reddit
- `twitter` - Twitter/X

### 学术与资讯
- `arxiv` - arXiv 论文搜索
- `hackernews` - Hacker News
- `stackoverflow` - Stack Overflow
- `wikipedia` - Wikipedia
- `bbc` - BBC News

### 金融与股票
- `yahoo-finance` - 雅虎财经
- `xueqiu` - 雪球
- `sinafinance` - 新浪财经
- `barchart` - Barchart 期权数据

### 其他
- `antigravity` - Antigravity AI
- `apple-podcasts` - Apple Podcasts
- `linkedin` - LinkedIn
- `ctrip` - 携程
- `smzdm` - 什么值得买

---

## 🧪 实践测试（2026-03-21）

### 测试结果

| 测试项 | 状态 | 说明 |
|--------|------|------|
| `opencli doctor` | ⚠️ 部分通过 | Daemon 未运行（自动启动） |
| `opencli arxiv search` | ✅ 成功 | 返回 10 条论文结果 |
| `opencli hackernews top` | ✅ 成功 | 返回 HN 热榜 |
| `opencli list` | ✅ 成功 | 列出 50+ 预置 CLI |

### 测试记录

**1. 诊断连接**
```bash
$ opencli doctor
[MISSING] Daemon: not running
[MISSING] Extension: not connected
[SKIP] Connectivity: not tested (use --live)
```
→ Daemon 会在运行浏览器命令时自动启动

**2. arXiv 论文搜索**
```bash
$ opencli arxiv search "large language models"
```
✅ 成功返回 10 条论文，包含标题、作者、发布日期

**3. Hacker News 热榜**
```bash
$ opencli hackernews top
```
✅ 成功返回热榜文章（排名、标题、分数、评论数）

**4. 查看可用命令**
```bash
$ opencli list
```
✅ 输出结构化列表，AI 可自动发现

---

## 💡 核心架构

### 双引擎架构

```
┌─────────────────────────────────────┐
│         OpenCLI Core                │
├─────────────────────────────────────┤
│  YAML 声明式引擎  │  TypeScript 注入引擎  │
│  - 简单场景       │  - 复杂交互        │
│  - 快速定义       │  - 动态逻辑        │
└─────────────────────────────────────┘
```

### 动态加载器

```
~/.opencli/
├── *.yaml    # 自动注册 YAML 定义
└── *.ts      # 自动注册 TypeScript 脚本
```

**特点：** 放入文件即自动注册，无需重启

### 浏览器会话复用

- ✅ 复用 Chrome 登录状态
- ✅ 无需 token/API Key
- ✅ 安全（本地会话）
- ✅ 支持 CDP 协议

### AI 驱动发现

**三件套：**
1. `explore` - 探索网站结构
2. `synthesize` - 合成 CLI 定义
3. `cascade` - 策略级联优化

---

## 🔗 OpenClaw 可借鉴

### 1. AI 自动发现机制

**当前状态：** OpenClaw 技能需手动配置  
**改进方向：**
- 技能发现命令 `openclaw explore <url>`
- 自动识别 Feishu/Notion 等 API 结构
- 推荐技能模板

### 2. 外部 CLI 集成模式

**当前状态：** 技能手动安装  
**改进方向：**
- `openclaw install <skill-name>`
- 统一技能仓库
- 自动依赖安装

### 3. 动态加载器（技能热加载）

**当前状态：** 需重启 Gateway  
**改进方向：**
- `~/.openclaw/workspace/skills/*.md` 自动注册
- 文件变更自动重载
- 无需重启

### 4. 自愈式 setup（doctor 增强）

**当前状态：** `openclaw status` 基础检查  
**改进方向：**
- `openclaw doctor` 深度诊断
- 自动修复建议
- 交互式 setup 向导

### 5. 双引擎架构（YAML + TypeScript 技能）

**当前状态：** SKILL.md 单一格式  
**改进方向：**
- 简单技能：YAML 声明式
- 复杂技能：TypeScript 脚本
- 混合模式支持

---

## 📝 下一步行动

### 立即实践

- [ ] 测试 `opencli doctor` 检查连接状态
- [ ] 尝试 `opencli explore` 探索一个网站
- [ ] 使用 `opencli bilibili hot` 测试预置 CLI
- [ ] 查看 `~/.opencli/` 目录结构

### OpenClaw 改进计划

- [ ] 设计技能热加载方案
- [ ] 编写 `openclaw doctor` 诊断命令
- [ ] 研究 CDP 协议集成可能性
- [ ] 设计 YAML 声明式技能格式

---

## 🔗 相关资源

**官方资源：**
- npm: https://npm.im/@jackwener/opencli
- GitHub: https://github.com/opencli/opencli

**延伸阅读：**
- [OpenCLI 学习笔记](../memory/opencli 学习笔记.md)（待补充）

---

**最后更新：** 2026-03-21  
**分类：** tools  
**标签：** #CLI #AI #Browser #Automation #OpenClaw  
**原文版权：** OpenCLI Team
