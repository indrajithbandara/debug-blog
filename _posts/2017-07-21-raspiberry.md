---
layout: post
title:  "Raspiberry - Configurações iniciais"
date:   2017-07-21 18::01 -0300
categories: blog
---

## Como deixar o raspberry pi nas pontas dos casfcos pra desenvolver

#### Trocar dns e o mtu
fconfig eth0 mtu 1420

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
$ sudo apt-get install omxplayer 
* se nao funfar chmod 777 /dev/vchiq)

#### Node 8x e npmm atualizados
curl -sL https://deb.nodesource.com/setup_8.x | sudo bash -
sudo apt-get install nodejs -y



### Vim
$ sudo apt-get install git exuberant-ctags ncurses-term curl
$ pip3 install --user --upgrade neovim
Download your own vimrc file at http://www.vim-bootstrap.com

vim: mv ~/Downloads/generate.vim ~/.vimrc

vim +PlugInstall +qall



$ vim +PlugInstall


