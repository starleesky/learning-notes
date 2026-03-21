# AI 设计技能栈 - 从无法设计到每周发布

**原文作者：** @neethanwu  
**推文链接：** https://x.com/neethanwu/status/2034786360356204934  
**整理日期：** 2026-03-21  
**分类：** AI Agent/设计工具

---

## 📌 核心摘要

> 作者不是设计师，但通过三层技能栈，从完全不会设计到每周发布设计作品。核心模式：**技能（专业知识）+ Canvas（工作表面）+ 灵感（训练眼光）**

**关键洞察：**
- 三层架构：Skills → Canvases → Inspiration
- 不需要成为设计师，需要正确的 harness
- 3 个月从 0 到每周发布

---

## 🏗️ 三层技能栈

### Layer 1: Skills（专业知识）

**作用：** 编码设计思维和最佳实践

| 技能 | 作者 | 用途 |
|------|------|------|
| **/delight** | - | 添加动画和 UI polish |
| **Design Engineer Skill** | @emilkowalski | 动画、UI 细节、设计思维 |
| **Interface Design** | @Dammyjay93 | 持久化设计规范（system.md） |
| **UI Skills** | @ibelick | 15 个开源技能（基础 UI/无障碍/动效） |

**核心价值：**
- 将专家思维编码为可复用技能
- 免费版本可借用专家思维
- 持久化设计决策（避免每轮对话遗忘）

---

### Layer 2: Agent Canvas（工作表面）

**作用：** 设计表面，使用你自己的 Agent（Claude Code/Codex 等）

| Canvas | 特点 | 用途 |
|--------|------|------|
| **Paper** (@paper) | 真实 HTML/CSS，非专有格式 | 设计系统、设计令牌、页面迭代 |
| **Pencil** (@tomkrcha) | JSON 格式 .pen，Git 可 diff | 版本化设计文件、多 Agent 协作 |

**Paper 优势：**
- 真实代码，无需转换层
- MCP 工具完全读写访问
- 本地 Agent 开箱即用

**Pencil 特色：**
- **Swarm Mode** - 最多 6 个 Agent 同时工作
  - 1 个处理排版
  - 1 个处理布局
  - 1 个传播设计系统
- 设计文件存放在 repo 中，像代码一样版本化

---

### Layer 3: Inspiration（训练眼光）

**作用：** 知道什么是好的设计

| 工具 | 用途 |
|------|------|
| **Variant** (@variantui) | 输入想法，滚动查看无尽设计解释；Style Dropper 吸收视觉 DNA |
| **Mobbin** | 查看顶级 App 如何处理 onboarding/settings/checkout |
| **Awwwards** | 网络设计前沿，jury 评分 |
| **Cosmos** (@thecosmos) | 收集灵感：网页设计/排版/摄影/建筑等 |

**Variant 工作流：**
1. 输入想法生成变体
2. 探索不同方向
3. 复制代码或导出 React
4. 交给 coding agent 实现
5. 提取令牌或组件
6. 构建更多视图和页面

---

## 🎯 核心价值

### 作者的成长路径

**3 个月前：**
- ❌ 完全不会设计
- ❌ 没有训练过的直觉
- ❌ 品味仍在发展中

**现在：**
- ✅ 每周发布设计
- ✅ 对输出满意
- ✅ 每天 20 分钟训练眼光

### 核心模式

```
Skills（专业知识）
    ↓
Canvases（工作表面）
    ↓
Inspiration（训练眼光）
    ↓
每周发布设计
```

---

## 💡 OpenClaw 可借鉴

### 1. 技能持久化

**当前问题：** Agent 每轮对话遗忘设计决策

**解决方案：**
```markdown
# system.md - 持久化设计规范

## Spacing
- Base: 8px
- Scale: 8, 16, 24, 32, 48, 64

## Colors
- Primary: #007AFF
- Secondary: #5856D6

## Components
- Button: padding 12px 24px, radius 8px
```

### 2. 多 Agent 协作（Swarm Mode）

**Pencil 的 Swarm Mode：**
- 6 个 Agent 同时工作
- 分工：排版/布局/设计系统传播

**OpenClaw 应用：**
```bash
# 多 Agent 并行设计
sprint-001: 排版 Agent
sprint-002: 布局 Agent
sprint-003: 设计系统 Agent
```

### 3. 设计 harness

**核心理念：**
> "You don't need to become a designer. You need the right harness."

**OpenClaw 应用：**
- 设计技能库（类似 gstack 的 15 个专家角色）
- 设计 Canvas（真实代码，非专有格式）
- 灵感收集系统

---

## 📝 待办事项

### 立即实践

- [ ] 创建持久化设计规范（system.md）
- [ ] 实现设计技能（/delight 类似功能）
- [ ] 集成 Variant 灵感工具

### OpenClaw 改进计划

- [ ] 设计专家角色（参考 gstack + AI 设计技能栈）
- [ ] 多 Agent 协作设计（Swarm Mode）
- [ ] 设计 Canvas 集成（Paper/Pencil 类似功能）

---

## 🔗 相关资源

**工具链接：**
- Emil Kowalski's Design Engineer Skill: @emilkowalski
- Interface Design: @Dammyjay93
- UI Skills: @ibelick
- Paper: @paper
- Pencil: @tomkrcha
- Variant: @variantui

**延伸阅读：**
- [gstack 专家角色](./garrytan-gstack.md)
- [多 Agent 协调器](../skills/multi-agent-coordinator/SKILL.md)

---

**最后更新：** 2026-03-21  
**分类：** ai-agents  
**标签：** #AIDesign #Skills #Canvas #Inspiration #AgentEngineering
