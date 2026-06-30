# Framework-first Coding Skill

## Overview

`Framework-first Coding Skill` is an engineering-oriented skill for code generation, code modification, bug fixing, and refactoring tasks.

Its core purpose is to guide an agent to first inspect and reuse the framework capabilities, dependencies, SDKs, utilities, shared components, and existing abstractions already available in the project, instead of immediately writing custom code from scratch.

This skill is suitable for Claude Code, Cursor, custom coding agents, MCP-based agents, or any intelligent coding system that supports rules, skills, or prompt injection at the project level.

---

## Why This Skill Exists

In real-world software development, AI coding models often make the following mistakes:

* Reimplementing functionality that the framework already provides
* Creating new utility classes when similar utilities already exist in the project
* Writing repetitive `try-catch` blocks instead of using existing global exception handling
* Bypassing existing authentication, authorization, pagination, validation, serialization, or security mechanisms
* Producing excessive code for a small feature
* Introducing implementations that do not match the existing project architecture
* Consuming unnecessary context and output tokens

`Framework-first Coding Skill` enforces a “reuse first, implement second” workflow. It reduces duplicated code, improves maintainability, and lowers unnecessary token consumption.

---

## Core Principle

> Prefer existing framework, dependency, SDK, and project-level APIs before writing custom code.

For any coding task, the agent should follow this priority order:

1. Prefer existing project utilities, shared components, and business abstractions
2. Prefer framework-native APIs
3. Prefer official SDKs
4. Prefer dependencies already included in the project
5. Write a small custom implementation only when existing capabilities are insufficient
6. Avoid duplicate abstractions, duplicate utilities, and duplicate infrastructure

---

## Suitable Use Cases

This skill is suitable for:

* Adding new APIs
* Modifying business logic
* Fixing bugs
* Refactoring code
* Integrating third-party services
* Writing database queries
* Adding authentication or authorization logic
* Validating request parameters
* Handling file upload and download
* Processing JSON or XML
* Making HTTP client calls
* Handling logs
* Adding cache logic
* Creating scheduled tasks
* Integrating message queues
* Writing unit tests and integration tests
* Reviewing project code

---

## What This Skill Prevents

When this skill is active, the agent should avoid:

* Rewriting functionality already provided by the framework
* Handwriting security-sensitive logic unnecessarily
* Manually concatenating SQL
* Reimplementing pagination, sorting, validation, or serialization
* Creating unnecessary utility classes
* Introducing abstractions inconsistent with the existing project style
* Outputting entire files when focused patches are enough
* Explaining basic framework concepts unless required
* Implementing features outside the existing project conventions

---

## Typical Examples

### Spring Boot

Prefer using:

* `@Validated`
* `@ConfigurationProperties`
* `HandlerInterceptor`
* `OncePerRequestFilter`
* `ControllerAdvice`
* Spring Security extension points
* Spring transaction management
* `RestTemplate` / `WebClient`
* The project’s existing `Result<T>` response structure

Avoid:

* Writing manual parameter validation in every controller
* Parsing JWT tokens manually
* Concatenating SQL manually
* Creating a new response format
* Bypassing existing global exception handling

---

### MyBatis / MyBatis-Plus

Prefer using:

* `BaseMapper`
* `LambdaQueryWrapper`
* `Page`
* Pagination plugins
* Type handlers
* Existing mapper conventions

Avoid:

* Manually concatenating SQL strings
* Creating duplicate pagination response objects
* Accessing the database directly outside the existing mapper layer

---

### FastAPI

Prefer using:

* Pydantic models
* Dependency injection
* Middleware
* Exception handlers
* Response models
* Existing service or client abstractions

Avoid:

* Manually parsing request bodies
* Writing repetitive field validation logic
* Placing complex business logic directly inside route handlers

---

### Vue / React

Prefer using:

* Existing project component libraries
* Existing API clients
* Router guards
* Stores
* Hooks / composables
* Form validation libraries
* Existing UI component capabilities

Avoid:

* Recreating request utilities
* Rewriting existing form components
* Introducing state management patterns inconsistent with the project

---

## How It Works

Before writing code, the skill asks the agent to check:

