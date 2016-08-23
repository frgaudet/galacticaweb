---
title: g Bug
categories: platform
background-image: background.jpg
excerpt: ""
author: fred
---

# Description du bug :
Après avoir lancé une VM, puis ouvert une connection SSH, vous avez édité un fichier texte. Le premier caractère du fichier est remplacé par la lettre 'g'.

# OS concerné:
- Ubuntu 16.04 LTS (xenial)

# Tools: 
- vi 7.4.1689-3ubuntu1.1
- Mobaxterm 7.7 personnal edition

# Commentaire
A ma connaissance, le bug est fixé avec une version récente de vi, mais en attendant que la mise à jour atterisse dans les dépôts voici deux workarounds : vous pouvez utiliser putty plutôt que mobaxterm, ou bien utiliser l'éditeur nano plutôt que vi. 