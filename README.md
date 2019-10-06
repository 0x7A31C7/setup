# Getting Started With Manjaro Linux

## Installation

Follow the instructions given in [this](https://forum.manjaro.org/t/wiki-windows-10-manjaro-dual-boot-step-by-step/52668) Manjaro forum post to install Manjaro alongside Windows 10 (dual boot).

## Set the Fastest Download Server

```bash
sudo pacman-mirrors -f
```

`-f` stands for `--fasttrack` where you can specify the number of servers you want written to your mirror list. For example, `-f 10` will save 10 mirrors. The mirrors will be saved in `/etc/pacman.d/mirrorlist`. 

More information is available in the [Majaro wiki](https://wiki.manjaro.org/index.php?title=Use_pacman-mirrors_to_Set_the_Fastest_Download_Server).

> **NOTE:** You can also update the mirrors from within Pamac Package Manager.

## Update All Packages

```bash
sudo pacman -Syyu
```

`-yy`: force refresh and download package databases from the server
`-u`: upgrade installed packages

## Install Pamac Package Manager

```bash
sudo pacman -S pamac
```

Pamac is a GUI Software Management (or Package Management) program that can be used instead of, or in addition to, using pacman in the terminal. Pamac is the default choice for the XFCE and Gnome Manjaro flavours.

The default Graphical Software Manager for the KDE flavour - Octopi - can be removed after installing Pamac.

More information on Pamac is available [here](https://wiki.manjaro.org/index.php/Pamac).

## Change Swappiness Value

The [swappiness](https://wiki.archlinux.org/index.php/Swap#Swappiness) parameter represents the kernel's preference (or avoidance) of swap space. Swappiness can have a value between 0 and 100, the default value is 60.

A low value causes the kernel to avoid swapping, a higher value causes the kernel to try to use swap space. Using a low value on sufficient memory is known to improve responsiveness on many systems.

```bash
cat /proc/sys/vm/swappiness
```

The above command shows the current swappiness value.

In order to reduce this value to 10, add the line `vm.swappiness=10` to `100-manjaro.conf` file in `/etc/sysctl.d/`. Create this file if it doesn't exist.

## Install Firewall

A [firewall](https://en.wikipedia.org/wiki/Firewall_%28computing%29) is a network security system that monitors and controls incoming and outgoing network traffic based on predetermined security rules.

[GUFW](https://wiki.manjaro.org/index.php?title=UFW_%26_GUFW) is a GUI firewall software that aims to make managing a Linux firewall as accessible and easy as possible. It is a front-end for UFW, which itself is a front-end for iptables.

Once GUFW is installed, enable and start UFW via systemd.

```bash
sudo systemctl enable ufw
sudo systemctl start ufw
```
You may also have to run the command `sudo ufw enable` to start the service on boot.

## Enable TRIM for SSD

```bash
sudo systemctl enable fstrim.timer
```

A [trim command](https://en.wikipedia.org/wiki/Trim_%28computing%29) allows an operating system to inform a solid-state drive (SSD) which blocks of data are no longer considered in use and can be wiped internally.

SSD TRIM provides important benefits in the areas of performance and drive longevity.
