Un perceptron sert à séparer des éléments linéairement (placer une ligne droite entre des éléments sur un graphique). La ligne de séparation des catégorie s'appelle une frontière de décision.

Il est à la base de tous le Machine Learning par réseau de neurones car il est un neurone.

![[perceptronShema.svg|494]]

C'est grâce à "$Z$" que l'ont sait de quelle côté de la frontière de décision ce trouve les éléments.
Mais on utilise "$a(z)$" car cela donne une probabilité de faire partie d'un côté ou l'autre de la frontière de décision.

**Calcul du $Z$  en fonction des inputs x:**
$$
Z(x_1, x_2, ...) = w_1 x_1 + w_2 x_2 + ... + b
$$
- $w_1$ : poids de la branche 1
- $b$ : biais du perceptron

**Calcul du $a(z)$ :**
[[A(Z)]]

**Fonction coût :**
Où *Log Loss* function
[[Log Loss]]

**Descante de gradients :**
[[Descante de gradients]]



**Mais** pour économiser (énormément) de temps de calcul on utilise des matrice et non des boucle qui répète (pour chaque données) les calculs de $z$, $a(z)$, $\mathcal{L}$, ...
**Vectorisation des fonctions**
[[Vectorisation des fonctions]]
