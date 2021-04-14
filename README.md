# git-cheatsheet
A list of useful git commands

To add all changes to staging
===============================
```bash
git add .
```

To make a branch
================
```bash
git branch foo
git checkout foo
```

To make a branch in one step
============================
```bash
git checkout -b foo
```

To delete a branch
==================
```bash
git branch -D my-branch
```

To list all branches
====================
```bash
git branch -a
```

To add a new commit that undoes the given commit
================================================
```bash
git revert <sha>
```

To go back to an old commit and destroy all future commits (dangerous)
======================================================================
```bash
git reset <sha> --hard
```

To merge a branch into master
=============================
```bash
git checkout master
git merge my-branch1
git merge my-branch2
```
Now resolve conflicts and then:
```bash
git add .
git commit
```

Pushing to a remote repo
========================
```bash
git push git@github.com:goblinhack/zorbash.git <which-branch>
```

To avoid typing "git push <destination> <which-branch>" always, do:
===================================================================
```bash
git remote add origin git@github.com:goblinhack/zorbash.git
```
so we can now do
```bash
git push origin master
git pull origin master
```

To see where we are pushing and pulling currently to
====================================================
```bash
git remote -v                                                                                                  (1) (*master+2093) 14:00:29
"origin  git@github.com:goblinhack/zorbash.git (fetch)"
"origin  git@github.com:goblinhack/zorbash.git (push)"
```

To push a branch to the remote
==============================
```bash
git checkout master
git pull origin master
git checkout -b my-branch1
do stuff
```
```bash
git commit -m "..."
git push origin my-branch1 # you can repeat this add/push
```
Then do a pull request

An alternative to merging is rebase
===================================
This replays all commits onto the master and so avoids messy branch history
```bash
git checkout master
git pull origin master
git rebase mfo
```

To change a commit message (pre push)
=====================================
```bash
git commit --ammend -m "my-branch"
```

To add files to an existing commit (pre push)
=============================================
```bash
git add .
git commit --ammend -m "my-branch"
```

Move accidental changes from master to a branch
===============================================
```bash
git log # to get SHAs
git checkout -b feature-branch
git cherry-pick <SHA>
git master
git reset --soft <SHA> # resets, but leaves  changes in staging
git reset        <SHA> # resets, but leaves  changes in working area
git reset --hard <SHA> # resets, and removes changes in staging
                       # also removes tracked but leaves untracked files
git clean -df          # gets rid of untracked files (handy to remove
                       $ an accidental untar/zip in a git repo)
```

See just the commits since last clone
=====================================
```bash
git reflog
```
