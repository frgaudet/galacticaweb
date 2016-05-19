---
title: Cluster Rulnet
categories: works
background-image: background.jpg
excerpt: ""
author: ccepeda
---
# Objectif du projet "RulNet"
Disposer d'un cluster de calcul pour l'application web externe [RulNet](rulnet.isima.fr), dont l'objectif est d'inférer différents types de règles à partir d'un grand volume de données et dont l'application principale est la génération de réseaux biologiques à partir de données "omiques".

# Résumé du projet
[RulNet](rulnet.isima.fr) est une application en ligne permettant à ses utilisateurs de découvrir différents types de règles à partir d'une base de données ou de fichiers de données transmis, puis de visualiser ces règles sous forme de réseaux directement sur l'application ou via d'autres outils comme par exemple Cytoscape. La particularité de cet outil est l'utilisation d'un langage de requêtes simple nommé RQL.

Une règle est de la forme X=>Y, où X et Y sont des ensembles de variables et reflète ainsi une relation entre ces variables. L'utilisateur définit grâce au langage RQL quel type de relations l'intéresse. Par exemple G1,G2=>G3 peut avoir comme signification qu'une délétion des gènes G1 et G2 implique systématiquement un niveau d'expression faible pour G3.

Une fois que l'utilisateur a spécifié sa (ou ses) requête RQL correspondant au type de relations qui l'intéressent, celle-ci est réécrite dans un langage de requête classique permettant de récupérer directement les données utiles pour l'inférence des règles.

Pour plus de détails, consultez la [documentation de RulNet](http://rulnet.isima.fr/guide.html).

# Descriptif des ressources
- 1 machine master (gabarit *m1.medium*) :
    -  2 CPU (XEON E5-2630 2.4GHz)
    -  RAM : 4 GB
    -  Disque dur de 40 GB


- 2 machines workers (gabarit *h1.large*), avec pour chaque machine :
    - 4 CPU (XEON E5-2630 2.4GHz)
    - RAM : 16 GB
    - Disque dur de 80 GB

# Descriptif des logiciels et jeux de données utilisés
- Cluster Spark 1.5.1 (API Java) sur Ubuntu Server
- Librarie Spark MLlib

Les données transmises au cluster ont toujours le même format. Leur taille varie en fonction de la taille des données utilisateur (pouvant être très grande pour les données omiques) et de leurs requêtes.

# Descriptif des requêtes
Voici les opérations réalisées pour le projet RulNet :

| N° | Description |
|-|-|
|1| Transformation des données d'entrée en RDD (Resilient Distributed Dataset) |
|2| Recherche des itemsets fréquents |
|3| Génération des règles à partir des itemsets fréquents |
|4| Ecriture des règles dans des fichiers |

# Description de la procédure d'exécution
Les requêtes Spark sont archivées dans un fichier JAR. Cette archive et les données sont ensuite transmises à la machine master du cluster. Via une ligne de commande sur le master, un job est soumis au cluster Spark, avec pour arguments les fichiers transférés. L'application principale (master) lit le contenu de ces fichiers et lance le traitement Spark détaillé précédemment.

Les transferts de fichiers et l'exécution de la ligne de commande sont assurés par la librairie JSch. Cette librairie permet de se connecter à une machine distante par SSH et d'y réaliser différents types d'opérations.

# Résultats attendus
Les résultats consistent en une liste de règles avec différents paramètres qui seront ensuite traduites pour répondre à la requête initiale des utilisateurs.