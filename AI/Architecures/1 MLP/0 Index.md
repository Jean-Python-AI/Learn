# MLP — Multi-Layer Perceptron

Un MLP (*Multi-Layer Perceptron*) est un assemblage de couches de [[AI/Architecures/0 Perceptron/0 Index|perceptrons]]. Chaque couche transforme les données reçues, et ses activations deviennent les entrées de la couche suivante.

![[MLP_shema.svg|559]]

Un réseau plus profond ou plus large peut représenter des relations plus complexes. En contrepartie, il demande davantage de données, de calcul et de soin pendant l’entraînement ; il n’est pas automatiquement meilleur.

## Calcul dans une couche

Pour quelques perceptrons, les calculs scalaires ressemblent à :

$$
z_1^{[1]}
=w_{11}^{[1]}x_1+w_{12}^{[1]}x_2+w_{13}^{[1]}x_3+b_1^{[1]}
$$

$$
z_3^{[2]}
=w_{31}^{[2]}a_1^{[1]}+w_{32}^{[2]}a_2^{[1]}+\dots+b_3^{[2]}
$$

En général, pour le neurone $m$ de la couche $c$ :

$$
z_m^{[c]}
=\sum_{j=1}^{n_{c-1}}w_{mj}^{[c]}a_j^{[c-1]}+b_m^{[c]}
$$

- $z_m^{[c]}$ : sortie linéaire du neurone $m$ de la couche $c$ ;
- $a_j^{[c-1]}$ : activation $j$ de la couche précédente ;
- $w_{mj}^{[c]}$ : poids reliant l’activation $j$ au neurone $m$ ;
- $b_m^{[c]}$ : biais du neurone $m$ ;
- $n_{c-1}$ : nombre de neurones dans la couche précédente.

Après le calcul de $z_m^{[c]}$, une fonction d’activation produit $a_m^{[c]}$. Une sigmoïde est utilisée dans les exemples de ces notes, mais d’autres fonctions d’activation sont possibles.

## Trois étapes pour utiliser un MLP

1. [[AI/Architecures/1 MLP/Vectorisation|Vectoriser les calculs]] pour représenter une couche entière avec des matrices.
2. Faire une [[AI/Architecures/1 MLP/Forward Propagation|propagation avant]] des entrées vers les sorties.
3. [[AI/Architecures/1 MLP/Entrainement du réseau|Entraîner le réseau]] en calculant les gradients puis en mettant à jour les paramètres.

## Liens utiles

- [[AI/Architecures/1 MLP/Back-Propagation|Rétropropagation]]
- [[AI/Architecures/1 MLP/z Sources|Sources — MLP]]
