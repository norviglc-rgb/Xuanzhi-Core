# 玄织 (Xuanzhi-Core)

OpenClaw 主控系统 - 一个智能化的治理核心与协调平台

## 概述

玄织是一个基于多层级架构的智能代理系统，作为 OpenClaw 的主控核心。它采用治理驱动的架构设计，提供统一的工作流调度、智能路由、持续治理和记忆管理功能。

## 系统定位

玄织首先是：
- **治理中枢** - 统一控制与协调中心
- **控制平面** - 任务路由与状态管理
- **汇报中心** - 结果汇总与可追踪性

玄织其次才是：
- 秘书长风格的战略助手
- 学者型架构顾问

玄织不是：
- 无条件执行器
- 顶层全能执行面
- 情绪安抚机

## 核心架构

### 技术栈组件

| 组件 | 角色 |
|------|------|
| 玄织/OpenClaw | 主控 agent、治理中枢 |
| Claude Code | 默认开发执行器 |
| Higress | 模型入口网关/路由层 |
| GitLab CE | 代码与项目边界系统 |
| Coze Studio | AI 应用中枢 |
| n8n | 自动化与编排系统 |
| NocoBase | 后台与人工审核平面 |
| QMD | 检索与记忆支撑 |
| Docker | 部署底座 |

### 分层结构

```
Layer 0: 根层常驻上下文层
    └── 高频、稳定、短小的全局信息
Layer 1: 治理规范层 (governance/)
    └── 状态机、风险模型、术语、审批原则
Layer 2: 契约层 (contracts/)
    └── 结构化输入输出契约 (JSON Schema)
Layer 3: 策略层 (policies/)
    └── 机器可读配置 (YAML)
Layer 4: 集成层 (integrations/)
    └── 外部系统接入规范
Layer 5: 执行资产层 (workflows/, skills/)
    └── 工作流与场景流程
Layer 6: 记忆与沉淀层 (memory/)
    └── 时间切片记忆与阶段复盘
```

## 目录结构

```
xuanzhi-core/
├── 根层配置文件
│   ├── IDENTITY.md       # 身份定义
│   ├── SOUL.md           # 性格和行为准则
│   ├── AGENTS.md         # 代理操作契约
│   ├── USER.md           # 用户关系与交互边界
│   ├── BOOT.md           # 启动指南
│   ├── BOOTSTRAP.md      # 初始化阶段文档
│   ├── TOOLS.md          # 工具路由偏好
│   ├── HEARTBEAT.md      # 心跳检查
│   └── MEMORY.md         # 长期记忆
│
├── governance/           # 治理规范
│   ├── ROOT_FILE_POLICY.md         # 根文件写入政策
│   ├── RULE_HARDENING_POLICY.md    # 规则硬化政策
│   ├── GOVERNANCE_GLOSSARY.md      # 治理词汇表
│   ├── FIELD_CANON.md              # 字段命名规范
│   ├── STATE_MACHINE.md            # 状态机
│   ├── RISK_MODEL.md               # 风险模型
│   ├── TRACE_SPEC.md               # 追踪规范
│   ├── DEV_TASK_MODEL.md           # 开发任务模型
│   ├── MEMORY_WRITE_POLICY.md      # 记忆写入策略
│   ├── APPROVAL_POLICY.md          # 审批政策
│   ├── AGENT_REGISTRY_SPEC.md      # 代理注册规范
│   ├── WORKFLOW_REGISTRY_SPEC.md   # 工作流注册规范
│   ├── REPO_TEMPLATE_SPEC.md       # 仓库模板规范
│   ├── CONTROLLER_API_SPEC.md      # 控制器 API 规范
│   └── PROJECT_BOOTSTRAP_SPEC.md   # 项目启动规范
│
├── contracts/            # 机器可读契约
│   ├── dev_task_packet.schema.json      # 开发任务包
│   ├── dev_result_packet.schema.json    # 开发结果包 (待完善)
│   ├── main-agent-step.schema.json      # 主代理步骤
│   ├── trace_event.schema.json          # 追踪事件
│   ├── agent_registry.schema.json       # 代理注册表
│   └── workflow_registry.schema.json    # 工作流注册表
│
├── policies/             # 策略规则
│   ├── state_transitions.yaml    # 状态转换规则
│   ├── risk_policy.yaml          # 风险策略
│   ├── approval_rules.yaml       # 审批规则
│   └── memory_write_rules.yaml   # 记忆写入规则
│
├── integrations/         # 系统集成
│   ├── CLAUDE_CODE_EXECUTION_SPEC.md   # Claude Code 执行规范
│   ├── GITLAB_INTEGRATION.md           # GitLab 集成
│   ├── HIGRESS_INTEGRATION.md          # Higress 集成
│   ├── COZE_STUDIO_INTEGRATION.md      # Coze Studio 集成
│   ├── N8N_INTEGRATION.md              # n8n 集成
│   ├── NOCOBASE_INTEGRATION.md         # NocoBase 集成
│   ├── COMFYUI_PIPELINE.md             # ComfyUI 管道
│   ├── FASTGPT_INTEGRATION.md          # FastGPT 集成
│   ├── PUBLISH_PIPELINE.md             # 发布管道
│   └── VIDEO_PIPELINE.md               # 视频管道
│
├── workflows/            # 工作流资产
│   ├── daily_brief/       # 日报
│   ├── media_generation/  # 媒体生成
│   ├── publish/           # 发布
│   └── weekly_review/     # 周报
│
├── memory/               # 记忆存储
│   └── YYYY-MM-DD.md      # 日常笔记
│
├── skills/               # 技能定义
│   └── README.md
│
├── legacy/               # 历史遗留文件
│
└── Dev-Doc/              # 开发文档
    └── 需求说明书.md      # 需求说明书
```

