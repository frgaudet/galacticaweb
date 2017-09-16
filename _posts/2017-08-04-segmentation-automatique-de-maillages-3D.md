---
title: SAM-3D - Segmentation automatique de maillages 3D

categories: works
background-image: background.jpg
excerpt: ""
author: jmfavreau
---

# Objectif du projet

L'objectif du projet est de proposer une approche de segmentation en régions
fonctionnelles et géométriques distinctes d'objets 3D utilisées au quotidien
par des usagers non experts. En particulier, on s'intéressera à proposer des
solutions fonctionnelles sur des données réalistes, souvent ignorées par les
approches scientifiques et logiciels du commerce. Parmi les nœuds techniques
identifiés, on peut citer le cas des maillages à triangles non homogènes, les
configurations où la topologie n'est pas une surface, ou encore l'hétérogénéité
des formes traitées (depuis les primitives simples jusqu'aux formes moins
mathématiques). La problématique de la rapidité de l'algorithme est également
un problème central que nous souhaitons considérer, tout en intégrant des
moyens simples pour l'utilisateur d'interagir avec la méthode.


# Résumé du projet

La segmentation de maillages 3D en zones géométriques distinctes est une
problématique centrale en traitement des maillages. Avec l'émergence des
solutions d'impression 3D, le besoin d'outils intuitifs de manipulation de ces
données est devenu essentiel.

Dans ce projet, on souhaite proposer un outil d'assistance à la segmentation
de maillages en régions géométriquement distinctes. Cette problématique est
centrale, généralement à la base de toute manipulation plus complexe des
maillages. Une approche type « outil d'assistance » permet ici de séparer le
savoir-faire en traitement géométrique des maillages du côté algorithmique,
tout en laissant à l'utilisateur l'opportunité d'ajuster au contexte
applicatif les résultats produits par le système.

En particulier, on souhaite proposer un outil qui puisse prendre en charge les
données telles qu'elles sont partagées aujourd'hui sur internet, sans pré-
requis important sur leur qualité géométrique. On se concentrera
majoritairement sur les formes géométriques dites « conçues par ordinateur »
(CAO), lesquelles sont issues de modèles paramétriques composés
essentiellement de formes géométriques aux propriétés mathématiques
raisonnables.
On s'intéressera également à proposer des méthodes où le temps de calcul est
raisonnable pour une utilisation quotidienne.

Ce projet fait l'objet d'un soutien de la part de la région Auvergne sous la
forme d'une Bourse Innovation Transfert.

# Descriptif des ressources
1 serveur de calcul
* 8Go RAM
* 4 VCPU
* 80Go Disque

# Descriptif des logiciels et jeux de données

Logiciels développés pour le projet, et utilisant les librairies:
* CGAL
* Eigen3
* libigl
Données fournies par l'entreprise partenaire (Polymagine); maillages 3D.

# Descriptif des requêtes et du déroulement des expérimentations

Expérimentations autour de la segmentation non supervisée, du transfert de
segmentation, de la co-segmentation.

# Description de la procédure d'exécution

Scripts bash pour automatiser l'exécution.

# Résultats attendus
A venir...
