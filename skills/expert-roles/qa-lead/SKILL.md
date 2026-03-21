---
name: qa-lead
description: |
  QA Lead 角色 - 真实浏览器测试，发现并修复 bug。
  
  TRIGGER WHEN:
  - 功能完成需要测试
  - 需要真实浏览器验证
  - 用户流程测试
  
  功能:
  - 真实浏览器操作（opencli）
  - 用户流程测试
  - Bug 发现与修复
  - 回归测试生成
  
  输出:
  - 测试报告
  - Bug 列表
  - 修复验证

metadata:
  pattern: pipeline
  steps: "5"
  requires: { anyBins: ["opencli"] }
  openclaw: { emoji: "🧪" }
  version: "1.0"
  created: "2026-03-21"
  reference: "garrytan/gstack - /qa"
---

# 🧪 QA Lead 角色 v1.0

**版本：** v1.0  
**创建：** 2026-03-21  
**参考：** Garry Tan gstack - /qa

---

## 🎯 核心职责

**真实浏览器测试，发现并修复 bug**

---

## 🔧 执行流程

### Step 1: 测试计划

**测试场景：**

| 场景 | 说明 |
|------|------|
| **主流程** | 核心功能正常使用 |
| **边界流程** | 极端数据测试 |
| **异常流程** | 错误输入处理 |
| **性能测试** | 大数据量响应 |

---

### Step 2: 真实浏览器测试

**使用 opencli：**

```bash
# 打开应用测试
opencli browser open <URL>

# 执行用户操作
opencli browser click "登录按钮"
opencli browser fill "用户名" "test@example.com"
opencli browser submit

# 验证结果
opencli browser text "欢迎信息"
```

---

### Step 3: Bug 发现与修复

**Bug 分类：**

| 级别 | 说明 | 处理 |
|------|------|------|
| **P0** | 阻塞性 bug | 立即修复 |
| **P1** | 严重 bug | 优先修复 |
| **P2** | 一般 bug | 计划修复 |
| **P3** | 轻微问题 | 后续优化 |

---

### Step 4: 修复验证

**验证流程：**

1. 应用修复
2. 重新测试
3. 验证通过
4. 生成回归测试

---

### Step 5: 回归测试生成

**为每个修复生成回归测试：**

```javascript
// 回归测试示例
describe('登录功能', () => {
  it('应该接受有效邮箱', async () => {
    await page.fill('#email', 'test@example.com');
    await page.click('#submit');
    expect(await page.text('.welcome')).toContain('欢迎');
  });
  
  it('应该拒绝无效邮箱', async () => {
    await page.fill('#email', 'invalid');
    await page.click('#submit');
    expect(await page.text('.error')).toContain('邮箱格式错误');
  });
});
```

---

## 📝 输出模板

```markdown
# QA Lead Report - {任务名称}

**测试时间：** {时间}  
**测试人：** QA Lead

---

## 测试概览

| 场景 | 总数 | 通过 | 失败 |
|------|------|------|------|
| 主流程 | 5 | 5 | 0 |
| 边界流程 | 3 | 2 | 1 |
| 异常流程 | 4 | 3 | 1 |
| 性能测试 | 2 | 2 | 0 |

---

## Bug 列表

### P0 - 阻塞性

- ❌ 登录按钮在移动端无法点击

### P1 - 严重

- ❌ 邮箱格式验证缺失

### P2 - 一般

- ⚠️ 错误信息不够友好

---

## 修复状态

| Bug | 状态 | 验证 |
|-----|------|------|
| 登录按钮问题 | ✅ 已修复 | ✅ 通过 |
| 邮箱验证 | ✅ 已修复 | ✅ 通过 |
| 错误信息 | ⏳ 待修复 | - |

---

## 回归测试

生成 3 个回归测试：
- [ ] 登录按钮点击测试
- [ ] 邮箱格式验证测试
- [ ] 错误信息显示测试

---

## 测试结论

**发布建议：** ⚠️ 有条件发布

**条件：**
- 修复 P2 bug 后可发布
- P0/P1 已全部修复
```

---

## 🔗 相关资源

- [gstack /qa](https://github.com/garrytan/gstack)
- [多 Agent 协调器](../multi-agent-coordinator/SKILL.md)

---

**维护：** 根据实际使用情况优化。
