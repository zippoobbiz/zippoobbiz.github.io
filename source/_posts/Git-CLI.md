---
title: Git CLI
date: 2017-02-15 20:53:41
tags: [Version Control, Git]
categories: [Tools, Version Control]
---

# Commands Sequence
{% qnimg git_cycle.png %}

# Git Basics
|name|Description|
|----------|:---------|
|master|default development branch|
|origin|default upstream repository|
|HEAD|current branch|
|HEAD^|parent of HEAD|
|HEAD~4|the great-great grandparent of HEAD|


# Create
From existing data
```
cd ~/projects/myproject
git init
git add .
```

From existing repo
```
git clone ~/existing/repo ~/new/repo
git clone git://host.org/project.git
git clone ssh://you@host.org/proj.git
```

# Show
|Description|Command|
|----------|:---------|
|Files changed in working directory|git status|
|Changes to tracked files|git diff|
|What changed between $ID1 and $ID2|git diff $id1 $id2|
|History of changes|git log|
|History of changes for file with diffs|git log -p $file $dir/ec/tory/|
|Who changed what and when in a file|git blame $file|
|A commit identified by $ID|git show $id|
|A specific file from a specific $ID|git show $id:$file|
|All local branches|git branch|

# Revert
|Description|Command|
|----------|:---------|
|Return to the last committed state|git reset --hard|
|Revert the last commit|git revert HEAD|
|Revert specific commit|git revert $id|
|Fix the last commit|git commit -a --amend|
|Checkout the $id version of a file|git checkout $id $file|

# Branch
|Description|Command|
|----------|:---------|
|Switch to the $id branch|git checkout $id|
|Merge branch1 into branch2|git checkout $branch2<br>git merge $branch1|
|Create branch named $branch bansed on<br>the HEAD|git branch $branch|
|Create branch $new_branch based on branch<br>$other and switch to it|git checkout -b $new_branch $other|
|Delete branch $branch|git branch -d $branch|

# Update
|Description|Command|
|----------|:---------|
|Fetch latest changes from origin<br>(but this does not merge them).|git fetch|
|Pull latest changes from origin<br>(does a fetch followed by a merge)|git pull|
|Apply a patch that some sent you|git am -3 patch.mbox|

# Push
|Commit all your local changes|git commit -a|
|Prepare a patch for other developers|git format-patch origin|
|Push changes to origin|git push|
|Mark a version / milestone|git tag v1.0|

# Useful Commands
To view the merge conclicts
```
git diff
git diff --base $file
git diff --ours $file
git diff --theirs $file
```
To discard conflicting patch
```
git reset --hard
git rebase --skip
```
After resolving conflicts, merge with
```
git add $conflicting_file
git rebase --continue
```
Finding regressions
```
git bisect start
git bisect good $id
git bisect bad $id
git bisect bad/good
git bisect visualize
git bisect reset
```

Check for errors and cleanup repository
```
git fsck
git gc --prune
```

Search working directory for foo()
```
git grep "foo()"
```



