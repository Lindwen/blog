---
title: "Résoudre bug de lancement de Farming Simulator 17 sur processeur Intel gen 12"
date: 2023-06-11T08:02:00+02:00
draft: false
tags:
  - bug
  - farming simulator
  - intel processor
---

# Farming Simulator 17
## Solution au problème de connexion de Farming Simulator 17 sur STEAM avec un processeur Intel de 12e génération

Si vous rencontrez des problèmes de connexion avec votre jeu Farming Simulator 17 sur STEAM, spécialement avec un processeur Intel de 12e génération.
Vous devez créer une règle sortante dans le pare-feu Windows pour bloquer TOUTES les connexions de l'application du jeu.

Voici les étapes à suivre :

1. Ouvrez "Pare-feu Windows Defender avec fonctions avancées de sécurité" et accédez à la page "Règles de trafic sortant" dans le menu de gauche.
2. Créez une nouvelle règle sortante :
   2.1. Type de règle : Programme
   2.2. Programme : sélectionnez le fichier .exe du jeu dans le répertoire de Steam (`\Steam\steamapps\common\Farming Simulator 17\x64\FarmingSimulator2017Game.exe`)
   2.3. Action : Bloquer la connexion
   2.4. Profil : tous sélectionnés (Domaine, Privé, Public)
   2.5. Nom : Farming Simulator 2017 - Patch Bug Intel gen12

Cette règle bloque toutes les connexions sortantes de l'application du jeu. Donc le multijoueur ne fonctionnera pas.
Pour résoudre ce problème, vous devez ajouter une exception à cette règle pour autoriser les connexions sortantes vers le site web farming-simulator.com.

3.Cliquez sur propriétés, allez à la page "Étendue".
4. Dans l'option "Adresse IP distante", sélectionnez "Ces adresses IP" et cliquez sur Ajouter...
5. Dans la zone "Cette adresse IP ou ce sous-réseau", insérez l'adresse IP du site web farming-simulator.com (195.201.15.2).
   5.1. Vous pouvez vérifier l'adresse IP de ce site en utilisant l'invite de commande (CMD) avec la commande : `ping farming-simulator.com`
6. Cliquez sur Appliquer et sur OK.

Maintenant, votre Farming Simulator démarrera normalement et le mode multijoueur fonctionnera également.

N'oubliez pas que cette solution est spécifique aux problèmes de connexion rencontrés avec un processeur Intel de 12e génération.
