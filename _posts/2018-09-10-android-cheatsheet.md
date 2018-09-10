---
layout: post
title: Android cheatsheet
date: 2018-09-10 20:15 +0800
categories: Android
---

## dumpsys

- [Get foreground activity name](https://stackoverflow.com/questions/13193592/adb-android-getting-the-name-of-the-current-activity) with dumpsys
``` shell
   dumpsys window windows |grep -E 'mCurrentFocus|mFocusedApp''
```

