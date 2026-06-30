# Skills

这是一个用于沉淀、管理和复用个人 Agent Skills 的仓库。

本仓库主要收集在 AI Agent、Coding Agent、文档生成、代码审查、工具调用、工程规范、上下文管理、Token 优化等场景中可复用的 Skill。每个 Skill 都以独立目录形式组织，包含明确的使用场景、触发条件、执行流程、约束规则和示例说明。

## 目标

本仓库的目标不是简单收集 prompt，而是将可复用的 Agent 能力沉淀为结构化、可维护、可验证的 Skill。

核心目标包括：

* 沉淀个人常用 Agent 工作流
* 统一 Skill 的组织结构和编写规范
* 提升 Coding Agent 和通用 Agent 的执行稳定性
* 减少重复 prompt 编写
* 降低上下文 token 消耗
* 让 Agent 优先复用工具、框架和已有工程能力
* 让复杂任务具备明确的执行步骤、边界和失败策略
* 为后续构建自研 Agent、MCP Agent 或 Agent OS 提供可复用能力模块

## 什么是 Skill

在本仓库中，Skill 指的是一组面向特定任务的结构化能力说明。

一个 Skill 通常包含：

* 适用场景
* 激活条件
* 执行流程
* 输入要求
* 输出格式
* 约束规则
* 工具使用策略
* 失败处理策略
* 示例用法
* 质量检查清单

Skill 不等同于普通 prompt。普通 prompt 往往是一次性指令，而 Skill 更强调长期复用、工程化组织和稳定执行。

## 仓库结构

推荐目录结构如下：

```text
skills/
├── README.md
├── framework-first-coding/
│   ├── SKILL.md
│   └── README.md
├── minimal-patch-coding/
│   ├── SKILL.md
│   └── README.md
├── code-review/
│   ├── SKILL.md
│   └── README.md
├── document-generation/
│   ├── SKILL.md
│   └── README.md
├── tool-failure-strategy/
│   ├── SKILL.md
│   └── README.md
└── references/
    ├── skill-template.md
    ├── writing-guide.md
    └── quality-checklist.md
```

其中：

* `README.md`：仓库总说明
* `*/SKILL.md`：Skill 的核心规则文件，供 Agent 使用
* `*/README.md`：Skill 的人类可读说明，供开发者理解和维护
* `references/`：通用模板、规范、检查清单和参考资料

## 当前已收录 Skill

### Framework-first Coding Skill

目录：

```text
framework-first-coding/
```

用途：

约束 Coding Agent 在实现功能前，优先检查并复用项目已有框架、依赖库、SDK、工具类、公共组件和既有封装，不要直接重新手写已有能力。

适用场景：

* 新增接口
* 修复 Bug
* 重构代码
* 接入第三方 API
* 数据库查询
* 参数校验
* 权限处理
* 文件上传
* HTTP 调用
* 日志、缓存、定时任务等通用工程能力

核心原则：

```text
先找已有能力，再写新增代码。
```

该 Skill 的主要价值是减少重复造轮子、降低 token 消耗、提高代码一致性和工程可维护性。

## Skill 编写规范

每个 Skill 建议至少包含两个文件：

```text
skill-name/
├── SKILL.md
└── README.md
```

### SKILL.md

`SKILL.md` 是给 Agent 读取和执行的核心文件，应该尽量清晰、可执行、少废话。

建议结构：

```markdown
---
name: skill-name
metadata:
  version: "1.0"
  category: "category-name"
description: "One-sentence description of when and why to use this skill."
---

# Skill Name

## Purpose

## When to Use

## Inputs

## Execution Procedure

## Output Requirements

## Constraints

## Tool Usage Rules

## Failure Strategy

## Quality Checklist

## Examples
```

### README.md

`README.md` 是给人看的说明文件，可以更详细地解释 Skill 的背景、用途、适用场景和示例。

建议结构：

```markdown
# Skill Name

## Overview

## Why This Skill Exists

## Suitable Use Cases

## How It Works

## Expected Agent Behavior

## Directory Structure

## Usage

## Examples

## Limitations

## Recommended Pairing
```

## 命名规范

