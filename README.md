# Optimisation des échanges de reins

Modéliser un programme d’échange de reins sous forme de graphe orienté et sélectionner les cycles compatibles maximisant le bénéfice total des greffes.

## Enjeu

Lorsqu’un donneur vivant n’est pas compatible avec son proche, plusieurs couples donneur-patient peuvent être associés dans des cycles d’échanges.

Le problème consiste à sélectionner des cycles :

- compatibles ;
- disjoints ;
- simultanés ;
- de longueur limitée ;
- maximisant le nombre ou le bénéfice total des greffes.

## Données

Les instances simulées contiennent :

- 16 à 2 048 couples donneur-patient ;
- des arcs orientés représentant les compatibilités ;
- un poids associé à chaque greffe potentielle ;
- aucun donneur altruiste.

Aucune donnée médicale réelle ni donnée personnelle n’est utilisée.

## Méthodologie

1. lecture des fichiers `.wmd` ;
2. construction d’un dictionnaire d’adjacence ;
3. génération des cycles compatibles par parcours en profondeur ;
4. calcul du poids de chaque cycle ;
5. formulation d’un programme linéaire en nombres entiers ;
6. résolution avec PuLP et CBC ;
7. vérification automatique de la faisabilité ;
8. comparaison à une borne inférieure par matching et à une borne supérieure par flot.

La variable de décision associée à chaque cycle vaut 1 si le cycle est retenu, 0 sinon. Une contrainte garantit que chaque couple apparaît au plus une fois.

## Résultats

- les solutions obtenues respectent la longueur maximale des cycles ;
- les cycles sélectionnés sont disjoints ;
- la valeur du PLNE est correctement encadrée par les bornes ;
- le nombre de cycles et le temps de calcul augmentent fortement avec la taille des instances et avec `k` ;
- à partir de `k = 3`, le gain supplémentaire devient souvent limité alors que le coût de calcul continue d’augmenter.

Le principal enseignement est le compromis entre **optimalité** et **passage à l’échelle**.

## Technologies

`Python` · `PuLP` · `CBC` · graphes orientés · DFS · PLNE · optimisation combinatoire · benchmarking

## Ce que ce projet démontre

- traduction d’un problème réel en modèle mathématique ;
- manipulation de graphes ;
- développement d’un algorithme de génération de cycles ;
- résolution d’un problème d’optimisation exact ;
- validation automatique des solutions ;
- analyse de complexité.

## Limites et améliorations

La génération exhaustive des cycles devient rapidement le principal goulot d’étranglement. Des approches par génération de colonnes, branch-and-price ou heuristiques seraient nécessaires pour traiter de très grandes instances.

## Auteur

Projet universitaire réalisé en équipe, avec participation de **Benjamin BAILLET**, à l’Université de Bordeaux.

---