## 核心功能

### 1. 智能路由
根据任务类型自动选择合适的执行器：
- **玄织**: 解释性、治理相关、总结报告类任务
- **Claude Code**: 开发密集型、实现导向、长线开发任务
- **工作流系统**: 重复性、媒体生成、自动化任务

### 2. 治理核心
- 任务理解和清晰框架
- 治理审查和风险控制
- 执行策略的优化选择
- 长期连贯性维护

### 3. 风险管理
系统采用五级风险分类 (R0-R4)：
- **R0**: 只读、近零副作用
- **R1**: 低风险可逆修改
- **R2**: 有意义的变更
- **R3**: 高风险、敏感、破坏性操作
- **R4**: 紧急阻断级别

### 4. 记忆系统
- 多层级记忆结构
- 持久化偏好和决策
- 日常进度跟踪
- 检索引导的响应

## 快速开始

### 启动流程
1. 读取根层配置文件进行初始定位
2. 确定任务类型和最佳执行器
3. 应用治理规则进行任务路由
4. 执行并监控任务进展
5. 记录和总结任务结果

### 执行器选择指南
- **玄织**: 任务解读、治理审查、总结报告
- **Claude Code**: 长期开发、仓库更改、实现密集工作
- **工作流系统**: 重复性任务、媒体生成、集成密集任务

## 设计原则

### 薄主控原则
顶层只做：治理、分类、分发、摘要、记忆、汇报

### 薄根层原则
根目录标准文件必须：短、高频、稳定、会话起始即值得加载

### 默认下沉原则
新增细则默认放入 `governance/`, `contracts/`, `policies/`, `integrations/`, `memory/`

### prose 与执行分离
Markdown 适合治理规范和说明性规则，但不应独立承担严格字段校验、状态迁移等执行职责

## 阶段性交付状态

| 阶段 | 交付内容 | 状态 |
|------|---------|------|
| 阶段0 | 总护栏文件 | 已完成 |
| 阶段1 | 根目录标准文件 | 已完成 |
| 阶段2 | 语义基准文档 | 已完成 |
| 阶段3 | 执行契约 | 部分完成 (dev_result_packet 待完善) |
| 阶段4 | 核心治理与首轮硬化 | 已完成 |

## 已知问题

1. `contracts/dev_result_packet.schema.json` 文件内容为空，需要补充
2. 根目录存在额外的中文文档，应考虑下沉到 `governance/`
3. 部分新增集成文档 (Higress, Coze Studio, n8n, NocoBase) 缺少具体实现细节
4. `legacy/` 目录中的历史文件需要确认是否保留

## 许可证

本项目采用 [Apache License 2.0](LICENSE) 许可证。

---

*玄织 - 让智能系统保持治理核心的清晰与理性*
