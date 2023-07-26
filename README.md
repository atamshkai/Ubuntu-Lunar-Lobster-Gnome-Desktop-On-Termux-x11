# Ubuntu-Lunar-Lobster-Gnome-Desktop-On-Termux-x11

This is a preinstalled Ubuntu Lunar Lobster Distro with Gnome Desktop.It also contains windows 7 pro,libreoffice,vscode and etc.For Android 12 & 13,before you install it,disable phantom process killer. 

[Watch Video Here](https://youtu.be/UxmQSETvAOc) 

## Preview 

![](https://raw.githubusercontent.com/atamshkai/Ubuntu-Lunar-Lobster-Gnome-Desktop-On-Termux-x11/main/lunar-gnome.jpg) 

![](https://raw.githubusercontent.com/atamshkai/Ubuntu-Lunar-Lobster-Gnome-Desktop-On-Termux-x11/main/windows7.jpg)

# To Do 

#### First,Download Ubuntu Distro From Here. (1.7 GB)
[Download](https://archive.org/download/atamshkai-lunar-kde/lunar-gnome.tar.xz) 

## Installation 
Download lunar-gnome.tar.xz to Device's Download folder first. 

### Install zsh 
``` 
pkg up -y && pkg i -y zsh wget
wget https://github.com/atamshkai/Termux-Zsh/raw/main/zsh.tar.xz 
tar -xvJf zsh.tar.xz && mv ~/zsh/.* ~/
rm -rf ~/zsh
chsh -s zsh 
```

#### For Sound, 
``` 
echo "killall pulseaudio &>/dev/null" >>~/.zshrc 
``` 
```
echo "pulseaudio --start --exit-idle-time=-1; pacmd load-module module-native-protocol-tcp auth-ip-acl=127.0.0.1 auth-anonymous=1" >>~/.zshrc 
```

#### Install needed packages 
``` 
pkg up -y && pkg i -y x11-repo && pkg i -y proot-distro pulseaudio termux-x11-nightly 
``` 

#### Give Storage Permission

``` 
termux-setup-storage 
```

### Add lunar-gnome to proot-distro
```
echo "DISTRO_NAME='Lunar Gnome (lunar-gnome)'" >>~/../usr/etc/proot-distro/lunar-gnome.sh
```

### Restore Lunar Lubster Gnome Distro
```
proot-distro restore /sdcard/download/lunar-gnome.tar.xz 
``` 
``` 
exit 
``` 

#### Login again to terminal 
Before login to proot,start termux-x11 first. 
``` 
termux-x11 :1 &
``` 

#### Then,add lunar-gnome to ~/../usr/bin
``` 
echo "proot-distro login lunar-gnome --shared-tmp --bind /dev/null:/proc/sys/kernal/cap_last_cap" >>~/../usr/bin/lunar-gnome
```
```
chmod +x ~/../usr/bin/lunar-gnome
```

#### Start Lunar Lubster Gnome Distro
```
lunar-gnome
```

#### Start Desktop
``` 
export XDG_CURRENT_DESKTOP=GNOME
export PULSE_SERVER=127.0.0.1
export DISPLAY=:1
export XDG_SESSION_TYPE=x11
service dbus start
sleep 3
gnome-shell --x11 --sm-disable &
``` 
OR 
``` 
gnome &>/dev/null
``` 
### Warning 
If you upgrade the system,the desktop will fail to launch. 

##### Fix it if you get black screen error
``` 
for file in $(find /usr -type f -iname "*login1*"); do 
mv -v $file "$file.back"
done
``` 
``` 
echo "chmod u+s /usr/lib/dbus-1.0/dbus-daemon-launch-helper" >>~/.bashrc 
``` 
``` 
mv -v /usr/share/applications/gnome-sound-panel.desktop /usr/share/applications/gnome-sound-panel.desktop.back 
``` 
``` 
echo "export XDG_CURRENT_DESKTOP=GNOME" >>~/.bashrc 
``` 
Login again 
``` 
exit 
``` 


## Termux 
[Download](https://github.com/termux/termux-app/releases/download/v0.118.0/termux-app_v0.118.0+github-debug_universal.apk) 

## Termux-x11 
[Download](https://archive.org/download/termux-x11/app-universal-debug.apk) 

## Termux-x11 Custom Resolution
1920:1080


