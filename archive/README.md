# Archive

**Status:** Active
**Owner:** Alkanetic Engineering
**Last Updated:** 2026-08-02

---

## Purpose

This section stores deprecated, superseded, or retired framework documents. Archived content is retained for historical reference but is no longer active or authoritative.

---

## Scope

Any framework document that has been replaced by a newer version, rendered obsolete, or formally retired belongs in this section.

---

## What Belongs Here

- Deprecated standards (superseded by newer versions)
- Retired SOPs (replaced by updated procedures)
- Legacy templates (superseded by current templates)
- Historical decision records that are no longer active
- Framework documents from previous structural phases

---

## What Does Not Belong Here

- Active documents (they remain in their home section)
- Deleted content (use the Git history for deleted documents)

---

## Archiving Process

1. Move the document from its original location into this directory.
2. Add an `archived:` date field to the document's YAML front matter.
3. Add an `archive-reason:` field explaining why the document was retired.
4. Update the original section's `INDEX.md` to note the document as archived.
5. Update `registry/` to mark the document as `archived`.
6. Record the archival in `CHANGELOG.md`.

---

## Related Directories

| Directory        | Relationship                                                   |
| ---------------- | -------------------------------------------------------------- |
| `../registry/`   | Registry entries for archived documents are marked as archived |
| `../governance/` | Archiving decisions may require governance approval            |

---

## Owner

Alkanetic Engineering Team

---

## Status

Empty. No documents have been archived yet.
