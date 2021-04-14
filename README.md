# git-cheatsheet
A list of useful git commands

To add all changes to staging
===============================
```bash
$ git add .
```

To make a branch
================
```bash
$ git branch foo
$ git checkout foo
```

To make a branch in one step
============================
```bash
$ git checkout -b foo
```

To delete a branch
==================
```bash
$ git branch -D my-branch
```

To list all branches
====================
```bash
$ git branch -av
```

To add a new commit that undoes the given commit
================================================
(and does not delete history)
```bash
$ git revert <sha>
```

To go back to an old commit and destroy all future commits (dangerous)
======================================================================
```bash
$ git reset <sha> --hard
```

To merge a branch into master
=============================
```bash
$ git checkout master
$ git merge my-branch1
$ git merge my-branch2
```
Now resolve conflicts and then:
```bash
$ git add .
$ git commit
```

Pushing to a remote repo
========================
```bash
$ git push git@github.com:goblinhack/zorbash.git <which-branch>
```

To avoid typing "git push <destination> <which-branch>" always, do:
===================================================================
```bash
$ git remote add origin git@github.com:goblinhack/zorbash.git
```
so we can now do
```bash
$ git push origin master
$ git pull origin master
```

To see where we are pushing and pulling currently to
====================================================
```bash
$ git remote -v
"origin  git@github.com:goblinhack/zorbash.git (fetch)"
"origin  git@github.com:goblinhack/zorbash.git (push)"
```

To push a branch to the remote
==============================
```bash
$ git checkout master
$ git pull origin master
$ git checkout -b my-branch1
```
Now add some files and stuff
```bash
$ git commit -m "..."
$ git push origin my-branch1 # you can repeat this add/push
```
Then do a pull request

An alternative to merging is rebase
===================================
This replays all commits onto the master and so avoids messy branch history
```bash
$ git checkout master
$ git pull origin master
$ git rebase my-branch
```

To change a commit message (pre push)
=====================================
```bash
$ git commit --ammend -m "my-branch"
```

To add files to an existing commit (pre push)
=============================================
```bash
$ git add .
$ git commit --ammend -m "my-branch"
```

Move accidental changes from master to a branch
===============================================
```bash
$ git log # to get SHAs
$ git checkout -b feature-branch
$ git cherry-pick <SHA>
$ git master
$ git reset --soft <SHA> # resets, but leaves  changes in staging
$ git reset        <SHA> # resets, but leaves  changes in working area
$ git reset --hard <SHA> # resets, and removes changes in staging
                       # also removes tracked but leaves untracked files
$ git clean -df          # gets rid of untracked files (handy to remove
                       $ an accidental untar/zip in a git repo)
```

To see all changes since checking out/cloning
=============================================
The ‘reflog’ command keeps a track of all changes made in a repository.
```bash
$ git reflog
```

To undelete a branch
====================
```bash
$ git checkout -b test-branch
$ git checkout master
$ git branch -D test-branch
$ git reflog
542359ca (HEAD -> master, origin/master, origin/HEAD) HEAD@{1}: checkout: moving from master to test-branch
$ git checkout -b test-branch HEAD@{1}
```

See just the last commit
========================
```bash
$ git log -1 HEAD
```

A variety of single line output git logs
========================================
```bash
$ git log --oneline
$ git log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all
```

Get logs after a certain date
=============================
```bash
$ git log --after="apr 1" --oneline --decorate
$ git log --after="apr 1" --before="yesterday" --oneline --decorate
```

Get logs for a certain user
===========================
```bash
$ git log --committer="My name" --oneline
```

Get only n logs
===============
```bash
$ git log -n 3
```

View just the last commit diffs
===============================
```bash
$ git log -n1 -p --format=fuller
```

View all commits diffs
======================
```bash
$ git log -p --format=fuller
```

Recursive submodule diff
========================
```bash
$ git diff -a --submodule=diff origin
```

Look at git commit object SHAS
==============================
```bash
$ find .git | grep obj | tail -1
.git/objects/13/2fc0aa1789ce26a97b1bed0a9eefa58b12a96e
$ git cat-file -p 132fc0aa1789ce26a97b1bed0a9eefa58b12a96e
```

Calculate a git hash
====================
```bash
$ echo hello | git hash-object --stdin
```

Get the common ancestor of two branches
=======================================
```bash
$ git merge-base NPSUITE-2094-test-hang maste
```
