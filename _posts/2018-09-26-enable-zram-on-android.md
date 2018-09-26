---
layout: post
title: Enable zram on Android
date: 2018-09-26 07:49 +0800
categories: [Android]
tags: [Android, zram]
---

## What is zram
Kernel [Documentation](https://www.kernel.org/doc/Documentation/blockdev/zram.txt) says
it is Compressed RAM based block devices

## How to enable zram on Android devices

### Enable kernel [options](https://source.android.com/devices/tech/perf/low-ram#zram)
```
CONFIG_SWAP
CONFIG_CGROUP_MEM_RES_CTLR
CONFIG_CGROUP_MEM_RES_CTLR_SWAP
CONFIG_ZRAM
```
### zram [config](https://packages.ubuntu.com/bionic/zram-config)
```shell
#!/system/bin/sh

# load dependency modules
NRDEVICES=$(grep -c ^processor /proc/cpuinfo | sed 's/^0$/1/')
if modinfo /system/lib/modules/zram.ko | grep -q ' zram_num_devices:' 2>/dev/null; then
  MODPROBE_ARGS="zram_num_devices=${NRDEVICES}"
elif modinfo /system/lib/modules/zram.ko | grep -q ' num_devices:' 2>/dev/null; then
  MODPROBE_ARGS="num_devices=${NRDEVICES}"
else
  exit 1
fi
insmod /system/lib/modules/zram.ko $MODPROBE_ARGS

# Calculate memory to use for zram (1/2 of ram)
totalmem=`LC_ALL=C free | grep -e "^Mem:" | sed -e 's/^Mem: *//' -e 's/  *.*//'`
mem=$(((totalmem / 2 / ${NRDEVICES}) * 1024))

# initialize the devices
for i in $(seq ${NRDEVICES}); do
    DEVNUM=$((i - 1))
    echo $mem > /sys/block/zram${DEVNUM}/disksize
    mkswap /dev/zram${DEVNUM}
    swapon -p 5 /dev/zram${DEVNUM}
done
```

In case zram was built into kernel pass zram parameter from bootargs:
```shell
zram.num_devices=2
```

## Performance
[zram-perf](https://android.googlesource.com/platform/system/extras/+/master/zram-perf/)
can be used for read/write speed test
