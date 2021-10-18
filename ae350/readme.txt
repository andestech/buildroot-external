Intro
=====

Andestech AE350 Platform

The AE350 prototype demonstrates the AE350 example platform on the FPGA. 
This configuration builds with Linux 5.4 and OpenSBI 0.7 tarballs in 
AndeSight 5.0.0 package.

How to build it
===============

Configure Buildroot
-------------------

  $ make andes_ae350_defconfig

If you want to customize the packages:

  $ make menuconfig

Build everything
----------------
Note: you will need to have access to the network, since Buildroot will
download the packages' sources.

  $ make

Result of the build
-------------------

After building, you should obtain these files:

  output/images/
  +-- Image
  +-- ae350.dtb
  +-- boot.scr
  +-- boot.vfat
  +-- fw_dynamic.bin
  +-- fw_dynamic.elf
  +-- fw_jump.bin
  +-- fw_jump.elf
  +-- rootfs.cpio
  +-- rootfs.ext2
  +-- rootfs.ext4 -> rootfs.ext2
  +-- rootfs.tar
  +-- sdcard.img
  +-- u-boot-spl.bin
  +-- u-boot.itb

Copy the sdcard.img onto an SD card with "dd":

  $ sudo dd if=sdcard.img of=/dev/sdX bs=4096

Then, your SD card should be something looks like:

  Disk /dev/mmcblk0: 31457280 sectors, 3072M
  Logical sector size: 512
  Disk identifier (GUID): 546663ee-d2f1-427f-93a5-5c7b69dd801c
  Partition table holds up to 128 entries
  First usable sector is 34, last usable sector is 385062

  Number  Start (sector)    End (sector)  Size Name
       1              34          262177  128M u-boot
       2          262178          385057 60.0M rootfs

Insert SD card and reset the board, it will boot Linux from mmc.
