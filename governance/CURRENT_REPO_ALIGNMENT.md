# 当前仓库对齐

## 1. 目的
本文件用于把当前仓库中的现有文件和目录，统一映射到工程化基线体系之下，明确：

- 哪些是核心真相
- 哪些是解释性文档
- 哪些是空壳或占位
- 哪些已经过时或需要重写
- 下一步应先修什么

---

## 2. 判断口径

### 2.1 状态分级
- **核心**：当前必须保留，且直接支撑项目基线或治理闭环
- **草案**：有价值，但内容尚未稳定，不能当最终依据
- **空壳**：文件存在但无实际内容，不能视为完成
- **过时**：曾有价值，但已与当前技术栈或目录现实不一致
- **待删除/待合并**：角色重复、误导性强或应并入其他文件

### 2.2 所属基线
- **目标**
- **边界**
- **架构**
- **阶段推进**
- **变更控制**
- **质量门禁**
- **其他治理支撑**
- **集成说明**
- **工作流资产**
- **记忆沉淀**

### 2.3 优先级
- **P0**：影响项目理解、架构一致性、当前推进判断
- **P1**：影响中期工程化收敛
- **P2**：影响表达质量或后续维护便利性

---

## 3. 根层文件对齐

| 文件 | 当前状态 | 所属基线 | 主要问题 | 处理动作 | 优先级 |
|---|---|---:|---|---|---:|
| `AGENTS.md` | 草案 | 其他治理支撑 | 需确认是否承担过多执行细节 | 保留，核定职责边界 | P0 |
| `AGENTS.bak.md` | 过时 | 其他治理支撑 | 备份体量过大，易造成事实漂移 | 移出主线认知，仅作历史档案 | P1 |
| `BOOT.md` | 草案 | 其他治理支撑 | 需确认与 `BOOTSTRAP.md` 的关系 | 保留，收敛定义 | P1 |
| `BOOTSTRAP.md` | 空壳 | 其他治理支撑 | 空文件，占据关键命名位 | 补内容或删除 | P0 |
| `HEARTBEAT.md` | 草案 | 其他治理支撑 | 可能与记忆/状态文档边界重叠 | 保留，后续判边界 | P1 |
| `IDENTITY.md` | 核心 | 目标 / 边界 | 若内容稳定，应视为根层核心之一 | 保留 | P0 |
| `MEMORY.md` | 核心 | 其他治理支撑 / 记忆原则 | 需确认与 `memory/` 的关系 | 保留 | P0 |
| `MEMORY.bak.md` | 过时 | 记忆沉淀 | 历史备份可能污染当前认知 | 降级为档案 | P1 |
| `README.md` | 核心 | 目标 / 架构 / 边界 | 需与新技术栈同步 | 重写为统一入口 | P0 |
| `SOUL.md` | 草案 | 目标 / 原则 | 可能偏哲学化，需防止抽象溢出 | 收缩为原则层 | P1 |
| `SOUL.bak.md` | 过时 | 原则历史 | 历史文本易形成双重真相 | 档案化 | P2 |
| `TOOLS.md` | 核心 | 其他治理支撑 | 需同步 Higress / Coze Studio / n8n / NocoBase | 更新 | P0 |
| `TOOLS.bak.md` | 过时 | 工具历史 | 同上 | 档案化 | P2 |
| `USER.md` | 核心 | 边界 / 用户关系 | 可能是根层必要常驻面 | 保留 | P0 |
| `USER.bak.md` | 过时 | 用户关系历史 | 备份不应进入主线判断 | 档案化 | P2 |
| `LICENSE` | 核心 | 其他 | 无 | 保留 | P2 |
| `.gitignore` | 核心 | 工程配置 | 无 | 保留 | P2 |

### 根层结论
1. 根层**数量偏多**，但不是全部都该删。
2. 当前最大问题不是"文件多"，而是**核心文件、草案文件、历史备份混在同一认知层**。
3. 根层需要尽快形成三类分层：
   - 常驻核心
   - 解释性草案
   - 历史档案（不参与当前判断）

---

## 4. `.claude/` 目录对齐

