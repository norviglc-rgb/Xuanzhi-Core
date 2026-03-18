# NOCOBASE_INTEGRATION.md

## 1. 文档目的
定义 NocoBase 在 Xuanzhi-Core 系统中的角色、边界、接入方式与当前状态。

---

## 2. 组件定位
NocoBase 是当前系统中的**后台、表单、配置、人工审核平面**。

它负责：
- 后台管理
- 表单承载
- 配置管理
- 人工审核
- 审批与运营支撑

---

## 3. 与 Xuanzhi-Core 的关系
Xuanzhi-Core 负责治理规则、状态流转与结果收敛；
NocoBase 负责承载人工审核与后台配置等操作平面。

两者关系是：
- Xuanzhi-Core 定义"何时需要审批 / 审核"
- NocoBase 提供"在哪里完成这些动作"的承载层
- 审核结果回传 Xuanzhi-Core 做状态更新与记录

---

## 4. 边界
NocoBase 不负责：
- 项目目标定义
- 风险模型源头定义
- 全局架构基线定义
- 取代治理中枢的决策地位

---

## 5. 输入输出关系

### 5.1 输入来源
- 待审核任务（来自 Xuanzhi-Core 或 n8n）
- 待审批表单
- 配置项维护请求
- 例外处理请求

### 5.2 输出内容
- 审核结果（通过/拒绝/需补充信息）
- 审批决定
- 配置更新结果
- 可回传治理层的结构化记录

---

## 6. 审批表单模型

### 6.1 通用审批表单字段
| 字段名 | 类型 | 说明 |
|-------|------|------|
| request_id | string | 请求唯一标识 |
| request_type | enum | 请求类型（workflow_activation, registry_change, etc.） |
| requester | string | 发起方 |
| risk_level | enum | 风险等级 (R0-R4) |
| summary | text | 请求摘要 |
| detail | text | 详细说明 |
| artifacts | json | 相关产物引用 |
| created_at | datetime | 创建时间 |
| status | enum | 状态（pending/approved/rejected） |

### 6.2 审批动作字段
| 字段名 | 类型 | 说明 |
|-------|------|------|
| reviewer | string | 审核人 |
| reviewed_at | datetime | 审核时间 |
| decision | enum | 决定（approved/rejected/need_info） |
| comment | text | 审核意见 |

---

## 7. 人工审核队列设计

### 7.1 队列分类
| 队列名称 | 优先级 | 内容 |
|---------|-------|------|
| urgent | 高 | R3/R4 级别审批请求 |
| normal | 中 | R2 级别审批请求 |
| low | 低 | 配置变更、非紧急请求 |

### 7.2 队列规则
- 紧急队列：24 小时内必须处理
- 普通队列：72 小时内必须处理
- 低优先级队列：7 天内处理

### 7.3 超时处理
- 超时未处理：自动升级通知
- 重复超时：触发告警

---

## 8. 与策略文件的映射

### 8.1 与 approval_rules.yaml 的映射
```yaml
# approval_rules.yaml 中的规则映射到 NocoBase 表单
approval_modes:
  - governance_required  # NocoBase 自动流转
  - human_required      # NocoBase 生成人工审核单
```

### 8.2 与 risk_policy.yaml 的映射
```yaml
# risk_policy.yaml 中的规则决定审批流程
R3:
  approval_required: true
  escalation_likely: conditional
  # -> NocoBase 创建高优先级审批单

R4:
  immediate_block: true
  escalate: true
  # -> NocoBase 创建紧急审批单 + 告警
```

---

## 9. 审核日志与审计落点

### 9.1 日志内容
- 审批请求创建记录
- 审核动作记录（谁、何时、什么决定）
- 状态变更记录
- 评论和附件记录

### 9.2 审计要求
- 所有审核动作不可删除
- 保留完整历史记录
- 支持导出审计报告

### 9.3 与 TRACE_SPEC.md 的集成
- 每个审批请求生成 `trace_id`
- 审核动作作为 `trace_event` 记录
- 支持完整链路追踪

---

## 10. 当前状态
- ✅ NocoBase 已部署
- ✅ 基本后台框架搭建
- ⏳ 审批表单模型待细化
- ⏳ 审核队列设计待实施

---

## 11. 待补事项
- [ ] 完整的审批表单模板
- [ ] 审核队列 UI 设计
- [ ] 与 Xuanzhi-Core 的 API 对接
- [ ] 审计日志导出功能

---

## 12. 维护要求
- 若审批与人工审核机制变化，必须同步更新本文件
- 若 NocoBase 在系统中承担新的后台职责，应修订边界描述
- 新增审批类型时，应更新审批表单模型
