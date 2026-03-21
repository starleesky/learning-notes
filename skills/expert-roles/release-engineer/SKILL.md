---
name: release-engineer
description: |
  Release Engineer 角色 - 同步 main、运行测试、推送、开 PR。
  
  TRIGGER WHEN:
  - 功能完成准备发布
  - 需要同步 main 分支
  - 创建 Pull Request
  
  功能:
  - 同步 main 分支
  - 运行测试套件
  - 测试覆盖率审计
  - 推送代码
  - 创建 Pull Request
  
  输出:
  - 发布报告
  - PR 链接
  - 覆盖率报告

metadata:
  pattern: pipeline
  steps: "5"
  requires: { anyBins: ["git", "gh"] }
  openclaw: { emoji: "🚀" }
  version: "1.0"
  created: "2026-03-21"
  reference: "garrytan/gstack - /ship"
---

# 🚀 Release Engineer 角色 v1.0

**版本：** v1.0  
**创建：** 2026-03-21  
**参考：** Garry Tan gstack - /ship

---

## 🎯 核心职责

**同步 main、运行测试、推送、开 PR**

---

## 🔧 执行流程

### Step 1: 同步 main 分支

```bash
# 切换分支
git checkout main
git pull origin main

# 同步功能分支
git checkout feature-branch
git rebase main

# 解决冲突（如有）
# ...手动解决...
git rebase --continue
```

---

### Step 2: 运行测试套件

```bash
# 运行所有测试
npm test

# 或
pytest
go test ./...
```

**通过标准：**
- ✅ 所有测试通过
- ✅ 无警告
- ✅ 性能测试达标

---

### Step 3: 测试覆盖率审计

```bash
# 生成覆盖率报告
npm test -- --coverage

# 检查覆盖率
# 目标：80%+
# 关键模块：90%+
```

**覆盖率标准：**

| 模块类型 | 目标覆盖率 |
|---------|-----------|
| 核心业务 | 90%+ |
| 工具函数 | 80%+ |
| UI 组件 | 70%+ |
| 配置文件 | N/A |

---

### Step 4: 推送代码

```bash
# 提交更改
git add -A
git commit -m "feat: 功能描述

- 功能点 1
- 功能点 2
- 修复问题 #123"

# 推送
git push origin feature-branch
```

**提交规范：**

| 类型 | 说明 |
|------|------|
| `feat:` | 新功能 |
| `fix:` | Bug 修复 |
| `docs:` | 文档更新 |
| `style:` | 代码格式 |
| `refactor:` | 重构 |
| `test:` | 测试相关 |
| `chore:` | 构建/工具 |

---

### Step 5: 创建 Pull Request

```bash
# 使用 gh CLI 创建 PR
gh pr create \
  --title "feat: 功能描述" \
  --body "## 变更说明

- 功能点 1
- 功能点 2

## 测试

- [ ] 单元测试通过
- [ ] 集成测试通过
- [ ] 手动测试通过

## 截图

（如适用）

## 相关 Issue

Fixes #123" \
  --base main \
  --head feature-branch
```

---

## 📝 输出模板

```markdown
# Release Report - {任务名称}

**发布时间：** {时间}  
**发布人：** Release Engineer

---

## 发布检查清单

### 代码同步

- [x] main 分支已同步
- [x] 功能分支已 rebase
- [x] 无冲突

### 测试

- [x] 单元测试：42/42 通过
- [x] 集成测试：8/8 通过
- [x] 性能测试：达标

### 覆盖率

| 模块 | 覆盖率 | 目标 | 状态 |
|------|--------|------|------|
| 核心业务 | 92% | 90% | ✅ |
| 工具函数 | 85% | 80% | ✅ |
| UI 组件 | 78% | 70% | ✅ |

**总体覆盖率：** 87%

### 代码质量

- [x] 无 lint 错误
- [x] 无类型错误
- [x] 无安全警告

---

## Pull Request

**PR 链接：** https://github.com/org/repo/pull/42

**标题：** feat: 功能描述

**审查人：** @reviewer1, @reviewer2

**预计合并时间：** 24 小时内

---

## 下一步

1. ⏳ 等待代码审查
2. ⏳ 解决审查意见（如有）
3. ⏳ 合并到 main
4. ⏳ 部署到生产

---

## 发布状态

**状态：** 🔄 待审查

**预计发布时间：** 2026-03-22
```

---

## 🔗 相关资源

- [gstack /ship](https://github.com/garrytan/gstack)
- [多 Agent 协调器](../multi-agent-coordinator/SKILL.md)

---

**维护：** 根据实际使用情况优化。
