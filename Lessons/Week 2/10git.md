# 01/28/21: Git

- **git init**
    - creates empty repo in current directory
    - no commits or files tracked
- **git clone {url}**
    - downloads external repo from github and sets it up as local repo in current directory
- **git status**
    - shows the status of the files in current directory 
- **git add {file/directory}**
    - marks files to be committed 
    - doesn't mean an automatically commit 
    - "git add ." to add all files
    - "git add -u" to add files that you changes 
- **git commit -m "my message"**
    - commits added files to repo
    - attaches name/email when you commit 
    - "git commit -am "commit all changed" (adds all files and commits in one command)
- **git push**
    - uploads new commits to origin (github)

## Branches
- diverge the linear history of git version control by splitting into branches
- **checking out** is the process of creating a new branch and diverging from initial branch
    - changes can be made in this branch 
    - if all goes well, these can be merged if no conflicts! 
- **merge conflicts** need to be resolved when same code is modified 

### Git Commands
- **git checkout**
    - "checks out" new branch
    - also used to create new branches
    - Usage: git checkout "existing-branch"
    - Usage: git checkout -b "add-new-branch"
    - all commits on this branch remain on this branch, and do not affect main! 
- **git merge**
    - without conflict
    - "merges" branch into current branch
    - Usage: git merge "other-branch" 
- **git merge** with merge conflicts
    - in vscode, you can either select choices or physically go in the code and delete the conflict parts 
- **pull requests**
    - used in bigger companies/repos
    - allows people to review code before merging
    - you can add labels, assign people, etc. to organize pull requests! 
    - done on the github website