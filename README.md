# check-the-tree-before-you-commit

[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)](./LICENSE)

A Claude Code skill that forces agents to verify exactly what is being staged before every commit.

## What it does

No surprise files in the commit. Before committing, the agent must:

* **Run `git status`** — see every modified, new, and deleted file.
* **Run `git diff --cached`** — review exactly what will be committed.
* **Verify the scope** — confirm the commit contains only what it should.
* **Fix before commit** — unstage or remove anything that doesn't belong.
* **Commit** — only now, with a clean, intentional diff.

## Install

```bash
mkdir -p ~/.claude/skills
cp -r check-the-tree-before-you-commit ~/.claude/skills/check-the-tree-before-you-commit
```

Load it in your session:

```
/skill check-the-tree-before-you-commit
```

Or add it to your `CLAUDE.md` so it's active in every session.

## How it works

```
about to commit
    ↓
agent runs `git status`
    ↓
agent runs `git diff --cached`
    ↓
agent verifies scope matches intent
    ↓
agent fixes anything that doesn't belong
    ↓
agent commits clean diff
```

## Example

```
$ git status
Changes to be committed:
  modified:   components/Header.jsx
  new file:   hooks/useTheme.js
  new file:   debug.log   ← does not belong

$ git reset debug.log
$ git commit -m "feat(header): add dark-mode toggle"
```

The commit contains only `Header.jsx` and `useTheme.js` — nothing more.

## Files

| File | Purpose |
|------|---------|
| `SKILL.md` | The skill — the rule, protocol, and example |

## Contributing

Pull requests welcome. Open an issue to discuss changes first.

## License

MIT