| 文件 | 当前状态 | 所属基线 | 主要问题 | 处理动作 | 优先级 |
|---|---|---:|---|---|---:|
| `CURRENT_WORKSPACE_STATUS.md` | 过时 | 阶段推进 / 现状说明 | 与当前仓库现实存在冲突 | 不作事实源，仅作阶段参考 | P0 |
| `DESIGN_CORE_PRINCIPLES_AND_RED_LINES.md` | 草案 | 边界 / 质量门禁 | 有价值，但需并入正式基线 | 抽取内容并归并 | P0 |
| `NEW_SESSION_MASTER_CONTEXT.md` | 草案 | 其他治理支撑 | 偏会话交接，不应当项目基线 | 保留为交接材料 | P1 |
| `NEXT_PHASE_EXECUTION_PLAN.md` | 草案 | 阶段推进 | 可参考，但不能代替正式阶段文档 | 归并到 `DELIVERY_STAGES.md` | P0 |
| `OFFICIAL_COMPATIBILITY_AND_PRACTICE.md` | 草案 | 边界 / 集成说明 | 有经验价值，但平台事实需谨慎 | 抽取可信部分 | P1 |
| `OPEN_QUESTIONS_AND_TECH_DEBT.md` | 核心 | 阶段推进 / 质量门禁 | 对技术债识别有价值 | 保留，转为正式债务清单 | P0 |
| `settings.local.json` | 核心 | 本地配置 | 非基线文档 | 保留 | P2 |

### `.claude/` 结论
这是**会话层和阶段交接层**，不是项目宪法层。
应保留，但必须明确降级：**可参考，不可直接当主事实源**。

---

## 5. `contracts/` 目录对齐

| 文件 | 当前状态 | 所属基线 | 主要问题 | 处理动作 | 优先级 |
|---|---|---:|---|---|---:|
| `agent_registry.schema.json` | 核心 | 架构 / 规则硬化 | 需校验与治理文档一致性 | 保留并对齐术语 | P0 |
| `dev_result_packet.schema.json` | 核心 | 架构 / 质量门禁 | 需确认与执行闭环一致 | 保留 | P0 |
| `dev_task_packet.schema.json` | 核心 | 架构 / 阶段推进 | 需确认是否仍适配当前执行器地图 | 保留 | P0 |
| `main-agent-step.schema.json` | 草案 | 架构 / 规则硬化 | 文档中已提到其放置与角色未完全定 | 保留，后续校准 | P1 |
| `trace_event.schema.json` | 核心 | 架构 / 质量门禁 | 对追踪链路重要 | 保留 | P0 |
| `workflow_registry.schema.json` | 核心 | 架构 / 边界 | 需与 `workflows/` 的真实角色对齐 | 保留 | P1 |

### `contracts/` 结论
这是目前仓库中**最像工程化骨架的部分之一**。
问题不在"有没有"，而在**是否与 prose 文档、真实技术栈和 workflow 资产一致**。

---

## 6. `governance/` 目录对齐

| 文件 | 当前状态 | 所属基线 | 主要问题 | 处理动作 | 优先级 |
|---|---|---:|---|---|---:|
| `AGENT_REGISTRY_SPEC.md` | 核心 | 架构 | 需与 schema 对齐 | 保留 | P0 |
| `APPROVAL_POLICY.md` | 核心 | 变更控制 / 质量门禁 | 需与 NocoBase 的引入对齐 | 更新 | P0 |
| `CONTROLLER_API_SPEC.md` | 草案 | 架构 / 运行化 | 若无 bridge 实现，可能偏前置 | 保留，标记阶段性 | P1 |
| `DEV_TASK_MODEL.md` | 核心 | 架构 / 阶段推进 | 需与执行器映射一致 | 保留 | P0 |
| `FIELD_CANON.md` | 核心 | 架构 / 质量门禁 | 极重要，防止字段漂移 | 保留 | P0 |
| `GOVERNANCE_GLOSSARY.md` | 核心 | 边界 / 质量门禁 | 应成为统一术语源 | 保留并扩充新组件 | P0 |
| `MEMORY_WRITE_POLICY.md` | 核心 | 质量门禁 / 记忆沉淀 | 需与 `memory_write_rules.yaml` 对齐 | 保留 | P0 |
| `PROJECT_BOOTSTRAP_SPEC.md` | 草案 | 阶段推进 / 运行化 | 与 `BOOTSTRAP.md` 关系需收敛 | 保留并对齐 | P1 |
| `REPO_TEMPLATE_SPEC.md` | 草案 | 阶段推进 | 若当前重点不是模板扩散，可降优先级 | 保留 | P2 |
| `RISK_MODEL.md` | 核心 | 质量门禁 / 变更控制 | 需与新增人工审核平面对齐 | 更新 | P0 |
| `ROOT_FILE_POLICY.md` | 核心 | 边界 | 当前非常关键 | 保留 | P0 |
| `RULE_HARDENING_POLICY.md` | 空壳 | 质量门禁 / 阶段推进 | 占据高价值位置却为空 | 立即补或移除 | P0 |
| `STATE_MACHINE.md` | 核心 | 架构 / 质量门禁 | 需与 `state_transitions.yaml` 一致 | 保留 | P0 |
| `TRACE_SPEC.md` | 核心 | 架构 / 质量门禁 | 对可追踪性重要 | 保留 | P0 |
| `WORKFLOW_REGISTRY_SPEC.md` | 核心 | 架构 / 边界 | 需与 `workflows/` 实际状态对齐 | 保留 | P1 |
| `templates/RULE_CHANGE_TEMPLATE.md` | 核心 | 变更控制 | 有实用价值 | 保留 | P1 |

