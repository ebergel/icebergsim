---
id: sop-docs
title: SOP — Document Manifests & Versioning
isbrs: program
kind: sop
status: draft
version: 0.3.2
date: 2026-07-03
updated: 2026-07-03
tags: [isbrs/program]
---

# SOP-DOCS.md — Document Manifests & Versioning

**Canonical home: the umbrella repo (`ebergel/icebergsim`). Referenced by
CONSTITUTION-LD.md L11. Applies to every markdown file in every program
repository and to structured notes in the vault, present and future.**

---

## 1. The manifest (frontmatter schema — 8 fields, closed by default)

```yaml
---
id: <permanent-slug>       # NEVER changes. Files move; ids don't.
title: <human title>
isbrs: program|rct|integrity|alfa|classic|ua
kind: law|sop|seal|map|spec|guide|changelog|session|decision|ledger
status: draft|signed|active|blind|exposed|shelved|superseded
version: x.y.z             # artifacts only — omit for dated events
date: YYYY-MM-DD           # created
updated: YYYY-MM-DD
tags: [isbrs/<lineage>]    # for the tag pane; facts live in fields
---
```

**The namespace key is `isbrs`** — a coined, collision-free token (the
word "ism" drowns in any philosophy vault: dualism, organism…). Spoken
handles remain `ISM_*`; the value vocabulary is unchanged; only the
field/tag root uses the odd signature. Two search registers follow:
`isbrs` = precision (exactly the manifested corpus, anywhere — Obsidian,
grep, GitHub); `icebergsim` = recall (everything project-flavored, via
prose). Renamed 2026-07-03, pre-publication — the last legal rename, per
this SOP's own field-rename ban.

**The root tag is implicit — never write it.** Obsidian nested tags are
hierarchical: `#isbrs/<lineage>` already contains `#isbrs`, retrievable
via the parent (tag pane, `tag:#isbrs` in search, `FROM #isbrs` in
Dataview, subtags included). Adding an explicit root would encode the
same fact twice — derive, don't duplicate. The migration-proof
membership signal is the `isbrs:` field itself (`WHERE isbrs`), which
the constitutional test enforces.

New fields require a MINOR bump of this SOP. Field renames are MAJOR and
essentially forbidden — Dataview tables across years depend on them.

## 2. The three rules

1. **`id` is a permanent contract** — the chart-id principle (WIDGET_SPEC
   §4.2) applied to documents. Rename files freely; the id survives.
2. **Artifacts are versioned; events are dated.** Constitutions, SOPs,
   maps, specs, guides → semver. Sessions, decisions, ledger rows →
   dated, never versioned. **Seals are append-only ledgers:** the pin is
   immutable, the exposure log grows, and the only mutable field is
   `status: blind → exposed`.
3. **Headers carry state; git carries history.** Status lines say what a
   document *is now*, in one or two lines. Biographies live in the
   repo's `CHANGELOG.md` and in git itself. The commit hash is always
   the truth underneath the number: semver is the render, the commit is
   the bite.

## 3. Semver semantics for prose

- **MAJOR** — obligations change: a law added, removed, or altered in
  force; a procedure's requirements change.
- **MINOR** — additive, non-breaking: new sections, new registry rows,
  clarifications that extend scope.
- **PATCH** — wording, typos, formatting, manifest retrofits.

The constitution's signature event sets `1.0.0` and flips
`status: draft → signed` (its §7). After signature, every bump is a Gate
G1 event with a CHANGELOG entry.

## 4. Changelogs

One `CHANGELOG.md` per repository (`kind: changelog`), newest first, one
line per version per document. Migration rule of the 2026-07-03 reset:
no document carries its own history in its header from now on.

## 5. The vault window

Working clones of the program repos live at `IcebergSim/70 Repos/`
inside the Obsidian vault — a **window, not a copy**: the clone is the
canonical working file; Obsidian merely indexes it. Precautions: add
`70 Repos/` to the vault's own `.gitignore`; treat repo folders as
read-mostly inside Obsidian; commits flow through git as always.
Dataview then spans thought and truth in one table.

## 6. Enforcement (how the system applies itself)

A law that can be a test must become one. Four producers, four
mechanisms — only the first is load-bearing; the rest are conveniences:

1. **Repos (CCd):** `tests/constitutional/test_manifests.py` — canonical
   copy ships alongside this SOP — walks every `.md`, validates the
   schema, enforces **id uniqueness** across the repo, and blocks merge
   when red. Exemptions are structural, never per-file whims: generated
   dirs (`scratch/`, caches, builds), `_templates/` (molds are not
   documents), `_about.md` (folder markers are not documents).
2. **CCd's standing order:** every ISM repo's `CLAUDE.md` carries the
   line: *"Every new `.md` opens with the SOP-DOCS manifest (id, isbrs,
   kind, status, version-or-date). `test_manifests.py` enforces it —
   write the manifest first."*
3. **The vault (EB):** capture hotkeys (QuickAdd or Templater) create
   notes pre-filled with template, `kind`, and date — the vault is a
   flat cabinet, tags-first; folders exist only where a machine consumes
   the path (git-ignore for `70 Repos/`, search-exclusion for
   `90 Archive/`). The Linter plugin (or "Update time on edit")
   maintains `updated:`. The vault has no CI; the capture hotkeys are
   its rail.
4. **Claude (conversation):** a standing memory instruction, set
   2026-07-03 — every program document born in chat arrives already
   manifested.

**Single canonical copy rule (added after the landmark incident):** one
working copy per document, ever. The 2026-07-03 sealing run caught a
namespace zombie resurrected by two diverged working copies — the exact
disease this system treats. When staging areas exist, one is canonical
and the others are regenerated from it, never patched in parallel.
