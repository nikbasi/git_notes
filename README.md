# How to Get All Updates from a GitHub Project

## **1. Get All Updates and DISCARD Local Changes**  
If you want to fetch the latest updates and **discard** all local changes:

```bash
git fetch --all
git reset --hard origin/main  # Replace 'main' with the branch you're using
git pull origin main
```
This will:

fetch --all: Get the latest updates from the remote repository.

reset --hard origin/main: Reset your local branch to match the remote branch, discarding all local changes.

pull origin main: Ensure everything is up to date.

⚠️ Warning: This cannot be undone, so make sure you want to lose all local changes before running it.

## 2. Get Updates and KEEP Local Changes
If you have local changes and want to keep them while updating to the latest version, use:

```bash
git stash  # Save your local changes temporarily
git pull origin main  # Pull the latest changes
git stash pop  # Reapply your local changes
```
This will:

stash: Temporarily save your local changes.

pull: Get the latest changes from GitHub.

stash pop: Reapply your local changes.

## 3. Get Updates and MERGE Local Changes (Auto-Resolve Conflicts If Possible)
```bash
git pull --rebase origin main
```
This will try to rebase your changes on top of the latest commits, keeping both the new updates and your modifications.

If there are conflicts, Git will ask you to resolve them manually.

## 4. Get Updates and Commit Local Changes Before Pulling
If you don't want to stash but also don't want to lose your changes, commit them first:

```bash
git add .
git commit -m "Saving my changes before pulling"
git pull origin main
```
This way, your changes are saved, and Git will attempt to merge the new updates.

## Which One Should You Use?
If you want a clean reset and don't care about local changes: Use Method 1 (reset --hard).

If you want to update without losing your changes: Use Method 2 (stash).

If you want to merge new updates smoothly: Use Method 3 (rebase).

If you want to be extra safe before updating: Use Method 4 (commit first).
