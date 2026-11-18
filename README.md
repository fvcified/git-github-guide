# Git & GitHub Guide

## Table of Contents

### Getting Started & Setup
- [1. Create a repository on GitHub](#1️⃣-create-a-repository-on-github)
- [2. Prepare your local folder](#2️⃣-prepare-your-local-folder)
- [3. Connect to GitHub remote](#3️⃣-connect-to-github-remote)
- [4. Rename local branch to main](#4️⃣-rename-local-branch-to-main)
- [5. Set upstream branch](#5️⃣-set-upstream-branch)
- [6. Authentication (Recommended)](#6️⃣-authentication-recommended)
- [7. Clone an existing repository](#7️⃣-clone-an-existing-repository)

### Everyday Workflow & Syncing
- [11. Everyday workflow](#1️⃣1️⃣-everyday-workflow)
- [13. Fetch without merge](#1️⃣3️⃣-fetch-without-merge)
- [14. Update branch with latest main](#1️⃣4️⃣-update-branch-with-latest-main)
- [24. Check commit history](#2️⃣4️⃣-check-commit-history)
- [25. Stash changes](#2️⃣5️⃣-stash-changes)
- [29. Diff & inspect](#2️⃣9️⃣-diff--inspect)

### Branching, Merging & Collaboration
- [15. Pull Request workflow](#1️⃣5️⃣-pull-request-workflow)
- [16. Fork & Upstream workflow](#1️⃣6️⃣-fork--upstream-workflow)
- [26. Branching](#2️⃣6️⃣-branching)
- [27. Merging branches](#2️⃣7️⃣-merging-branches)
- [28. Tagging](#2️⃣8️⃣-tagging)
- [30. Cherry-pick](#3️⃣0️⃣-cherry-pick)
- [33. Submodules](#3️⃣3️⃣-submodules)
- [41. Conventional Commits (Team Standard)](#4️⃣1️⃣-conventional-commits-team-standard)

### Fixing Mistakes & Recovery
- [8. Handle rejected push](#8️⃣-handle-rejected-push)
- [9. Handle merge conflicts during rebase](#9️⃣-handle-merge-conflicts-during-rebase)
- [10. Force push (last resort)](#🔟-force-push-last-resort)
- [12. Upstream branch mismatch](#1️⃣2️⃣-upstream-branch-mismatch)
- [17. Amend commit](#1️⃣7️⃣-amend-commit)
- [18. Handle merge conflicts (non-rebase)](#1️⃣8️⃣-handle-merge-conflicts-non-rebase)
- [19. Undo last commit (keep changes)](#1️⃣9️⃣-undo-last-commit-keep-changes)
- [20. Undo last commit (discard changes)](#2️⃣0️⃣-undo-last-commit-discard-changes)
- [21. Rescue commits from protected main (GH006 error)](#2️⃣1️⃣-rescue-commits-from-protected-main-gh006-error)
- [22. Hard reset local branch to match remote](#2️⃣2️⃣-hard-reset-local-branch-to-match-remote)
- [23. Restore & unstage](#2️⃣3️⃣-restore--unstage)
- [31. Revert](#3️⃣1️⃣-revert)
- [32. Clean untracked files](#3️⃣2️⃣-clean-untracked-files)
- [37. Fix detached HEAD](#3️⃣7️⃣-fix-detached-head)
- [38. Recover deleted branch](#3️⃣8️⃣-recover-deleted-branch)
- [39. Interactive rebase](#3️⃣9️⃣-interactive-rebase)
- [40. Squash commits](#4️⃣0️⃣-squash-commits)

### Configuration & Reference
- [34. Aliases](#3️⃣4️⃣-aliases)
- [35. Global config](#3️⃣5️⃣-global-config)
- [36. .gitignore](#3️⃣6️⃣-gitignore)
- [Notes](#-notes)

---

## 1️⃣ Create a repository on GitHub
- Go to **GitHub → New repository**
- Enter the repository name **same as your folder** (e.g., `my_repository`)
- **Do NOT** check README / .gitignore / License
- Copy the repository URL

Example:

```bash
https://github.com/<github_username>/<repository_name>.git
```

## 2️⃣ Prepare your local folder
```bash
cd /path/to/your/folder

git init
git add .
git commit -m "Initial commit"
```

If the folder is empty:

```bash
touch .gitkeep
git add .
git commit -m "Initial commit"
```

## 3️⃣ Connect to GitHub remote
```bash
git remote add origin https://github.com/<github_username>/<repository_name>.git
```

Verify:

```bash
git remote -v
```

Show detailed remote information:

```bash
git remote show origin
```

## 4️⃣ Rename local branch to main
```bash
git branch -M main
```

## 5️⃣ Set upstream branch
```bash
git push -u origin main
```

After first push:

```bash
git push
```

## 6️⃣ Authentication (Recommended)
Windows:

```bash
git config --global credential.helper manager
```

GitHub CLI:

```bash
gh auth login
```

Verify login:

```bash
gh auth status
```

## 7️⃣ Clone an existing repository
```bash
git clone https://github.com/<user>/<repo>.git

cd <repo>
```

Clone a specific branch:

```bash
git clone -b <branch_name> https://github.com/<user>/<repo>.git
```

## 8️⃣ Handle rejected push
If you see:

```text
rejected - fetch first
non-fast-forward
```

Run:

```bash
git pull origin main --rebase
```

Then:

```bash
git push origin main
```

## 9️⃣ Handle merge conflicts during rebase
Keep your version:

```bash
git checkout --ours <file>
git add <file>
git rebase --continue
```

Keep remote version:

```bash
git checkout --theirs <file>
git add <file>
git rebase --continue
```

Abort rebase:

```bash
git rebase --abort
```

Editor shortcuts:

Vim:

```text
:wq
```

Nano:

```text
Ctrl+X
```

## 🔟 Force push (last resort)
Safer:

```bash
git push origin main --force-with-lease
```

Dangerous:

```bash
git push origin main --force
```

Only use when necessary.

## 1️⃣1️⃣ Everyday workflow
```bash
git add .
git commit -m "your message"
git push
```

## 1️⃣2️⃣ Upstream branch mismatch
If you see:

```text
fatal: The upstream branch of your current branch does not match
```

Run:

```bash
git branch --set-upstream-to=origin/main main
```

## 1️⃣3️⃣ Fetch without merge
Fetch latest changes:

```bash
git fetch origin
```

Fetch all remotes:

```bash
git fetch --all
```

Difference:

```bash
git fetch
```

Downloads changes only.

```bash
git pull
```

Downloads + merges/rebases.

Clean deleted remote branches from local list:

```bash
git fetch --prune
```

## 1️⃣4️⃣ Update branch with latest main
Using rebase:

```bash
git checkout <branch_name>

git fetch origin

git rebase origin/main
```

Using merge:

```bash
git checkout <branch_name>

git fetch origin

git merge origin/main
```

## 1️⃣5️⃣ Pull Request workflow
```bash
git checkout -b feature-name

git add .

git commit -m "feat: description"

git push -u origin feature-name
```

Then:

1. Open GitHub
2. Click **Compare & Pull Request**
3. Create Pull Request
4. Wait for review

After PR is merged on GitHub (Clean up):

```bash
git switch main
git pull origin main
git branch -d feature-name
git fetch --prune
```

Using GitHub CLI (`gh`) instead of browser:

```bash
gh pr create --base main --title "feat: description" --body "PR details"
gh pr list
gh pr checkout <pr_number>
gh pr review --approve
gh pr merge --merge --delete-branch
```

## 1️⃣6️⃣ Fork & Upstream workflow
Add original repository as upstream:

```bash
git remote add upstream https://github.com/<original_owner>/<repo>.git
```

Sync fork with original repository:

```bash
git fetch upstream
git switch main
git merge upstream/main
git push origin main
```

## 1️⃣7️⃣ Amend commit
Change last commit message:

```bash
git commit --amend -m "new message"
```

Add forgotten files:

```bash
git add .

git commit --amend --no-edit
```

## 1️⃣8️⃣ Handle merge conflicts (non-rebase)
Check conflicts:

```bash
git status
```

Keep local version:

```bash
git checkout --ours <file>
```

Keep remote version:

```bash
git checkout --theirs <file>
```

Resolve:

```bash
git add <file>

git commit -m "resolve merge conflict"

git push
```

## 1️⃣9️⃣ Undo last commit (keep changes)
```bash
git reset --soft HEAD~1
```

## 2️⃣0️⃣ Undo last commit (discard changes)
```bash
git reset --hard HEAD~1
```

## 2️⃣1️⃣ Rescue commits from protected main (GH006 error)
Move accidental commits made directly on `main` to a new branch and reset local main:

```bash
git switch -c fix-branch-name
git push -u origin fix-branch-name
git switch main
git reset --hard origin/main
```

## 2️⃣2️⃣ Hard reset local branch to match remote
Discard all local changes/commits and match GitHub 100%:

```bash
git fetch origin
git reset --hard origin/main
```

## 2️⃣3️⃣ Restore & unstage
Discard file changes:

```bash
git restore <file>
```

Discard all unstaged changes:

```bash
git restore .
```

Unstage file:

```bash
git restore --staged <file>
```

Legacy:

```bash
git reset HEAD <file>
```

## 2️⃣4️⃣ Check commit history
```bash
git log --oneline
```

```bash
git log --oneline --graph --all
```

```bash
git log --pretty=format:"%h %an %ad %s" --date=short
```

## 2️⃣5️⃣ Stash changes
```bash
git stash
```

```bash
git stash list
```

```bash
git stash pop
```

```bash
git stash apply stash@{0}
```

```bash
git stash drop stash@{0}
```

```bash
git stash clear
```

## 2️⃣6️⃣ Branching
Create:

```bash
git branch <branch_name>
```

Switch:

```bash
git checkout <branch_name>
```

Modern:

```bash
git switch <branch_name>
```

Create and switch:

```bash
git checkout -b <branch_name>
```

Modern:

```bash
git switch -c <branch_name>
```

List:

```bash
git branch -a
```

Delete local:

```bash
git branch -d <branch_name>
```

Force delete:

```bash
git branch -D <branch_name>
```

Delete remote:

```bash
git push origin --delete <branch_name>
```

Rename:

```bash
git branch -m <new_name>
```

## 2️⃣7️⃣ Merging branches
```bash
git checkout main
```

```bash
git merge <branch_name>
```

```bash
git merge --no-ff <branch_name> -m "merge: <branch_name> into main"
```

Abort:

```bash
git merge --abort
```

## 2️⃣8️⃣ Tagging
```bash
git tag v1.0.0
```

```bash
git tag -a v1.0.0 -m "Release version 1.0.0"
```

```bash
git tag
```

```bash
git push origin v1.0.0
```

```bash
git push origin --tags
```

```bash
git tag -d v1.0.0
```

```bash
git push origin --delete tag v1.0.0
```

## 2️⃣9️⃣ Diff & inspect
```bash
git diff
```

```bash
git diff --staged
```

```bash
git diff main..<branch_name>
```

```bash
git show <commit_hash>
```

```bash
git blame <file>
```

## 3️⃣0️⃣ Cherry-pick
```bash
git cherry-pick <commit_hash>
```

```bash
git cherry-pick <commit_hash> --no-commit
```

Abort:

```bash
git cherry-pick --abort
```

## 3️⃣1️⃣ Revert
```bash
git revert <commit_hash>
```

```bash
git revert <commit_hash> --no-commit
```

## 3️⃣2️⃣ Clean untracked files
Preview:

```bash
git clean -n
```

Delete files:

```bash
git clean -f
```

Delete files + folders:

```bash
git clean -fd
```

Delete everything:

```bash
git clean -fdx
```

## 3️⃣3️⃣ Submodules
```bash
git submodule add https://github.com/<user>/<repo>.git <path>
```

```bash
git clone --recurse-submodules https://github.com/<user>/<repo>.git
```

```bash
git submodule update --remote
```

Remove:

```bash
git submodule deinit <path>

git rm <path>
```

## 3️⃣4️⃣ Aliases
```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.lg "log --oneline --graph --all"
```

Usage:

```bash
git st
git co main
git br
git lg
```

## 3️⃣5️⃣ Global config
```bash
git config --global user.name "Your Name"
```

```bash
git config --global user.email "you@example.com"
```

VSCode:

```bash
git config --global core.editor "code --wait"
```

Vim:

```bash
git config --global core.editor "vim"
```

Nano:

```bash
git config --global core.editor "nano"
```

Default branch:

```bash
git config --global init.defaultBranch main
```

View config:

```bash
git config --list
```

## 3️⃣6️⃣ .gitignore
Create:

```bash
touch .gitignore
```

Common entries:

```gitignore
node_modules/
.env
.env.local
.DS_Store
dist/
build/
*.log
.next/
.vercel/
```

Stop tracking a file:

```bash
git rm --cached <file>

git add .

git commit -m "remove file from tracking"
```

## 3️⃣7️⃣ Fix detached HEAD
```bash
git checkout -b <new_branch_name>
```

Then:

```bash
git checkout main

git merge <new_branch_name>
```

## 3️⃣8️⃣ Recover deleted branch
```bash
git reflog
```

```bash
git checkout -b <branch_name> <commit_hash>
```

## 3️⃣9️⃣ Interactive rebase
```bash
git rebase -i HEAD~<N>
```

Commands:

- pick
- reword
- squash
- drop

Never rewrite shared branch history.

## 4️⃣0️⃣ Squash commits
```bash
git reset --soft HEAD~3

git commit -m "combined commit"

git push origin main --force-with-lease
```

## 4️⃣1️⃣ Conventional Commits (Team Standard)
- `feat:` add a new feature (e.g., `feat: add login page`)
- `fix:` fix a bug (e.g., `fix: resolve null pointer error`)
- `docs:` documentation updates (e.g., `docs: update setup guide`)
- `style:` formatting/CSS changes without logic changes
- `refactor:` code restructuring without changing behavior
- `chore:` maintenance tasks, dependencies, or config updates

## ⚠️ Notes

- Git ignores empty folders → use `.gitkeep`
- `git fetch` does not merge
- `git pull` = fetch + merge/rebase
- `git revert` is safer than `git reset`
- `git reflog` can recover most mistakes
- Prefer `--force-with-lease` over `--force`
- Use `.gitignore` early
- Never force push to shared production branches
- Always pull or fetch before major work
- `--ours` keeps local changes
- `--theirs` keeps incoming changes
- Detached HEAD is not dangerous if you create a branch before leaving it
