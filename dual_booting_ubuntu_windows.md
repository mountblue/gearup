# Guide to Dual Boot Windows and Ubuntu

* This guide assumes you are installing Ubuntu 18.04 or later (64 bit version)
* This guide is an overview. It does not cover a lot of corner cases which often come up while doing the process. Also some points might be confusing to the new user. 
* There are reference links to other resources which explain the steps in further detail. I highly recommend reading them.
* If your Windows is installed in legacy mode i.e. MBR(Master Boot Record) style partitioning, install Linux in legacy mode
* If your Linux is installed in UEFI mode i.e. GPT style hard disk partitioning, install Linux in UEFI mode
* Do not skip any step. Go in sequence.
* Running your **Linux distribution live without installing** is a good way to test if wifi, sound and graphics are working properly.
* Disabling Fast Boot, Hibernation and Secure Boot are **really important**.
* If you want to keep Windows as an option, then detection of Windows Boot Manager in Step 4 of the installation process is really important.
* Remember Ubuntu likes ext4 partitioning, Windows likes ntfs. You can change the partition type using Gparted for the target partition for Linux installation.

Reference Links:

[Installing Ubuntu in UEFI mode](https://help.ubuntu.com/community/UEFI)

[Installing Ubuntu with pre-installed Windows](https://askubuntu.com/questions/221835/how-do-i-install-ubuntu-alongside-a-pre-installed-windows-with-uefi?noredirect=1&lq=1) - Highly recommended link. Covers a lot of corner cases

[Video to dual boot with Secure boot and UEFI enabled](https://www.youtube.com/watch?v=18F3CZveMwg&feature=youtu.be)

## Windows 10

### Disable Fast Startup

By default, Windows 10 has fast startup enabled that leaves Windows in a saved state even when it is shut down.

In start menu, open Power and Sleep Options > Open Settings that are currently unavailable > Choose what Power button does > Open settings that are currently unavailable

### Disable Hibernation

Open the Command Prompt in Administrator mode by right clicking the Command Prompt menu item in the Start menu.

Enter the command:

```
powercfg -h off
```

### Check Disk Partitioning Mode

Open the Command Prompt in Administrator mode by right clicking the Command Prompt menu item in the Start menu.

Enter the commands

```
diskpart

list disk
```

Check whether the partition style is GPT or not.

### Create some unallocated space

We need to install Linux on partition in the hard disk. I recommend more than 100 GB partition for installing Linux root directory and 16 GB for Swap partition.

If the hard disk has no unallocated area or partition with ext4 style partitioning, Ubuntu installer will not give the option of installing alongside Windows 10.

If your hard disk partitioning style is GPT. Create unallocated space in the hard disk by shrinking one of the volumes.

If your hard disk partitioning style is MBR, you are only restricted to 4 primary partitions. You will need to cut down to 3 primary partitions and then create a logical partition. A logical partition can be further broken down into further partitions.

### BIOS Screen

#### Disable Secure Boot

You have to open the BIOS setup screen in your laptop. You can get it by hitting the Del or F2 or F9 or F10 keys when booting up. It depends on your laptop model.

Find the Secure boot option and disable it. 

#### Change boot device order to give USB priority

In BIOS setup screen, change boot device order to give USB priority.

## Boot into Live Ubuntu

If you have UEFI boot enabled, try Ubuntu in UEFI mode. Or if you have legacy boot enabled, try Ubuntu in MBR mode.

### Check for Wifi

If your Live Ubuntu is detecting Wifi (you can find the icon in the top right bar), we are good. Make sure internet works by running Firefox and checking internet.

If Wifi driver did not get detected, check if USB tethering works. At this point you have to take a call. If you have a mobile with USB tethering or a JioFi deveice, USB tethering can work but it is a bit cumbersome.

Try again with an Ubuntu 19.04 live check or Ubuntu 20.04 live check.

### Gparted

Start the application Gparted. Hope you have unallocated space or have a drive that you can potentially delete.

#### GPT

Create 2 partitions, one more than 100 GB formatted ext4 and another 16 GB formatted as linux-swap.

#### MBR
MBR style partitioning can have a max 4 primary partitions. To get around, we need at least 1 logical partition.

Make sure you have a logical partition. Create 2 partitions, one more than 100 GB formatted ext4 and another 16 GB formatted as linux-swap.

#### Next step

Once this is done, note down the number of the ext4 drive. For example /dev/sda6 or something else

### Start Ubuntu Installation

#### Steps 1 and 2

First screen and second screen asks for language and keyboard language preferences. Choose the relevant options, default is English and click continue.

#### Step 3

In 3rd screen, choose install drivers and 3rd party software option, it will save you a lot of trouble later. 

Click continue.

#### Step 4 - Important

If the option, Install Ubuntu alongside Windows comes, awesome. We are on track.

If not **ABORT MISSION!!** You want to preserve your pre-installed Windows OS right.

Click Continue.

#### Step 5 - Choose Custom Partitioning

Click custom partitioning .

#### Step 6 - Format the ext4 partition as root

Select the previously created partition (more than 100 GB formatted as ext4) and mark it for formatting as /

Click continue.

#### Step 7 and Step 8

Choose your time zones and set user name and password.

#### Step 9 - installation

Make sure your computer has a power connection. Let the steps happen and take a walk.

### Post Installation

Once installation finishes it asks for restart. Click restart and remove the installation media.

Check if you are getting the grub menu. The default option would be Ubuntu. Boot into it and check whether everything is working fine. 

If your computer is booting directly into Windows 10, then you might need to go the BIOS setup screen again and change boot OS order.

----

Congratulations!!







