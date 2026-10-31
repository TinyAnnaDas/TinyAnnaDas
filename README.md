---
description: Rulebook for naming git branches and commit messages (with prefixes and specific scopes)
alwaysApply: true
---

# Branch and commit naming rulebook

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

### Always use prefix + specific scope

Format:

```
<prefix>(<scope>): <plain-English outcome>
```

Allowed prefixes:

| Prefix | Meaning |
|--------|---------|
| `feat` | New user-facing capability |
| `fix` | Bug fix or hardening of broken/unsafe behavior |
| `refactor` | Same behavior, clearer/shared structure |
| `chore` | Cleanup, deps, config, dead code removal |
| `style` | UI/spacing/copy polish with no behavior change |
| `revert` | Explicitly undoes a previous change |

### Scope rules (important)

1. Scope = the **specific feature area**, not only the broad module
2. Use **kebab-case**
3. Prefer the screen/flow name people use in conversation
4. Do **not** stop at a vague module name when a tighter scope exists

Within registration, prefer scopes like:

| Prefer | Avoid when a tighter scope fits |
|--------|----------------------------------|
| `drop-registration` | `registration` |
| `bulk-drop` | `registration` |
| `mass-registration` | `registration` |
| `bulk-registration` | `registration` |
| `add-registration` | `registration` |
| `student-registration` | `registration` |
| `faculty-approval` | `registration` |

Same idea elsewhere:

| Prefer | Avoid when tighter exists |
|--------|---------------------------|
| `slotbook-editor` | `slotbook` alone |
| `slotbook-preview` | `slotbook` alone |
| `student-efile` | `profile` alone |
| `my-advisees` | `profile` alone |

Use the broad module (`registration`, `slotbook`) only when the change truly spans several flows and no single tighter scope fits.

### Commit rules

1. **One commit = one reason** a teammate would care
2. If the subject needs “and”, split into two commits
3. Prefer a **plain outcome sentence** after the scope (team-readable, not jargon soup)
4. Never use: `WIP`, `update`, `fix stuff`, `good gemini`, `gemini fix`
5. Review-bot follow-ups still get a real message: say **what** you fixed
6. Suggested commit messages from the agent must include **prefix + specific scope**
7. A revert should be explicit: `revert(<scope>): <what you are undoing>`

### Commit examples

```
Good: feat(bulk-drop): add Excel download for registered students
Good: feat(drop-registration): show success toast after drop confirms
Good: fix(bulk-drop): prevent Excel export crash when API data is missing
Good: fix(drop-registration): check filter button ref before measuring panel
Good: refactor(drop-registration): reuse CommonDataTable on students list
Good: refactor(drop-registration): reuse CommonDataTable on courses list
Good: chore(drop-registration): remove unused RegisteredCoursesTable
Good: style(drop-registration): tighten header density
Good: feat(mass-registration): show Ready Warn Blocked chips on cohort grid
Good: fix(add-registration): keep category dropdown visible for all rows
Good: revert(slotbook-editor): undo period resolution change in class composition modal

Bad: feat(registration): add excel download
Bad: fix(registration): gemini issues
Bad: good gemini
Bad: Update DropByCourseNo.tsx
Bad: fix
Bad: feat(registration): refactor migrate clash soft-warn path to hard-fail semantics in attempt_register
Bad: WIP
```

### Quick self-check before committing

1. Does the prefix match the kind of change?
2. Is the scope specific enough (`drop-registration` / `mass-registration`, not just `registration`)?
3. Can a teammate understand the outcome without opening the diff?
4. Would reverting **only this commit** leave the branch in a sensible state?
5. Is this still the same story as the branch, or should it be a new branch/PR?

---

## How branch + commits work together

Example story: Bulk Drop Excel

```
Branch: feature/bulk-drop-excel

Commits:
  feat(bulk-drop): add Excel download for registered students
  feat(bulk-drop): wire Excel upload to select rows
  feat(bulk-drop): replace students table from Excel upload
  fix(bulk-drop): harden Excel load when API data is missing
```

Follow-up story (separate):

```
Branch: refactor/drop-tables-use-common-data-table

Commits:
  refactor(drop-registration): reuse CommonDataTable on students list
  refactor(drop-registration): reuse CommonDataTable on courses list
```
