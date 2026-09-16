# Espace d'actions discret

> Un espace d'actions discret contient un ensemble fini d'actions parmi lesquelles une policy choisit en fonction de l'état $s$, contrairement à un [[4 Continuous Action Space|espace d'actions continu]].

Par exemple :

$$
\mathcal A=\{\text{gauche},\text{ne rien faire},\text{droite}\}.
$$

Une [[1 Deterministic Policy|policy déterministe]] choisit une action précise :

$$
a_t=\pi(s_t)=\text{gauche}.
$$

Une [[2 Stochastic Policy|policy stochastique]] produit une probabilité pour chaque action, puis échantillonne l'une d'elles :

$$
\pi(\cdot \mid s_t)=
\begin{bmatrix}
\text{gauche} & 0.6 \\
\text{ne rien faire} & 0.3 \\
\text{droite} & 0.1
\end{bmatrix}.
$$

Ici, les valeurs $0.6$, $0.3$ et $0.1$ somment à $1$. Cette matrice décrit une **distribution d'actions**, pas un état.

Un réseau de neurones ne peut pas sortir une probabilité pour chaque action qui toute cumulé font $1$ la sortie resemblera plutôt à:
$$
\pi(\cdot \mid s_t) = \begin{bmatrix} gauche && 2.1 \\ rien faire && -3.8746 \\ droite && 0.75272 \end{bmatrix}
$$
Pour transformer toutes ces valeurs en une probabilité pour chaque action, on utilise la fonction [[SoftMax]].