### `governance/` 结论
这是项目的**解释性治理核心**。
整体骨架不错，但有两个刺点：
1. `RULE_HARDENING_POLICY.md` 空着，像门牌写了"中央银行"，推门进去是储物间。
2. 若引入 Coze Studio / n8n / NocoBase / Higress 后不更新术语与风险/审批模型，治理文档会开始失真。

---

## 7. `integrations/` 目录对齐

| 文件 | 当前状态 | 所属基线 | 主要问题 | 处理动作 | 优先级 |
|---|---|---:|---|---|---:|
| `CLAUDE_CODE_EXECUTION.md` | 核心 | 架构 / 集成说明 | 需与"默认开发执行器"定位一致 | 保留 | P0 |
| `COMFYUI_PIPELINE.md` | 空壳 | 集成说明 | 无内容，价值未证实 | 延后或删除 | P2 |
| `FASTGPT_INTEGRATION.md` | 空壳 / 过时风险 | 集成说明 | 生态已变化，且 Coze Studio 已加入 | 重判角色，补或降级 | P1 |
| `GITLAB_INTEGRATION.md` | 核心 | 集成说明 | 需与当前边界文档一致 | 保留 | P1 |
| `PUBLISH_PIPELINE.md` | 空壳 | 集成说明 | 无内容 | 延后 | P2 |
| `VIDEO_PIPELINE.md` | 空壳 | 集成说明 | 无内容 | 延后 | P2 |

### `integrations/` 当前缺口
应新增或补齐这些文档位：
- `HIGRESS_INTEGRATION.md`
- `COZE_STUDIO_INTEGRATION.md`
- `N8N_INTEGRATION.md`
- `NOCOBASE_INTEGRATION.md`

### `integrations/` 结论
这是当前**最明显落后于真实技术栈**的目录之一。
旧世界还写在纸上，新世界已经搬进屋里了。

---

## 8. `policies/` 目录对齐

| 文件 | 当前状态 | 所属基线 | 主要问题 | 处理动作 | 优先级 |
|---|---|---:|---|---|---:|
| `approval_rules.yaml` | 核心 | 变更控制 / 质量门禁 | 需映射人工审核平面 | 更新 | P0 |
| `memory_write_rules.yaml` | 核心 | 质量门禁 / 记忆沉淀 | 需与 prose 一致 | 保留 | P0 |
| `risk_policy.yaml` | 核心 | 质量门禁 / 变更控制 | 需对接 NocoBase / 审批流 | 更新 | P0 |
| `state_transitions.yaml` | 核心 | 架构 / 质量门禁 | 需与 `STATE_MACHINE.md` 一致 | 保留 | P0 |

### `policies/` 结论
这是目前仓库里**最接近可硬化规则层**的部分。
重点不是重写，而是：
- 和 prose 对齐
- 和新组件对齐
- 和最小闭环对齐

---

## 9. `memory/` 目录对齐

| 文件 | 当前状态 | 所属基线 | 主要问题 | 处理动作 | 优先级 |
|---|---|---:|---|---|---:|
| `2026-03-15.md` | 空壳 | 记忆沉淀 | 记忆机制未真正运行 | 补样例或删除占位 | P1 |

### `memory/` 结论
目前更像"预留容器"，还不是有效记忆层。
说明系统还没真正形成**稳定的阶段复盘与沉淀机制**。

---

## 10. `skills/` 目录对齐

| 文件 | 当前状态 | 所属基线 | 主要问题 | 处理动作 | 优先级 |
|---|---|---:|---|---|---:|
| `README.md` | 空壳 | 工作流资产 / 其他 | 技能层角色未定义 | 若暂无明确用途，延后 | P2 |

