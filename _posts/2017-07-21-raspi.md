---
layout: post
title:  "Raspiberry - Configurações iniciais"
date:   2017-07-21 18::01 -0300
categories: blog
---

## Como deixar o raspberry pi nas pontas dos casfcos pra desenvolver

#### Add usuario
$ sudo adduser rx
$ sudo adduser rx sudo


#### Trocar dns e o mtu
$ sudo ifconfig eth0 mtu 1420

#### Iniciar programas
$ cd ~/.config/autostart
$ vim chromium.desktop
```
[Desktop Entry]
Name=Chromium-Browser
Exec=chromium-browser
Type=Application

```
#### Programas (opcionais)
$ sudo apt-get install xpdf

#### Node 8x e npmm atualizados
curl -sL https://deb.nodesource.com/setup_8.x | sudo bash -
sudo apt-get install nodejs -y


#### Erros
*Omxplayer
$ sudo chmod 777 /dev/vchiq
