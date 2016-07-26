---
title: Debian Post-install
author:
- Sergio Alvariño <salvari@gmail.com>
tags: [Pandoc, Documentación, makefile, git]
date: julio-2016
lang: es-ES
abstract: |
  Instalación de Debian
  
  Solo para referencia rápida y personal.
---

# Introducción

Comentar los problemas con calentamiento en Ubuntu

Comentar la creación de usb bootable
Instalación

Aptitude


firmware-linux-nonfree
Bumblebee-nvidia primus

Instalado pandoc descargando paquete FALTA DESCARGAR PLANTILLAS

Instalado emacs desde aptitude emacs

Instalado chrome añadiendo fuentes a aptitude, hay que borrar el fichero que sobra. chrome

comentado cdrom en sources.list

Instalado keepass2

Instalado terminator

Instalado git desde aptitude

configurado d-apt, instalados todos los programas incluidos

gimp ya estaba instalado, instalado el gimp data-extra

solventado deb multimedia
sudo apt-get -y --allow-unauthenticated install --reinstall deb-multimedia-keyring

sudo apt-get install libav-tools

sudo apt-get install faad gstreamer0.10-ffmpeg gstreamer0.10-x
gstreamer0.10-fluendo-mp3 gstreamer0.10-plugins-base
gstreamer0.10-plugins-good gstreamer0.10-plugins-bad
gstreamer0.10-plugins-ugly ffmpeg lame twolame vorbis-tools
libquicktime2 libfaac0 libmp3lame0 libxine2-all-plugins libdvdread4
libdvdnav4 libmad0 sox libxvidcore4 libstdc++5

sudo apt-get install w64codecs

sudo apt-get install rar unrar zip unzip unace bzip2 lzop p7zip p7zip-full p7zip-rar

Desarrollo sw

sudo apt-get install build-essential checkinstall make automake cmake autoconf git git-core dpkg wget
Instalado apt-d y todos los programas asociados

Open Java

apt-get install openjdk-7-jre icedtea-7-plugin

compresores

Disk manager
apt-get install ntfs-3g disk-manager

apt-get -t jessie-backports install gnucash

apt-get install rsync grsync

# Docker
apt-get install apt-transport-https ca-certificates
apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
edit docker.list with
deb https://apt.dockerproject.org/repo debian-jessie main

apt-cache policy docker-engine   -- comprobamos que todo está bien.


sudo apt-get install docker-engine   -- da un error en makedev por udev activo


sudo service docker start

sudo docker run hello-world   - todo bien

sudo gpasswd -a salvari docker


apt-cache policy inkscape
apt-get -t jessie-backports install inkscape

apt-get install librecad

apt-get -t jessie-backports install freecad

Instalado calibre


TODO

zsh
krita
mypaint

Cambiar lenguaje
/etc/locale-gen
sudo locale-gen

Inkscape
https://elizsarobhasa.makes.org/thimble/MTMwNDIzMjE5Mg==/3d-printing-from-a-2d-drawing
Instalar tb jessyink

LaTeX Vanilla

tor
openframeworks

chibios
* http://wiki.chibios.org/dokuwiki/doku.php?id=chibios:community:setup:openocd_chibios
* http://www.josho.org/blog/blog/2014/11/30/nucleo-gcc/
* http://www.stevebate.net/chibios-rpi/GettingStarted.html



Cuentas online abiertas

google
pocket (plugin de chrome) 

