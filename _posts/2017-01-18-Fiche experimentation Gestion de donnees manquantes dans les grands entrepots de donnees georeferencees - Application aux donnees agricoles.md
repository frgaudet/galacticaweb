---
title: Gestion de données manquantes dans les grands entrepôts de données géoreférencées - Application aux données agricoles.
categories: works
background-image: background.jpg
excerpt: ""
author: nkouyea
---

# Objectif
Estimer les valeurs manquantes dans un contexte où le volume de donnés est relativement élevé, est une opération coûteuse. Dans beaucoup de cas l’opération est faite en dehors de la base de données, ce qui suppose la lecture et le stockage en mémoire des données.
L’objectif ici est de comparer les coûts d’estimation des valeurs manquantes grâce au moteur de base de données cassandra (Intra base de données) et Spark (en dehors de la base de donnés ). Sachant que le coût d’estimation avec Spark intègre le coût de lecture des données.

# Implémentation
Un cluster Cassandra (Cassandra-stack-nestor) constitué de 4 instances dont un seeder et de 3 slaves a été mis sur pieds sur la plateforme Galactica. Dans laquelle nous avons chargé les données issues des expériences sur la mesure des poids des animaux. Les bruits sont artificiellement introduits en supprimant certaines valeurs. L’idée étant de tester les performances de nos algorithmes d’estimation.
La première implémentation est faite en utilisant les User Defined Function (UDF) et les User Defined Aggregated (UDA). Le script d’estimation est chargé à partir du seeder et nous mesurons les temps d’exécution d’abord dans le cas où tous les noeuds ont la même copie des données (Replication) ensuite dans le cas où les données sont partitionnées sur les différents noeuds (Sharding).
La second phase encours sera de tester les performances en utilisant spark et en lisant les même données dans cassandra.

# Descriptif des ressources

1 machine master (gabarit m1.medium) 

 + 4 CPU (XEON E5-2630 2.4GHz)
 + RAM:8GB
 + Disque dur de 80 GB

3 machines workers (gabarit q1.large), avec pour chaque machine :

 + 4 CPU (XEON E5-2630 2.4GHz) 
 + RAM:8GB
 + Disque dur de 80 GB
