Bien sûr, voici le texte avec les points remplacés par des tirets ("-") :

# test_senscritique

1- But
Le but du projet est de pouvoir **simuler le comportement des utilisateurs** en reconstituant un top 100 de films à partir du dataset *sc_films* afin que ce top 100 soit le plus proche possible de celui obtenu à travers les études de SensCritique contenu dans le dataset *top_100_films*.

2- Démarche
Le machine learning dans ce cas ne serait pas une bonne idée car :
- Le dataset labélisé ne contient que 100 données, ce qui est très peu pour entraîner un modèle.
- Le type de machine learning dans ce cas où il aurait été approprié de le faire aurait été la régression, car il faut prédire un rang (valeur continue). Or, il n'y a pas vraiment de corrélation entre la variable cible "rank" et les autres features.

Par conséquent, la méthode que j'ai adoptée a été de me constituer ma propre métrique afin de calculer les films du dataset *top_100_films*.

3- Méthode de résolution
Il s'agit de combiner des features de façon linéaire sous la forme ```aX+bY+cZ``` avec :
- X : rate_year
- Y : rating
- Z : review_count
Ces choix sont justifiables. L'énoncé stipule que :
- les films sortis après 2015 sont probablement moins bien notés : ainsi, l'on crée une colonne avec des 0 et 1 pour pénaliser les films sortis après 2015 (valeur=0) et favoriser les autres (valeur=1).
- le rating étant établi par **SensCritique** et moins affecté par les *manipulations* des comptes *booster*, il est important d'en tenir compte.
- Le review_count : valeur importante car l'énoncé demande que le top 100 contienne aussi les films les plus visionnés. Or, si un film est beaucoup critiqué, cela signifie (selon mon hypothèse) qu'il a été assez vu.

On fait donc varier a, b et c entre 1 et 4 afin d'avoir toutes les combinaisons linéaires possibles.

4- Evaluation
- On trie notre dataset en fonction de nos métriques et on affecte un rang à chaque film.
- On soustrait le rang des films dans *top_100_films* à leur correspondant que j'ai obtenu dans mon dataset et j'obtiens un score **i**.
- Ce score s'interprète de la façon suivante : il y a **i** rangs d'écart entre ma prédiction et la valeur exacte.
