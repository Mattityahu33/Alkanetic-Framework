# Architecture — TODO

**Status:** Planning
**Last Updated:** 2026-08-02

---

## Purpose

This file tracks all planned documents for the `architecture/` section.

---

## Planned Documents

| Document                                 | Type      | Priority | Status      |
| ---------------------------------------- | --------- | -------- | ----------- |
| `architectural-principles.md`            | Standard  | High     | Not Started |
| `decisions/ADR-template.md`              | Template  | High     | Not Started |
| `decisions/ADR-index.md`                 | Index     | High     | Not Started |
| `technology-selection-guidelines.md`     | Standard  | Medium   | Not Started |
| `api-design-standards.md`                | Standard  | High     | Not Started |
| `integration-patterns.md`                | Standard  | Medium   | Not Started |
| `data-architecture-standards.md`         | Standard  | Medium   | Not Started |
| `non-functional-requirements.md`         | Standard  | Medium   | Not Started |
| `reference-architecture-web-platform.md` | Reference | Low      | Not Started |
| `reference-architecture-api-service.md`  | Reference | Low      | Not Started |

---

## Current Status

No documents written. Scaffold only (v0.1.0).

---

## Priority Order

1. `architectural-principles.md`
2. `decisions/ADR-template.md` and `decisions/ADR-index.md`
3. `api-design-standards.md`
4. `technology-selection-guidelines.md`

---

## Dependencies

- `../business-analysis/` — Requirements must inform architectural decisions.
- `../governance/` — ADRs require approval before becoming active.

---

## Notes

A `decisions/` subfolder should be created when the first ADR is written. All ADRs must follow the ADR template and be indexed in `decisions/ADR-index.md`.

---

## Future Improvements

- `patterns/` subfolder for reusable architecture patterns
- `reference/` subfolder for system-level reference diagrams
