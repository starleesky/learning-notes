# 5 Agent Skill 设计模式 - Google ADK 开发者必读

**来源：** Google Cloud Tech (@googlecloudtech)  
**原文：** https://x.com/googlecloudtech/status/2033953579824758855  
**翻译整理：** 2026-03-19  
**分类：** AI Agents / 设计模式 / Google ADK

---

## 📌 核心观点

本文介绍了 5 个每个 Google Agent Development Kit (ADK) 开发者都应该掌握的 Agent Skill 设计模式。

---

## 📊 5 大设计模式

### 模式 1: 工具包装器 (Tool Wrapper)

**这是最简单的模式，也是最常见的起点。**

**核心思路：** 把某个领域的知识或约定封装进技能，让 Agent 在处理相关任务时自动调用这些知识，就像给它装了一个专家大脑。

**典型用法：** 把团队内部的编码规范塞进工作流。

**示例：FastAPI 开发专家**

```yaml
---
name: api-expert
description: FastAPI development best practices and conventions.
metadata:
  pattern: tool-wrapper
  domain: fastapi
---

你是 FastAPI 开发专家。把这些约定应用到用户的代码中。

## 核心约定
加载 'references/conventions.md' 获取完整的最佳实践列表。
```

**适用场景：**
- ✅ 内部库使用教学
- ✅ 编码规范执行
- ✅ 最佳实践应用

---

### 模式 2: 验证器 (Validator)

**用途：** 描述如何测试和验证代码是否正常工作。

**核心价值：** 验证类 Skill 直接影响 Agent 输出的质量。

**建议投入：** 让一个工程师花整整一周专门打磨验证 Skill，这个投入是值得的。

**高级用法：**
- 让 Agent 录制输出的视频，这样你能直接看到它测试了什么
- 在流程的每一步强制插入断言，验证状态是否正确
- 与 Playwright、tmux 等工具配合使用

**示例结构：**
```yaml
---
name: test-runner
description: Run tests and verify output
metadata:
  pattern: validator
  tools: [playwright, tmux]
---

## 验证流程
1. 执行代码
2. 录制输出视频
3. 在每步插入断言
4. 验证状态
```

---

### 模式 3: 工作流编排器 (Workflow Orchestrator)

**用途：** 自动化重复性工作流。

**示例：**
- 代码审查流程
- 部署流程
- 数据迁移流程

**核心优势：** 将复杂流程标准化，减少人为错误。

---

### 模式 4: 领域知识注入 (Domain Knowledge Injector)

**用途：** 为 Agent 注入特定领域的专业知识。

**示例：**
- 医疗行业术语和规范
- 金融行业合规要求
- 法律文档格式标准

**实现方式：**
- 创建领域术语表
- 添加合规检查清单
- 提供领域特定模板

---

### 模式 5: 代码风格规范 (Code Style Enforcer)

**用途：** 确保 Agent 输出的代码符合团队规范。

**包含内容：**
- 命名约定
- 注释规范
- 测试覆盖率要求
- 代码审查检查表

**示例：**
```yaml
---
name: code-style
description: Enforce team coding standards
metadata:
  pattern: style-enforcer
---

## 命名约定
- 类名：PascalCase
- 函数名：camelCase
- 常量：UPPER_SNAKE

## 测试要求
- 单元测试覆盖率 ≥ 80%
- 所有公共方法必须有测试
```

---

## 💡 关键洞察

### 洞察 1: Skills 是文件夹，不是文件

**错误理解：** Skills = 单个 SKILL.md 文件

**正确理解：** Skills = 文件夹结构 + 动态 hooks + 可探索内容

```
my-skill/
├── SKILL.md          # 技能说明
├── assets/           # 模板、数据、参考文件
├── references/       # 参考资料
├── scripts/          # 可执行脚本
└── examples/         # 使用示例
```

---

### 洞察 2: 验证类 Skill 值得重投入

**建议：** 让一个工程师花整整一周专门打磨验证 Skill

**回报：** 直接影响 Agent 输出的质量

---

### 洞察 3: 踩坑清单比文档更有价值

**不只是贴文档，而是包含：**
- 参考代码片段
- 「踩坑清单」——最容易犯哪些错
- 边界情况列表

---

## 🔗 相关资源

### Google ADK (Agent Development Kit)

**核心能力：**
- Agent 架构设计与部署
- 工具使用和 RAG 标准化
- 安全的多系统编排
- MCP (Model Context Protocol) 集成

**学习资源：**
- [Google Codelab: 使用 ADK 构建 AI 智能体](https://codelabs.developers.google.cn/devsite/codelabs/build-agents-with-adk-foundation)
- [Agentic AI with Google ADK & MCP Servers](https://www.udemy.com/course/agentic-ai-with-google-adk-mcp-servers/)

### 延伸阅读

- **《Agentic Design Patterns》** - Antonio Gullí (Google Cloud 资深工程总监)
  - 424 页，21 个核心模式 + 7 个高阶附录
  - 用"模式语言"把 AI Agent 从玩具级 Demo 提升到工业级可维护系统

---

## 📝 与我们的关联

### ai-skill-bench 项目

可以借鉴这 5 个模式来组织测试题目：

| 模式 | 对应测试维度 |
|------|-------------|
| 工具包装器 | 工具调用测试 |
| 验证器 | 代码生成测试（含验证） |
| 工作流编排器 | 复杂任务测试 |
| 领域知识注入 | 长文本理解测试 |
| 代码风格规范 | 代码规范测试 |

---

### agent-skills 项目

可以直接应用这 5 类分类法：

```
agent-skills/
├── tool-wrappers/      # 工具包装器
├── validators/         # 验证器
├── workflows/          # 工作流编排器
├── domain-knowledge/   # 领域知识注入
└── style-enforcers/    # 代码风格规范
```

---

### OpenClaw 工作区

可以为常用技能创建文件夹结构：

```
~/.openclaw/workspace/skills/
├── api-expert/         # FastAPI 专家
├── test-runner/        # 测试运行器
├── code-review/        # 代码审查流程
├── medical-domain/     # 医疗领域知识
└── code-style/         # 代码风格规范
```

---

## 🎯 下一步行动

- [ ] 为 ai-skill-bench 添加 5 类模式标签
- [ ] 为 agent-skills 创建 5 类文件夹结构
- [ ] 为内部工具创建工具包装器 Skill
- [ ] 打磨验证类 Skill（投入 1 周时间）

---

**最后更新：** 2026-03-19  
**分类：** AI Agents / 设计模式 / Google ADK  
**标签：** #AgentSkills #DesignPatterns #GoogleADK #最佳实践
