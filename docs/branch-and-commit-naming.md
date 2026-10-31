# Branch and commit naming rulebook

A practical guide for naming git branches and commit messages. Useful if you are early in your career and want a clear, consistent style teammates can scan in a PR list.

## Core idea

- **Branch** = the main user-visible story
- **Commit** = one beat of that story
- Name both for the **outcome**, not for every file touched
- If a second concern starts mid-way → new branch / new PR (and usually a new commit series)

---

## Branches

### Prefix by kind of work

| Prefix | Use when | Example |
|--------|----------|---------|
| `feature/` | New capability users did not have | `feature/bulk-drop-excel` |
| `fix/` | Broken or incorrect behavior | `fix/drop-pagination-double-fetch` |
| `refactor/` | Restructure / reuse with same behavior | `refactor/drop-common-data-table` |
| `chore/` | Tooling, cleanup, deps, non-product | `chore/remove-unused-registered-courses-table` |
| `hotfix/` | Urgent production break | `hotfix/drop-api-500` |

### Branch naming rules

1. Prefer **kebab-case** after the prefix
2. Name the **user-visible outcome**, not tickets-only or file names
3. Avoid trailing junk like `feature/bulk-drop1` when `feature/bulk-drop-excel` is clearer
4. One main concern per branch; do not mix large feature + large refactor in one PR if it can split
5. Keep it short enough to read in a PR list (~3–6 words after the prefix)

### Branch examples

```
Good: feature/bulk-drop-excel
Good: fix/drop-period-filter-clears-selection
Good: refactor/drop-tables-use-common-data-table

Bad: feature/bulk-drop1
Bad: fix/UI
Bad: asu-dev5-updates
Bad: feature/DropRegisteredStudentsTable-CommonDataTable-Excel-modal
```

---

## Commits

### Always use a prefix

Format:

```
<prefix>: <plain-English outcome>
```

Allowed prefixes:

| Prefix | Meaning |
|--------|---------|
| `feat:` | New user-facing capability |
| `fix:` | Bug fix or hardening of broken/unsafe behavior |
| `refactor:` | Same behavior, clearer/shared structure |
| `chore:` | Cleanup, deps, config, dead code removal |
| `style:` | UI/spacing/copy polish with no behavior change |
| `revert:` | Explicitly undoes a previous change |

### Commit rules

1. **One commit = one reason** a teammate would care
2. If the subject needs “and”, split into two commits
3. Prefer a **plain outcome sentence** after the prefix (team-readable, not jargon soup)
4. Never use: `WIP`, `update`, `fix stuff`, `good gemini`, `gemini fix`
5. Review-bot follow-ups still get a real message: say **what** you fixed
6. A revert should be explicit: `revert: <what you are undoing>`

### Commit examples

```
Good: feat: add Bulk Drop Excel download for students
Good: feat: show success toast after drop confirms
Good: fix: prevent Excel export crash when API data is missing
Good: fix: check filter button ref before measuring panel position
Good: refactor: reuse CommonDataTable on drop registered students list
Good: chore: remove unused RegisteredCoursesTable component
Good: style: tighten Drop Registration header density
Good: revert: undo period resolution change in class composition modal

Bad: good gemini
Bad: gemini fix
Bad: Update DropByCourseNo.tsx
Bad: fix
Bad: feat: refactor migrate clash soft-warn path to hard-fail semantics in attempt_register
Bad: WIP
```

### Quick self-check before committing

1. Does the prefix match the kind of change?
2. Can a teammate understand the outcome without opening the diff?
3. Would reverting **only this commit** leave the branch in a sensible state?
4. Is this still the same story as the branch, or should it be a new branch/PR?

---

## How branch + commits work together

Example story: Bulk Drop Excel

```
Branch: feature/bulk-drop-excel

Commits:
  feat: add Bulk Drop Excel download for students
  feat: wire Bulk Drop Excel upload to select rows
  feat: replace Bulk Drop table from Excel upload
  fix: harden Excel load when API data is missing
```

Follow-up story (separate):

```
Branch: refactor/drop-tables-use-common-data-table

Commits:
  refactor: reuse CommonDataTable on drop registered students list
  refactor: reuse CommonDataTable on drop registered courses list
```
