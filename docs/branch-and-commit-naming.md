# Branch and Commit Naming

A short guide for naming git branches and commit messages.

## Core Idea

- **Branch** = the main story
- **Commit** = one step of that story
- Name the **outcome**, not the files you touched
- New concern mid-way? Start a new branch/PR

---

## Branches

**Format:** `<prefix>/<short-kebab-case-outcome>` (about 3-6 words)

| Prefix      | Use for                         |
|-------------|---------------------------------|
| `feature/`  | New capability                  |
| `fix/`      | Broken behavior                 |
| `refactor/` | Same behavior, better structure |
| `chore/`    | Cleanup, deps, tooling          |
| `hotfix/`   | Urgent production break         |

```
Good: feature/bulk-drop-excel
Good: fix/drop-pagination-double-fetch
Bad:  feature/bulk-drop1
Bad:  fix/UI
```

One main concern per branch.

---

## Commits

**Format:** `<prefix>(<scope>): <plain outcome>`

| Prefix     | Meaning                             |
|------------|-------------------------------------|
| `feat`     | New user-facing capability          |
| `fix`      | Bug fix                             |
| `refactor` | Same behavior, cleaner code         |
| `chore`    | Cleanup, deps, config               |
| `style`    | UI/copy polish, no behavior change  |
| `revert`   | Undo a previous change              |

### Scope

- Use the **specific feature area** in kebab-case, not the broad module
- Use `drop-registration`, `bulk-drop`, `mass-registration` instead of just `registration`
- Use `slotbook-editor` instead of just `slotbook`
- Use the broad module only if the change truly spans many flows

### Rules

1. One commit = one reason (if you need "and", split it)
2. Write a plain sentence a teammate understands
3. Never use `WIP`, `update`, `fix stuff`, or `gemini fix`
4. Review-bot follow-ups still say what was fixed
5. Reverts: `revert(<scope>): <what you undo>`

```
Good: feat(bulk-drop): add Excel download for registered students
Good: fix(drop-registration): check filter button ref before measuring panel
Good: revert(slotbook-editor): undo period resolution change

Bad:  feat(registration): add excel download
Bad:  fix
Bad:  WIP
```

---

## Self-Check Before Committing

1. Does the prefix match the change?
2. Is the scope specific?
3. Is the outcome clear without opening the diff?
4. Could this commit be reverted alone safely?
5. Does it still belong to this branch's story?