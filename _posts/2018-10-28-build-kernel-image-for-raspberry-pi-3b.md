---
layout: post
title: Build kernel image for Raspberry Pi 3B
date: 2018-10-28 22:21 +0800
categories: [kernel]
tags: [raspberrypi, kernel]
---

## Download source code
```shell
git clone --depth=1 https://github.com/raspberrypi/linux.git
```

## Build zImage and modules
```shell
cd linux
KERNEL=kernel7
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- rpi3_defconfig
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- zImage modules dtbs
```

## References:
- [KERNEL BUILDING][kernel-building]

[kernel-building]: https://www.raspberrypi.org/documentation/linux/kernel/building.md
