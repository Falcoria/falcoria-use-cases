*See the full [Falcoria Documentation](https://falcoria.github.io/falcoria-docs/) for system overview and additional features.*

# Falcoria Use Cases

This section provides real-world examples of how different Falcoria features and import modes behave in practice.

Each example includes scan reports, expected results, and clear explanations to help you validate and understand Falcoria's behavior.

---

## Available Use Cases

| Use Case            | Description                                                              | Link                            |
| ------------------- | ------------------------------------------------------------------------ | ------------------------------- |
| `insert` mode       | Demonstrates how only new IPs are imported while duplicates are skipped. | [View ›](./import-mode-insert)  |
| `replace` mode      | Demonstrates how existing IPs are fully replaced with new scan data.     | [View ›](./import-mode-replace) |
| More coming soon... | Additional import modes and scan strategies will be added over time.     |                                 |

---

## Goal

Help users and teams:

* Understand Falcoria's import logic.
* Validate that scan results are processed correctly.
* Explore edge cases and integration flows with real data.

---

## How to Use

Each folder includes:

* Sample scan reports (`*.xml`)
* A dedicated README explaining the behavior
* CLI and `curl` commands
* Expected outputs

Run these examples against your local Falcoria instance to test or validate functionality.

---

## Related

To learn more about import modes and when to use them, visit the [Import Modes Overview](https://falcoria.github.io/falcoria-docs/import-modes/).

---

## Use Case Repositories

* [`insert` mode](https://github.com/Falcoria/falcoria-use-cases/tree/main/import-mode-insert)
* [`replace` mode](https://github.com/Falcoria/falcoria-use-cases/tree/main/import-mode-replace)
