# 0415-git undo

To cancel a commit in Git, there are a few different ways depending on **what exactly you want to cancel** and whether the commit has been **pushed** or not.

***

#### 🔹 1. **Cancel the last commit (but keep the changes)**

If you just want to **undo the commit**, but keep the code changes:

```bash
git reset --soft HEAD~1
```

This moves `HEAD` one commit back, but **preserves the changes** in your working directory and staging area.

***

#### 🔹 2. **Cancel the last commit and discard the changes**

If you want to **undo the commit and also remove all changes** (i.e., make it like it never happened):

```bash
git reset --hard HEAD~1
```

> ⚠️ This is destructive—use with caution.

***

#### 🔹 3. **Cancel a commit that's already pushed (safe way)**

If the commit has already been pushed, you should **not use reset**, especially in shared branches. Instead, use a **revert**:

```bash
git revert <commit_hash>
```

This creates a new commit that undoes the changes made by the original one, which is **safe for public branches**.

***

#### 🔹 4. **Cancel a specific older commit**

To remove a specific commit (not the most recent), use **interactive rebase**:

```bash
git rebase -i HEAD~n
```

Where `n` is the number of commits you want to go back. Then, in the interactive menu, change `pick` to `drop` for the commit you want to remove.

***

Let me know your exact scenario (e.g., has it been pushed? do you want to keep the changes?), and I can recommend the safest way.
