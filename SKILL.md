---
name: check-the-tree-before-you-commit
description: Before committing, run git status and diff to verify exactly what is being staged.
metadata:
  source: owner, 2026-10-31
  verified: false
---

# check-the-tree-before-you-commit

## Core rule

Before committing, verify exactly what is being staged. Run `git status` and `git diff --cached` — confirm the scope matches the intended change. No surprise files in the commit.

## Protocol

Before every commit:

1. **Run `git status`.** See every modified, new, and deleted file.
2. **Run `git diff --cached`.** Review exactly what will be committed.
3. **Verify the scope.** Does the commit contain only what it should? No stray files, no debug prints, no unrelated changes.
4. **Fix before commit.** If something doesn't belong, unstage it or remove it before committing.
5. **Commit.** Only now, with a clean, intentional diff.

## Gate

A commit with files you didn't intend to include is not clean. If you commit without checking the tree first, stop and amend.

## Example

```
$ git status
On branch main
Changes to be committed:
  modified:   components/Header.jsx
  new file:   hooks/useTheme.js
  new file:   debug.log   ← does not belong

$ git reset debug.log
$ git commit -m "add dark-mode toggle"
```

The commit now contains only `Header.jsx` and `useTheme.js` — nothing more.

## Exception

None. Every commit gets this check, no matter how small.