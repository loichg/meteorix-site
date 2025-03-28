# Conclusion

Les objectifs du projet Meteorix permettent la détection efficace du mouvement dans les vidéos et l'amélioration de la qualité d'image à l'aide du réseau de neurone FlowNet. Grâce à l'intégration de ces technologies, nous avons pu isoler les parties pertinentes des séquences vidéo tout en améliorant visuellement les images.

## Impacts éthiques/sociétaux

**Préoccupations** :

- **Détournement à des fins militaires** : Il existe un risque d'utiliser la détection de météores dans des contextes de défense ou de guerre, ce qui pourrait mener à des applications militaires non souhaitées.
- **Manipulation des résultats** : Il y a une possibilité de fausser les résultats concernant la caractérisation des météores, ce qui pourrait compromettre leur étude et leur gestion.
- **Concurrence entre pays** : La compétition entre nations pour envoyer le plus grand nombre de nanosatellites pourrait mener à une nouvelle forme de guerre froide, générant ainsi une pollution accrue dans l'espace.

**Bienfaits** :

- **Réduction des déchets spatiaux** : Une meilleure compréhension des déchets spatiaux pourrait sensibiliser le public et les autorités, permettant ainsi de mieux les gérer et de réduire leur accumulation dans l'espace.
- **Optimisation de l'environnement spatial** : Remplacer les satellites traditionnels par des nanosatellites offrirait un environnement plus propre et permettrait d'optimiser l'utilisation de l'énergie, ce qui pourrait améliorer les résultats scientifiques.
- **Réduction de l'impact écologique** : Utiliser des matériaux en quantités limitées pour construire des nanosatellites permettrait de réduire la pollution liée à l'extraction des ressources naturelles nécessaires à leur fabrication.
- **Avancées technologiques** : La contrainte énergétique dans la conception des nanosatellites pousse à des innovations technologiques majeures, permettant d'effectuer une multitude d'opérations dans l'espace tout en utilisant peu de ressources.

## Pistes de recherche pour la suite

**Pour Motion Vector Extractor** :
1. Réessayer d'adresser le GPU Radeon (identique à la puce spatiale) pour des tests en conditions réelles
2. Développer une fonction multi-images pour vérifier la cohérence des vecteurs sur plusieurs frames
3. Étendre l'analyse PCA avec plus de vidéos testées
4. Implémenter un algorithme de type knapsack pour l'optimisation des zones d'intérêt

**Pour FlowNet** :
1. Tester FlowNet2 avec ses architectures optimisées
2. Réentraîner FlowNetCorr avec les learning rates de FlowNet2
3. Étendre le dataset de météores :
   - Améliorer la qualité du détourage des motifs
   - Générer des paires de motifs (motifA/motifB) au lieu d'un seul motif translaté
   - Créer synthétiquement des motifs avec variations d'opacité
   - Ajouter des transformations aléatoires (bruit gaussien, etc.) comme dans Flying Chairs
4. Explorer les articles récents sur la génération de datasets (ex: Flying Things 3D)

**Documentation** :
- Compléter l'analyse par la lecture de l'article FlowNet2
- Référencer les avancées récentes en flot optique pour les petits objets