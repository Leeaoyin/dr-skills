# Framework-first Coding Skill

## Overview

`Framework-first Coding Skill` 是一个面向代码生成、代码修改、Bug 修复和重构任务的工程化 Skill。

它的核心目标是约束 Agent 在写代码前，优先检查并复用项目已有的框架能力、依赖库、SDK、工具类、公共组件和既有封装，而不是直接从零手写实现。

该 Skill 适用于 Claude Code、Cursor、自研 Coding Agent、MCP Agent 或其他支持规则/Skill 注入的智能编码系统。

---

## Why This Skill Exists

在实际开发中，AI 编码模型常见的问题包括：

* 明明框架已经提供能力，模型却重新手写一套实现
* 项目里已有工具类，模型却新增重复工具类
* 已有统一异常处理，模型却在业务代码里到处写 `try-catch`
* 已有权限、安全、分页、校验、序列化机制，模型却绕过框架自行实现
* 为了完成一个小功能，输出大量不必要代码
* 新增实现与项目原有架构风格不一致
* Token 消耗过高，代码维护成本上升

`Framework-first Coding Skill` 通过“先复用、再实现”的规则，减少重复造轮子，提高代码质量，并降低上下文和输出 token 消耗。

---

## Core Principle

> Prefer existing framework, dependency, SDK, and project-level APIs before writing custom code.

在任何编码任务中，Agent 都应该按照以下优先级处理问题：

1. 优先使用项目已有工具类、公共组件和业务封装
2. 优先使用框架原生 API
3. 优先使用官方 SDK
4. 优先使用项目已有依赖库
5. 只有在以上能力无法满足需求时，才编写少量自定义代码
6. 避免引入重复抽象、重复工具类和重复基础设施

---

## Suitable Use Cases

该 Skill 适合以下任务：

* 新增接口
* 修改业务逻辑
* 修复 Bug
* 重构代码
* 接入第三方服务
* 编写数据库查询
* 添加认证和权限逻辑
* 请求参数校验
* 文件上传下载
* JSON/XML 处理
* HTTP 客户端调用
* 日志处理
* 缓存处理
* 定时任务
* 消息队列
* 单元测试和集成测试
* 项目代码审查

---

## What This Skill Prevents

使用该 Skill 后，Agent 应尽量避免：

* 手写框架已有能力
* 手写安全敏感逻辑
* 手写 SQL 拼接
* 重复实现分页、排序、校验、序列化
* 新增不必要的工具类
* 新增与项目风格不一致的抽象
* 直接输出整份文件
* 大量解释基础框架知识
* 在已有项目规范之外另起一套实现方式

---

## Typical Examples

### Spring Boot

优先使用：

* `@Validated`
* `@ConfigurationProperties`
* `HandlerInterceptor`
* `OncePerRequestFilter`
* `ControllerAdvice`
* Spring Security 扩展点
* Spring Transaction
* `RestTemplate` / `WebClient`
* 项目已有 `Result<T>` 响应结构

避免：

* 在每个 Controller 里手写参数校验
* 自己解析 JWT
* 自己拼接 SQL
* 自己创建新的响应结构
* 绕过已有统一异常处理

---

### MyBatis / MyBatis-Plus

优先使用：

* `BaseMapper`
* `LambdaQueryWrapper`
* `Page`
* 分页插件
* TypeHandler
* 项目已有 Mapper 规范

避免：

* 手写字符串 SQL 拼接
* 重复创建分页返回对象
* 绕过已有 Mapper 层直接访问数据库

---

### FastAPI

优先使用：

* Pydantic Model
* Dependency Injection
* Middleware
* Exception Handler
* Response Model
* 项目已有 service/client 封装

避免：

* 手动解析请求体
* 手写大量字段校验
* 在接口函数中堆叠复杂业务逻辑

---

### Vue / React

优先使用：

* 项目已有组件库
* 项目已有 API Client
* Router Guard
* Store
* Hooks / Composables
* 表单校验库
* UI 组件库能力

避免：

* 重复封装请求方法
* 手写已有表单组件
* 新增与项目风格不一致的状态管理逻辑

---

## How It Works

该 Skill 会要求 Agent 在写代码前先完成以下判断：

