---
title: Algorithmes de corrélation
categories: works
background-image: background.jpg
excerpt: ""
author: nwagner
---

# Description du projet:
Le but des algorithmes de corrélation est de trouver le schéma fonctionnel global d’un système informatique depuis l’existant. 
Pour cela, on se base sur les communications entrantes et sortantes du système pour en déduire un processus métier. Les communications peuvent provenir de plusieurs sources telles que les logs, les emails, les notes internes, les factures, … 
Pour une entreprise, le fait de connaitre le schéma global de son système peut être très précieux. Par exemple, lorsqu’elle décide de l’améliorer, le fait d’en modifier une partie, peut avoir des conséquences globales imprévisibles. Avoir une vue générale, peut donc permettre à l’entreprise de prédire ces conséquences.

# But du projet:
Les algorithmes de corrélations ont déjà été implémentés sur un système Map-Reduce d’Hadoop, le but ici est de les implémenter sur un environnement Spark afin de comparer les performances entre les deux systèmes.

# Ressources utilisées:
Pour ce projet, j’ai utilisé un master et cinq workers de gabarit m1.medium, c’est à dire:

 - 2 vCPU (XEON E5-2630), 2.4GHz
 - 4GB de RAM
 - 40GB de disque dur

# Descriptif des algorithmes:
Pour ces algorithmes, on fait l’hypothèse que les données sont homogènes et normalisées. Ces données sont de la forme:

| N° | Attribut 1 | Attribut 2 | ... | An 
|-|-|-|-|-
| Message 1 | A | B | ... | m1An
| Message 2 | C | D | ... | m2An
| Message 3 | E | A | ... | m3An
| ... | | | |
|Message k | mkA1 | mkA2 | ... | mkAn |

Un message est un événement et un attribut est une caractéristique sur cet événement. Par exemple, un message peut être une ligne particulière dans les logs, ou bien une facture particulière, etc. Un attribut peut être un numéro de devis, un numéro de commande, un numéro de facture, un statu dans les logs, etc.

Le but de ces algorithmes est donc de regarder pour chaque paire d’attributs, si il y a un lien, c’est à dire une corrélation. Dans cet esprit, pour un site de vente en ligne, l’algorithme doit trouver une corrélation entre les attributs « devis » et « facture » et entre les attributs « factures » et « commande », car,  à partir d’un devis, en découle généralement une facture puis une commande. On en déduit ainsi, la liste des processus de notre système avec leur suite logique. C’est de cette manière que l’on peut trouver le schéma fonctionnel global d’un système informatique d’une entreprise.

Les algorithmes de corrélation se décomposent en deux grandes parties:
		
 1. Pour chaque paire d’attributs (Ai, Aj), il faut évaluer un critère de sélection qui déterminera si la corrélation entre ces deux attributs est pertinente ou non. Sans rentrer dans les détails, on doit utiliser des transformations « DISTINCTS » et des actions « COUNT ».
 
 2. Pour chaque paire d’attributs (Ai, Aj), il faut déterminer l’ensemble des couples de messages corrélés. Deux messages m1 et m2 sont corrélé si m1.Ai = m2.Aj. C’est à dire si la valeur de l’attribut i par le message 1 est égal à la valeur de l’attribut j par le message 2. Dans l’exemple ci-dessus, m1.A1 = m3.A2 = ‘A’, les messages 1 et 2 sont donc corrélés par les attributs 1 et 2. Cette étape nécessite des transformations de type « JOIN » et « GROUPBY ». 
Ensuite, il faut calculer la fermeture transitive de ces couples de messages. Pour cela, l’algorithme utilise des opérations de jointure. Un foi que l’on a les fermetures transitives, on regarde leur taille et selon les critères calculés en (1), on décide si oui ou non, la corrélation peut être retenue.
	

# Descriptif des tests:	
Pour effectuer ce test, j’ai eu besoin d’exécuter plusieurs fois l’algorithme sur un jeu de données de plus en plus gros.

Le jeux de données était un CSV enregistré dans HDFS, il comportait 17 attributs différents.

Le test a été effectué sur ce jeu de données avec 200.000 lignes, puis 400.000, puis 600.000, …, jusqu’a atteindre 1.8 M de lignes. 

# Résultats et conclusion:
Les tests ont montré que pour cet algorithme, Spark et Map-Reduce sont équivalents en temps de calculs. Cela vient du calcul des fermetures transitives qui nécessitent des jointures à répétitions, cette transformation est en effet très lourde à effectuer pour Spark.