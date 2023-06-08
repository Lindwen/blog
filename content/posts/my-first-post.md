---
title: "Jouer au snake dans un chroot"
date: 2023-06-08T10:12:37+02:00
draft: false
tags:
  - chroot
---

# Chroot

## Petit point historique :

- Unix V1 -- 1971
Très limité. Première version en assembleur sur le PDP-11/20

- Unix v4 – 1973
Première version écrite en C, conçu pour l’occasion

- Unix v6 -- 1975
Première version disponible en dehors des Bell Labs

- Unix v7 --  1979
Dernière version développée aux Bell Labs. Contient l’appel système chroot()

## Principes et idée

Le but du chroot est d'enfermer dans une arborescence un processus.
Cette arborescence ne contient que les fichiers dont le processus a besoin.

## Exemple avec le processus créé par /bin/bash

Qu'avons nous besoin ?
- le fichier /bin/bash
- Les bibliothèques partagées utilisées par /bin/bash
- Les fichiers de configuration du programme
- Et très souvent, la table de correspondance UID/User (/etc/passwd)

Création d'un dossier qui va contenir notre chroot :
```bash
mkdir ./chroot
```

Pour afficher les librairies nécessaires au programme /bin/bash il faut utiliser la commande :
```bash
ldd /bin/bash
```

Le retour de la commande :
```bash
linux-vdso.so.1 (0x00007ffe8e5e7000)
libtinfo.so.6 => /lib/x86_64-linux-gnu/libtinfo.so.6 (0x00007eff9379a000)
libdl.so.2 => /lib/x86_64-linux-gnu/libdl.so.2 (0x00007eff93794000)
libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007eff935bf000)
/lib64/ld-linux-x86-64.so.2 (0x00007eff93907000)
```

Nous allons devoir donc copier toutes les dépendances au bon endroit :
En premier nous devons créer les répertoires contenant nos librairies
```bash
mkdir ./chroot/lib
mkdir ./chroot/lib64
mkdir ./chroot/bin
```

Dans le dossier bin nous allons copier l'exécutable /bin/bash :
...