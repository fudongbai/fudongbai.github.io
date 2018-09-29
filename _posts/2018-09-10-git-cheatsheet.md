---
layout: post
title: git cheatsheet
date: 2018-09-10 20:05 +0800
categories: [Miscelaneous]
tags: [git, cheatsheet]
---

```
# Create a tag
git tag -a v1.0 -m "milestone: v1"
git push --tags

# Discard all changes
git reset --hard HEAD
git reset --hard HEAD^
git reset --hard HEAD^

git checkout -- <file or directory>

# checkout git repo with submodules
git clone --recursive https://github.com/android-rooting-tools/android_run_root_shell

# Used for ssh debugging
ssh -vT fudongbai@github.com

git rebase origin/name-of-upstream-branch

# Generate patches
git format-patch -6 --cover-letter

git send-email --to fudongbai@gmail.com --cc fudong@mail.com

# push to gerrit
git push origin HEAD:refs/for/master
# push straight to the master branch
git push origin HEAD:refs/heads/master
```
