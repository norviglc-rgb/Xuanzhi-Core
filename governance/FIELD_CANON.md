# FIELD_CANON.md

## 用途

本文档定义玄织工作空间的规范字段命名与结构约定。

其角色是减少：

- 字段漂移
- 别名蔓延
- 模式不一致
- 追踪不匹配
- 注册表不匹配
- 交接数据包模糊

本文档对机器可读与半结构化制品具有规范性。

它特别适用于：

- `contracts/*.json`
- `policies/*.yaml`
- 追踪类结构
- 注册表类结构
- 任务与结果数据包
- 未来验证逻辑

如果同一概念使用多个名称，本文档定义偏好的规范选择。

---

## 规范命名规则

### 1. 使用 snake_case

规范字段名必须使用 `snake_case`。

偏好：

- `task_id`
- `risk_level`
- `owner_ref`
- `approval_state`

避免：

- `taskId`
- `riskLevel`
- `ownerRef`
- `approvalState`

### 2. 单数值使用单数名称

单数值使用单数名称。

偏好：

- `task_id`
- `risk_level`
- `summary`
- `executor`

仅对列表类数值使用复数名称。

偏好：

- `artifact_refs`
- `risk_reasons`
- `allowed_transitions`
- `trigger_types`

### 3. 偏好明确名称而非短模糊名称

偏好跨文件保留含义的名称。

偏好：

- `task_state`
- `step_state`
- `lifecycle_state`
- `review_state`
- `approval_state`
- `risk_level`
- `risk_score`

避免使用过于通用的顶级名称，如：

- `state`
- `status`
- `type`
- `score`
- `data`
- `result`

除非对象极其本地化且无歧义。

### 4. 身份使用 `_id`，指针使用 `_ref`

当字段标识当前或规范对象时使用 `_id`。

示例：

- `task_id`
- `step_id`
- `trace_id`
- `workflow_id`

当字段指向另一对象、制品或外部记录时使用 `_ref`。

示例：

- `owner_ref`
- `repo_ref`
- `artifact_ref`
- `memory_ref`

### 5. 时间戳使用 `_at`

偏好的时间字段以 `_at` 结尾。

示例：

- `created_at`
- `updated_at`
- `approved_at`
- `last_seen_at`
- `archived_at`

### 6. 在有帮助处使用明确的数字后缀

使用使存储值自解释的后缀。

偏好：

- `retry_count`
- `failure_count`
- `estimated_runtime_seconds`
- `heartbeat_interval_seconds`
- `cost_limit`
- `risk_score`

---

## 规范对象族

### 身份族

当对象必须可明确识别时使用。

典型字段：

- `*_id`
- `name`
- `title`
- `description`

示例：

- `task_id`
- `workflow_id`
- `agent_id`
- `trace_id`

### 所有权族

当责任或治理所有权重要时使用。

偏好字段：

- `owner_type`
- `owner_ref`

当结构化所有权重要时使用这些，而非单一模糊的 `owner` 字段。

### 审计族

用于起源与修改追踪。

偏好字段：

- `created_at`
- `updated_at`
- `created_by`
- `updated_by`
- `approved_at`
- `approved_by`

### 状态族

对不同状态域使用不同字段。

偏好字段：

- `task_state`
- `step_state`
- `review_state`
- `approval_state`
- `lifecycle_state`

当它们有不同语义时，不要折叠为单一 `state` 字段。

### 风险族

偏好字段：

- `risk_level`
- `risk_score`
- `risk_summary`
- `risk_reasons`
- `risk_ceiling`

### 摘要族

偏好字段：

- `summary`
- `status_summary`
- `reasoning_summary`

使用这些以保留压缩信号而非长文本。

### 分发与执行族

偏好字段：

- `task_type`
- `executor`
- `recommended_executor`
- `execution_mode`
- `approval_mode`

### 链接族

偏好字段：

- `parent_task_id`
- `parent_step_id`
- `parent_trace_id`
- `artifact_refs`
- `repo_ref`

---

## 规范字段区分

### `task_id` vs `step_id`

- `task_id` 标识工作的主要实践单元
- `step_id` 标识任务内部的界定单元

不要用一个替代另一个。

### `task_state` vs `step_state`

- `task_state` 描述任务级运行时条件
- `step_state` 描述步骤级运行时条件

这些不可随意合并。

### `review_state` vs `approval_state`

- `review_state` 描述评估状态
- `approval_state` 描述许可状态

审查与批准不是同一过程。

### `lifecycle_state` vs 运行时状态

- `lifecycle_state` 描述持久管理状态
- 运行时状态字段如 `task_state` 或 `step_state` 描述当前执行条件

不要为另一目的复用其中一个。

### `owner_type` / `owner_ref` vs `owner`

- `owner_type` + `owner_ref` 在结构化制品中偏好
- `owner` 仍可出现在文本中，但不应是偏好的面向机器形式

### `risk_level` vs `risk_score`

- `risk_level` 是分类的
- `risk_score` 更细粒度

仅当两种含义实际需要时同时使用两者。

### `summary` vs `reasoning_summary`

- `summary` = 结果或状态的整体简洁描述
- `reasoning_summary` = 路径、决策或提议存在原因的简洁解释

