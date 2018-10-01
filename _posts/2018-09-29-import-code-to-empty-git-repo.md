---
layout: post
title: import code to empty git repo
date: 2018-09-29 21:12 +0800
categories: [shell]
tags: [shell, git]
---

I am planning to make android pie runnning on our latest proudct, Continuous Integration
team has initialized all the git project, inside citrix, but there is no code in them, I
synced android source code from local repo and copied to the Ubuntu in citrix, then I need
to add the source code and do git commit, the follow script help me to do the job:

``` shell
dirs=`find . -name .git`

for tmp in ${dirs}
do
	dir=${tmp%.git}
	cd $dir

	# If there are two commits in git repo, just skip to the next
	# already committed, ignore
	n=`git rev-list --all --count`
	if [ $n -eq 2 ]; then
		cd -
		continue
	fi

	# nothing to commit
	n=`git ls-files --others --exclude-standard|wc -l`
	if [ $n -eq 0 ]; then
		cd -
		continue
	fi

	# do commit
	find . -type f |xargs git add -f
	git commit -asm "import source code from google"
	git push origin HEAD:refs/heads/branch_name
	cd -
done
```
