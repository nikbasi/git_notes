# Complete GitHub Workflow: Clone, Commit, Push, Branches & Updates

## Table of Contents
1. [Cloning with a Token](#part-1-clone-using-a-personal-access-token)  
2. [Branch Management](#part-2-branch-management)  
3. [Committing & Pushing](#part-3-committing--pushing-changes)  
4. [Updating Strategies](#part-4-keeping-your-repository-updated)  
5. [Undoing Changes](#part-5-undoing-mistakes)  
6. [Essential Tools](#part-6-essential-tools--tips)  

---

## Part 1: Clone Using a Personal Access Token

### Generate Token:
1. **GitHub.com** → Settings → Developer Settings → Personal Access Tokens (classic)
2. Select `repo` and `workflow` scopes  
3. **Never store tokens in code**  

### Clone:
```bash
# Interactive (safer)
git clone https://github.com/username/repo.git
# When prompted: username = GitHub username, password = PASTE_TOKEN

# Embedded token (temporary use only)
git clone https://<TOKEN>@github.com/username/repo.git
```

---

## Part 2: Branch Management

### Key Commands:
```bash
# Create and switch to new branch
git checkout -b feature/new-login

# Push branch to remote & set upstream
git push -u origin feature/new-login

# List all branches (local & remote)
git branch -a

# Delete merged remote branch
git push origin --delete old-branch
```

---

## Part 3: Committing & Pushing Changes

### Basic Workflow:
1. Stage changes:
```bash
git add .                         # All files
git add src/component.js          # Specific file
```

2. Commit with message:
```bash
git commit -m "Add user login validation"
```

3. Push to remote:
```bash
git push origin main              # Push to specific branch
git push                          # Push to tracked branch
```

### Pro Tips:
- **Atomic Commits**: Commit small logical changes instead of bulk updates  
- **Meaningful Messages**: Use imperative tense ("Fix bug" not "Fixed bug")  
- **Push Frequency**: Push daily to avoid merge conflicts  

---

## Part 4: Keeping Your Repository Updated

### Update Strategies:
| Scenario                  | Command                              |
|---------------------------|--------------------------------------|
| Discard local changes     | `git reset --hard origin/main`       |
| Save changes temporarily | `git stash` → `pull` → `stash pop`   |
| Clean history             | `git pull --rebase`                  |
| Safe merge                | Commit first, then `git pull`        |

---

## Part 5: Undoing Mistakes

### 1. Unstage File:
```bash
git reset HEAD src/component.js
```

### 2. Discard Uncommitted Changes:
```bash
git checkout -- src/component.js  # Single file
git reset --hard HEAD             # All changes
```

### 3. Amend Last Commit:
```bash
git commit --amend                # Change message/files
git push --force                  # ⚠️ Only if not pushed yet!
```

### 4. Revert a Published Commit:
```bash
git revert abcd1234               # Creates undo commit
git push
```

---

## Part 6: Essential Tools & Tips

### 1. Status & History:
```bash
git status                        # Changed/untracked files
git log --oneline --graph         # Compact commit history
```

### 2. Remote Management:
```bash
git remote -v                     # List remotes
git remote set-url origin https://<NEW_URL>  # Change remote URL
```

### 3. .gitignore
Create `.gitignore` file to exclude:
- Node modules (`node_modules/`)  
- Environment files (`.env`)  
- Build artifacts (`dist/`, `.build/`)  

### 4. Tags (Releases):
```bash
git tag v1.0.0                    # Create tag
git push origin v1.0.0            # Push tag
```

---

## Workflow Cheat Sheet

| Action                      | Command                          |
|-----------------------------|----------------------------------|
| Commit all changes          | `git add . && git commit -m "msg"` |
| Push new branch             | `git push -u origin branch-name` |
| Pull latest changes         | `git pull --rebase`             |
| Compare changes             | `git diff HEAD^`                |
| Clean untracked files       | `git clean -fd`                 |

---

## Troubleshooting

**"Your branch is ahead of 'origin/main'"**  
```bash
git push  # You have unpushed commits
```

**"Updates were rejected"**  
```bash
git pull --rebase  # Fetch and rebase first
```

**Accidental commit to wrong branch**  
```bash
git reset HEAD~1              # Undo commit
git stash                     # Save changes
git checkout correct-branch
git stash pop
```

**Recover deleted branch**  
```bash
git reflog                    # Find lost commit hash
git checkout -b branch-name <hash>
```
