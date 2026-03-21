# 状态机规范

## 目的

本文档定义玄织工作空间的运行时状态模型。

其目的在于为以下事项提供稳定且明确的基线：

- 任务推进
- 步骤推进
- 评审推进
- 审批推进
- 长期开发工作
- 重试、重规划与升级行为

本文档对运行时状态语义具有规范性。

它不是追踪规范。
它不是注册表生命周期规范。
它不是完整的调度器实现手册。

这些内容属于相邻文档和策略制品。

---

## 核心原则

状态的存在是为了支撑控制，而非装饰。

一个好的状态机应当：

- 使进展可读
- 使失败处理明确
- 使升级可预测
- 使汇报可靠
- 使未来机器可读的转换表成为可能

一个坏的状态机会创造过多的状态、隐藏责任，或将多个状态域混入一个标签中。

因此，本工作空间保持状态域的分离。

---

## 状态域

本工作空间区分以下域：

- `task_state`（任务状态）
- `step_state`（步骤状态）
- `review_state`（评审状态）
- `approval_state`（审批状态）
- `epic_state`（史诗状态）
- `milestone_state`（里程碑状态）

这些状态不应被随意合并为单一的通用 `state`。

### 为什么

因为它们回答不同的问题：

- `task_state` -> 任务当前的运行时状态是什么？
- `step_state` -> 当前有界步骤的运行时状态是什么？
- `review_state` -> 评审的状态是什么？
- `approval_state` -> 审批的状态是什么？
- `epic_state` -> 长期史诗的当前状态是什么？
- `milestone_state` -> 当前里程碑的当前状态是什么？

---

## 任务状态模型

`task_state` 是任务的主要运行时状态。

### 标准任务状态

- `created`（已创建）
- `intake`（接收中）
- `planning`（规划中）
- `planned`（已规划）
- `running`（运行中）
- `waiting_review`（等待评审）
- `waiting_approval`（等待审批）
- `waiting_external`（等待外部）
- `waiting_user`（等待用户）
- `waiting_resource`（等待资源）
- `paused`（已暂停）
- `blocked`（已阻塞）
- `stalled`（已停滞）
- `replanning`（重规划中）
- `escalating`（升级中）
- `completed`（已完成）
- `failed`（已失败）
- `cancelled`（已取消）
- `archived`（已归档）
- `cooldown`（冷却中）

### 任务状态含义

#### `created`
任务已存在，但尚未被有意义地界定。

#### `intake`
任务正在被解释、分类和确定范围。

#### `planning`
正在设计可行路径。

#### `planned`
可行路径已产出，准备执行。

#### `running`
任务正在执行中积极进展。

#### `waiting_review`
执行已达到需要评审才能继续或关闭的阶段。

#### `waiting_approval`
执行已达到需要明确审批才能继续的阶段。

#### `waiting_external`
任务正在等待外部依赖。

示例：

- 外部 API 结果
- 远程作业完成
- 第三方回调
- 外部系统响应

#### `waiting_user`
任务正在等待用户直接输入或决策。

此状态应谨慎使用。

#### `waiting_resource`
任务正在等待内部执行能力或受限资源。

示例：

- 执行器槽位
- 分支或工作空间锁
- 运行时槽位
- 预算门禁

#### `paused`
任务已被有意停止，等待后续继续。

#### `blocked`
任务无法继续，因为缺少依赖、条件或权限要求。

#### `stalled`
任务似乎已停止取得有意义进展，需要检查。

`stalled` 与 `failed` 不相同。

#### `replanning`
系统正在不匹配、拒绝或失败后设计新路径。

#### `escalating`
任务正在被路由到更严格或更高权限的决策路径。

#### `completed`
任务已达到足够的成功结果。

#### `failed`
任务在当前路径上未能达到可行结果。

#### `cancelled`
任务在成功完成前被有意终止。

#### `archived`
任务已关闭，仅保留历史记录。

#### `cooldown`
完成、失败或重大转换后的短暂保持状态，等待下一个治理动作。

仅当这种冷却分离在操作上有用时才使用。

---

## 步骤状态模型

`step_state` 是有界执行步骤的运行时状态。

### 标准步骤状态

- `step_created`（步骤已创建）
- `step_ready`（步骤就绪）
- `step_running`（步骤运行中）
- `step_waiting_review`（步骤等待评审）
- `step_waiting_approval`（步骤等待审批）
- `step_retrying`（步骤重试中）
- `step_replanned`（步骤已重规划）
- `step_blocked`（步骤已阻塞）
- `step_completed`（步骤已完成）
- `step_failed`（步骤已失败）
- `step_cancelled`（步骤已取消）

### 步骤状态含义

#### `step_created`
步骤已定义，但尚未准备好执行。

#### `step_ready`
步骤已准备就绪，可以继续。

#### `step_running`
步骤正在活跃执行中。

#### `step_waiting_review`
步骤已产出需要评审的输出。

