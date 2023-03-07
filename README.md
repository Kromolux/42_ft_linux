# 42_ft_linux

## Description
The first project of the Kernel branch! This is a simple LFS so that you can build your own distribution which will be used in the next projects

## Keywords
* System administration

## Skills
* Unix
* Rigor
* Technology integration

# ft_linux
how_to_train_your_kernel

Summary: Make your own linux distribution

Version: 3

## Introduction
Welcome to ft_linux. In this subject, you have to build a basic, but functional, linux distribution.

This subject is not about Kernel programming, but it’s highly related. This distro will be the base for all your kernel projects, because all your kernel-code will be executed here, on your distro. Try to implement what you want/need to. This is your userspace, take care of it!

## Goals
* Build a Linux Kernel
* Install some binaries (See the list below)
* Implement a filesystem hierarchy compliant with the standards
* Connect to the Internet

## General instructions
### The links
* The Bible
* How to build a Kernel
* Autotools
### Instructions
* For this subject, you must use a virtual machine, live VirtualBox or VMWare.
* Though it is not REQUIRED, you SHOULD read this and that right now. Keep those standards in mind. You won’t be graded on your compliance with them, but still, it would be good practice.
* You must use a kernel version >= 4.0. Stable or not, as long as it’s a 4.0 >= version.
* The kernel sources must be in /usr/src/kernel-$(version)
* You must use at least 3 differents partitions. (root, /boot and a swap partition). You can of course make more partitions if you want to.
* Your distro must implement a kernel_module loader, like udev.
* The kernel version must contain your student login in it. Something like ‘Linux kernel 4.1.2-<student_login>‘
* The distribution hostname must be your student login
* You’re free to choose between a 32 or 64-bit system.
* You must use a sofware for central management and configuration, like SysV or SystemD.
* Your distro must boot with a bootloader, like LILO or GRUB.
* The kernel binary located in /boot must be named like this: vmlinuz-<linux_version>-<student_login>. Adapt your bootloader configuration to that.

## Mandatory part
### Packages to Install

> :information_source: The following versions are known to work together correctly. However, you are free to use the versions you want.

> :information_source: Some packages below (vim, bash, grub, udev) are examples. Feel free to change them by any equivalent you like.

* Acl (2.2.52)
* Attr (2.4.47)
* Autoconf (2.69)
* Automake (1.15)
* Bash (4.3.30)
* Bc (1.06.95)
* Binutils (2.25.1)
* Bison (3.0.4)
* Bzip2 (1.0.6)
* Check (0.10.0)
* Coreutils (8.24)
* DejaGNU (1.5.3)
* Diffutils (3.3)
* Eudev (3.1.2)
* E2fsprogs (1.42.13)
* Expat (2.1.0)
* Expect (5.45)
* File (5.24)
* Findutils (4.4.2)
* Flex (2.5.39)
* Gawk (4.1.3)
* GCC (5.2.0)
* GDBM (1.11)
* Gettext (0.19.5.1)
* Glibc (2.22)
* GMP (6.0.0a)
* Gperf (3.0.4)
* Grep (2.21)
* Groff (1.22.3)
* GRUB (2.02 beta2)
* Gzip (1.6)
* Iana-Etc (2.30)
* Inetutils (1.9.4)
* Intltool (0.51.0)
* IPRoute2 (4.2.0)
* Kbd (2.0.3)
* Kmod (21)
* Less (458)
* Libcap (2.24)
* Libpipeline (1.4.1)
* Libtool (2.4.6)
* M4 (1.4.17)
* Make (4.1)
* Man-DB (2.7.2)
* Man-pages (4.02)
* MPC (1.0.3)
* MPFR (3.1.3)
* Ncurses (6.0)
* Patch (2.7.5)
* Perl (5.22.0)
* Pkg-config (0.28)
* Procps (3.3.11)
* Psmisc (22.21)
* Readline (6.3)
* Sed (4.2.2)
* Shadow (4.2.1)
* Sysklogd (1.5.1)
* Sysvinit (2.88dsf)
* Tar (1.28)
* Tcl (8.6.4)
* Texinfo (6.0)
* Time Zone Data (2015f)
* Udev-lfs Tarball (udev-lfs-20140408)
* Util-linux (2.27)
* Vim (7.4)
* XML::Parser (2.44)
* Xz Utils (5.2.1)
* Zlib (1.2.8)

## Bonus part
You have a stable system ? Nice. Now let’s have some fun ! Install whatever you want. Any software, GUI, ANYTHING.
Make this system yours, with your touch. Special points for an X Server, and window managers / desktop environments, like GNOME / LXDE / KDE / i3 / dwm ...

> :warning: The bonus part will only be assessed if the mandatory part is PERFECT. Perfect means the mandatory part has been integrally done
and works without malfunctioning. If you have not passed ALL the mandatory requirements, your bonus part will not be evaluated at all.

## Submission and peer-evaluation
Turn in your assignment in your Git repository as usual. Only the work inside your repository will be evaluated during the defense. Don’t hesitate to double check the names of your folders and files to ensure they are correct. For obvious reasons, you will not push your entire virtual machine but a checksum of your disk image instead.

That can be done with something like:

`shasum < disk.vdi`

Keep your disk image somewhere for the peer-evaluation.

How to mount the drives?

```
sudo mount -v -t ext4 /dev/sdb3 $LFS
sudo mount -v -t vfat /dev/sdb1 $LFS/boot
sudo /sbin/swapon -v /dev/sdb2
```

How to check to swap partion?
```
cat /proc/swaps
```

How to check partions and disks?
```
fdisk -l
df -h
lsblk
blkid /dev/sdb*
```

How to create an environmental variable for multithread compilation with Makefile?
```
export MAKEFLAGS="-j$(expr $(nproc) \+ 1)"
```

How to mount the virtual Kernel drives?
```Bash
mount -v --bind /dev $LFS/dev
mount -v --bind /dev/pts $LFS/dev/pts
mount -vt proc proc $LFS/proc
mount -vt sysfs sysfs $LFS/sys
mount -vt tmpfs tmpfs $LFS/run
```

How to change to chroot environment?
```Bash
chroot "$LFS" /usr/bin/env -i   \
    HOME=/root                  \
    TERM="$TERM"                \
    PS1='(lfs chroot) \u:\w\$ ' \
    PATH=/usr/bin:/usr/sbin     \
    /bin/bash --login
```
