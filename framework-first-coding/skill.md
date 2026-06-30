---
name: framework-first-coding
description: Prefer capabilities already provided by a codebase, its framework, installed dependencies, and official SDKs before writing custom implementations. Use when implementing, fixing, refactoring, or reviewing code where an existing API, configuration mechanism, convention, service abstraction, utility, test pattern, or dependency may already solve the problem.
---

# Framework-First Coding

Minimize new code without sacrificing correctness, security, clarity, or maintainability. Reuse is a means, not the objective: do not preserve an unsuitable abstraction merely to avoid a small implementation.

## Workflow

### 1. Establish the project context

Before designing a change, inspect the relevant evidence:

- Dependency manifests and lockfiles for available packages and exact versions
- Framework configuration, plugins, middleware, and extension points
- Nearby code and analogous features for established conventions
- Shared services, utilities, types, errors, response wrappers, and test helpers
- Existing tests and examples that define intended behavior

Search by behavior and symbols, not only by the requested terminology. Read the implementation and callers of a candidate abstraction before reusing it.

For a review-only request, inspect and report; do not modify files.

### 2. Rank viable approaches

Prefer the first suitable option in this order:

1. Existing project abstraction or configuration
2. Framework-native API or extension point
3. Already-installed official SDK or mature dependency
4. Small local implementation
5. New dependency or broad shared abstraction

Treat the order as a heuristic. Choose a lower item when a higher one is incompatible, deprecated, insecure, harder to maintain, or substantially more complex for the actual requirement.

Before using an API, confirm that it exists in the installed version. Consult current official documentation when behavior is version-sensitive or uncertain.

### 3. Define the smallest coherent change

Identify:

- The existing capability to reuse
- The behavior not covered by that capability
- The minimum files and interfaces that must change
- The tests needed to protect the behavior

Prefer configuration over code when it expresses the requirement clearly. Prefer a focused local implementation over a generic utility created for one caller.

Do not add a dependency unless the codebase lacks a suitable capability and the dependency's maintenance, security, size, license, and integration costs are justified.

### 4. Implement in the project's idiom

Follow existing naming, dependency injection, error handling, logging, validation, configuration, response, and test patterns. Preserve public contracts unless the task requires changing them.

Use framework or library facilities for security-sensitive and infrastructure behavior such as:

- Authentication, authorization, password hashing, cryptography, and signature verification
- Parsing, validation, serialization, SQL parameterization, and transactions
- HTTP clients, retries, rate limiting, caching, scheduling, and file uploads
- Date/time handling, pagination, logging, and configuration loading

Do not add wrappers that merely rename a clear underlying API. Do not duplicate constants, schemas, validation rules, or domain logic.

### 5. Verify the selected path

Run the narrowest relevant checks first, then broader checks when warranted. Verify that:

- The reused API behaves as expected in the installed version
- Existing callers and contracts remain valid
- Tests cover the changed behavior and important failure paths
- The change introduces no parallel abstraction or duplicate logic
- Dependency and configuration changes are intentional and minimal

If the existing capability proves insufficient, document the concrete gap and implement the smallest isolated fallback.

## Decision Notes

Keep reasoning proportional to the task. In the final response, briefly identify:

- What existing capability was reused, or why reuse was insufficient
- Which files changed
- What verification ran and its result

Do not output a framework tutorial, exhaustive alternatives, unchanged files, or speculative abstractions unless the user asks for them.

## Common Failure Modes

Avoid:

- Assuming a package API without checking the installed version
- Adding a helper before searching for an equivalent
- Reimplementing framework lifecycle, security, validation, or persistence behavior
- Forcing reuse of a poorly matched abstraction
- Adding a new package for behavior already available locally
- Expanding a targeted fix into an unrelated refactor
- Claiming reuse based only on a matching name without inspecting semantics

## Completion Check

Before finishing, confirm:

- Project, framework, and dependency capabilities were inspected
- The selected approach is compatible with actual versions and conventions
- New code and new dependencies are justified
- Security-sensitive behavior uses established implementations
- The patch is focused and verified
