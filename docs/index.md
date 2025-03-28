![Nanosat](figure0.png)  

# Meteorix

## Introduction

### Projet global

Meteorix est une mission CubeSat universitaire menée par plusieurs instances notamment le LIP6, le CNRS ou encore l’observatoire de Paris. La mission est dédiée à la détection et à la caractérisation des météores. L’objectif principal est d’obtenir une statistique robuste de l’entrée des météoroides et des débris spatiaux dans l’atmosphère terrestre.

Ces estimations permettent de quantifier l’apport de matière extraterrestre sur Terre et d’étudier les conséquences possibles en aéronomie ainsi que le risque de collisions avec les satellites artificiels lors des pluies de météores. La connaissance du flux de débris spatiaux apportera une contrainte supplémentaire pour les modèles de surveillance de l’espace développés dans les agences spatiales.

L’objectif technologique de la mission est la détection automatique des objets en temps réel à bord d’un CubeSat. Ces objectifs entrent parfaitement dans le gabarit d’une petite mission spatiale de type CubeSat 3 Unités développée par des étudiants à Sorbonne Université.

Le défi technique concerne les algorithmes de détection en temps réel des météores et, dans une moindre mesure, le contrôle de l’attitude (orientation) du satellite et sa capacité à transmettre une grande quantité de données. La détection des météores depuis l’espace est un atout essentiel pour s’affranchir des conditions météorologiques et pour couvrir une large zone du ciel.

### Notre mission

Le nanosatellite envoyé dans l’espace aura une unité de calcul et une caméra. Le système de capture de météore sera limité par une contrainte énergétique de 10W pour tout le fonctionnement du système, c’est-à-dire capture de la vidéo, traitement et envoi des images.

Or un algorithme de détection efficace et satisfaisant la contrainte énergétique est déjà implémenté dans l’unité de calcul mais il fournit des images dont la qualité peut être largement améliorée en utilisant des méthodes modernes. Ce travail d’optimisation nous a été confié et est l’objectif principal de ce projet.

Pour cela nous utiliserons deux approches, la première consiste à récupérer les vecteurs issus de la compression pour essayer de détecter les zones d’intérêt d’une vidéo.

D’autre part, ces résultats pourront être utilisés pour l’autre approche qui est l’implémentation d’un réseau de neurones, FlowNet, qui permet de calculer le flot optique d’une vidéo.

De plus, une machine distante nous sera prêtée avec des propriétés similaires à l’unité de calcul qui sera envoyée dans l’espace dans le nanosatellite.