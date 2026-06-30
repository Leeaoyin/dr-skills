# Skills

A personal repository for collecting, organizing, and reusing Agent Skills.

This repository stores reusable skills for AI agents, coding agents, document generation agents, code review agents, tool-using agents, engineering workflows, context management, and token optimization.

Each skill is organized as an independent directory with clear usage scenarios, activation conditions, execution procedures, constraints, output requirements, and examples.

## Goals

This repository is not intended to be a simple prompt collection.

Its purpose is to turn reusable agent workflows into structured, maintainable, and verifiable skills.

The main goals are:

* Capture reusable agent workflows
* Standardize skill structure and authoring conventions
* Improve the reliability of coding agents and general-purpose agents
* Reduce repetitive prompt writing
* Lower unnecessary context token usage
* Encourage agents to reuse existing tools, frameworks, and project capabilities
* Give complex tasks explicit procedures, boundaries, and failure strategies
* Provide reusable capability modules for custom agents, MCP-based agents, and Agent OS designs

## What Is a Skill?

In this repository, a skill is a structured capability definition for a specific class of tasks.

A skill usually defines:

* Applicable scenarios
* Activation conditions
* Execution procedure
* Input requirements
* Output format
* Constraints
* Tool usage rules
* Failure strategy
* Examples
* Quality checklist

A skill is not the same as a one-off prompt. A prompt is usually written for a single interaction, while a skill is designed for long-term reuse, engineering consistency, and stable execution.

## Repository Structure

Recommended structure:

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

Where:

* `README.md` is the repository-level documentation
* `*/SKILL.md` is the core rule file used by the agent
* `*/README.md` is the human-readable explanation for developers and maintainers
* `references/` contains shared templates, authoring guides, checklists, and reference material

## Included Skills

### Framework-first Coding Skill

Directory:

```text
framework-first-coding/
```

Purpose:

Constrains a coding agent to inspect and reuse existing framework features, dependencies, SDKs, utilities, shared components, and project abstractions before writing custom implementation code.

Suitable for:

* Adding APIs
* Fixing bugs
* Refactoring code
* Integrating third-party APIs
* Writing database queries
* Request validation
* Authorization handling
* File upload
* HTTP calls
* Logging, caching, scheduling, and other common engineering tasks

Core principle:

```text
Find existing capabilities first. Write new code only when necessary.
```

This skill helps reduce duplicated implementation, lower token consumption, improve code consistency, and increase maintainability.

## Skill Authoring Convention

Each skill should normally contain at least two files:

```text
skill-name/
├── SKILL.md
└── README.md
```

### SKILL.md

`SKILL.md` is the core file read and executed by the agent. It should be clear, actionable, and concise.

Recommended structure:

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

`README.md` is written for humans. It can explain the background, purpose, suitable scenarios, behavior, and examples in more detail.

Recommended structure:

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

## Naming Convention

Skill directory names should use lowercase English words and hyphens:

```text
framework-first-coding
minimal-patch-coding
code-review
security-review
document-generation
tool-failure-strategy
```

Avoid:

```text
FrameworkFirstCoding
framework_first_coding
框架优先编码
skill1
my-skill-new
```

Naming principles:

* Short
* Clear
* Searchable
* Describes the core capability
* Avoids unnecessary abstraction

## Suggested Skill Categories

Skills can be grouped by task type.

### Coding Skills

For code generation, modification, refactoring, and review.

Examples:

* `framework-first-coding`
* `minimal-patch-coding`
* `code-review`
* `security-review`
* `test-first-coding`
* `dependency-inspection`
* `project-convention-following`

### Agent Skills

For agent execution flow, tool use, and task orchestration.

Examples:

* `tool-use-planning`
* `tool-failure-strategy`
* `multi-step-task-execution`
* `human-in-the-loop`
* `agent-loop-control`
* `context-compaction`

### Document Skills

For creating, editing, summarizing, and structuring documents.

Examples:

* `document-generation`
* `technical-report-writing`
* `research-summary`
* `docx-processing`
* `slide-generation`
* `proposal-writing`

### Retrieval Skills

For search, RAG, evidence extraction, and knowledge-base answering.

Examples:

* `rag-answering`
* `evidence-based-research`
* `academic-search`
* `web-research`
* `source-grounded-summary`

### Evaluation Skills

For evaluation, scoring, checking, and quality control.

Examples:

* `benchmark-design`
* `answer-evaluation`
* `rubric-scoring`
* `quality-check`
* `regression-test-analysis`

