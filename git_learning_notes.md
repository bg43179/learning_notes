## Git status
Inculde Untracked file
```bash
git status -s #show status concisely
```

```bash
git status -u #show untracked, default to all
git status -uall #also shows individual files in untracked directories.
git status -uno #show no untracked files
```

```bash
git status --porcelain #give the output in an easy-to-parse format for scripts.
```

Advanced
```bash
git status -suall -- porcelain #show changed and untracked file in short and easy to parse mode
```

## Git diff
```
git diff --name-only --relative | xargs ls -1 2>/dev/null | grep '\.rb$' | xargs rubocop
```

Compare currnet branch with the sha that current branch checked out from (Only check committed c)
```
git diff HEAD
git diff master...
git diff master... --name-only --relative
```

```
git diff --name-only --diff-filter=ACMTUXB
```

```
git status -suall --porcelain | awk '{print $2}' | grep '\.rb$' | xargs rubocop
git status -suall | awk '{print $2}' | grep '\.rb$' | xargs rubocop
```