Skill 目录名建议使用小写英文和连字符：

```text
framework-first-coding
minimal-patch-coding
code-review
security-review
document-generation
tool-failure-strategy
```

不推荐：

```text
FrameworkFirstCoding
framework_first_coding
框架优先编码
skill1
my-skill-new
```

命名原则：

* 简短
* 明确
* 可搜索
* 能体现核心能力
* 避免过度抽象

## Skill 分类建议

可以按照以下方向组织 Skill：

### Coding Skills

面向代码生成、修改、重构和审查。

示例：

* `framework-first-coding`
* `minimal-patch-coding`
* `code-review`
* `security-review`
* `test-first-coding`
* `dependency-inspection`
* `project-convention-following`

### Agent Skills

面向 Agent 执行流程、工具调用和任务编排。

示例：

* `tool-use-planning`
* `tool-failure-strategy`
* `multi-step-task-execution`
* `human-in-the-loop`
* `agent-loop-control`
* `context-compaction`

### Document Skills

面向文档创建、编辑、总结和结构化输出。

示例：

* `document-generation`
* `technical-report-writing`
* `research-summary`
* `docx-processing`
* `slide-generation`
* `proposal-writing`

### Retrieval Skills

面向搜索、RAG、证据抽取和知识库问答。

示例：

* `rag-answering`
* `evidence-based-research`
* `academic-search`
* `web-research`
* `source-grounded-summary`

### Evaluation Skills

面向评测、打分、检查和质量控制。

示例：

* `benchmark-design`
* `answer-evaluation`
* `rubric-scoring`
* `quality-check`
* `regression-test-analysis`

## 推荐 Skill 模板

新建 Skill 时，可以使用下面的基础模板：

````markdown
---
name: example-skill
metadata:
  version: "1.0"
  category: "general"
description: "Use this skill when..."
---

# Example Skill

## Purpose

Describe the purpose of this skill.

## When to Use

Use this skill when:

- Condition 1
- Condition 2
- Condition 3

## Inputs

Expected inputs:

- Input 1
- Input 2

## Execution Procedure

### Step 1: Understand the Task

Clarify the goal, constraints, and expected output.

### Step 2: Inspect Available Context

Check existing files, tools, dependencies, documents, or prior state.

### Step 3: Execute the Task

Follow the defined workflow.

### Step 4: Validate the Result

Check correctness, completeness, safety, and formatting.

## Output Requirements

The output should include:

- Required item 1
- Required item 2
- Required item 3

## Constraints

The agent must:

- Constraint 1
- Constraint 2

The agent must not:

- Forbidden behavior 1
- Forbidden behavior 2

## Failure Strategy

If the task cannot be completed:

1. Explain what failed.
2. Explain what was attempted.
3. Provide the best partial result.
4. Suggest the next safe action.

## Quality Checklist

Before finalizing, check:

- [ ] The task goal is satisfied
- [ ] The output follows the requested format
- [ ] No unnecessary implementation is added
- [ ] Existing tools or context were used properly
- [ ] Risks and limitations are stated when relevant

## Examples

Example usage:

```text
Use this skill to...
````

````

## 设计原则

本仓库中的 Skill 应遵循以下原则。

### 1. 可执行

Skill 不应该只写抽象原则，而应该告诉 Agent：

- 什么时候使用
- 先做什么
- 后做什么
- 什么情况下停止
- 失败时怎么办
- 输出应该长什么样

### 2. 可复用

Skill 应该适用于一类任务，而不是只服务于某一次对话。

不推荐：

```text
帮我这次修复登录接口。
````

推荐：

```text
当修复后端接口问题时，先检查路由、请求方法、参数绑定、安全拦截、异常日志和已有项目约定。
```

### 3. 可组合

一个 Skill 可以和其他 Skill 配合使用。

例如：

```text
Framework-first Coding Skill
+ Minimal Patch Skill
+ Security Review Skill
+ Test Verification Skill
```

### 4. 可验证

Skill 应该包含检查清单，让结果可以被验证。

例如：

```text
- 是否复用了已有框架能力？
- 是否避免重复实现？
- 是否遵循项目已有风格？
- 是否说明了失败原因？
```