## Recommended Skill Template

Use the following template when creating a new skill:

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

## Design Principles

Skills in this repository should follow these principles.

### 1. Actionable

A skill should not only describe abstract principles. It should tell the agent:

- When to use it
- What to do first
- What to do next
- When to stop
- What to do when something fails
- What the output should look like

### 2. Reusable

A skill should apply to a class of tasks, not just one conversation.

Not recommended:

```text
Help me fix this login API this time.
````

Recommended:

```text
When fixing backend API issues, first check routing, HTTP method, parameter binding, security interception, exception logs, and existing project conventions.
```

### 3. Composable

A skill should be able to work with other skills.

Example:

```text
Framework-first Coding Skill
+ Minimal Patch Skill
+ Security Review Skill
+ Test Verification Skill
```

### 4. Verifiable

A skill should include a checklist so the output can be reviewed.

Example:

```text
- Did the agent reuse existing framework capabilities?
- Did the agent avoid duplicated implementation?
- Did the agent follow project conventions?
- Did the agent explain failure causes when relevant?
```

### 5. Token-efficient

A skill should reduce unnecessary output.

Recommended practices:

* Define output formats clearly
* Avoid long background explanations
* Avoid explaining basic concepts repeatedly
* Avoid outputting entire files unnecessarily
* Prefer diffs, focused steps, and minimal changes

## Usage

This repository can be used in several ways.

### As Claude Code Skills

Place a skill directory in a location recognized by Claude Code.

```text
skills/
└── framework-first-coding/
    ├── SKILL.md
    └── README.md
```

### As Cursor or IDE Rules

Extract the core rules from `SKILL.md` into a project-level rule file.

Example:

```text
.cursor/rules/framework-first-coding.mdc
```

### As Capability Modules for Custom Agents

In a custom agent system, a skill can be loaded as a capability declaration or strategy module:

```text
Agent receives task
→ Match skill by description
→ Load SKILL.md
→ Follow execution procedure
→ Validate with checklist
```

### As Tool-use Constraints for MCP Agents

For MCP-enabled agents, skills can constrain tool selection, file reading, code search, build checks, test execution, and failure handling.

## Maintenance Workflow

When adding a new skill:

1. Define the problem the skill solves.
2. Confirm that it applies to a reusable class of tasks.
3. Create an independent directory.
4. Write `SKILL.md`.
5. Write `README.md`.
6. Add example inputs and expected outputs.
7. Add a quality checklist.
8. Register the skill in the root `README.md`.
9. Iterate based on real failure cases.

## Skill Quality Checklist

Before adding or modifying a skill, check:

* [ ] The skill has a clear name
* [ ] The skill has a clear description
* [ ] Applicable scenarios are defined
* [ ] Non-applicable scenarios are defined
* [ ] Execution steps are explicit
* [ ] Output requirements are defined
* [ ] Constraints are defined
* [ ] Failure strategy is included
* [ ] Quality checklist is included
* [ ] The skill reduces repeated work
* [ ] The skill reduces agent behavior uncertainty
* [ ] The skill can be composed with other skills
* [ ] The skill avoids excessive complexity
* [ ] The skill avoids vague principles without execution details

## Recommended Combinations

In real agent systems, multiple skills can be combined into a complete workflow.

### Coding Agent Combination

```text
framework-first-coding
+ minimal-patch-coding
+ project-convention-following
+ test-verification
+ security-review
```

### Research Agent Combination

```text
web-research
+ evidence-based-summary
+ source-citation
+ contradiction-check
+ report-writing
```

### Document Agent Combination

```text
document-generation
+ outline-planning
+ style-consistency
+ docx-processing
+ final-quality-check
```

### RAG Agent Combination

```text
retrieval-planning
+ query-rewriting
+ evidence-selection
+ answer-grounding
+ hallucination-check
```

## Versioning

Each skill should maintain its own version number.

Example:

```yaml
metadata:
  version: "1.0"
```

Suggested versioning:

* `1.0`: Initial usable version
* `1.1`: Minor rule adjustment
* `1.2`: Added examples or checklist items
* `2.0`: Major change to execution flow or design purpose

## Roadmap

Potential skills to add:

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

This repository manages personally accumulated Agent Skills.

Its core value is:

```text
Turn one-off prompt experience into reusable, composable, maintainable, and verifiable agent capability modules.
```

By continuously collecting and refining skills, this repository can become a reusable capability library for coding agents, research agents, document agents, MCP agents, and custom Agent OS implementations.
