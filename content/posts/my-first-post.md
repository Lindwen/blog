---
title: "Les différentes technologies de conteneurisation"
date: 2023-06-08T10:12:37+02:00
draft: false
tags:
  - docker conteneur lxc chroot systemd-nspawn
---

Nous voulons faire un conteneur dans lequel nous allons pouvoir lancer le jeu snake.

### Via CHROOT

1- Installation des paquets nécessaires :

```bash
sudo apt install binutils debootstrap
```

2- Créations des dossiers nécessaires :

```bash
mkdir ./exo1
mkdir ./exo1/bin
mkdir ./exo1/lib
mkdir ./exo1/lib64/
```

3- Copie des fichiers nécessaires pour le binaire bash :

```bash
cp /usr/bin/bash ./exo1/bin # exécutable
ldd ./exo1/bin/bash # affiche les dépendances de bash
cp /lib/x86_64-linux-gnu/libtinfo.so.6 ./exo1/lib/
cp /lib/x86_64-linux-gnu/libdl.so.2 ./exo1/lib/
cp /lib/x86_64-linux-gnu/libc.so.6 ./exo1/lib/
cp /lib64/ld-linux-x86-64.so.2 ./exo1/lib64/
```

4- Copie des fichiers nécessaires pour le binaire msnake :

```bash
cp /home/lindwen/msnake ./exo1/bin/ # exécutable
chmod +x /exo1/bin/msnake # on le rend exécutable
ldd /exo1/bin/msnake # affiche les dépendances de msnake
cp -r /lib/terminfo ./exo1/lib/
cp /lib/x86_64-linux-gnu/libncurses.so.6 ./exo1/lib/
cp /lib/x86_64-linux-gnu/libtinfo.so.6 ./exo1/lib/
cp /lib/x86_64-linux-gnu/libc.so.6 ./exo1/lib/
cp /lib64/ld-linux-x86-64.so.2 ./exo1/lib64/
```

5- On lance le chroot :

```bash
sudo chroot exo1 msnake
```