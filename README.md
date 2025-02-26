 # Clone, Manage Branches, and Keep a GitHub Project Updated

This guide covers cloning with tokens, branch management, and update workflows.

---

## Part 1: Clone Using a Personal Access Token

### Why Tokens?
GitHub [requires tokens instead of passwords](https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/) for HTTPS operations.

---

### Step 1: Generate Token
1. **GitHub.com** → Settings → Developer Settings → Personal Access Tokens → Tokens (classic)
2. **Scopes**: `repo` (full repo access) + `workflow` (if using Actions)
3. **Copy token** immediately after generation

---

### Step 2: Clone Repository
#### Interactive Clone (Recommended):
```bash
git clone https://github.com/username/repo.git
# When prompted:
# Username = GitHub username
# Password = PASTE_TOKEN_HERE
```

#### Embedded Token (Temporary Use Only):
```bash
git clone https://<TOKEN>@github.com/username/repo.git
```
⚠️ Token appears in command history - use cautiously

---

## Part 2: Branch Management

### 1. List Branches
```bash
git branch -a  # Local branches (green) and remote (red)
```

### 2. Create New Local Branch
```bash
git checkout -b feature/new-login  # Creates and switches to new branch
```

### 3. Push Local Branch to Remote
```bash
git push -u origin feature/new-login  # -u sets upstream tracking
```

### 4. Track Remote Branch
```bash
git checkout --track origin/dev  # Creates local 'dev' tracking remote
```

### 5. Delete Branches
```bash
# Local branch
git branch -d old-feature  

# Force delete unmerged branch
git branch -D broken-feature  

# Remote branch
git push origin --delete staging
```

### 6. Sync with Remote Branches
```bash
git fetch --all  # Get latest branches and commits
git remote prune origin  # Delete local refs to removed remote branches
```

---

## Part 3: Keeping Your Repository Updated

### 1. Nuclear Reset (DISCARD Changes)
```bash
git fetch --all
git reset --hard origin/main  # Replace with your branch
git clean -fd  # Remove untracked files
```

### 2. Safe Update (KEEP Changes)
```bash
git stash
git pull origin main
git stash pop  # May require conflict resolution
```

### 3. Clean History Rebase
```bash
git pull --rebase origin main
```

### 4. Commit Before Merging
```bash
git add .
git commit -m "Save before merge"
git pull origin main
```

---

## Workflow Cheat Sheet

| Scenario                      | Command                              |
|-------------------------------|--------------------------------------|
| Clone private repo            | `git clone https://<TOKEN>@github...`|
| See all branches              | `git branch -a`                     |
| Switch branch                 | `git checkout branch-name`          |
| Update & keep changes         | `stash` → `pull` → `stash pop`      |
| Delete merged remote branches | `git remote prune origin`           |
| Force sync with remote        | `reset --hard origin/main`          |

---

## Troubleshooting

- **Permission denied**: Token expired or missing `repo` scope
- **No tracking information**: Use `-u` when pushing new branches
- **Deleted branch still appears**: Run `git fetch --prune`
- **Merge conflicts**: Resolve manually in affected files, then `git add` and `git rebase --continue`
