# Contributing to the Alkanetic Framework

**Owner:** Alkanetic
**Status:** Active

---

## Overview

This document defines the process for contributing to the Alkanetic Framework repository.

---

## Who Can Contribute

All Alkanetic team members are permitted to contribute to this repository in accordance with these guidelines. External contributors require explicit approval.

---

## Contribution Types

| Type              | Description                                    |
| ----------------- | ---------------------------------------------- |
| New Document      | Adding a new standard, SOP, template, or guide |
| Document Update   | Revising or correcting an existing document    |
| Structural Change | Adding, renaming, or moving directories        |
| Registry Update   | Adding entries to registry index files         |

---

## Before Contributing

1. Review the relevant section `README.md` to confirm scope.
2. Check the section `TODO.md` to confirm the document is planned or approved.
3. Check the `registry/` to confirm no duplicate document exists.
4. Use the metadata template defined in [.metadata-template.md](./.metadata-template.md).

---

## Naming Conventions

- Use `kebab-case` for all file and folder names.
- Use lowercase only.
- Never use spaces in file or folder names.
- Markdown files must use the `.md` extension.

---

## Document Requirements

Every new document must include:

- YAML front matter using the `.metadata-template.md` fields
- A clear `# Title` heading
- A `## Purpose` section
- A `## Status` field at the end

---

## Review Process

1. Author creates or updates the document.
2. Author updates the relevant section `INDEX.md` and `TODO.md`.
3. Author updates the `registry/` index for the document type.
4. Document is reviewed by the section owner.
5. On approval, `CHANGELOG.md` is updated.

---

## Structural Changes

Structural changes (adding or reorganising directories) must be discussed and approved before implementation. Structural changes require an update to `README.md`, `ROADMAP.md`, and the root `INDEX.md`.

---

## Questions

Raise questions with the framework owner before making changes that affect multiple sections.
