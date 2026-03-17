# Basics

This guide explains the core tsk model before teams, SLAs, or advanced querying.

## Core Idea

- Tasks are markdown files
- Tasks belong to projects, which are directories with an optional readme.md

## Repository Layout

A minimal layout:

```text
/
  tasks/
    project-a/
      README.md
      task-1.md
```

## Canonical Paths

- Canonical paths are rooted at `tasks/` and omit file extensions.
- Paths are normalized and lowercased.
- `README.md` is a special case: `README.md` and `readme.md` are both accepted.
- `tasks/launch/README.md` resolves to canonical path `launch`.
- A task `task-1` in `project-a` has the id `project-a/task-1`

## Redirect Stubs

Use redirect stubs when a task moves or when the same task should appear in multiple places without duplication.

```markdown
---
redirect_to: platform/tasks/enable-sso
---
```

## Task Front Matter

Required task field:

- `created_at` (RFC3339 timestamp)

Common optional fields:

- `status`
- `summary`
- `assignee`
- `dependencies`
- `labels`
- `type`
- `estimate`
- `updated_at`
- `due`
- `change_log`

## Identifier Rules

Identifiers (used by `labels`, `type`, team names, SLA IDs, etc.) follow one format:

- Regex: `[a-z0-9][a-z0-9-]*`
- Lowercase alphanumeric with optional `-`

## Duration Rules

Duration format is `<number><unit>` with no spaces.

- Examples: `2h`, `1.5d`, `2w`, `3m`
- Units: `h` (hours), `d` (days), `w` (weeks), `m` (months)

## Examples

### Minimal Task

```markdown
---
created_at: 2026-03-17T10:00:00Z
summary: Build user login
status: todo
---
Implement OAuth2 login flow.
```

### Task with Dependencies

```markdown
---
created_at: 2026-03-17T10:00:00Z
dependencies: [backend/api-design]
summary: Create frontend login page
assignee: "team:frontend"
---
Wire up the login form to the API.
```
