# Ubuntu Tuning Note
My tuning note for Ubuntu 14.04

Hardware: Asus UX-305FA
WM: Gnome3

## Gnome Installation
```
sudo add-apt-repository ppa:gnome3-team/gnome3
sudo add-apt-repository ppa:gnome3-team/gnome3-staging
sudo apt-get update
sudo apt-get dist-upgrade
```

reference: [How To Install GNOME 3.12 On Ubuntu GNOME 14.04 Trusty Tahr](http://linuxg.net/how-to-install-gnome-3-12-on-ubuntu-gnome-14-04-trusty-tahr/)


## TouchPad
Using Touchegg for touchpad utility

Touchegg cannot use in Unity

#### Configuration file
1. touchegg.conf

   place in ~/.config/touchegg/

2. touch.sh

   use to overwrite some synclient settings

#### GUI configuration tool
[Touchegg-gce](https://github.com/Raffarti/Touchegg-gce)

#### Add startup program

add ```touch.sh``` and ```touchegg &``` to startup program (use ```gnome-session-properties```)
   
## System tuning

#### Brightness
```
sudo apt-get install xbacklight

# increase 10% brightness
xbacklight -inc 10
# decrease 10% brightness
xbacklight -dec 10
```

Use ```gnome-tweak-tool``` to define hotkey,

Fn key is not working when set hotkey,

Windows key can be the replacement.

```
Super+F5: xbacklight -dec 10
Super+F6: xbacklight -inc 10
```

#### Power management
```
sudo apt-get install powertop
sudo powertop --html
```

Place all tuning items to /etc/rc.local optimize on startup.

## PCMAN font
English: [Droid Sans Mono](https://github.com/powerline/fonts)

Chinese: [LiHei Pro](https://code.google.com/p/kingfont/downloads/detail?name=LiHei%20Pro.ttf)

## Ubuntu Theme
Numix

Install numix-folder makes gnome more beautiful

```
sudo apt-add-repository ppa:numix/ppa
sudo apt-get update
sudo apt-get install numix-icon-theme numix-icon-theme-circle numix-icon-theme-shine numix-icon-theme-utouch numix-folder
sudo apt-get install numix-gtk-theme

# change settings
gnome-tweak-tool
```

## XiaoMI Wifi (mt7601U)
[Source code](https://github.com/porjo/mt7601)

```
lsusb
cd ./DPO_MT7601U_LinuxSTA_3.0.0.4_20130913/
vim ./common/rtusb_dev_id.c

# add
{USB_DEVICE(0x2717,0x4106)}, /* XiaoMi wifi */

vim ./sta/sta_cfg.c

# modify
snprintf(extra, size, "Driver version-%s, %s %s\n", STA_DRIVER_VERSION, __DATE__, __TIME__ );
to
snprintf(extra, size, "Driver version-%s, (date and time removed for sanity)\n", STA_DRIVER_VERSION );

vim ./os/linux/rt_linux.c

# modify
pOSFSInfo->fsuid = current_fsuid();
pOSFSInfo->fsgid = current_fsgid();
to
pOSFSInfo->fsuid = (int )&current_fsuid();
pOSFSInfo->fsgid = (int )&current_fsgid();

make
sudo make install
sudo modprobe mt7601Usta
```

## System font 
```
gnome-tweak-tool
# Appearence -> Fonts
# Default font: LiHei 11
# Document font: LiHei 11
# Monospace font: Droid Sans Mono 13
# Windows title font: Hack Bold 11
```

## System default directory
```
vi ~/.config/user-dirs.dirs

# To be
# XDG_DESKTOP_DIR="$HOME/Desktop"
# XDG_DOWNLOAD_DIR="$HOME/Downloads"
# XDG_TEMPLATES_DIR="$HOME/Templates"
# XDG_PUBLICSHARE_DIR="$HOME/Public"
# XDG_DOCUMENTS_DIR="$HOME/Documents"
# XDG_MUSIC_DIR="$HOME/Music"
# XDG_PICTURES_DIR="$HOME/Picture"
# XDG_VIDEOS_DIR="$HOME/Movie"
```

After modification, must create those directories.
Re-login.

# Remark
Linode: 139.162.21.238
