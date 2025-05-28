# Falcoria Use Cases

📚 Part of the [Falcoria Documentation](https://falcoria.github.io/falcoria-docs/)

This repository contains real-world examples demonstrating how different features and modes of Falcoria work. Each folder includes scan reports, expected results, and a clear explanation of how Falcoria behaves in each case.

Falcoria is a modular scan coordination system that helps manage large-scale scanning workflows with precision and flexibility.

---

## 📂 Available Use Cases

| Use Case            | Description                                                                 | Link                            |
|---------------------|-----------------------------------------------------------------------------|---------------------------------|
| `insert` mode       | Demonstrates how only new IPs are imported while duplicates are skipped.    | [View ›](./import-mode-insert) |
| More coming soon... | Additional import modes and scan strategies will be added over time.        |                                 |

---

## 🎯 Goal

Help users and teams:
- Understand Falcoria’s import logic.
- Validate that scan results are processed correctly.
- Explore edge cases and integration flows with real data.

---

## 🛠 How to Use

Each folder includes:
- Sample scan reports (`*.xml`)
- A dedicated README explaining the behavior
- CLI and `curl` commands
- Expected outputs

You can run the examples against your local Falcoria instance to test or validate functionality.

---

## 🧭 Start Here

To understand how import modes work and where they are used in the system (e.g., during scans or manual uploads), visit the [Import Modes Overview](https://falcoria.github.io/falcoria-docs/import-modes/).

