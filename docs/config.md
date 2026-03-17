# Configuration

Configuration is stored in `config.toml` files.

## Scope and Precedence

- A `config.toml` applies to its directory subtree.
- Multiple configs can apply; the nearest config takes precedence.
- Config sections are deep-merged.

## Fields

| Field          | Scope     | Description                                                                                                                                                              |
| -------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `version`      | Root only | Spec version string (e.g., `"1.1.0"`). Only valid in the repository root `config.toml`; ignored in subdirectory configs.                                                 |
| `[status.map]` | Subtree   | Custom status definitions. Each entry maps a status name to `{category, order}`. Category must be `todo`, `in_progress`, or `done`. Order is optional (defaults to `0`). |

## Example

```toml
version = "1.1.0"

[status.map]
backlog = { category = "todo", order = 10 }
up_next = { category = "todo", order = 20 }
in_progress = { category = "in_progress", order = 30 }
review = { category = "in_progress", order = 40 }
done = { category = "done", order = 50 }
```

This config defines custom status values with base category mappings. Note that multiple statuses can map to the same base category (`backlog` and `up_next` both map to `todo`).
