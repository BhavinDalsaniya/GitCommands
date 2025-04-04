# Git Commands

## Staging and Committing

- When you run `git add .`, it adds all changes (new, modified, deleted files) to the **staging area**.
- After that, using `git commit -m "message"` commits the staged changes — this is called making a **commit**.

## Working with Branches

- If you **create a new branch** and then create a file without adding it to git:
  - The file will be visible when you run `ls`.
  - It will appear in both the **master** and the **new branch** (since it’s still untracked by git).

- However, once you **add** the file using `git add`, it moves to the **staging area**.
  - While in the staging area, the file is prepared for commit but not yet part of any branch.
  - It won't be committed to a specific branch until you use `git commit`.

## Summary

| Action            | Effect                                      |
|-------------------|----------------------------------------------|
| `git add .`       | Moves changes to staging area                |
| `git commit`      | Commits staged changes to the current branch |
| Untracked File    | Visible in both branches via `ls`            |
| Staged File       | Not visible in any branch until committed    |





# Git Scenario: Staging in One Branch, Committing in Another

## Scenario Overview
In this scenario, we create multiple branches, add a file in one branch but commit it in another, and analyze the impact on each branch.

## Steps and Commands

## 1. Create Multiple Branches
git branch branch1  
git branch branch2  
git branch branch3  

## 2. Switch to branch1 and Create a File
git checkout branch1  
touch myfile.txt  
echo "Hello Git" > myfile.txt  

## 3. Add the File to Staging (Without Committing)
git add myfile.txt  

## 4. Switch to branch2 Without Committing
git checkout branch2  

## 5. Commit the File in branch2
git commit -m "Added myfile.txt"  

## Expected Outcome
Branch1: No myfile.txt, No commit of myfile.txt, Unaffected  
Branch2: myfile.txt exists, Contains "Added myfile.txt" commit, Updated  
Branch3: No myfile.txt, No commit of myfile.txt, Unaffected  

## Branch-wise Breakdown

## Branch 1 (branch1)
myfile.txt is not committed here.  
Running git log will not show the commit.  
git status shows no changes.  

## Branch 2 (branch2)
The file myfile.txt is committed in this branch.  
git log --oneline --graph --all will show:  
* abc123 (HEAD -> branch2) Added myfile.txt  
* def456 Previous commit  

Running ls confirms the file exists.  

## Branch 3 (branch3)
myfile.txt does not exist here.  
git log shows no changes.  

## What Happens If You Switch Back to branch1?
git checkout branch1  

myfile.txt will not be there because it was never committed in branch1.  
If you want to bring the commit to branch1, you need to merge:  

git merge branch2  

## Final Git Log Structure
git log --oneline --graph --all  
* abc123 (HEAD -> branch2) Added myfile.txt  
| * (branch1) No commit of myfile.txt here  
| * (branch3) No changes here  
* def456 Previous commit  

## Key Takeaways
Commits are branch-specific – a commit in branch2 does not affect branch1 or branch3.  
Staged changes persist across branches – if you git add in branch1 and switch to branch2, you can commit there.  
Untracked files remain in the working directory – they don't disappear when switching branches.  

## Best Practice
Always commit or stash your changes before switching branches to avoid unexpected behavior:  
git stash  
git checkout branch2  
git stash pop  

## Additional Notes on Git

## 1. What Happens When You Run git add .?
This moves files to the staging area.  
The files are not yet committed, but they are ready for a commit.  

## 2. Is a Git Commit Branch-Specific?
Yes! A commit belongs to the branch where it was created.  
Commits do not automatically appear in other branches unless merged.  

## 3. What Happens if You Create a File in One Branch and Switch?
If the file is not staged (git add), it stays in the working directory.  
If the file is staged (git add), but not committed, it remains staged across branches.  
If the file is committed (git commit), it belongs only to that branch.  

## End of README
