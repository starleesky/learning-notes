# Claude Code 使用技巧 45 条

**来源：** https://github.com/ykdojo/claude-code-tips  
**作者：** ykdojo  
**翻译整理：** 2026-03-19  
**阅读时间：** 约 20 分钟

---

## 📺 快速演示

[观看演示视频](https://www.youtube.com/watch?v=hiISl558JGE) - 多 Claude 工作流和语音输入的实际操作演示

---

## 📋 技巧目录

### 基础技巧 (Tip 0-10)

- [Tip 0](#tip-0-自定义状态栏) - 自定义状态栏
- [Tip 1](#tip-1-学习必要的斜杠命令) - 学习必要的斜杠命令
- [Tip 2](#tip-2-用语音与 Claude 交流) - 用语音与 Claude 交流
- [Tip 3](#tip-3-将大问题分解为小问题) - 将大问题分解为小问题
- [Tip 4](#tip-4-像专业人士一样使用 Git 和 GitHub CLI) - 像专业人士一样使用 Git 和 GitHub CLI
- [Tip 5](#tip-5-ai-上下文就像牛奶) - AI 上下文就像牛奶
- [Tip 6](#tip-6-从终端获取输出) - 从终端获取输出
- [Tip 7](#tip-7-设置终端别名以便快速访问) - 设置终端别名
- [Tip 8](#tip-8-主动压缩上下文) - 主动压缩上下文
- [Tip 9](#tip-9-完成编写测试的循环) - 完成编写测试的循环
- [Tip 10](#tip-10-cmda-和-ctrla-是你的好朋友) - Cmd+A 和 Ctrl+A

### 进阶技巧 (Tip 11-25)

- [Tip 11](#tip-11-使用-gemini-cli-作为备用) - 使用 Gemini CLI 作为备用
- [Tip 12](#tip-12-投资于自己的工作流) - 投资于自己的工作流
- [Tip 13](#tip-13-搜索对话历史) - 搜索对话历史
- [Tip 14](#tip-14-使用终端标签多任务处理) - 终端标签多任务处理
- [Tip 15](#tip-15-精简系统提示) - 精简系统提示
- [Tip 16](#tip-16-git-worktrees-并行工作) - Git Worktrees 并行工作
- [Tip 17](#tip-17-长时间任务的手动指数退避) - 手动指数退避
- [Tip 18](#tip-18-claude-code-作为写作助手) - 作为写作助手
- [Tip 19](#tip-19-markdown-是最棒的) - Markdown 是最棒的
- [Tip 20](#tip-20-使用-notion-保留链接) - 使用 Notion 保留链接
- [Tip 21](#tip-21-容器运行长时间高风险任务) - 容器运行高风险任务
- [Tip 22](#tip-22-使用是变好的最佳方式) - 使用是变好的最佳方式
- [Tip 23](#tip-23-克隆和半克隆对话) - 克隆对话
- [Tip 24](#tip-24-使用-realpath-获取绝对路径) - 使用 realpath
- [Tip 25](#tip-25-理解-claudemd-与-skills-等) - 理解 CLAUDE.md

### 高级技巧 (Tip 26-45)

- [Tip 26](#tip-26-交互式-pr-审查) - 交互式 PR 审查
- [Tip 27](#tip-27-claude-code-作为研究工具) - 作为研究工具
- [Tip 28](#tip-28-掌握输出验证方法) - 掌握输出验证方法
- [Tip 29](#tip-29-claude-code-作为-devops-工程师) - 作为 DevOps 工程师
- [Tip 30](#tip-30-保持-claudemd-简单) - 保持 CLAUDE.md 简单
- [Tip 31](#tip-31-claude-code-作为通用接口) - 作为通用接口
- [Tip 32](#tip-32-选择正确的抽象级别) - 选择正确的抽象级别
- [Tip 33](#tip-33-审计批准的命令) - 审计批准的命令
- [Tip 34](#tip-34-多写测试并使用-tdd) - 多写测试并使用 TDD
- [Tip 35](#tip-35-在未知情况下更勇敢) - 在未知情况下更勇敢
- [Tip 36](#tip-36-后台运行-bash-命令和子代理) - 后台运行命令
- [Tip 37](#tip-37-个性化软件时代已到来) - 个性化软件时代
- [Tip 38](#tip-38-导航和编辑输入框) - 导航和编辑输入框
- [Tip 39](#tip-39-花时间规划但快速原型) - 花时间规划但快速原型
- [Tip 40](#tip-40-简化过度复杂的代码) - 简化过度复杂的代码
- [Tip 41](#tip-41-自动化自动化) - 自动化自动化
- [Tip 42](#tip-42-分享你的知识) - 分享你的知识
- [Tip 43](#tip-43-保持学习) - 保持学习
- [Tip 44](#tip-44-安装-dx-插件) - 安装 dx 插件
- [Tip 45](#tip-45-快速设置脚本) - 快速设置脚本

---

## 详细技巧

### Tip 0: 自定义状态栏

你可以自定义 Claude Code 底部的状态栏，显示有用信息。我的设置显示：模型、当前目录、git 分支（如果有）、未提交文件数量、与 origin 的同步状态，以及 token 使用量的可视化进度条。它还显示第二行显示我的最后一条消息，这样我可以看到对话是关于什么的：

```
Opus 4.5 | 📁claude-code-tips | 🔀main (scripts/context-bar.sh uncommitted, synced 12m ago) | ██░░░░░░░░ 18% of 200k tokens
💬 This is good. I don't think we need to change the documentation...
```

这对于监控上下文使用和记住工作内容特别有帮助。该脚本支持 10 种颜色主题（橙色、蓝色、青色、绿色、薰衣草色、玫瑰色、金色、石板色、青色或灰色）。

**设置方法：** 使用 [示例脚本](https://github.com/ykdojo/claude-code-tips/blob/main/scripts/context-bar.sh) 并查看 [设置说明](https://github.com/ykdojo/claude-code-tips/blob/main/scripts/README.md)

---

### Tip 1: 学习必要的斜杠命令

有很多内置的斜杠命令（输入 `/` 查看全部）。以下是一些值得了解的：

**查看使用限额：**
```
/usage
```
显示当前会话、本周的使用情况，以及重置时间。

**切换 Chrome 集成：**
```
/chrome
```
启用/禁用 Claude 的原生浏览器集成。

**管理 MCP 服务器：**
```
/mcp
```
管理 Model Context Protocol 服务器。

**查看使用统计：**
```
/stats
```
显示 GitHub 风格的活动图表。

**清除对话：**
```
/clear
```
清除对话并重新开始。

---

### Tip 2: 用语音与 Claude 交流

我发现用语音交流比用手打字快得多。使用本地语音转录系统非常有帮助。

**Mac 上的选项：**
- [superwhisper](https://superwhisper.com/)
- [MacWhisper](https://goodsnooze.gumroad.com/l/macwhisper)
- [Super Voice Assistant](https://github.com/ykdojo/super-voice-assistant) (开源，支持 Parakeet v2/v3)

即使转录有错误，Claude 也能理解你的意思。

---

### Tip 3: 将大问题分解为小问题

不要一次性让 Claude 解决复杂问题。将大问题分解为小步骤，逐步完成。

**示例：**
```
❌ "帮我构建一个完整的电商网站"
✅ "第一步：创建用户登录页面"
✅ "第二步：添加产品列表功能"
✅ "第三步：实现购物车"
```

---

### Tip 4: 像专业人士一样使用 Git 和 GitHub CLI

学习使用 Git 和 GitHub CLI 可以大大提高效率：

```bash
# 查看 PR
gh pr list

# 审查 PR
gh pr review

# 创建分支
git checkout -b feature/xxx
```

---

### Tip 5: AI 上下文就像牛奶

**AI 上下文就像牛奶；新鲜和浓缩时最好！**

- 保持上下文新鲜（定期清理）
- 浓缩上下文（只提供必要信息）
- 避免上下文污染

---

### Tip 6: 从终端获取输出

将 Claude Code 的输出保存到文件：

```bash
claude "分析这个代码库" > analysis.md
```

---

### Tip 7: 设置终端别名

```bash
alias cc='claude'
alias cc-review='claude "审查最近的代码变更"'
```

---

### Tip 8: 主动压缩上下文

定期总结对话并清除不需要的内容：

```
"请总结我们目前讨论的内容，然后我们开始新的话题"
```

---

### Tip 9: 完成编写测试的循环

让 Claude 编写代码后，一定要让它编写测试：

```
"现在为这个功能编写单元测试"
```

---

### Tip 10: Cmd+A 和 Ctrl+A 是你的好朋友

在输入框中使用 Cmd+A/Ctrl+A 全选，然后粘贴新内容可以快速替换输入。

---

### Tip 11: 使用 Gemini CLI 作为备用

某些网站可能被 Claude 的浏览器阻止，可以使用 Gemini CLI 作为备用。

---

### Tip 12: 投资于自己的工作流

花时间优化你的工作流是值得的：
- 创建脚本自动化重复任务
- 设置终端别名
- 配置自定义状态栏

---

### Tip 13: 搜索对话历史

使用搜索功能查找之前的对话内容。

---

### Tip 14: 使用终端标签多任务处理

使用终端标签同时运行多个 Claude Code 会话。

---

### Tip 15: 精简系统提示

减少系统提示的长度可以节省 token。

---

### Tip 16: Git Worktrees 并行工作

使用 Git Worktrees 在多个分支上并行工作。

---

### Tip 17: 长时间任务的手动指数退避

对于长时间运行的任务，使用指数退避策略。

---

### Tip 18: Claude Code 作为写作助手

Claude Code 可以帮助写作、编辑和翻译。

---

### Tip 19: Markdown 是最棒的

使用 Markdown 格式化输出，易于阅读和分享。

---

### Tip 20: 使用 Notion 保留链接

使用 Notion 粘贴内容时可以保留链接。

---

### Tip 21: 容器运行长时间高风险任务

对于长时间或高风险任务，在容器中运行。

---

### Tip 22: 使用是变好的最佳方式

提高 Claude Code 技能的最佳方式就是多使用它。

---

### Tip 23: 克隆对话

克隆或半克隆对话以继续之前的工作。

---

### Tip 24: 使用 realpath 获取绝对路径

```bash
realpath file.txt
```

---

### Tip 25: 理解 CLAUDE.md 与 Skills 等

- **CLAUDE.md** - 项目特定的配置和说明
- **Skills** - 可复用的技能
- **Slash Commands** - 内置命令
- **Plugins** - 扩展功能

---

### Tip 26-45: 更多高级技巧

（详见原文）

---

## 📎 相关链接

- [原项目](https://github.com/ykdojo/claude-code-tips)
- [演示视频](https://www.youtube.com/watch?v=hiISl558JGE)
- [dx 插件](https://github.com/ykdojo/claude-code-tips#tip-44-install-the-dx-plugin)

---

**最后更新：** 2026-03-19  
**分类：** Claude Code / 使用技巧