### `artifact_refs` vs 嵌入载荷

- `artifact_refs` 指向输出或文件
- 大型输出不应内联到每个数据包，除非必要

偏好引用而非载荷蔓延。

---

## 任务与步骤准则

### 任务级偏好字段

当适用时对结构化任务类对象使用这些字段：

- `task_id`
- `task_type`
- `summary`
- `task_state`
- `risk_level`
- `recommended_executor`
- `deliverable`
- `constraints`
- `created_at`
- `updated_at`

可选但通常有用：

- `approval_mode`
- `execution_mode`
- `repo_ref`
- `artifact_refs`
- `parent_task_id`

### 步骤级偏好字段

当适用时对界定清晰的步骤类对象使用这些：

- `step_id`
- `task_id`
- `summary`
- `step_state`
- `action`
- `expected_output`
- `risk_level`

可选但通常有用：

- `parent_step_id`
- `reasoning_summary`
- `artifact_refs`

如果步骤结构变得正式化，模式应优先于文本示例。

---

## 交接数据包准则

### 任务数据包字段

对于控制面到执行器交接数据包，偏好字段包括：

- `task_id`
- `task_type`
- `summary`
- `goal`
- `deliverable`
- `constraints`
- `risk_level`
- `recommended_executor`
- `repo_ref`
- `approval_mode`
- `execution_mode`

### 结果数据包字段

对于执行器到控制面结果数据包，偏好字段包括：

- `task_id`
- `summary`
- `status_summary`
- `task_state`
- `artifact_refs`
- `risk_level`
- `review_state`

可选但有用：

- `changed_files`
- `tests_run`
- `blockers`
- `next_step`
- `reasoning_summary`

如果数据包模式后续变得正式化，那些模式成为强制层，而本文档保持命名基准。

---

## 注册表准则

### 代理注册表偏好字段

定义结构化代理注册表对象时使用：

- `agent_id`
- `name`
- `description`
- `owner_type`
- `owner_ref`
- `risk_ceiling`
- `lifecycle_state`
- `created_at`
- `updated_at`

可选但有用：

- `permissions`
- `capability_scope`
- `isolation_level`
- `heartbeat_interval_seconds`
- `last_seen_at`

### 工作流注册表偏好字段

定义结构化工作流注册表对象时使用：

- `workflow_id`
- `name`
- `description`
- `owner_type`
- `owner_ref`
- `lifecycle_state`
- `risk_level`
- `created_at`
- `updated_at`

可选但有用：

- `trigger_types`
- `permissions`
- `version`
- `approved_at`
- `approved_by`

---

## 追踪准则

对于追踪类对象，偏好这些字段：

- `trace_id`
- `task_id`
- `step_id`
- `summary`
- `reasoning_summary`
- `risk_level`
- `review_state`
- `approval_state`
- `created_at`
- `artifact_refs`

可选但有用：

- `parent_trace_id`
- `executor`
- `status_summary`

避免将追踪结构变成叙述堆放。

追踪应保留有用的审计信号，而非完整对话蔓延。

---

## 记忆准则

对于长期记忆摘要条目或记忆相关的结构化引用，偏好：

- `summary`
- `category`
- `created_at`
- `updated_at`
- `artifact_refs`

对于稳定的根层记忆节，偏好语义分组而非伪数据库过度结构化。

`MEMORY.md` 应保持人类可读且摘要导向。

详细记忆规则属于策略与治理文件，而非根记忆摘要本身。

---

## 枚举字段指导

本文档不尝试全局冻结每个枚举值。

然而，以下原则适用：

- 枚举在稳定时应明确
- 枚举含义应跨文件一致
- 枚举变更应在相关处触发模式与策略审查

可能是枚举密集的字段包括：

- `task_state`
- `step_state`
- `review_state`
- `approval_state`
- `lifecycle_state`
- `risk_level`
- `task_type`

当这些变得关键时，它们应在模式或策略制品中硬化。

---

## 别名避免规则

不要随意为同一概念引入并行名称。

应避免的漂移示例：

- `status` 而非 `task_state`
- `kind` 而非 `task_type`
- `owner` 而非 `owner_type` + `owner_ref`
- `risk` 而非 `risk_level`
- `output_refs` 而非 `artifact_refs`
- `updated_on` 而非 `updated_at`

如果别名已存在于遗留材料中，在新工作中向偏好的字段名规范化。

---

## 迁移与重构规则

当字段被重命名或澄清时：

1. 识别旧名称
2. 识别新的规范名称
3. 更新模式与策略（如相关）
4. 注明变更的语义原因
5. 避免长期双重使用

目标是收敛，而非永久同义词共存。

---

## 新文件的实际规则

创建新结构化制品时：

1. 偏好现有规范字段名
2. 避免发明新的顶级通用名称
3. 明确分离状态域
4. 一致使用 `_id`、`_ref` 和 `_at`
5. 保持摘要简洁且可复用
6. 偏好制品引用而非嵌入批量输出
7. 如果结构变得重要则触发硬化审查

---

## 最终原则

字段命名不是装饰性的。

当字段漂移，结构就漂移。
当结构漂移，验证、分发、记忆、追踪与报告都变得更难。

本准则的存在是让结构化制品在工作空间成长时保持收敛。
