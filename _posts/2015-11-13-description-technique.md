---
title: Description technique de la plateforme
categories: platform
background-image: background.jpg
excerpt: ""
author: fred
---

# Description générale
La plateforme GALACTICA est un cluster présentant une puissance de calcul totale de 80 coeurs (160 avec l’hyperthreading) à 2,40 GHz, 1,2 To de RAM et une capacité de stockage brute de 130 To. Le cluster est composé d’éléments de calcul et de stockage dont voici les caractéristiques principales :

# Compute nodes
Ces nœuds sont des Dell R630, aujourd’hui au nombre de 5. Chaque nœud est équipé de 2 processeurs Intel Xeon E5 2630 de 8 cœurs. Ce qui porte la capacité à 16 cœurs par noeuds.

L’OS est installé sur deux disques en RAID 1, nous disposons en outre de 6 To de stockage local.

* Bi Xeon E5-2630
* 256 Go RAM
* 2 Disques SAS 300 Go 15K RPM
* 6 disques SAS 1To 7200 RPM

# Stockage Ceph
* Les nœuds de stockage sont des Dell R730Xd. Nous en avons 3. Ils sont équipé de 2 processeurs Intel Xeon E5 2630, de 8 cœurs chacun. L’OS est déployé sur deux disques rapides de 300 Go en RAID 1, tandis que le stockage proprement dit se réparti sur 24 disques de 1,8 To chacun. Ce qui porte la capacité brute de chaque noeud à près de 43 To.

* Bi Xeon E5-2630
* 64 Go RAM
* 2 disques SAS de 300 Go 15K RPM
* 24 disques SAS de 1,8 To 7200 RPM


# Serveurs d’infrastructure

5 serveurs d’infrastructures (2*Dell R430 et 3*R630) sont également utilisés afin de fournir les services de gestion du cluster, d’interconnexion avec l’extérieur (proxys) ainsi que de supervision/benchmarking.

Tous ces éléments sont interconnectés grâce à un réseau full 10G.