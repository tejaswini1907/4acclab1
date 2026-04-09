# Git Troubleshooting Guide

This guide provides solutions to common errors you might encounter while using Git.

## 1. Authentication Failed (`fatal: Authentication failed for...`)

**Error:**
When running `git push` or `git clone`, you receive an authentication failed error.

**Troubleshooting Steps:**
- **Check Credentials:** Ensure you are using the correct username and password/Personal Access Token (PAT).
- **Use a Personal Access Token:** GitHub no longer supports password authentication. You must generate a PAT from your GitHub Developer Settings and use that as your password.
- **Update Credential Manager:** Clear your cached credentials using your OS's credential manager (e.g., Windows Credential Manager, macOS Keychain) and try again.

## 2. Refusing to Merge Unrelated Histories (`fatal: refusing to merge unrelated histories`)

**Error:**
When pulling or merging, Git complains that the branches have unrelated histories. This usually happens when you try to pull a remote repo into a completely different local repo.

**Troubleshooting Steps:**
- **Force the Merge:** Run `git pull origin <branch-name> --allow-unrelated-histories` to force the merge. Be careful to resolve any conflicts that arise.

## 3. Merge Conflicts (`CONFLICT (content): Merge conflict in...`)

**Error:**
Git cannot automatically merge changes because the same part of a file was modified differently on two branches.

**Troubleshooting Steps:**
- **Identify Conflicting Files:** Run `git status` to see which files are in conflict.
- **Resolve Manually:** Open the files in your editor and look for conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`). Decide which changes to keep, edit the file, and remove the markers.
- **Add and Commit:** After resolving, run `git add <file>` and then `git commit` to finalize the merge.

## 4. Failed to Push Some Refs (`error: failed to push some refs to...`)

**Error:**
This occurs when the remote branch has commits that you do not have locally.

**Troubleshooting Steps:**
- **Fetch and Merge (Pull):** Run `git pull origin <branch-name>` to get the remote changes and merge them into your local branch.
- **Force Push (Use with Caution!):** If you are certain you want to overwrite the remote history, run `git push origin <branch-name> --force` or `-f`. Note: This is dangerous if others are working on the same branch.

## 5. Detached HEAD State (`You are in 'detached HEAD' state.`)

**Error:**
You checked out a specific commit or a tag instead of a branch. If you make commits here, they won't belong to any branch.

**Troubleshooting Steps:**
- **Create a New Branch:** If you want to keep changes made in this state, create a new branch: `git checkout -b <new-branch-name>`.
- **Return to a Branch:** If you don't want to keep changes, just switch back to an existing branch: `git checkout main` (or `master`).

## 6. Cannot Delete Branch (`error: branch 'X' not found` or `Cannot delete branch 'X' checked out at...`)

**Error:**
You are trying to delete a branch, but Git refuses.

**Troubleshooting Steps:**
- **Switch Branches:** You cannot delete the branch you are currently on. Checkout a different branch first: `git checkout main`.
- **Force Delete:** If the branch hasn't been fully merged and you still want to delete it, use a capital `-D`: `git branch -D <branch-name>`.

## 7. Discard Local Changes

**Error:**
You want to revert your local files to match the last commit, throwing away uncommitted changes.

**Troubleshooting Steps:**
- **Specific File:** `git checkout -- <file>` or `git restore <file>`
- **All Files:** `git reset --hard HEAD` (Warning: This permanently deletes uncommitted changes).
