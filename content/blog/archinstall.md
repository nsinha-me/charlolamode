---
title: Install Arch Linux using archinstall script
date: 2023-03-22
description: 
type: page
---

One of the dreams of linux users is to install Arch or Gentoo linux (atleast it was for me). There are many distros that are Arch based like ArcoLinux or EndeavourOS. But they don't give the feeling of installing arch. Installing Arch is little tricky (Gentoo users be like: hold my beer), but there is already archinstall script prebuilt inside the arch live iso. Lets see how easy it is to install arch using the archinstall script.  

### 1. Connect to internet
Once you have booted arch from the live usb stick, the very first step is to connect to the internet. The arch install requires internet connection to download packages on the go.  
### 1.1 LAN
If you are connected to LAN, then simply check the connectivity by using the ping command.
``` bash
# ping google.com
```
If the internet connection is working, then the above command will return bytes sent and the time taken. And if the connection is not working, then it will return error.  
### 1.2 WIFI
If you are on wifi, then you have to do little more work. `iwctl` is the tool we will be using to connect to wifi network. It will give us the `iwd` interactive prompt.
``` bash
# iwctl
```
First, if you do not know your wireless device name, list all Wi-Fi devices: 
``` bash
[iwd]# device list
```
If the device or its corresponding adapter is turned off, turn it on:
``` bash
[iwd]# device deviceName set-property Powered on
```
``` bash
[iwd]# adapter adapterName set-property Powered on
```
Then, to initiate a scan for networks (note that this command will not output anything):
``` bash
[iwd]# station deviceName scan
```
You can then list all available networks:
``` bash
[iwd]# station deviceName get-networks
```
Finally, to connect to a network:
``` bash
[iwd]# station deviceName connect SSID
```
Then exit.
``` bash
[iwd]# exit
```
Now to check the connectivity, use the ping command as shown in above section.


### 2. Configure the pacman.conf 
Before installing arch, lets edit the pacman configuration file to speed up our install process.  
By default pacman downloads only one package at a time. This setting can be overridden by changing the configuration file. Open the config file-
``` bash
# nano /etc/pacman.conf
```
Find the `#ParallelDownloads = 5` line, uncomment it and change the value to 30.
``` bash
ParallelDownloads = 30
```
Save it and exit.


### 3. Install Arch
Use the archinstall magic script.
``` bash
# archinstall
```
After this, the process is very simple. So I am not writing each step of this. You can figure it out easily. For more details you can have a look at [this doc](https://python-archinstall.readthedocs.io/en/latest/installing/guided.html#description-individual-steps).

### 4. Post Installation
After the installation is complete, you will be given a prompt to chroot into the newly installed os to do some additional work as required. If you have installed some desktop environment like gnome or kde, then this step is not important. You can skip this step and reboot to your new installed Arch Linux.  
But if you have installed some window manager, then you might require some tweaking. The amount of configuration to be done varies from wm's to wm's. I will show you the post install bspwm config you should do.
### 4.1 BSPWM
The example configuration is located in `/usr/share/doc/bspwm/examples/`. Once you chroot-ed in the newly installed os. Make the config directory for bspwm and sxhkd.
``` bash 
# mkdir /home/(your user name here)/.config/bspwm
# mkdir /home/(your user name here)/.config/sxhkd
```
After that, you can copy the default config files and make them executable or you can install it with executable rights.
``` bash
# cp /usr/share/doc/bspwm/examples/bspwmrc /home/(your username here)/.config/bspwm/bspwmrc
# chmod +x /home/(your user name here)/.config/bspwm/bspwmrc

# cp /usr/share/doc/sxhkd/examples/sxhkdrc /home/(your username here)/.config/sxhkd/sxhkdrc
# chmod +x /home/(your user name)/.config/sxhkd/sxhkdrc
```

OR

``` bash
# install -Dm755 /usr/share/doc/bspwm/examples/bspwmrc ~/.config/bspwm/bspwmrc
# install -Dm644 /usr/share/doc/bspwm/examples/sxhkdrc ~/.config/sxhkd/sxhkdrc
```

For changing the terminal of your choice or the keybindings, edit the sxhkd config.
``` bash
# nano /home/(your user name)/.config/sxhkd/sxhkdrc
```
Save it and exit. Finally exit the chroot and then reboot. Hurrayyyyyyy!!!!


### Final thought
Installing arch is little tricky and tiresome for newbie's. But at the end, it was fun for me. Got to learn many things that I would have never learnt otherwise. And now I can also say the very famous line, "I use Arch, btw". But this is just the beginning. I have to install arch without using the archinstall script.

I would love to hear your opinions and experiences about this topic. And also the mistakes and improvements in the code/blog. You can mail me at nikhil@nsinha.me .  