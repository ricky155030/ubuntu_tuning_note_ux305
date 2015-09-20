# Ubuntu Tweak Note
Tweak for Ubuntu 14.04

### Traverse windows from all work space
Change key mapping from <Super><Shift-w> to <Super>w
```
sudo apt-get install unity-tweak-tool
unity-tweak-tool
```

### PCMAN font
English: Droid Sans Mono (Download from github: powerline-font)

Chinese: [LiHei Pro](https://code.google.com/p/kingfont/downloads/detail?name=LiHei%20Pro.ttf)

### Ubuntu Gnome Theme
Numix

Install numix-folder makes gnome more beautiful

```
sudo apt-add-repository ppa:numix/ppa
sudo apt-get update
sudo apt-get install numix-icon-theme numix-icon-theme-circle numix-icon-theme-shine numix-icon-theme-utouch numix-folder
sudo apt-get install numix-gtk-theme

# change settings
unity-tweak-tool
```

### XiaoMI Wifi (mt7601U)
[Source code](https://github.com/porjo/mt7601)
```
$ lsusb
$ cd ./DPO_MT7601U_LinuxSTA_3.0.0.4_20130913/
$ vim ./common/rtusb_dev_id.c

### add
{USB_DEVICE(0x2717,0x4106)}, /* XiaoMi wifi */

$ vim ./sta/sta_cfg.c

### modify
snprintf(extra, size, "Driver version-%s, %s %s\n", STA_DRIVER_VERSION, __DATE__, __TIME__ );
to
snprintf(extra, size, "Driver version-%s, (date and time removed for sanity)\n", STA_DRIVER_VERSION );

$ vim ./os/linux/rt_linux.c

### modify
pOSFSInfo->fsuid = current_fsuid();
pOSFSInfo->fsgid = current_fsgid();
to
pOSFSInfo->fsuid = (int )&current_fsuid();
pOSFSInfo->fsgid = (int )&current_fsgid();

$ make
$ sudo make install
$ sudo modprobe mt7601Usta
```

### Add startup program 
```
gnome-session-config
```

### System font 
```
unity-tweak-tool
# Appearence -> Fonts
# Default font: LiHei 11
# Document font: LiHei 11
# Monospace font: Droid Sans Mono 13
# Windows title font: Hack Bold 11
```