1. Does the framework already provide this capability?
2. Does the project already contain a similar implementation?
3. Is there an existing utility, base class, annotation, interceptor, filter, or configuration option?
4. Can the problem be solved through configuration instead of code?
5. Is a custom implementation truly necessary?
6. What is the smallest safe change?
7. Will the new code duplicate existing logic?
8. Does the new implementation follow existing project conventions?

The agent should only write new code after reuse options have been checked and found insufficient.

---

## Recommended Directory Structure

You can place this skill in the following structure:

```text
skills/
└── framework-first-coding/
    ├── SKILL.md
    └── README.md
```

Where:

* `SKILL.md` contains the actual rules used by the agent
* `README.md` explains the purpose, usage, and behavior of the skill for developers and maintainers

---

## Usage

In an agent system that supports skills, register this as a project-level skill.

Typical triggering requests include:

```text
Add a new API endpoint.
```

```text
Fix this Spring Boot error.
```

```text
Refactor this code.
```

```text
Integrate a third-party API.
```

```text
Implement a file upload feature.
```

```text
Check whether this code reinvents existing framework or project functionality.
```

When this skill is active, the agent should first analyze the project’s existing framework and dependency capabilities, then provide the smallest viable implementation plan.

---

## Expected Agent Behavior

With this skill enabled, the agent’s response should focus on:

* Checking existing capabilities first
* Explaining the reuse strategy
* Providing minimal code changes
* Avoiding full-file rewrites
* Avoiding unnecessary explanations of basic concepts
* Avoiding unnecessary dependencies
* Avoiding duplicated implementations

Recommended response format:

```text
Reused capabilities:
- Use existing project xxx
- Use framework-provided xxx

Why custom implementation is not necessary:
- xxx already satisfies the requirement

Files to modify:
- xxx.java
- xxx.yml

Minimal changes:
- ...
```

---

## When Custom Code Is Allowed

This skill does not prohibit writing code.

Custom implementation is allowed when:

* The framework does not provide the required capability
* The project has no reusable implementation
* Existing APIs cannot satisfy the business constraints
* Existing implementations have security or compatibility issues
* A custom implementation is clearly simpler, safer, and easier to maintain

Even when custom code is required, the agent should still follow these rules:

* Keep the change local
* Keep the implementation small
* Avoid over-abstraction
* Avoid duplicating infrastructure
* Follow the project’s existing style
* Add tests when the behavior is non-trivial

---

## Benefits

This skill helps:

* Reduce duplicated code
* Lower maintenance costs
* Improve code consistency
* Reduce security risks
* Lower token consumption
* Improve agent-generated code quality
* Align agent behavior with real engineering practices
* Prevent arbitrary new implementations in unfamiliar codebases

---

## Limitations

This skill depends on the agent’s ability to read and understand project context.

If the agent cannot access project files, dependency manifests, framework configuration, or existing code, it can only make limited judgments based on the information provided by the user.

For practical use, this skill works best when combined with:

* File reading
* Project search
* Dependency inspection
* Code search
* Test execution
* Build verification
* Static analysis
* MCP tool calls

---

## Recommended Pairing

This skill can be combined with:

* Code Review Skill
* Refactoring Skill
* Security Review Skill
* Test-first Skill
* Minimal Patch Skill
* Dependency Inspection Skill
* Project Convention Skill
* Tool Failure Strategy Skill

Recommended priority order:

1. Security rules
2. Project constraints
3. Framework-first Coding Skill
4. Minimal patch rules
5. Test and verification rules

---

## Example Prompt

```text
Please use the Framework-first Coding Skill to implement this feature.

Requirements:
1. First check whether the project already has framework capabilities or existing utilities for this task.
2. Prefer reusing existing implementations.
3. Do not reinvent the wheel.
4. Output only the necessary code changes.
5. If a custom implementation is required, explain why.
```

---

## Summary

`Framework-first Coding Skill` is an engineering constraint for coding agents:

> Find existing capabilities first. Write new code only when necessary.

It shifts the agent from “generate implementation immediately” to “reuse framework and project capabilities first,” which better aligns with maintainability, stability, and cost control in real software engineering.
