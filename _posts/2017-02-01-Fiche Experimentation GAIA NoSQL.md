---
title: Extension en Surcouche d'un système NoSQL dans l'ecosystème Hadoop pour l'accès aux données d'Astronomie
categories: works
background-image: background.jpg
excerpt: ""
author: lyeh
---

# Objectif du projet:
Le but du projet est d'explorer les limites d'une approche d'extension en surcouche d'un système NoSQL pour traiter des opérateurs comme le cone search, distance en SQL sur les données volumineuses d'astronomie.

# Résumé du projet:

Dans le monde des systèmes NoSQL, de nombreux moteurs SQL orientés grandes mémoires ont été recement développés. Pour accélérer l'accès aux données des requêtes de sélections spatiales, et afin d'éviter de lire la totalité d'un lot de données, ces systèmes offrent la possibilité de partitionner les données afin de réduire le nombre de données lu sur disque. Cependant, ces systèmes trouvent rapidement une limite technique lorsque le nombre de partitions est très important et/ou de très petites tailles comme lors d'une décomposition en HealPix. En outre le partitionnement s'effectue sur des valeurs alphanumérique et non spatiale. Le nombre d'objets par partition peut varier grandement posant le problème d'équilibrage de charge des noeuds.

Pour cela, l'objectif est de combiner le paradigme Map-Reduce qui à l'aide d'un algorithme préservant l'équilibrage de charge, construit un lot de données partitionné en HealPix et équilibré sur une importante volumétrie. Puis, d'utiliser un moteur SQL orienté grande mémoire comme SparkQL ou Drill pour interroger les partitions relevants. Les partitions relevants sont determiné par la surcouche qui extrait de la requête utilisateur les prédicats spatiales pour formuler une nouvelle requête plus aiguisée. Nous explorons une approche en re-ecriture de requêtes pour:
1) ne pas être invasive vis à vis d'un quelconque système sous-jacent. Ainsi, le principe peut fonctionneer avec une large gamme de moteur SQL.
2) exécuter la jointure distance ou le cross-match en évitant le produit cartésien !

Cette optimisation physique par ré-écriture est à comparer avec d'autres approches, notamment avec une approche en cours d'étude qui consiste a étendre l'optimiseur SQL Catalyst au sein de Spark.

# Ressources utilisées:
Pour ce projet, une configuration minimaliste pour traiter les données GUMS11 serait:

1 machine master (gabarit m1.medium)
  - 2 vCPU (XEON E5-2630), 2.4GHz
  - RAM : 16-32 GB
  - Disque dur de 1 TO

4 machines slave (gabarit m1.medium)
  - 2 vCPU (XEON E5-2630), 2.4GHz
  - RAM : 16 GB
  - Disque dur de 250 G0

Pour mesurer le passage à l'échelle, le nombre de machines slaves pourra être multiplié par un facteur K en fonction des premières mesures. 

# Descriptif des logiciels et jeux de données:
FrameWork Hadoop >2.0, spark ≥ 2, Drill.

Les données transmises au cluster proviennent du projet Gaia. Nous chargerons également une partie des données du projet LSST.

# Descriptif des requêtes et du déroulement des expérimentations

Nous nous focalisons principalement sur deux types de requêtes Spatiales correspondant à l'équivalent d'un prédicat de sélection et de jointure en SQL mais au niveau spatiale. Il est possible de combiner ces trois requêtes entre eux ou avec des prédicats portant sur les valeurs alphanumériques. Comme le langage SQL est étendu avec une grande partie des fonctions existantes dans la librairie Healpix, il est possible d'exprimer des requêtes comme le regroupement en pixels Healpix.

### Requête Type 1 : Cone Search

Le cone Seach est à la base de beaucoup de requêtes, il permet de sélectionner une zone du ciel. Une telle requête est exprimable en SQL avec l'ajout d'opérateurs d'Astronomie. 
Mais dans l'approche en Surcouche, la requête est ré-écrite pour s'appliquer uniquement sur les partitions relevantes.

a) Exemple 1: ```SELECT id FROM gaia.root.`gums11/parquet/data/` WHERE angle(alpha, delta, 179,-54) < 0.01;```

La surcouche calcule les pixels Healpix puis sélectionne les partitions relevants, tout en produisant ré-écrivant la requête initiale.

b) Exemple 2 : ```SELECT id FROM gaia.root.`gums11/parquet/data/` WHERE HealPix(876543, 2, 'nested');```

Ici le surcouche de ré-écriture utilise la libraire Healpix pour calculer les pixels Healpix relevants. Puis il ré-écrite la requête en fonction des partitions issues de la phase Map-Reduce.

D'autres fonctions de la libraire Healpix sont également remontées au niveau du langage SQL étendu. Le moteur de ré-écriture effectue cette traduction par rapport aux données organisées sous Hadoop.

### Requête Type 2 : Jointure Distance

Drill et Spark QL effectue un produit cartésien lorsque deux tables sont liées par une condition autre que l'équi-jointure. Sur une importante volumétrie, ceci conduit à des temps de calcules très important. Pour éviter cela, une table de jointure qui récence l'ensemble des couples pouvant être joint à une distance D est pré-calculée par un job map-reduce. La surcouche ré-écrit les requêtes de jointure distance en faisant intervenir la table de jointure. 

* Exemple 3 : 
```SELECT id FROM gaia.root.`gums11/parquet/data/` G1, gaia.root.`gums11/parquet/data/` G2 WHERE G2.magGBp<0.02 and angle(G1.alpha, G1.delta, G2.alpha, G2.delta) < 0.01;```

D'autres requêtes seront exprimées sur la machine Galactica. 



# Description de la procédure d'exécution

La phase de partitionnement et de construction de méta-données sur les partitions sera déjà exécutée en MapReduce par une commande en ligne.

Formulation des requêtes ci-dessus ou d'autres sera faite à l'aide d'une commande Shell.

# Résultats attendus

Affichage des comparaisons de temps d’exécutions entre une approche de base (utilisation direct de Drill SQL et SparkQL) et l'optimisation apportée par la ré-écriture de requêtes d'Astronomie.
Ces comparaisons permets de mesurer l'accélération d'une approche qui s'appuie sur l'écosystème Hadoop.
