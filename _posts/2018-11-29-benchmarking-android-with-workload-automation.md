---
layout: post
title: Benchmarking android with workload automation
date: 2018-11-29 20:58 +0800
categories: [benchmark]
tags: [android, wa, workload-automation, profiling]
---
## What is wa

> Workload Automation (WA) is a framework for executing workloads and collecting
> measurements on Android and Linux devices. WA includes automation for nearly 40
> workloads and supports some common instrumentation (ftrace, hwmon) along with
> a number of output formats.


## Installation

### Install wlauto
To avoid install failure, it is recommended that you update pip and setuptools
before proceding with installation:
```shell
pip install --upgrade --user pip
pip install --upgrade --user setuptools
```

Now, install workload-automation with:
```shell
pip install --user wlauto
```

Alternatively, you may wanna install latest development version from github:
```shell
git clone https://github.com/ARM-software/workload-automation.git
pip install --user ./workload-automation
```

### Install Android SDK

To use wa, Android SDK is required to be installed and properly setup, download
**SDK tools package** from [sdk-tools-linux-4333796.zip][sdk] and setup ANDROID_HOME:
```shell
export ANDROID_HOME=/opt/android-sdk/
```

## Run a simple workload
In order to run workload we need to know what workloads wa supports, *wa list
workloads* will show all the workloads currently supported by wa.

wa has a default config file under $HOME/.workload_automation/, named config.yaml

As we will run workloads on Android devices, additional configuration needs to be
added to this file:
```
device_config:
    device: 192.168.123.15:5555
    working_directory: '/data/local'
    load_default_modules: false
```
The last two lines are optional.

Now, do '*wa run dhrystone*' will make wa run workload dhrystone with the default
configuration with addtions for android devices. wa_output contains all results
of this run.


## Agenda
Running a single workload is easy, and normally of little use, what if I wanna
run several workloads, what if I wanna setup android devices in boost mood.

To do complicated jobs, we need to create an "agenda", to get an general idea
what aganda looks like, see [lisa agenda examples][agenda].


## References
- [User Information][user]
- [Developer Information][developer]


[user]: https://workload-automation.readthedocs.io/en/latest/user_information.html
[developer]: https://workload-automation.readthedocs.io/en/latest/developer_information.html
[sdk]: https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip
[agenda]: https://github.com/ARM-software/lisa/tree/master/tools/wltests/agendas
[devlib]: https://github.com/ARM-software/devlib
[devlib-doc]: https://devlib.readthedocs.io/en/latest/