### `skills/` 结论
当前角色不清。
除非很快要把某类流程做成明确 skill 资产，否则不应优先投入。

---

## 11. `workflows/` 目录对齐

| 文件 | 当前状态 | 所属基线 | 主要问题 | 处理动作 | 优先级 |
|---|---|---:|---|---|---:|
| `daily_brief/README.md` | 空壳 | 工作流资产 | 无实际定义 | 延后或补最小说明 | P2 |
| `media_generation/README.md` | 空壳 | 工作流资产 | 无实际定义 | 延后 | P2 |
| `publish/README.md` | 空壳 | 工作流资产 | 无实际定义 | 延后 | P2 |
| `weekly_review/README.md` | 空壳 | 工作流资产 | 无实际定义 | 延后或选一个先做闭环 | P1 |

### `workflows/` 结论
目前这是**占位层，不是运行层**。
如果继续往这里堆 README，却没有任何一条链路跑通，就会变成一个很有气势的纸板布景。

---

## 12. 六类工程化基线的落位建议

| 基线类别 | 建议文件 |
|---|---|
| 目标 | `PROJECT_CHARTER.md` |
| 边界 | `BOUNDARY_AND_SCOPE.md` |
| 架构 | `ARCHITECTURE_BASELINE.md` |
| 阶段推进 | `DELIVERY_STAGES.md` |
| 变更控制 | `CHANGE_CONTROL.md` |
| 质量门禁 | `QUALITY_GATES.md` |

### 当前映射判断
- **目标**：已有部分内容分散在 `README.md` / `IDENTITY.md` / `SOUL.md`
- **边界**：已有部分内容分散在 `ROOT_FILE_POLICY.md` / `DESIGN_CORE_PRINCIPLES_AND_RED_LINES.md`
- **架构**：已有较强骨架，主要在 `ARCHITECTURE_BASELINE.md` 与 `contracts/`
- **阶段推进**：目前分散在会话交接文档中，需正式收编
- **变更控制**：目前部分存在于治理与经验文档，需正式独立
- **质量门禁**：目前隐含在红线 / 风险 / 状态 / 记忆策略中，需正式集中定义

---

## 13. 当前最重要的问题清单（P0）

### P0-1：基线文档尚未正式落位
虽然已有不少内容，但六类工程化基线还未形成正式主轴。

### P0-2：技术栈更新未完全同步
至少以下变更必须进入正式基线：
- LiteLLM -> Higress
- 新增 Coze Studio
- 新增 n8n
- 新增 NocoBase

### P0-3：空壳文件占据关键位置
尤其：
- `BOOTSTRAP.md`
- `RULE_HARDENING_POLICY.md`

### P0-4：会话交接文档与项目基线混层
`.claude/` 中若不降级处理，会持续污染"当前事实判断"。

### P0-5：集成层明显滞后
`integrations/` 还没有反映当前真实组件地图。

---

## 14. 建议处理顺序

### 第一步：正式落位六类基线文档
先建立：
- `PROJECT_CHARTER.md`
- `BOUNDARY_AND_SCOPE.md`
- `ARCHITECTURE_BASELINE.md`
- `DELIVERY_STAGES.md`
- `CHANGE_CONTROL.md`
- `QUALITY_GATES.md`

### 第二步：同步技术栈与术语
统一替换并更新：
- LiteLLM -> Higress
- 引入 Coze Studio / n8n / NocoBase
- 更新术语表 / 架构 / README / 工具 / 集成

### 第三步：处理关键空壳
优先处理：
- `RULE_HARDENING_POLICY.md`
- `BOOTSTRAP.md`

### 第四步：给 `.claude/` 降级
明确其为：
- 会话交接材料
- 阶段参考材料
- 不作为项目主事实源

### 第五步：收敛 `integrations/`
补齐真实集成文档，标记无效占位项。

---

## 15. 当前总评

### 核心判断
这个仓库**不是没有骨架**，恰恰相反，骨架已经不差。
真正的问题是：**基线、会话交接、历史备份、空壳占位、实时技术栈变化，几层东西叠在一起了。**

### 当前阶段判断
最合理的阶段应是：
- **Stage 0：基线确立**
- **Stage 1：结构收敛**

还不适合直接大规模扩 workflow 或复杂运行化。

### 一句话结论
当前不是"从零开始"，而是"从已有骨架中抽出可信主轴，清理幻觉层和空壳层，然后再跑第一条最小闭环"。
