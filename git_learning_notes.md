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

Compare currnet branch with the sha that current branch checked out from

```bash
git diff HEAD # Before commit
git diff master... # After commit
git diff master.. # This will include changes after the current branch diverge

git diff master... --name-only --relative
```

```
git diff --name-only --diff-filter=ACMTUXB
```


```
git ls-files --others --exclude-standard
git log --abbrev-commit master..
git diff-tree --no-commit-id --name-only --relative
```