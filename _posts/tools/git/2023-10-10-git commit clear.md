---
categories: [Tools, Git]
tag: [tool, git]
---
# 2023-10-10-git commit clear
```git
git checkout --orphan new_branch     // --orphan create independent branch
git add -A    // add changed files
git commit -m  "" 
git branch -D master // delete old branch
git branch -m master  // rename current branch
git push -f remote_machine local_branch 
```