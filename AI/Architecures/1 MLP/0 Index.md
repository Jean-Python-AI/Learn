Un **MLP** est un **M**ulti **L**ayers **P**erceptrons, ce qui signifie que c'est un assemblage de plusieurs couches de [[AI/Architecures/0 Perceptron/0 Index|perceptrons]]

Plus un réseau est profond (grand), plus il est cappable d'apprendre des choses compliquées mais cela rend aussi l'apprentissage plus long.
![[MLP_shema.svg|559]]
Pour les calculs de $z$ et $a$ de quelques perceptron d'exemple
$$
z_1^{[1]} = w_{11}^{[1]} x_1 + w_{12}^{[1]} x_2 + w_{13}^{[1]} x_3 + b_1^{[1]}
$$
$$
z_3^{[2]} = w_{31}^{[2]} a_1^{[1]} + w_{32}^{[2]} a_2^{[1]} + b_3^{[2]}
$$
Où
- $z_m^{[C]}$ : $C$ = numéro de la couche où se trouve le perceptron du $z$ ET $m$ = numéro du perceptron dans la couche
- $w_{mj}^{[C]}$ : $j$ = numéro du input ET $m$ et $C$ comme au dessus
$$
Z_m^{[C]} = w_{mj}^{[C]} a_1^{[C-1]} + \dots + b_m
$$


Pour les réseaux de neurones, cela prendrais trop de temps d'écrire chaque fonctions à calculer, à la place, ont vas véctorisé afin de représenter chaque couche du réseau par des matrices.
[[Vectorisation]]

**Forward Propagation** = étape qui consiste à faire passée les données du débuts jusqu'à la fin du réseau de neurones.
Voici les étapes expliquée en détails => [[Forward Propagation]]


Pour entrainer le MLP => [[Entrainement du réseau]]
