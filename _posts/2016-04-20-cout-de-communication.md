---
title: MIND, coût de communication dans les systèmes d’intégration de données
categories: works
background-image: background.jpg
excerpt: ""
author: abelghoul
---

# Résumé du projet

Il s’agit d’étudier les paramètres physiques qui influencent le coût communication de données dans un système d’intégration de données. Les paramètres étudiés sont les tailles du fetch et du message de données. Pour les expérimentations, trois machines ont été implémentées sur la plateforme GALACTICA, une VM cliente, une MV pour la médiation et la troisième VM est une source de données. 

# Descriptif des ressources utilisées

* Disque dur du médiateur et la machine client : 250 GB de 7200 RPM
* Disque dur de la source de données : 250 GB de 10 000 RPM
* CPU : 2 CPU (XEON E5-2630 2.4GHz)
* Mémoire : 8 GB
* Descriptif des logiciels et jeu de données utilisés :
* OS Ubuntu 12.04 LTS
* SGBD Oracle 11.2g
* Jeu de données PT1.1 du LSST

# Descriptif des requêtes et du déroulement des expérimentations
Requêtes exécutées :

|N°|Requêtes|Taille résultat (tuple)|Taille tuple (byte)|Volume|
---|---|---|---|---
Q1|SELECT objectid, taimidpoint, psfflux  FROM source|164 989 538|27|4,5 GB
Q2|SELECT objectid, ra_ps, decl_ps FROM object|4 012 341|29|110 MB
Q3|SELECT objectid, taimidpoint, psfflux  FROM source order by objectid|164 989 538|27|4,5 GB
Q4|SELECT objectid, taimidpoint, psfflux  FROM source WHERE ra_ps between 0.5 and 3 and decl_ps between -0.5 and 4||27|
Q5|SELECT count(objectid) FROM source|1|11|11 Bytes
Q6|SELECT objectid, sourceid, ra, decl, taimidpoint, psfflux  FROM source|164 989 538|54 |9 GB
Q7|SELECT * FROM source|164 989 538|205|31 GB

# Déroulement des expérimentations
* Valeurs du SDU
1430 bytes, 2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30 et 32 Kb  (17 config.)

* Valeurs du Fetch size (37 config.)
110, 220, 330, 440, … 990 tuples  (pas de 110 tuples)
1 100, 2 200, 3 300, … 9 900 tuples (pas de 1100 tuples)
11 000, 22 000, 33 000, … 99 000 tuples (pas de 11 000 tuples)
1 10 000, 2 20 000, 3 30 000, … 1 100 000 tuples (pas de 110 000 tuples)

# Canevas des résultats
Le nombre de configurations exécutées est le produit cartésien des configurations de SDU size et Fetch size, ceci qui donne 629 configurations (SDU, Fetch). Chaque configuration est exécutée 10 fois. Le total des exécutions pour une requête = 6 290 exécutions.  Un calcul de la moyenne de chaque configuration est effectué et le résultat est obtenu selon le schéma du tableau suivant : 

|SDU|Fetch|Elapsed|CPU|Comtime|#pkW0|TotimeW0|W0|MaxW0|#pkW1|totimeW1|W1|MaxW1|
---|---|---|---|---|---|---|---|---|---|---|---|---
xxx|xxx|xxx|xxx|xxx|xxx|xxx|xxx|xxx|xxx|xxx|xxx|xxx

# Description de la procédure d’exécution des requêtes 

Un script Shell est exécuté sur la machine appelée client. Ce script contient l’ensemble de configuration du SDU, du fetch ainsi que le nombre d’itération de chaque configuration. Le script réalise les tâches suivantes :

* Redémarrer les bases de données au niveau du médiateur et la source de données et flasher la mémoire de leurs systèmes d’exploitation
* Fixer une taille du SDU et commence à varier la taille du Fetch. Cette opération est faite 10 fois, selon le nombre d’itération fixé  à 10 itérations. 
* Analyser le fichier trace de chaque exécution de la requête aux niveaux du médiateur et la source de données. Dans cette analyse permet une extraction des données de l’exécution et de les écrire dans un fichier data.csv. 
* Changer la taille du SDU suivant qui sera effectué au niveau du médiateur et exécuter la tâche (2).
* A la fin de l’exécution d’une requête, on aura le fichier data.csv qui contient les données des 6 290 exécutions + les 6 290 fichiers trace analysés. 