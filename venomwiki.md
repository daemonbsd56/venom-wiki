
# Introduction
=========================

## Welcome


# Venom Linux
===========
Venom Linux is an LFS (Linux From Scratch) based linux distribution but highly modified for daily use targetting experienced users. This distro is inspired by CRUX (crux.nu) of its simplicity and KISS philosophy and i am CRUX fan and was core user before i started this distro. This distro is use BSD-style initscripts and BSD-like ports system for packages. Packages is managed by my own package manager called scratchpkg that has dependencies checking and its full written in bash, so it might slower than any package manager existed but it works :)

## Features


Venom Linux is source based linux distribution based on Linux From Scratch (LFS)
with multilib support and heavily modified for daily usage.
Features
    Highly customizable. 
    Has package manager: allows you to create your own packages. Believe us: writing and creating packages
        is dead simple. 
    Package build script is similar to BSD's ports style: you can create your own repos and ports on top of existing one
    Using BSD-style init (rc init)
    Installable using dialog based installer
    Multilib support which allows you to run the famous games application/site, or run your 32 bit coded printer drvers like the Brother ones.
    has lxde, mate, xfce4, kde5, i3, dwm, openbox and etc in the repo



## Sources
https://github.com/venomlinux
mail emmett1.2miligrams@gmail.com
Telegram desktop:
Website :https://www.venomlinux.org
Sourceforge link : https://sourceforge.net/projects/venomlinux/

 





## Structure of Venom installation

### Using a precompiled, ready to use life Venom version

#####  Downloading an iso
The Venom Linux distribution iso's are available at the
following address:
https://sourceforge.net/projects/venomlinux/files/
Different flavors are available like xfce4, lxde, mate. Those
versions are ready to use. They are well suited for a Linux
beginner. They offer a full live iso desktop environment. At
the very moment, the iso's are running in a uefi and a mbr
environment. You can use those iso images for installation
on your hard disk or even in a VM (Virtualbox, qemu ..;).
The latest image at the time of writing is dated 20190412 or
later. Don't forget to check the images with md5sum. The check file
is available in the same directory.

#### Using the Venom build script (for advanced users).

### Booting the iso:
Don't forget that the keybord in console mode and in graphical mode
are set to the standard US keyboard. When you are logged in the graphical
mode, open a console and change your keyboard to the one you are using for
your keyboard setup:

graphical mode  : setxkbmap fr      # (it, be,de......)
console mode    : loadkeys fr       # (idem....)

### Default login/users/passwords for the downloaded iso:


#### Login for live iso
-------------
user : venom
password : venom

user : root
password : root

### Network detection
Normally spinns off automatically. Nethertheless if you have a
problem look at the dedicated topic below.

#### interface names
As root in the terminal have a look for the classical ifconfig output command.
You can use as well the ip command in the terminal finding out the network
devices.
We will develop later on if necessary the network setup. 


## How to install 

Venom installation on your hard disk (HDD)or in VM, can be done by running 'venom-installer' from terminal/tty
As root run the following command:
./venom-installer

A new ncurses based screen will pop up in your terminal where you can configure the final installation.
Choose your keyboard according to your language. After that you may if necessary choose to format your disk.
If you say no, you will be faced with the available disks/partitions where you can install your Venom.
You will be asked for the fs type (ext4, btrfs ...) Formatting will be done at the end of the process.
Next will be asked for the name of the new user and to set it's password. The new password for root will be
asked and set as well.
Next topic will be the grub bootloader. You may install a new grub if necessary on your HDD. If you have already
a linux distro on your desktop you may answer to not install the grub loader and using ofcourse the previous installed grub. Dont forget to update your primary grub after full installation and rebooting.



### Rebooting and system configuration, daemons
After rebooting, you obtain the graphincal interface of the iso you choosed. If all went well
you are able to log as the user you defined with its appropriate new password. You will be
already with the previous selected keyboard. Nevertheless you have always the control of your
            Venom through the rc daemon and rc conf files.

#### System configuration

The file for controlling the system setup is defined  in /etc/rc.conf. 
You can configure the following items:
hostname, timezone, clock, font, keymap and daemons.
 
Below you will find a typical example of the rc.conf content


 system configuration


HOSTNAME="venom"
TIMEZONE="Europe/Paris"
CLOCK="utc"
FONT=""
KEYMAP="fr-latin9"
DAEMONS=(sysklogd dbus lxdm alsa bluetooth networkmanager)

#### Daemons
The daemon script is located in /etc/rc.d/ directory. Enabling and disabling a daemon
is achieved by adding/removing the daemon from DAEMONS array in the previous defined 
/etc/rc.conf file in the order you choose. 
A script manages the checking/starting/stop/restart daemon but you still have to configure
manually the rc.conf file in order to add/remove a daemon from the spinoff/booting process. 

You can always control the rc process with the following command in a tty/console.

Command
 rc -h

Usage:
    rc <option> <daemon>

