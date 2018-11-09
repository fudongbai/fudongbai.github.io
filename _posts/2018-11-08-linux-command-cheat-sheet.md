---
layout: post
title: Linux Command Cheat Sheet
date: 2018-11-08 23:21 +0800
categories: [linux]
tags: [cheatsheet, script]
---

## Basic
```shell
# find files created today
find . -type f -daystart -ctime -1

# find files create in the last 24 hours
find . -type f -ctime -1

# delete empty directory
find . -type d -empty | xargs rmdir

# redirect top info to text file
top -b -d 1 p 1100 >>info.txt

# play pcm audio file extracted from hidraw
aplay -f S16_LE -r 16000 *.pcm

# move files to specified directory
find . -name *.jpg |xargs -i mv {} ~/moments

# print line number, used for debug
echo $LINENO

# power off ubuntu when process exits
sudo su -c 'while [[ -d /proc/6077 ]]; do sleep 10; done; poweroff'

# connect via VPN
sudo openconnect ssl.linuxabc.com -b -u linuxabc

# add wav header to pcm files
ffmpeg -f s16le -ar 16k -ac 1 -i file.pcm file.wav

# mount nfs
sudo mount -t nfs 192.168.1.89:/opt/nfsroot nfs/

# mount iso
mount -t iso9660 ~/ubuntu-14.04.iso /media/cdrom/ -o loop

# mount vfat partition
mount -t vfat /dev/sda6 /tmp/

# install raspbian image to sd card
umount /dev/sdc1
sudo dd bs=4M if=2016-05-27-raspbian-jessie.img of=/dev/sdc

# Set VI Mode in Bash
set -o vi

# set mac address
ifconfig eth0 hw ether 001986060757

cscope -Rbkq
ctags -R

# renaming files with whitespaces
rename 's/ /./g' *

kill -9 `pidof adbd`
```


## sed
```shell
# Replace string
sed -i 's/find /find -L /g' build/core/Makefile

# add prefix string to each line
sed -i -e 's/^/prefix/' file
```


## awk
```shell
# extract dalvikvm related stuff to file
awk /"dalvikvm"/ logcat.txt > tmp.txt
```
