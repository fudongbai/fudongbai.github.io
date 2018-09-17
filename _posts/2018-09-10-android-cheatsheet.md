---
layout: post
title: Android cheatsheet
date: 2018-09-10 20:15 +0800
categories: [Android]
tags: [Android, dumpsys]
---

## dumpsys

- [Get foreground activity name](https://stackoverflow.com/questions/13193592/adb-android-getting-the-name-of-the-current-activity) with dumpsys
``` shell
   dumpsys window windows |grep -E 'mCurrentFocus|mFocusedApp''
```

## capture screen on android
```shell
screencap "/data/android-`date +%F-%H%M%S`.png"
```
## send toast in C
```c
#define ANDROID_DATA “ANDROID_DATA=/data”
putenv (ANDROID_DATA)
system(“am broadcast -a com.example.DFU_COMPLETE - -ez dfu_complete true”);
```
Then when received the broadcast in the app, send a toast to the user.