#### `step_waiting_approval`
步骤无法在未经审批的情况下继续。

#### `step_retrying`
步骤在有界失败后正在再次尝试。

#### `step_replanned`
原始步骤路径已变更，修订后的步骤现已生效。

#### `step_blocked`
步骤无法继续，因为缺少依赖或条件。

#### `step_completed`
步骤已成功。

#### `step_failed`
步骤未成功，且当前未在重试。

#### `step_cancelled`
步骤已被有意终止。

---

## 评审状态模型

`review_state` 追踪结果评估，而非执行。

### 标准评审状态

- `review_not_required`（无需评审）
- `review_pending`（评审待定）
- `review_running`（评审运行中）
- `review_passed`（评审通过）
- `review_failed`（评审失败）
- `review_conflicted`（评审冲突）

### 评审状态含义

#### `review_not_required`
当前上下文无需评审。

#### `review_pending`
需要评审，但尚未开始。

#### `review_running`
评审正在进行中。

#### `review_passed`
结果充分通过评审。

#### `review_failed`
结果未通过评审。

默认下游动作通常是重规划，而非盲目继续。

#### `review_conflicted`
评审信号存在实质性不一致，需要更严格的决策路径。

典型的下游动作是升级或治理仲裁。

---

## 审批状态模型

`approval_state` 追踪权限门禁，而非输出质量。

### 标准审批状态

- `approval_not_required`（无需审批）
- `approval_pending`（审批待定）
- `approval_running`（审批运行中）
- `approval_granted`（审批通过）
- `approval_rejected`（审批拒绝）
- `approval_escalated`（审批升级）

### 审批状态含义

#### `approval_not_required`
当前上下文无需审批。

#### `approval_pending`
需要审批，但尚未开始。

#### `approval_running`
审批评估正在进行中。

#### `approval_granted`
已获得继续的许可。

#### `approval_rejected`
继续的许可已被拒绝。

默认下游动作通常是重规划，除非策略要求取消或升级。

#### `approval_escalated`
审批无法在当前路径上解决，已被升级。

---

## 长期开发状态模型

长期开发工作可以使用：

- `epic_state`
- `milestone_state`
- `task_state`
- `step_state`

此层级结构仅应在工作确实从中受益时使用。

不要强制将每个任务放入史诗/里程碑结构中。

### 史诗状态

首选的 `epic_state` 值：

- `epic_created`（史诗已创建）
- `epic_running`（史诗运行中）
- `epic_paused`（史诗已暂停）
- `epic_blocked`（史诗已阻塞）
- `epic_completed`（史诗已完成）
- `epic_failed`（史诗已失败）
- `epic_cancelled`（史诗已取消）
- `epic_archived`（史诗已归档）

### 里程碑状态

首选的 `milestone_state` 值：

- `milestone_created`（里程碑已创建）
- `milestone_running`（里程碑运行中）
- `milestone_waiting_review`（里程碑等待评审）
- `milestone_waiting_approval`（里程碑等待审批）
- `milestone_blocked`（里程碑已阻塞）
- `milestone_replanning`（里程碑重规划中）
- `milestone_completed`（里程碑已完成）
- `milestone_failed`（里程碑已失败）
- `milestone_cancelled`（里程碑已取消）

### 长期层级规则

较低层级的失败不会自动意味着整个史诗的失败。

示例：

- 步骤可能失败，然后重规划
- 里程碑可能失败，然后重规划
- 史诗可以在修订里程碑结构后继续

系统应在升级到全局失败之前为受控恢复保留空间。

---

## 标准推进逻辑

### 正常任务推进

典型路径：

`created -> intake -> planning -> planned -> running -> completed`

### 评审门控推进

典型路径：

`running -> waiting_review -> running or completed`

### 审批门控推进

典型路径：

`running -> waiting_approval -> running or replanning`

### 外部等待推进

典型路径：

`running -> waiting_external -> running`

### 资源等待推进

典型路径：

`planned or running -> waiting_resource -> running`

### 暂停与恢复推进

典型路径：

`running -> paused -> running`

### 失败与恢复推进

典型路径：

`running -> failed -> replanning -> planned or running`

### 升级推进

典型路径：

`waiting_review or waiting_approval or failed -> escalating -> replanning or cancelled`

---

## 重试规则

重试是有界的。

### 默认重试限制

`max_retry = 2`

这意味着系统不应无限期地重试同一失败的步骤或路径。

### 重试范围

重试应被狭义解释。

默认含义是：

- 在有界限制内重试相同步骤或近似相同的步骤模式
- 不要通过重命名相同的失败模式来掩盖重复失败

### 限制后的重试

当达到重试限制时，默认的下一个动作不是再次盲目重试。

默认的下一个动作是：

- `replanning`
- 或如果失败足够严重，则 `escalating`

### 评审和审批失败的重试规则

