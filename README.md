# 玄织 (Xuanzhi-Core)

OpenClaw 主控系统 - 一个智能化的治理核心与协调平台

## 🌟 概述

玄织是一个基于多层级架构的智能代理系统，作为 OpenClaw 的主控核心。它采用治理驱动的架构设计，提供统一的工作流调度、智能路由、持续治理和记忆管理功能。

## 🏗️ 系统架构

### 核心组件

- **玄织 (Xuanzhi)**: 治理核心和控制面协调器
- **Claude Code**: 主要执行器，负责开发任务
- **工作流系统**: 专门化的执行系统，用于特定任务
- **合约层**: 机器可读的协议和模式定义
- **策略层**: 决策和转换规则
- **集成层**: 执行器和系统集成细节

### 文件结构

```
├── 📄 根层配置
│   ├── IDENTITY.md       # 身份定义
│   ├── SOUL.md           # 性格和行为准则
│   ├── AGENTS.md         # 代理操作契约
│   ├── BOOT.md           # 启动指南
│   ├── TOOLS.md          # 工具路由偏好
│   ├── HEARTBEAT.md      # 心跳检查
│   └── MEMORY.md         # 长期记忆
│
├── 📁 governance/        # 治理规范
│   ├── AGENT_REGISTRY_SPEC.md     # 代理注册规范
│   ├── GOVERNANCE_GLOSSARY.md     # 治理词汇表
│   ├── MEMORY_WRITE_POLICY.md     # 记忆写入策略
│   ├── RISK_MODEL.md               # 风险模型
│   ├── STATE_MACHINE.md           # 状态机
│   └── ...
│
├── 📁 contracts/         # 机器可读合约
│   ├── agent_registry.schema.json
│   ├── dev_task_packet.schema.json
│   ├── dev_result_packet.schema.json
│   └── ...
│
├── 📁 policies/          # 策略规则
│   ├── approval_rules.yaml
│   ├── memory_write_rules.yaml
│   ├── risk_policy.yaml
│   └── ...
│
├── 📁 integrations/       # 系统集成
│   ├── CLAUDE_CODE_EXECUTION.md
│   ├── COMFYUI_PIPELINE.md
│   ├── FASTGPT_INTEGRATION.md
│   ├── GITLAB_INTEGRATION.md
│   ├── PUBLISH_PIPELINE.md
│   └── VIDEO_PIPELINE.md
│
├── 📁 workflows/         # 工作流资产
│   ├── daily_brief/
│   ├── media_generation/
│   ├── publish/
│   └── weekly_review/
│
└── 📁 memory/            # 记忆存储
    └── YYYY-MM-DD.md    # 日常和临时笔记
```

## 🎯 核心功能

### 1. 智能路由
根据任务类型自动选择合适的执行器：
- **玄织**: 适合解释性、治理相关的任务
- **Claude Code**: 适合开发密集型、实现导向的任务
- **工作流系统**: 适合重复性、媒体生成等专门任务

### 2. 治理核心
- 任务理解和清晰框架
- 治理审查和风险控制
- 执行策略的优化选择
- 长期连贯性维护

### 3. 记忆系统
- 多层级记忆结构
- 持久化偏好和决策
- 日常进度跟踪
- 检索引导的响应

### 4. 合规管理
- Apache 2.0 许可证
- 详细的状态转换规则
- 风险评估模型
- 批准策略

## 🔧 主要特性

### 玄织的职责
- 理解真实任务
- 框架任务清晰性
- 选择适当的执行器
- 应用治理判断
- 保持输出简洁结构化
- 维护总结级记忆
- 生成集中的状态理解和报告

### 风格特征
- **冷静理性**: 学者-建筑师风格
- **克制观察**: 不过度表演
- **结构导向**: 偏好清晰和结构
- **长期价值**: 优先考虑长期连贯性
- **判断导向**: 优先于表演性的有用性

## 🚀 快速开始

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

## 📝 配置规范

### 治理原则
- 控制清晰优先
- 执行适配优先
- 上下文使用界限优先
- 长期可维护性优先

### 记忆规则
- 保守地写入记忆
- 使用 `MEMORY.md` 存储持久偏好
- 使用 `memory/YYYY-MM-DD.md` 存储日常笔记
- 避免存储完整记录和重复过程

## 📊 许可证

本项目采用 [Apache License 2.0](LICENSE) 许可证。

---

*玄织 - 让智能系统保持治理核心的清晰与理性*