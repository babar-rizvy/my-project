# Git Lab Assignment — Git & GitHub

This repository contains the work completed for the Git Lab Assignment. The assignment demonstrates practical Git and GitHub operations including feature branch development, multi-level merging, stashing changes, merge conflict resolution, restoring files, and undoing commits using Git reset.

## Repository

**GitHub Repository:** `babar-rizvy/my-project`

---

# Table of Contents

1. [Task 1 — Feature Branch Development and Multi-Level Merging](#task-1--feature-branch-development-and-multi-level-merging)
2. [Task 2 — Stash Changes and Work on Another Feature](#task-2--stash-changes-and-work-on-another-feature)
3. [Task 3 — Create and Resolve a Merge Conflict](#task-3--create-and-resolve-a-merge-conflict)
4. [Task 4 — Restore Uncommitted File Changes](#task-4--restore-uncommitted-file-changes)
5. [Task 5 — Undo Commits Using Git Reset](#task-5--undo-commits-using-git-reset)
6. [Final Repository Status](#final-repository-status)

---

# Task 1 — Feature Branch Development and Multi-Level Merging

## Objective

The objective of this task was to practice feature branch development and multi-level merging. A `dev` branch was created from `main`, followed by three feature branches. Each feature branch contained a separate change, which was committed and pushed to GitHub. The three feature branches were then merged into `dev`, and finally `dev` was merged into `main`.

## Branches Used

* `main`
* `dev`
* `feature-login`
* `feature-profile`
* `feature-dashboard`

## Step 1: Create `dev` from `main`

```bash
git checkout main
git pull origin main
git checkout -b dev
git push -u origin dev
```

The `dev` branch was created from the latest version of `main` and pushed to the remote repository.

## Step 2: Create `feature-login`

```bash
git checkout dev
git checkout -b feature-login
```

A login feature file was created:

```bash
echo "Login feature implemented" > login.txt
cat login.txt
```

The file was staged and committed:

```bash
git add login.txt
git commit -m "Add login feature"
```

The feature branch was pushed:

```bash
git push -u origin feature-login
```

### Result

`login.txt` was added with the login feature information.

---

## Step 3: Create `feature-profile`

```bash
git checkout dev
git checkout -b feature-profile
```

A profile feature file was created:

```bash
echo "Profile feature implemented" > profile.txt
cat profile.txt
```

The changes were staged and committed:

```bash
git add profile.txt
git commit -m "Add profile feature"
```

The branch was pushed:

```bash
git push -u origin feature-profile
```

### Result

`profile.txt` was added with the profile feature information.

---

## Step 4: Create `feature-dashboard`

```bash
git checkout dev
git checkout -b feature-dashboard
```

A dashboard feature file was created:

```bash
echo "Dashboard feature implemented" > dashboard.txt
cat dashboard.txt
```

The changes were staged and committed:

```bash
git add dashboard.txt
git commit -m "Add dashboard feature"
```

The branch was pushed:

```bash
git push -u origin feature-dashboard
```

### Result

`dashboard.txt` was added with the dashboard feature information.

---

## Step 5: Merge Feature Branches into `dev`

First, the `dev` branch was selected:

```bash
git checkout dev
```

The feature branches were merged:

```bash
git merge feature-login
git merge feature-profile
git merge feature-dashboard
```

The merge result was checked:

```bash
git status
```

The updated `dev` branch was pushed:

```bash
git push origin dev
```

## Step 6: Merge `dev` into `main`

```bash
git checkout main
git merge dev
git push origin main
```

### Task 1 Result

All three feature branches were successfully developed, committed, pushed, and merged into `dev`. The completed `dev` branch was then merged into `main`.

### Branch Structure

```text
main
 │
 └── dev
      ├── feature-login
      ├── feature-profile
      └── feature-dashboard
```

---

# Task 2 — Stash Changes and Work on Another Feature

## Objective

The objective of this task was to temporarily save uncommitted work using Git Stash, switch to another feature branch, complete another task, and then restore the previously saved work.

## Step 1: Create an Uncommitted Change

The `feature-search` branch was used:

```bash
git checkout feature-search
```

A new file was created:

```bash
echo "Search feature - work in progress" > search.txt
```

The current status was checked:

```bash
git status
```

The file appeared as an untracked file.

## Step 2: Stash the Changes

Because the file was untracked, the `-u` option was used:

```bash
git stash push -u -m "WIP search feature"
```

The working directory was then checked:

```bash
git status
```

## Step 3: Work on Another Feature

The `feature-notification` branch was selected:

```bash
git checkout feature-notification
```

A notification feature was created:

```bash
echo "Notification feature completed" > notification.txt
```

The file was staged and committed:

```bash
git add notification.txt
git commit -m "Add notification feature"
```

## Step 4: Return and Restore the Stashed Work

The original feature branch was selected:

```bash
git checkout feature-search
```

The stashed changes were restored:

```bash
git stash pop
```

The restored file was verified:

```bash
cat search.txt
```

Expected content:

```text
Search feature - work in progress
```

## Git Stash Explanation

`git stash` temporarily stores uncommitted changes so that the working directory can be cleaned and another task can be performed.

The `-u` option was used because `search.txt` was an untracked file.

```bash
git stash push -u -m "WIP search feature"
```

The changes were later restored using:

```bash
git stash pop
```

### Task 2 Result

The search feature work was successfully stashed, another feature was completed and committed, and the original search feature work was restored.

---

# Task 3 — Create and Resolve a Merge Conflict

## Objective

The objective of this task was to create a merge conflict by modifying the same file differently in two feature branches and then resolve the conflict manually.

## Branches Used

* `dev`
* `feature-conflict-a`
* `feature-conflict-b`

## Step 1: Create Feature Branch A

```bash
git checkout dev
git checkout -b feature-conflict-a
```

The conflict file was created/modified:

```bash
echo "Change from Developer A" > conflict.txt
```

The changes were committed:

```bash
git add conflict.txt
git commit -m "Update conflict file from Developer A"
```

## Step 2: Create Feature Branch B

The `dev` branch was selected:

```bash
git checkout dev
```

Then the second feature branch was created:

```bash
git checkout -b feature-conflict-b
```

The same file was modified differently:

```bash
echo "Change from Developer B" > conflict.txt
```

The changes were committed:

```bash
git add conflict.txt
git commit -m "Update conflict file from Developer B"
```

## Step 3: Merge Feature Branch A

```bash
git checkout dev
git merge feature-conflict-a
```

Feature branch A was successfully merged into `dev`.

## Step 4: Merge Feature Branch B

```bash
git merge feature-conflict-b
```

Git detected a merge conflict because both branches had modified the same file differently.

## Step 5: Resolve the Conflict

The conflicted file was opened in Visual Studio Code.

The conflict was manually resolved by keeping both changes:

```text
Change from Developer A
Change from Developer B
```

After resolving the conflict, the file was staged:

```bash
git add conflict.txt
```

The resolved changes were committed:

```bash
git commit -m "Resolve merge conflict"
```

The result was verified:

```bash
cat conflict.txt
git status
```

The updated `dev` branch was pushed:

```bash
git push origin dev
```

## Merge Conflict Explanation

A merge conflict occurs when Git cannot automatically combine changes from different branches. This commonly happens when different branches modify the same part of the same file.

In this task, `feature-conflict-a` and `feature-conflict-b` made different changes to `conflict.txt`. Git therefore required manual resolution.

### Task 3 Result

The merge conflict was successfully created, manually resolved using Visual Studio Code, committed, and pushed to the remote `dev` branch.

---

# Task 4 — Restore Uncommitted File Changes

## Objective

The objective of this task was to demonstrate how to inspect and discard unwanted uncommitted changes using `git diff` and `git restore`.

## Step 1: Check Repository Status

```bash
git status
```

## Step 2: Create an Unwanted Modification

An unwanted change was added to the existing tracked file:

```bash
echo "Unwanted modification" >> conflict.txt
```

## Step 3: View the Difference

```bash
git diff
```

The command displayed the newly added unwanted modification.

## Step 4: Restore the Original File

The unwanted modification was discarded using:

```bash
git restore conflict.txt
```

## Step 5: Verify

```bash
git diff
cat conflict.txt
git status
```

After restoration, the unwanted modification was removed.

## Git Restore Explanation

`git restore` is used to restore files to their previous state and discard uncommitted working-directory changes.

For example:

```bash
git restore conflict.txt
```

restores `conflict.txt` and removes its uncommitted modification.

### Task 4 Result

The unwanted modification was successfully identified using `git diff` and removed using `git restore`.

---

# Task 5 — Undo Commits Using Git Reset

## Objective

The objective of this task was to demonstrate how Git commits can be undone using both soft reset and hard reset.

## Files Used

* `reset-test.txt`
* `reset-test-2.txt`

## Step 1: Create and Commit the First Change

```bash
echo "First reset test" > reset-test.txt
git add reset-test.txt
git commit -m "Add first reset test"
```

The first commit created was:

```text
ac44c5a Add first reset test
```

## Step 2: Create and Commit the Second Change

```bash
echo "Second reset test" > reset-test-2.txt
git add reset-test-2.txt
git commit -m "Add second reset test"
```

The commit history was checked:

```bash
git log --oneline -4
```

The latest commit was:

```text
fbbf0fd Add second reset test
```

## Step 3: Perform a Soft Reset

The latest commit was removed from the commit history while keeping its changes staged:

```bash
git reset --soft HEAD~1
```

The result was checked:

```bash
git status
git log --oneline -4
```

The second commit was removed from the history, but the changes from `reset-test-2.txt` remained staged.

## Step 4: Recommit the Changes

The staged changes were committed again:

```bash
git commit -m "Recommit second reset test"
```

The history was checked:

```bash
git log --oneline -4
```

## Step 5: Perform a Hard Reset

The latest commit was removed together with its associated working-directory changes:

```bash
git reset --hard HEAD~1
```

The final state was checked:

```bash
git status
git log --oneline -5
ls
```

The final directory listing showed:

```text
conflict.txt
dashboard.txt
login.txt
profile.txt
README.md
reset-test.txt
search.txt
```

The file `reset-test-2.txt` was no longer present.

## Git Reset Explanation

`git reset` moves the current branch pointer to another commit.

### Soft Reset

```bash
git reset --soft HEAD~1
```

A soft reset removes the selected commit from the branch history but keeps the changes staged.

### Hard Reset

```bash
git reset --hard HEAD~1
```

A hard reset removes the selected commit and also removes the associated changes from the working directory.

### Task 5 Result

Both soft reset and hard reset were successfully demonstrated. The soft reset preserved the changes for recommitting, while the hard reset removed the latest commit and its associated file.

---

# Final Repository Status

The final repository contains the main project files and files created during the Git lab tasks.

```text
conflict.txt
dashboard.txt
login.txt
profile.txt
README.md
reset-test.txt
search.txt
```

The `search.txt` file remains untracked intentionally because it was used to demonstrate Git Stash in Task 2.

It should **not** be added with `git add .` unless specifically required by the assignment.

---

# Important Git Commands Summary

| Command                          | Purpose                                            |
| -------------------------------- | -------------------------------------------------- |
| `git status`                     | Check repository and working-tree status           |
| `git branch`                     | View branches                                      |
| `git checkout <branch>`          | Switch branches                                    |
| `git checkout -b <branch>`       | Create and switch to a new branch                  |
| `git add <file>`                 | Stage a file                                       |
| `git commit -m "message"`        | Create a commit                                    |
| `git push origin <branch>`       | Push a branch to GitHub                            |
| `git pull origin <branch>`       | Download and integrate remote changes              |
| `git merge <branch>`             | Merge another branch                               |
| `git stash push -u -m "message"` | Temporarily save uncommitted and untracked changes |
| `git stash pop`                  | Restore the latest stashed changes                 |
| `git diff`                       | View uncommitted changes                           |
| `git restore <file>`             | Discard uncommitted changes in a file              |
| `git log --oneline`              | View compact commit history                        |
| `git reset --soft HEAD~1`        | Undo latest commit while keeping changes staged    |
| `git reset --hard HEAD~1`        | Undo latest commit and remove associated changes   |
| `git ls`                         | List files in the current directory                |

---

# Conclusion

This Git Lab Assignment provided practical experience with Git and GitHub. The completed tasks covered feature branch development, branch-based collaboration, multi-level merging, Git Stash, merge conflict resolution, restoring uncommitted changes, and undoing commits using soft and hard reset.

The assignment demonstrates the basic workflow of managing changes safely and maintaining project history using Git and GitHub.
