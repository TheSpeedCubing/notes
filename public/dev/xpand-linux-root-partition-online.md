---
date: 2026-04-04 22:21:00
slug: 1b331e54
title: "Expand Linux Root Partition Online After Growing VM Disk"
---

### before

root@test:~# lsblk
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda      8:0    0  128G  0 disk
├─sda1   8:1    0 60.7G  0 part /
└─sda2   8:2    0    1K  0 part
sr0     11:0    1    4M  0 rom
sr1     11:1    1  754M  0 rom

root@test:~# df -h
Filesystem      Size  Used Avail Use% Mounted on
udev            3.9G     0  3.9G   0% /dev
tmpfs           795M  700K  794M   1% /run
/dev/sda1        60G   39G   18G  69% /
tmpfs           3.9G     0  3.9G   0% /dev/shm
tmpfs           5.0M     0  5.0M   0% /run/lock
tmpfs           1.0M     0  1.0M   0% /run/credentials/systemd-journald.service
tmpfs           3.9G     0  3.9G   0% /tmp
tmpfs           1.0M     0  1.0M   0% /run/credentials/getty@tty1.service
overlay          60G   39G   18G  69% /var/lib/docker/overlay2/c3b74d73715ca211d47db32f4b0b0bf54ebeae331527cd8adfbcd277601ddf79/merged
tmpfs           795M   12K  795M   1% /run/user/0


### delete sda2

fdisk /dev/sda
d
2
w

Disk /dev/sda: 128 GiB, 137438953472 bytes, 268435456 sectors
Disk model: QEMU HARDDISK
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0xf5d7f1a3

Device     Boot     Start       End   Sectors  Size Id Type
/dev/sda1  *         2048 127299583 127297536 60.7G 83 Linux
/dev/sda2       127301630 134215679   6914050  3.3G  f W95 Ext'd (LBA)
root@test:~# fdisk /dev/sda

Welcome to fdisk (util-linux 2.41).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.

This disk is currently in use - repartitioning is probably a bad idea.
It's recommended to umount all file systems, and swapoff all swap
partitions on this disk.


Command (m for help): d
Partition number (1,2, default 2): 2

Partition 2 has been deleted.

Command (m for help): w
The partition table has been altered.
Syncing disks.



### grow sda1

growpart /dev/sda 1

CHANGED: partition=1 start=2048 old: size=127297536 end=127299583 new: size=268433375 end=268435422

root@test:~# df -h
Filesystem      Size  Used Avail Use% Mounted on
udev            3.9G     0  3.9G   0% /dev
tmpfs           795M  688K  794M   1% /run
/dev/sda1        60G   39G   18G  69% /
tmpfs           3.9G     0  3.9G   0% /dev/shm
tmpfs           5.0M     0  5.0M   0% /run/lock
tmpfs           1.0M     0  1.0M   0% /run/credentials/systemd-journald.service
tmpfs           3.9G     0  3.9G   0% /tmp
tmpfs           1.0M     0  1.0M   0% /run/credentials/getty@tty1.service
overlay          60G   39G   18G  69% /var/lib/docker/overlay2/c3b74d73715ca211d47db32f4b0b0bf54ebeae331527cd8adfbcd277601ddf79/merged
tmpfs           795M   12K  795M   1% /run/user/0
root@test:~# lsblk
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda      8:0    0  128G  0 disk
└─sda1   8:1    0  128G  0 part /
sr0     11:0    1    4M  0 rom
sr1     11:1    1  754M  0 rom


### grow fs

resize2fs /dev/sda1

root@test:~# lsblk
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda      8:0    0  128G  0 disk
└─sda1   8:1    0  128G  0 part /
sr0     11:0    1    4M  0 rom
sr1     11:1    1  754M  0 rom
root@test:~# df -h
Filesystem      Size  Used Avail Use% Mounted on
udev            3.9G     0  3.9G   0% /dev
tmpfs           795M  688K  794M   1% /run
/dev/sda1       126G   39G   82G  33% /
tmpfs           3.9G     0  3.9G   0% /dev/shm
tmpfs           5.0M     0  5.0M   0% /run/lock
tmpfs           1.0M     0  1.0M   0% /run/credentials/systemd-journald.service
tmpfs           3.9G     0  3.9G   0% /tmp
tmpfs           1.0M     0  1.0M   0% /run/credentials/getty@tty1.service
overlay         126G   39G   82G  33% /var/lib/docker/overlay2/c3b74d73715ca211d47db32f4b0b0bf54ebeae331527cd8adfbcd277601ddf79/merged
tmpfs           795M   12K  795M   1% /run/user/0
