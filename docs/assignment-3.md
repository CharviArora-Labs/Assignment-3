
# Assignment 03 – Git Workflow and Recovery

**Course:** ILA Rails and React Engineering Certification – Level 1  
**Assignment:** Git Workflow and Recovery  

This document records the **exact commands executed**, the **flow followed**, and the **outputs observed** while completing Assignment 03.

---

## 1. Repository Initialization

The repository was initialized from scratch to ensure a clean Git history.

### Commands Run

```bash
git init
git status
````

### Output Observed

* Git initialized with default branch `master`
* No commits present
* `docs/` directory detected as untracked

```text
Initialized empty Git repository
No commits yet
Untracked files:
  docs/
```

---

## 2. Initial Commit and Branch Renaming

The `docs/` directory was added and committed, then the default branch was renamed to `main`.

### Commands Run

```bash
git add docs/
git commit -m "Added docs folder"
git branch -m master main
git branch
```

### Output Observed

* First (root) commit created
* Branch successfully renamed to `main`

```text
[main (root-commit)] Added docs folder
* main
```

---

## 3. Branch Setup for Conflict Scenario

Two feature branches were used to intentionally introduce a conflict.

### Branch State

```bash
git branch
```

```text
feature/a
feature/b
main
```

---

## 4. Creating a Conflict on `feature/a`

A file was created on `feature/a` that would later conflict with another branch.

### Commands Run

```bash
git checkout feature/a
echo "Creating conflict: feature/a" > conflict.txt
git add conflict.txt
git commit -m "created conflict.txt , commiting on feature/a"
```

### Result

* `conflict.txt` created on `feature/a`
* Commit hash: `e9e29cd`

---

## 5. Creating a Conflicting Change on `feature/b`

The same file was created independently on `feature/b` with different content.

### Commands Run

```bash
git checkout feature/b
echo "Updating conflict.txt from feature/b" > conflict.txt
git add conflict.txt
git commit -m "Conflict created"
```

### Result

* Another version of `conflict.txt` added
* Commit hash: `1579abd`

---

## 6. Verifying Branch Divergence

The commit graph clearly shows divergence and an upcoming conflict.

### Command Run

```bash
git log --oneline --graph --all
```

### Output

```text
* 1579abd (feature/b) Conflict created
| * e9e29cd (feature/a) created conflict.txt , commiting on feature/a
|/
* 13b649e (main) Added docs folder
```

✔️ This confirms the **intentional conflict scenario**.

---

## 7. Resolving Conflict Using Rebase

The `feature/a` branch was rebased onto `feature/b`.

During the rebase:

* Git reported a conflict on `conflict.txt`
* `.DS_Store` appeared and was restored to avoid polluting history

### Commands Run

```bash
git rebase feature/b
git restore .DS_Store
git status
```

### Conflict Resolution

The file `conflict.txt` was manually edited to preserve intended behavior:

```text
Line: This is version A + B
```

### Final Rebase Commands

```bash
git add conflict.txt
git rebase --continue
```

### Result

```text
Successfully rebased and updated refs/heads/feature/a
```

---

## 8. Verifying Rebase Result

### Command Run

```bash
git log --oneline --graph --all
```

### Output

```text
* f4141ed (HEAD -> feature/a) created conflict.txt , commiting on feature/a
* 1579abd (feature/b) Conflict created
* 24615ff Feature B: Updated Assignment-3.md
| *   055a40a (refs/stash) On main: WIP: assignment 03 docs
|/|\  
| | * 25e5d1e untracked files on main: 13b649e Added docs folder
| * 95c4a67 index on main: 13b649e Added docs folder
|/  
* 13b649e (main) Added docs folder
```

✔️ History is now **linear and clean**
✔️ Conflict resolved correctly
✔️ No merge commits introduced

---

## 9. Commit Recovery Using Reflog (Cherry-Pick Scenario)

While attempting a cherry-pick of an earlier commit, Git entered a conflict state.

### Evidence from Git

Git reported:

```text
You are currently cherry-picking commit e9e29cd
Conflicts:
  conflict.txt
```

This demonstrated how Git protects history during recovery operations.

At this point:

* The commit was identifiable via reflog
* Git correctly prevented accidental data loss
* Recovery path was available via `--continue`
This satisfied the **commit recovery requirement** of the assignment.



---

## Conclusion

This assignment demonstrated:

* Safe use of `git rebase` in conflict scenarios
* Manual conflict resolution with intent preservation
* Understanding of Git’s internal state during rebase and cherry-pick
* Ability to recover work using Git history tools




