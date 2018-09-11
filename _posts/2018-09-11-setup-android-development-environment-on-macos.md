---
layout: post
title: Setup Android Development Environment on MacOS
date: 2018-09-11 22:19 +0800
categories: [Android]
tags: [macos, android]
---

## Install Java

``` shell
brew cask install java
```

You can use the following command to verify which version it will install.
```shell
brew cask info java
```

## Install Android SDK

Goto [Android Command Line Tools](https://developer.android.com/studio/),
Scroll down to the Command line tools only section:

[Download Android Command Line Tools for Mac](https://dl.google.com/android/repository
/sdk-tools-darwin-4333796.zip)

Speed up the download process with the following command:
```shell
curl https://dl.google.com/android/repository/sdk-tools-darwin-4333796.zip \
                                -o ~/software/sdk-tools-darwin-4333796.zip
```

Unzip sdk-tools-darwin-4333796.zip to directory $HOME/Library/Android/sdk

Set PATH variable
```
export PATH=$HOME/Library/Android/sdk/tools/bin:$PATH
export PATH=$HOME/Library/Android/sdk/platform-tools:$PATH
```

Before using [sdkmanager](https://developer.android.com/studio/command-line/sdkmanager)
to download the desired version of SDK, slight modification need to made to the sdkmanager
script to avoid [NoClassDefFoundError](https://stackoverflow.com/a/47150411/5411817),
credit goes to [Siu Ching Pong -Asuka Kenji](https://stackoverflow.com/users/142239/siu-ching-pong-asuka-kenji)

Find and replace the follow:
```shell
DEFAULT_JVM_OPTS='"-Dcom.android.sdklib.toolsdir=$APP_HOME”’
```
with:
```shell
DEFAULT_JVM_OPTS='"-Dcom.android.sdklib.toolsdir=$APP_HOME" -XX:+IgnoreUnrecognizedVMOptions --add-modules java.se.ee'
```

### Install platform-tools
Android SDK only install basic tools such as sdkmanager, apkanalyzer, monkeyrunner,
but commands such as adb, systrace are not included, using sdkmanager to install
latest version of platform-tools as follows:
```shell
sdkmanager "platform-tools" "platforms;android-28"
```

sdkmanager -- list to list installed and available packages

sdkmanager -- help for more


## Installing adb

If you only need adb command, the easiest way to is Using
[Homebrew](https://github.com/Homebrew)
```shell
brew cask install android-platform-tools
```

The command above will download platform tools from official
[website](https://dl.google.com/android/repository/platform-tools_r28.0.0-darwin.zip)
and the following binaries will be also installed:
```
==> Linking Binary 'dmtracedump' to '/usr/local/bin/dmtracedump'.
==> Linking Binary 'etc1tool' to '/usr/local/bin/etc1tool'.
==> Linking Binary 'fastboot' to '/usr/local/bin/fastboot'.
==> Linking Binary 'hprof-conv' to '/usr/local/bin/hprof-conv'.
==> Linking Binary 'mke2fs' to '/usr/local/bin/mke2fs'.
```

[brismuth](https://stackoverflow.com/users/1569320/brismuth) at stackoverflow provided
other [two options](https://stackoverflow.com/questions/31374085/installing-adb-on-macos).

## References
- [How to install Java 8 on Mac](https://stackoverflow.com/questions/24342886/how-to-install-java-8-on-mac)
