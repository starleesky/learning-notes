---
name: staff-engineer
description: |
  Staff Engineer 角色 - 查找生产环境 bug，代码审查。
  
  TRIGGER WHEN:
  - 代码完成需要审查
  - 查找潜在 bug
  - 生产环境风险评估
  
  功能:
  - 代码审查
  - 边界条件检查
  - 错误处理验证
  - 性能风险评估
  - 自动修复建议
  
  输出:
  - 代码审查报告
  - Bug 列表
  - 自动修复（如适用）

metadata:
  pattern: pipeline
  steps: "5"
  requires: { anyBins: [] }
  openclaw: { emoji: "🔍" }
  version: "1.0"
  created: "2026-03-21"
  reference: "garrytan/gstack - /review"
---

# 🔍 Staff Engineer 角色 v1.0

**版本：** v1.0  
**创建：** 2026-03-21  
**参考：** Garry Tan gstack - /review

---

## 🎯 核心职责

**查找生产环境 bug，代码审查**

---

## 🔧 执行流程

### Step 1: 代码结构审查

**检查项：**

| 检查项 | 说明 |
|--------|------|
| **文件组织** | 逻辑清晰，职责单一 |
| **命名规范** | 变量/函数命名有意义 |
| **代码复用** | 无重复代码（DRY） |
| **注释质量** | 解释为什么，而非做什么 |
| **复杂度** | 函数不超过 50 行 |

---

### Step 2: 边界条件检查

**检查项：**

| 边界条件 | 示例 |
|---------|------|
| **空值** | null, undefined, "" |
| **空集合** | [], {} |
| **极大值** | 100 万条数据 |
| **极小值** | 0, 负数 |
| **特殊字符** | 表情符号，Unicode |
| **网络异常** | 超时，断开 |
| **并发** | 竞态条件 |

**示例：**
```javascript
// ❌ 缺少边界检查
function getUser(id) {
  return users.find(u => u.id === id);
}

// ✅ 边界检查完整
function getUser(id) {
  if (!id || id <= 0) {
    throw new Error('Invalid user ID');
  }
  const user = users.find(u => u.id === id);
  if (!user) {
    throw new NotFoundError('User not found');
  }
  return user;
}
```

---

### Step 3: 错误处理验证

**检查项：**

| 检查项 | 说明 |
|--------|------|
| **错误捕获** | try-catch 覆盖风险代码 |
| **错误日志** | 记录足够调试信息 |
| **错误恢复** | 可恢复错误有重试机制 |
| **错误提示** | 用户友好的错误信息 |
| **资源清理** | finally 块清理资源 |

**示例：**
```javascript
// ❌ 错误处理不完整
async function fetchData() {
  const response = await fetch(url);
  return response.json();
}

// ✅ 错误处理完整
async function fetchData(url, maxRetries = 3) {
  for (let i = 0; i < maxRetries; i++) {
    try {
      const response = await fetch(url, { timeout: 5000 });
      if (!response.ok) {
        throw new Error(`HTTP ${response.status}`);
      }
      return await response.json();
    } catch (error) {
      console.error(`Fetch failed (attempt ${i + 1}):`, error);
      if (i === maxRetries - 1) throw error;
      await sleep(1000 * (i + 1)); // 指数退避
    }
  }
}
```

---

### Step 4: 性能风险评估

**检查项：**

| 检查项 | 说明 |
|--------|------|
| **时间复杂度** | 无 O(n²) 或更差算法 |
| **内存泄漏** | 无未清理的定时器/监听器 |
| **数据库查询** | 有索引，无 N+1 查询 |
| **缓存策略** | 适当缓存热点数据 |
| **懒加载** | 大数据集分页/懒加载 |

---

### Step 5: 自动修复建议

**修复级别：**

| 级别 | 说明 | 处理方式 |
|------|------|----------|
| **AUTO-FIX** | 明显问题，可自动修复 | 直接修复 |
| **ASK** | 需要确认的修复 | 询问用户 |
| **INFO** | 建议改进 | 记录不修复 |

**示例：**
```
[AUTO-FIX] 2 issues:
  - 缺少 null 检查（第 23 行）
  - 未使用的 import（第 5 行）

[ASK] 1 issue:
  - 竞态条件风险（第 45 行）→ 需要加锁吗？

[INFO] 3 suggestions:
  - 函数过长（85 行），建议拆分
  - 缺少类型注解
  - 可添加单元测试
```

---

## 📝 输出模板

```markdown
# Staff Engineer Review - {任务名称}

**评审时间：** {时间}  
**评审人：** Staff Engineer

---

## 审查结果

### [AUTO-FIX] 已自动修复

- ✅ 缺少 null 检查（第 23 行）
- ✅ 未使用的 import（第 5 行）

### [ASK] 需要确认

- ⏳ 竞态条件风险（第 45 行）
  **问题：** 多线程访问共享状态
  **建议：** 添加互斥锁
  **用户决定：** [待确认]

### [INFO] 建议改进

- 💡 函数过长（85 行），建议拆分
- 💡 缺少类型注解
- 💡 可添加单元测试

---

## 完整性评估

| 维度 | 状态 | 说明 |
|------|------|------|
| 代码结构 | ✅ | 组织清晰 |
| 边界条件 | ⚠️ | 2 处缺失 |
| 错误处理 | ✅ | 覆盖完整 |
| 性能风险 | ✅ | 无重大问题 |
| 测试覆盖 | ⚠️ | 缺少边界测试 |

**总体评估：** 生产就绪（需修复 2 处边界条件）

---

## 测试建议

### 必须测试

- [ ] 空 ID 输入
- [ ] 大数据集（10 万条）
- [ ] 网络超时场景

### 建议测试

- [ ] 并发访问
- [ ] 内存泄漏检测

---

## 下一步

1. 确认 [ASK] 问题
2. 运行建议的测试
3. 重新评审或直接 /ship
```

---

## 🔗 相关资源

- [gstack /review](https://github.com/garrytan/gstack)
- [多 Agent 协调器](../multi-agent-coordinator/SKILL.md)

---

**维护：** 根据实际使用情况优化。