- 评审失败 -> 默认下一个动作是 `replanning`
- 审批拒绝 -> 默认下一个动作是 `replanning`
- 重复未解决的冲突 -> 考虑 `escalating`

---

## 重规划规则

重规划是有界失败的默认恢复姿态。

重规划适用于以下情况：

- 里程碑失败
- 评审失败
- 审批拒绝
- 重复的有界步骤失败
- 路径被证明结构上不可靠
- 重大上下文或约束变更

重规划并不意味着"盲目重新开始"。

它意味着：

- 保留仍然有效的内容
- 替换失败的内容
- 修订路径质量
- 保持变更的可追溯性

---

## 升级规则

当当前治理路径不足时使用升级。

升级适用于以下情况：

- 风险过高
- 权限不足
- 评审存在实质性冲突
- 有界恢复尝试后持续重复失败
- 破坏性或结构上重要的决策无法在本地解决
- 策略要求人工干预

升级不应被用作深思熟虑的重规划的默认替代。

---

## 停滞规则

`stalled` 是一个诊断状态，而非 `failed` 的通用同义词。

当任务似乎已停止取得有意义进展，且原因尚未被其他更清晰的状态捕获时（例如：

- `waiting_external`
- `waiting_user`
- `waiting_resource`
- `blocked`
- `paused`

），应被视为停滞。

### 默认停滞阈值

`2 小时`

此阈值应被视为操作默认值，而非形而上真理。

### 标记停滞前

系统应首先检查任务是否实际上：

- 正在等待预期依赖
- 被有意暂停
- 因已知原因被阻塞
- 仍在接收有效心跳但无进展信号

只有在此之后才应应用 `stalled`。

---

## 长期活跃窗口

长期工作的默认单一活跃运行窗口为：

`24 小时`

这并不意味着整个项目必须在 24 小时内完成。

它意味着系统应将每个活跃运行窗口视为有界且可评审的。

在长时间活跃窗口后，系统应期望：

- 检查点
- 进展摘要
- 评审点
- 继续决策

---

## 控制器扫描频率

默认控制器扫描频率：

`5 分钟`

此频率旨在支持：

- 停滞检测
- 等待状态检查
- 审批/评审进展检查
- 长期任务监督
- 基本调度器可见性

本文档不定义完整的调度器实现。

它定义预期的时序姿态。

---

## 并行步骤规则

允许并行步骤。

但并行性绝非免费。

并行执行需要明确考虑：

- 资源调度
- 工作空间或仓库锁
- 环境冲突
- 代理槽位限制
- 碰撞风险
- 死锁风险

### 并行步骤指导

仅在以下情况下使用并行步骤：

- 工作实际上是可分离的
- 执行环境安全隔离
- 协调开销是合理的
- 回滚复杂性仍然可控

如果这些条件不成立，则首选顺序执行。

---

## 死锁与锁意识

本状态文档不定义完整的锁语义。

然而，它确立了以下运行时原则：

- 锁压力可能产生 `waiting_resource`
- 冲突的资源声明可能产生 `blocked`
- 未解决的执行停滞可能随后产生 `stalled`

详细的锁设计应存在于专用的锁或调度器规范中。

---

## 汇报期望

状态机的存在部分是为了支持可靠的汇报。

至少，每日汇报应能够呈现：

- 运行中的任务
- 运行中的代理
- 阻塞的任务
- 停滞的任务
- 等待审批的任务
- 近期失败
- 近期完成

本文档不定义汇报模板。
它定义汇报所依赖的状态可见性。

---

## 状态设计规则

### 规则 1：分离状态域

不要合并任务、步骤、评审、审批和生命周期状态。

### 规则 2：偏好有意义的状态而非装饰性状态

每个状态都应通过改善控制或汇报来证明其存在价值。

### 规则 3：偏好明确的等待原因

当知道 `waiting_external`、`waiting_user` 和 `waiting_resource` 这些原因时使用它们。

不要将它们隐藏在模糊的通用状态中。

### 规则 4：失败应倾向于先重规划再失控

有界失败通常应导致受控恢复，而非立即失控升级。

### 规则 5：升级是更严格的路径，而非严重性的同义词

当当前权限或治理不足时使用升级，而不仅仅是因为某事感觉困难。

---

## 与其他文档的关系

本文档应与以下文档对齐：

- `RISK_MODEL.md`
- `TRACE_SPEC.md`
- `DEV_TASK_MODEL.md`
- `contracts/dev_task_packet.schema.json`
- `contracts/dev_result_packet.schema.json`
- `main-agent-step.schema.json`
- 未来的 `policies/state_transitions.yaml`

本文档定义状态含义。
机器可读的转换表应定义可执行的允许转换。

---

## 最终原则

一个好的状态机使系统更易于治理、更易于恢复、更易于汇报。

如果状态在增加但不能改善控制，模型就在漂移。

正确的状态模型不是最复杂的那个。

它是使进展、阻塞、恢复和升级变得可读的那个。
