---
layout: post
title:  "Pequenos tutoriais - Raspiberry, Servidor e etc"
date:   2017-07-21 18::01 -0300
categories: blog
---

#### Trocar dns e o mtu
fconfig eth0 mtu 1420

#### Iniciar programas
$ cd ~/.config/autostart $

$ vim chromium.desktop
```
[Desktop Entry]
Name=programname
Exec=lxterminal –e “home/pi/yourprogram”
Type=Application
```
#### Programas
$ sudo apt-get install xpdf

https://neverbenever.wordpress.com/2015/02/11/how-to-autostart-a-program-in-raspberry-pi-or-linux/

#### Audio
$ sudo apt-get install omxplayer
$ sudo chmod 777 /dev/vchiq


$ vim +PlugInstall
