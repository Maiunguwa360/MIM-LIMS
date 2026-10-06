# MIM-LIMS

## Advanced Git commands

These commands help manage unfinished work, move changes between branches, and
undo commits. Replace placeholder branch names and commit IDs with values from
your repository.

### `git stash`

Temporarily save uncommitted changes so you can work on something else. By
default, Git stashes tracked file changes; use `-u` to include untracked files.

```sh
git stash push -u -m "work in progress: sample intake"
git switch main
# Later, return to your branch and restore the saved changes:
git switch feature/sample-intake
git stash pop
```

Use `git stash apply` instead of `pop` to restore changes while keeping the
stash entry. List saved stashes with `git stash list`.

### `git cherry-pick`

Apply the changes from an existing commit to the branch you are currently on.
This creates a new commit with the same changes and a different commit ID.

```sh
git switch release
git cherry-pick abc1234
```

If conflicts occur, resolve them, stage the files, and run
`git cherry-pick --continue`. To abandon the operation, run
`git cherry-pick --abort`.

### `git revert`

Undo the changes from a commit by creating a new commit. This preserves existing
history and is generally appropriate for commits that have already been shared.

```sh
git revert abc1234
```

Git may open an editor for the new commit message. If conflicts occur, resolve
them, stage the files, and run `git revert --continue`; use
`git revert --abort` to cancel.

### `git reset`

Move the current branch pointer to another commit. The reset mode controls what
happens to changes in your index and working tree:

```sh
git reset --soft HEAD~1   # Undo the latest commit; keep changes staged
git reset --mixed HEAD~1  # Undo the latest commit; keep changes unstaged (default)
git reset --hard HEAD~1   # Undo the latest commit and discard its changes
```

`--hard` permanently discards uncommitted changes, so verify your work first.
Reset rewrites local history; avoid resetting commits that others may already
have based work on. To undo a shared commit without rewriting history, use
`git revert` instead.