1. 框架是否已经提供该能力？
2. 项目是否已有类似实现？
3. 是否存在可复用的工具类、基础类、注解、拦截器、过滤器或配置项？
4. 是否可以通过配置解决，而不是写代码？
5. 是否必须新增自定义实现？
6. 最小安全改动是什么？
7. 新增代码是否会造成重复逻辑？
8. 新实现是否符合项目原有风格？

只有在复用方案不足时，Agent 才应该编写新的代码。

---

## Recommended Directory Structure

可以按以下结构放置该 Skill：

```text
skills/
└── framework-first-coding/
    ├── SKILL.md
    └── README.md
```

其中：

* `SKILL.md`：给 Agent 使用的正式规则文件
* `README.md`：给开发者和维护者阅读的说明文档

---

## Usage

在支持 Skill 的 Agent 系统中，可以将该 Skill 注册为项目级 Skill。

典型触发场景包括：

```text
帮我新增一个接口
```

```text
帮我修复这个 Spring Boot 报错
```

```text
帮我重构这段代码
```

```text
帮我接入一个第三方 API
```

```text
帮我写一个文件上传功能
```

```text
帮我检查这段代码有没有重复造轮子
```

当该 Skill 生效时，Agent 应该优先分析项目已有框架和依赖能力，再给出最小化实现方案。

---

## Expected Agent Behavior

使用该 Skill 后，Agent 的回答应该更偏向：

* 先判断已有能力
* 再说明复用方案
* 最后给出最小代码改动
* 避免整文件重写
* 避免重复解释基础概念
* 避免无必要新增依赖
* 避免重复造轮子

推荐输出格式：

```text
复用能力：
- 使用项目已有 xxx
- 使用框架自带 xxx

不需要自定义实现的原因：
- xxx 已经满足需求

需要修改的文件：
- xxx.java
- xxx.yml

最小改动：
- ...
```

---

## When Custom Code Is Allowed

该 Skill 并不是禁止写代码。

只有在以下情况下，才允许新增自定义实现：

* 框架没有提供对应能力
* 项目中没有可复用实现
* 现有 API 无法满足业务约束
* 现有实现存在安全或兼容问题
* 自定义实现明显更简单、更安全、更易维护

即使需要写自定义代码，也应遵循：

* 小范围修改
* 局部实现
* 不过度抽象
* 不引入重复基础设施
* 遵循项目原有风格
* 必要时补充测试

---

## Benefits

使用该 Skill 可以带来以下收益：

* 减少重复代码
* 降低维护成本
* 提高代码一致性
* 减少安全风险
* 降低 token 消耗
* 提升 Agent 代码输出质量
* 让 Agent 更符合真实工程开发习惯
* 避免模型在不熟悉项目时随意新增实现

---

## Limitations

该 Skill 依赖 Agent 能够读取和理解项目上下文。

如果 Agent 没有访问项目文件、依赖清单、框架配置或已有代码的能力，那么它只能根据用户提供的信息做有限判断。

因此，建议在实际使用时配合以下能力：

* 文件读取
* 项目检索
* 依赖分析
* 代码搜索
* 测试执行
* 编译检查
* 静态分析
* MCP 工具调用

---

## Recommended Pairing

该 Skill 可以与以下 Skill 或规则组合使用：

* Code Review Skill
* Refactoring Skill
* Security Review Skill
* Test-first Skill
* Minimal Patch Skill
* Dependency Inspection Skill
* Project Convention Skill
* Tool Failure Strategy Skill

组合使用时，建议优先级如下：

1. 安全规则
2. 项目约束
3. Framework-first Coding Skill
4. 最小改动规则
5. 测试与验证规则

---

## Example Prompt

```text
请使用 Framework-first Coding Skill 帮我实现这个功能。
要求：
1. 先检查项目是否已有框架能力或工具类
2. 优先复用现有实现
3. 不要重复造轮子
4. 只输出必要代码改动
5. 如果必须自定义实现，请说明原因
```

---

## Summary

`Framework-first Coding Skill` 的本质是一条工程化编码约束：

> 先找已有能力，再写新增代码。

它让 Agent 从“直接生成实现”转向“优先复用框架和项目能力”，更符合真实软件工程中的可维护性、稳定性和成本控制要求。