### 5. Token 友好

Skill 应该尽量减少无效输出。

推荐：

* 明确输出格式
* 避免长篇背景说明
* 避免重复解释基础概念
* 避免输出整份文件
* 优先输出差异、步骤和最小改动

## 使用方式

可以在以下场景中使用本仓库的 Skill：

### 作为 Claude Code Skill

将某个 Skill 目录放入 Claude Code 可识别的 skills 目录中。

```text
skills/
└── framework-first-coding/
    ├── SKILL.md
    └── README.md
```

### 作为 Cursor / IDE Rules

将 `SKILL.md` 中的核心规则提取到项目级规则文件中。

例如：

```text
.cursor/rules/framework-first-coding.mdc
```

### 作为自研 Agent 的能力模块

在自研 Agent 中，可以将 Skill 作为能力声明或策略模块加载：

```text
Agent receives task
→ Match skill by description
→ Load SKILL.md
→ Follow execution procedure
→ Validate with checklist
```

### 作为 MCP Agent 的工具使用约束

对于支持 MCP 工具调用的 Agent，可以将 Skill 用于约束工具选择、文件读取、代码搜索、编译测试和失败处理策略。

## 维护流程

新增一个 Skill 时，建议按照以下流程：

1. 明确 Skill 要解决的问题
2. 判断它是否是一类可复用任务
3. 新建独立目录
4. 编写 `SKILL.md`
5. 编写 `README.md`
6. 添加示例输入和预期输出
7. 添加质量检查清单
8. 在仓库根 `README.md` 中登记
9. 实际使用后根据失败案例迭代

## Skill 质量检查清单

新增或修改 Skill 前，建议检查：

* [ ] 是否有明确名称
* [ ] 是否有清晰描述
* [ ] 是否说明了适用场景
* [ ] 是否说明了不适用场景
* [ ] 是否有明确执行步骤
* [ ] 是否有输出要求
* [ ] 是否有约束规则
* [ ] 是否有失败策略
* [ ] 是否有质量检查清单
* [ ] 是否能减少重复劳动
* [ ] 是否能降低 Agent 行为不确定性
* [ ] 是否能与其他 Skill 组合使用
* [ ] 是否避免了过度复杂的规则
* [ ] 是否避免了只写空泛原则

## 推荐组合

在真实 Agent 系统中，可以将多个 Skill 组合成完整工作流。

### Coding Agent 推荐组合

```text
framework-first-coding
+ minimal-patch-coding
+ project-convention-following
+ test-verification
+ security-review
```

### Research Agent 推荐组合

```text
web-research
+ evidence-based-summary
+ source-citation
+ contradiction-check
+ report-writing
```

### Document Agent 推荐组合

```text
document-generation
+ outline-planning
+ style-consistency
+ docx-processing
+ final-quality-check
```

### RAG Agent 推荐组合

```text
retrieval-planning
+ query-rewriting
+ evidence-selection
+ answer-grounding
+ hallucination-check
```

## 版本管理

建议每个 Skill 都维护独立版本号。

示例：

```yaml
metadata:
  version: "1.0"
```

版本建议：

* `1.0`：初始可用版本
* `1.1`：小幅规则调整
* `1.2`：新增示例或检查项
* `2.0`：执行流程或设计目标发生明显变化

## 未来计划

后续可以继续补充以下方向：

* Minimal Patch Coding Skill
* Tool Failure Strategy Skill
* Dependency Inspection Skill
* Project Convention Skill
* Code Review Skill
* Security Review Skill
* RAG Answering Skill
* Evidence-based Research Skill
* Document Generation Skill
* Agent Loop Control Skill
* Context Compaction Skill
* Human-in-the-loop Skill

## Summary

本仓库用于管理个人积累的 Agent Skills。

它的核心价值是：

```text
把一次性的 prompt 经验，沉淀成可复用、可组合、可维护、可验证的 Agent 能力模块。
```

通过持续积累 Skill，可以逐步形成一套个人或团队可复用的 Agent 能力库，为 Coding Agent、Research Agent、Document Agent 和自研 Agent OS 提供稳定的行为基础。
