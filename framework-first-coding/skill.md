---

name: framework-first-coding
metadata:
version: "1.0"
category: "software-engineering"
purpose: "Prefer framework, dependency, SDK, and existing project APIs before writing custom implementations."
description: "Use this skill when implementing, modifying, reviewing, or refactoring code. It forces a framework-first and dependency-first workflow to reduce duplicated code, lower token usage, improve maintainability, and avoid reinventing existing capabilities."
---

# Framework-first Coding Skill

## Core Principle

When solving a coding task, do **not** immediately write custom implementation code.

First, inspect and reuse the capabilities already available in the project:

1. Framework APIs
2. Official SDKs
3. Existing dependencies
4. Existing project utilities
5. Existing service abstractions
6. Existing configuration mechanisms
7. Existing coding conventions
8. Existing tests and examples

Only write new custom code when existing framework or project-level capabilities are insufficient.

The preferred implementation is usually the one that uses the least new code while remaining correct, readable, secure, and maintainable.

---

## When to Use This Skill

Use this skill for tasks involving:

* Adding a new feature
* Fixing a bug
* Refactoring existing code
* Writing API endpoints
* Integrating third-party services
* Database access
* Authentication or authorization
* Validation
* Serialization or deserialization
* File processing
* Date and time handling
* Logging
* Error handling
* Caching
* Scheduling
* Message queues
* HTTP clients
* Configuration loading
* Testing

---

## Execution Procedure

### Step 1: Inspect Existing Project Capabilities

Before writing code, check whether the project already has:

* A framework feature for this task
* A dependency that already solves the problem
* A wrapper, helper, utility, base class, annotation, interceptor, filter, middleware, or plugin
* A similar implementation elsewhere in the codebase
* An established project convention
* A configuration option instead of a code change
* A test fixture or existing integration pattern

Do not introduce a new implementation until this inspection is complete.

---

### Step 2: Prefer Built-in Framework Features

Prefer framework-native mechanisms over custom code.

Examples:

* In Spring Boot, prefer annotations, configuration properties, interceptors, filters, validators, converters, `RestTemplate` / `WebClient`, transaction management, and Spring Security extension points.
* In MyBatis / MyBatis-Plus, prefer built-in wrappers, mappers, pagination plugins, type handlers, and existing base mapper patterns.
* In Vue / React, prefer existing component libraries, hooks, stores, router guards, form libraries, and project-level API clients.
* In Python, prefer standard library, official SDKs, mature packages, framework hooks, and existing project modules.
* In FastAPI, prefer dependency injection, Pydantic models, middleware, exception handlers, and response models.
* In Django, prefer ORM, forms, serializers, middleware, permissions, signals, and settings.
* In Node.js, prefer official SDKs, framework middleware, existing service clients, and mature utilities.

---

### Step 3: Prefer Existing Project Abstractions

Before adding new abstractions, look for existing ones.

Reuse:

* Existing service classes
* Existing repository or mapper patterns
* Existing DTO / VO / BO / entity conventions
* Existing exception classes
* Existing response wrappers
* Existing permission checks
* Existing logging utilities
* Existing constants and enums
* Existing validation rules
* Existing configuration objects
* Existing test utilities

Do not create parallel abstractions that duplicate existing ones.

---

### Step 4: Avoid Reimplementing Common Infrastructure

Do not manually reimplement common infrastructure unless there is a clear requirement.

Avoid custom implementations for:

* Authentication
* Authorization
* JWT parsing
* Password hashing
* Encryption
* Signature verification
* Input validation
* JSON parsing
* XML parsing
* Date and time conversion
* Pagination
* Sorting
* Logging
* Retry logic
* Rate limiting
* HTTP clients
* Database transactions
* SQL escaping
* File upload handling
* Object mapping
* Caching
* Scheduling
* Configuration loading

Use framework or dependency-provided APIs whenever possible.

---

### Step 5: Minimize New Code

When custom code is necessary:

