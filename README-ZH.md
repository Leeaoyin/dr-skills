# Skills

[English](README.md) | 中文

这里存放我在实际开发中使用的 Agent Skills。每个 Skill 解决一类明确的问题，并把触发条件、执行步骤、约束和检查项放在独立目录中，方便复用和维护。

它不是 prompt 合集。临时 prompt 只需要解决当前问题；Skill 还要说明何时使用、如何执行、做到什么程度，以及遇到例外时如何处理。

## 已收录的 Skill

### [Framework-First Coding](framework-first-coding/README-ZH.md)

写代码前，先检查项目、框架和现有依赖是否已经提供了合适的能力。能复用就复用；现有方案不合适时，再补充范围尽可能小的实现。

适用于新增功能、修复 Bug、重构和代码审查，尤其是这些场景：

- 参数校验、异常处理和权限控制
- 数据库查询、事务和分页
- HTTP 请求、文件上传、缓存和定时任务
- 组件、工具类、SDK 及项目公共封装的复用

这个 Skill 并不要求为了复用而复用。已有抽象如果不兼容、已过时、不安全，或者明显增加复杂度，应说明具体原因并选择更合适的实现。

核心原则：

> 先找已有能力，再写新增代码。

## 目录结构

```text
skills/
├── README.md
├── README-ZH.md
└── framework-first-coding/
    ├── SKILL.md
    ├── README.md
    ├── README-ZH.md
    └── agents/
        └── openai.yaml
```

- `SKILL.md`：Agent 实际读取的规则文件。
- `README.md` / `README-ZH.md`：面向使用者和维护者的说明。
- `agents/openai.yaml`：Skill 在 OpenAI 客户端中的展示名称、简介和默认提示词。

## 使用方式

把完整的 Skill 目录放到 Agent 或开发工具能够识别的 skills 目录中。不同工具的目录位置和加载方式可能不同，请以对应工具的文档为准。

安装后，可以在任务中直接指定 Skill：

```text
使用 $framework-first-coding 完成这个改动。先检查项目里的现有实现和依赖，只做必要修改，并运行相关测试。
```

如果使用的工具不支持 Skill，也可以把 `SKILL.md` 作为项目规则或任务上下文使用。不要只复制其中一句原则；执行流程、约束和检查项需要一起保留，否则容易失去原本的边界。

## 新增 Skill

新增前先确认它解决的是一类会重复出现的问题，而不是某次任务的临时要求。建议按下面的顺序处理：

1. 明确要解决的问题，以及适用和不适用的场景。
2. 使用小写英文和连字符创建目录，例如 `minimal-patch-coding`。
3. 编写 `SKILL.md`，把规则写成 Agent 可以直接执行的步骤。
4. 补充 README，解释用途、使用方式、限制和典型示例。
5. 如需客户端展示信息，添加对应的 `agents/` 配置。
6. 用实际任务验证后，在本页登记。

一个最小的 `SKILL.md` 可以从下面的结构开始：

```markdown
---
name: example-skill
description: Describe when this skill should be used and what problem it solves.
---

# Example Skill

## Workflow

1. Inspect the relevant context.
2. Choose an approach based on the evidence.
3. Make the scoped change.
4. Verify the result.

## Constraints

- Required behavior
- Prohibited behavior
- Conditions that require user confirmation

## Completion Check

- [ ] The requested outcome is complete
- [ ] Relevant checks passed
- [ ] Risks or limitations are stated
```

模板只是起点。章节数量不重要，关键是规则能直接指导执行，并且不会让 Agent 在信息不足时自行补全关键事实。

## 编写要求

### 写清楚触发条件

`description` 应该说明“什么情况下使用”，而不只是概括 Skill 的主题。触发范围过宽，会让 Skill 在无关任务中介入；范围过窄，则难以复用。

### 使用可执行的表述

少写“提高质量”“遵循最佳实践”这类无法检查的要求，改为具体动作，例如：

- 修改前搜索相近实现和调用方。
- 使用 API 前核对项目安装的版本。
- 先运行与改动直接相关的测试，再决定是否扩大检查范围。
- 复用失败时，说明现有能力缺少什么。

### 说明边界和例外

规则不应只有理想流程，还要覆盖这些问题：

- 哪些操作不能做。
- 哪些情况需要用户确认。
- 缺少文件、权限或工具时如何继续。
- 什么条件下可以偏离默认流程。
- 怎样判断任务已经完成。

### 让结果可验证

检查项应对应实际证据，例如测试结果、编译结果、文件差异或引用来源。不要把“已检查”“质量良好”本身当作验证结果。

### 控制篇幅

只保留会影响决策和执行的内容。背景、原则和示例各写一次即可，避免换一种说法重复同一结论。示例用于说明边界，不需要穷举所有技术栈。

## 提交前检查

- [ ] 名称和目录名清楚、可搜索。
- [ ] `description` 能支持准确触发。
- [ ] 执行步骤有明确顺序。
- [ ] 输入、输出和停止条件没有歧义。
- [ ] 约束、例外和失败处理已覆盖。
- [ ] 检查项可以通过实际结果验证。
- [ ] 没有重复现有 Skill 的职责。
- [ ] README 与 `SKILL.md` 的行为一致。
- [ ] 已在至少一个真实任务中试用。

## 维护原则

Skill 应根据实际使用中暴露的问题迭代。修改时优先补足错误决策的原因、缺失的边界或无法验证的步骤，不要因为单个案例不断增加零散规则。改完后再用原任务跑一遍，确认问题确实得到解决。
