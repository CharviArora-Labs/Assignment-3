# Assignment-3
Git Workflow Recovery

## Objective

The goal of this assignment was to **practice real-world Git recovery scenarios** by intentionally creating conflicts, resolving them correctly using rebase, and recovering lost commits while maintaining a clean and reviewable history.

---

## Prerequisites

Before starting this assignment, the following concepts were required:

- Basic Git branch management
- Understanding of merge conflicts
- Familiarity with Git history and commits
- Prior reading:
  - Pro Git Book
  - Git documentation on `git rebase`
  - Git documentation on `git reflog`

---

## What Was Done

### 1. Created Branch Divergence with Intentional Conflict

- Created multiple branches from a common base (`main` , `feature/a` and `feature/a`)
- Introduced conflicting changes to the same file on different branches
- This simulated a real collaboration scenario where parallel changes collide

---

### 2. Resolved Conflict Using Rebase

- Rebasing was performed to apply feature branch commits onto the base branch
- A conflict occurred during rebase due to the same file being added/modified
- The conflict was manually resolved by preserving the intended combined behavior
- The resolved file was staged and the rebase was continued successfully

This ensured:
- No unnecessary merge commits
- A linear and clean commit history

---

### 3. Recovered a Dropped Commit Using Reflog

- During history rewriting, a commit was intentionally dropped
- `git reflog` was used to identify the lost commit reference
- The commit was successfully recovered and reapplied
- Verified that the recovered changes were restored correctly

---

### 4. Verified and Documented Final History

- Final Git history was inspected to ensure:
  - Linear structure
  - No duplicated or dangling commits
- A commit graph screenshot was captured
- All commands and observations were documented in:
  - `docs/assignment-03.md`

---

## Deliverables Produced

- `docs/assignment-03.md` with:
  - Full command transcript
  - Conflict resolution steps
  - Reflog recovery process
- Screenshot of the final commit graph
- Short explanation of the branch strategy used

---
## Conclusion

This assignment reinforced disciplined Git workflows by simulating realistic failure and recovery situations.  
It provided hands-on confidence in handling rebases, resolving conflicts correctly, and recovering lost work—skills essential for professional software development.