* Keep the implementation small
* Follow existing project style
* Add only the minimum required abstraction
* Avoid premature generalization
* Avoid large utility classes
* Avoid duplicating framework behavior
* Avoid unnecessary wrappers around already clear APIs
* Keep changes local unless broader refactoring is justified

Prefer deleting or simplifying code over adding more code.

---

## Decision Rules

Use the following priority order:

1. Existing project utility or abstraction
2. Framework-native API
3. Official SDK
4. Mature existing dependency
5. Small custom implementation
6. New dependency
7. New framework-level abstraction

A lower-priority option should only be used when higher-priority options are unavailable, unsafe, incompatible, or too complex.

---

## Required Reasoning Before Coding

Before providing code, answer these internally:

1. Does the framework already provide this feature?
2. Does the project already have a similar implementation?
3. Is there an existing helper, base class, annotation, configuration, or plugin?
4. Can this be solved by configuration instead of code?
5. Is a custom implementation actually necessary?
6. What is the smallest safe change?
7. Will this introduce duplicate logic?
8. Will this conflict with project conventions?

If the answer is uncertain, inspect more context instead of guessing.

---

## Output Requirements

When producing a solution, briefly state:

* Which existing framework API, dependency, or project abstraction is being reused
* Why custom implementation is or is not necessary
* What files or modules should be changed
* The minimal code change needed

Avoid long explanations unless the user explicitly asks for design details.

---

## Implementation Style

Prefer:

* Small patches
* Existing conventions
* Existing naming style
* Existing error handling
* Existing response structures
* Existing dependency injection style
* Existing configuration style
* Existing test style

Avoid:

* Rewriting large modules
* Introducing new dependencies without justification
* Creating duplicate helper methods
* Hardcoding values that belong in configuration
* Writing manual parsing when framework parsing exists
* Writing custom security logic when security framework hooks exist
* Adding generic abstractions for a single use case
* Creating utility classes that duplicate standard library or dependency APIs

---

## Token-saving Rules

To reduce unnecessary token usage:

* Do not explain basic framework concepts unless needed
* Do not output entire files when a patch or focused snippet is enough
* Do not rewrite unchanged code
* Do not generate boilerplate that the framework can provide
* Do not list every possible alternative unless asked
* Prefer precise file-level and method-level changes
* Prefer existing APIs over long custom implementations
* Prefer configuration examples over code when configuration solves the problem

---

## Review Checklist

Before finalizing an answer, verify:

* Existing framework APIs were considered
* Existing dependencies were considered
* Existing project abstractions were considered
* No duplicate infrastructure was introduced
* New code is minimal
* New code follows project conventions
* Security-sensitive logic is not handwritten unnecessarily
* Error handling matches the existing project style
* The solution is maintainable
* The solution does not over-engineer the task

---

## Examples of Good Behavior

### Good

Use Spring Validation annotations and a global exception handler instead of writing manual null checks in every controller.

### Good

Use MyBatis-Plus `LambdaQueryWrapper` instead of manually concatenating SQL strings.

### Good

Use an existing `Result<T>` response wrapper instead of creating a new response format.

### Good

Use FastAPI dependencies and Pydantic models instead of manually parsing request bodies.

### Good

Use the project’s existing HTTP client wrapper instead of creating a new raw client.

---

## Examples of Bad Behavior

### Bad

Writing a custom JWT parser when the project already uses Spring Security or a JWT library.

### Bad

Creating a new pagination response class when the project already has one.

### Bad

Manually concatenating SQL when the ORM or query wrapper supports the query.

### Bad

Adding a new utility class for date formatting when the project already has a date utility or standard formatter.

### Bad

Introducing a new dependency for a task already handled by the framework.

---

## Fallback Policy

If no existing framework API, dependency, or project abstraction can satisfy the requirement:

1. Explain briefly why reuse is not sufficient.
2. Implement the smallest custom solution.
3. Keep the implementation isolated.
4. Add tests if the behavior is non-trivial.
5. Avoid making the custom implementation more generic than necessary.

Custom code is allowed only after reuse options have been checked.