Options:
    list                 List available daemons
    start    <daemons>   Start daemons
    stop     <daemons>   Stop daemons
    restart  <daemons>   Restart daemons
    status   <daemons>   Show daemon status

#### Locale

By default the 'venom-installer' will install en_US.UTF-8 locale.
If you need to change to your local language, uncomment your desired 
locale in /etc/locales file.Edit the file with the default installed
editor vim and uncomment the desired line:

By default the 'venom-installer' will install en_US.UTF-8 locale.If you 
need to change it uncomment your desired locale in /etc/locales file then run
in a console the following command

genlocales

### Venom Administration

#### Editors

Vim is the default text editor. You can always use other editors like emacs, nano etc ...
by installing them. See below for further installation in the scratchpkg ( the 
Venom package manager).
#### Upgrading after first reboot
We strongly advise to update as root the ports database after the first reboot and make a full upgrade.
Keep in mind to upgrade first of all the database and proceed with the upgrading of 
scratchpkg first. After that you may upgrade the full installed distro. Roll off to control 
the linked libraries (broken packages) with the revdep -r  command.

As root run off the following commands

scratch sync
scratch upgrade scratchpkg
scratch sync
revdep -r

#### Scratchpkg cheatsheet 


Run 'scratch help' from the terminal to see available options, anyway here is  the quick usage: 

Usage:
    scratch help <operation>
    
Operation:
    build           build only packages
    install         install packages
    remove          remove packages in system
    upgrade         upgrade packages and install new dependencies (if any)
    extra           various extra options

revdep      checing for broken packages and their shared libs
updateconf  updating configuration files

A fully detailed chapter will be dedicated to scratchpkg later on with the further
extra features.






## Scratchpkg
Linux is built by compiling several files called packages. We based
ourselves upon ports for building them up. Scratchpkg is used right
away after the building of the toolchain, during the building of the
the final core Venom/ Linux system. It is used all along the further
setup of your homemade system. 

### Ports - spkgbuild

#### What are ports.
Ports are necessary tools for building a package. You can compare it
with a recipe. All ports are located in /usr/ports. This tree is
synced/updated through the scratch sync command executed as root.

They are classified in:

- core
- extra
- kf5
- lxde
- lxqt
- mate
- xfce4
- xorg
- multilib

Under the core directory, you will find the essential, core packages
for your distro. They cover at least the so called LFS/BLFS packages. 
Within the extra directory, you will find the additional and personal
packages. The other ports are mainly related to your Desktop
environment (Plasma/kf5, lxde, lxqt, mate, xfce4). The xorg ports
cover the main graphical interface if you run X. The multilib
directory handles the 32 bit packages needed by some special programs
like wine, steam and brother printer drivers for example. 




#### Spkgbuild config => portmake
You can build a new port with the portmake command. It will create a
template in the ports directory you have chosen to put your spkgbuild
file. 


###  Scratchpkg backend

####  pkgbuild

Usage:
    $(basename $0) build [ <pkgname> <options> ]
    
Options:
    -f, --force-rebuild    force rebuild
    -m, --skip-mdsum       skip md5sum check for sources
    -d, --no-dep           skip dependency check
    -e, --extract          extract only
    -w, --keep-work        keep woring directory


#### pkgadd
#### pkgdel
#### pkgdeplist
#### pkglibdepends
#### pkgbase

### Scratchpkg frontend

This distro comes with a custom package manager called scratchpkg. These are the 
basic commands of this package manager that you should know:



#### scratch overall usage
    installing packages:

      # scratch install <pkg1> <pkg2> <pkgN>

    removing packages:

      # scratch remove <pkg1> <pkg2> <pkgN>

    search packages:

      # scratch search <pattern>

    update packages repo:

      # scratch sync

    full system upgrade (should run after updating packages repo):

      # scratch sysup

    fix broken packages (recommended run after full system upgrade or after removing packages):

      # revdep -r

    update packages configuration files (recommended run after packages upgraded):

      # updateconf

Notes

    run scratch help to see available options for scratch
    run revdep -h to see available options for revdep






#### scratch advanced usage

Scratchpkg has also some advanced features which allow you to master in depth
your Venom distro. 

Usage:
    $(basename $0) <operation> [ <pkgname/pattern/file> ]
    
Operation:
    depends   <package>       show depends of a package
    search    <pattern>       search packages in port's repos
    lock      <packages>      lock packages from upgrade
    unlock    <packages>      unlock packages from upgrade
    cat       <package>       view a package build scripts
    dependent <package>       show package's dependent
    own       <file>          show package's owner of file
    pkgtree   <package>       show list files of installed package
    path      <package>       show package's buildscripts path
    sync                      update port's repo
    sysup                     full system update
    dup                       print duplicate ports in repo
    readme                    print readme file if exist
    listinst                  list installed package in system
    listorphan                list orphan package
    integrity                 check integrity of package's files
    outdate                   check for outdate packages
    cache                     print leftover cache
    rmcache                   remove leftover cache
    missingdep                check for mising dependency of installed package
    foreignpkg                print package installed without port in repo
    listlocked                print locked packages



    
