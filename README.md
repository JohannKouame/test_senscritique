# test_senscritique

1- But
Le but du projet est de pouvoir **simuler le comportement des utilisateurs** en reconstituant un top 100 de films à partir du dataset *sc_films* afin que ce top 100 soit le plus proche possible de celui obtenu à travers les études de senscritique contenu dans le dataset *top_100_films*

2- Démarche
Le machine learning dans ce cas ne serait pas une bonne idée car :
-  Le dataset labélisé ne contient que 100 données, ce qui est très pour entraîner un modèle
-  Le type de machine learning dans ce cas 'il y avait lieux de le faire aurait été la régression car il faut prédire un rang (valeur continue). Or il n'y a pas vraiment de corrélation entre la variable cible "rank" et les autres features.

 Par conséquent, la méthode que j'ai adoptée a été de me constituer ma propre métrique afin de calculer les films du dataset *top_100_films*

 3- Méthode de résolution
 Il s'agit de combiner des features de façon linéaire sous la forme ```aX+bY+cZ``` avec :
 - X : rate_year
 - Y : rating
 - Z : review_count
Cest choix sont justifiables. L'énoncé stipule que :
 - les films sorties après 2015 sont probablement moins notées : ainsi,  l'on créer une colonne avec des 0 et 1 pour pénaliser les films sorties après 2015 (valeur=0) et favoirser les autres (valeur=1)
 - le rating étant établie par **SensCritque** et moins affecté par les *magouilles* des comptes *booster*, il est important d'en tenir compte
 - Le review_count : valeur importante car l'énoncé demande à ce que le top 100 contienne aussi les films les plus visionnées. Or, si un film est beaucoup critiquée, cela signifie (selon mon hypothèse) qu'il a été assez vu

On fait donc varier a, b et c entre 1 et 4 afin d'avoir toutes les combinaisons linéaires possibles.

4- Evaluation
- On trie notre dataset en fonction de nos métrique et on affecte un rank à chaque film
- On soustrait le rang des films dans *top_100_films* à leur correspondant que j'ai obtenu dans mon dataset et j'obtiens un score **i**
- Ce score s'interprête de la façon suivante : il y a **i** rang d'écart entre ma prédiction et la valeur exacte
