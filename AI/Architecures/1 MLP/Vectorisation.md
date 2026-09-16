# Vectorisation d’un MLP

Écrire les calculs neurone par neurone devient vite impossible. La vectorisation représente chaque couche du réseau par des matrices et calcule tous les exemples du batch simultanément.

## Convention utilisée

Les exemples sont placés en colonnes :

$$
X=A^{[0]}\in\mathbb{R}^{n_0\times m}
$$

- $n_0$ : nombre d’entrées par exemple ;
- $m$ : nombre d’exemples dans le batch ;
- $n_l$ : nombre de neurones dans la couche $l$ ;
- $A^{[l]}$ : activations de la couche $l$ ;
- $Z^{[l]}$ : sorties linéaires de la couche $l$.

## Couche 1 : calcul de $Z^{[1]}$

La matrice des poids de la première couche contient un poids par connexion entre une entrée et un neurone :

$$
W^{[1]}=
\begin{bmatrix}
w_{11}^{[1]} & w_{12}^{[1]} & \dots & w_{1n_0}^{[1]} \\
w_{21}^{[1]} & w_{22}^{[1]} & \dots & w_{2n_0}^{[1]} \\
\vdots & \vdots & \ddots & \vdots \\
w_{n_1 1}^{[1]} & w_{n_1 2}^{[1]} & \dots & w_{n_1 n_0}^{[1]}
\end{bmatrix}
\in\mathbb{R}^{n_1\times n_0}
$$

$$
X=
\begin{bmatrix}
x_1^{(1)} & x_1^{(2)} & \dots & x_1^{(m)} \\
x_2^{(1)} & x_2^{(2)} & \dots & x_2^{(m)} \\
\vdots & \vdots & \ddots & \vdots \\
x_{n_0}^{(1)} & x_{n_0}^{(2)} & \dots & x_{n_0}^{(m)}
\end{bmatrix}
\in\mathbb{R}^{n_0\times m}
$$

Le vecteur de biais possède un biais par neurone :

$$
b^{[1]}=
\begin{bmatrix}
b_1^{[1]} \\
b_2^{[1]} \\
\vdots \\
b_{n_1}^{[1]}
\end{bmatrix}
\in\mathbb{R}^{n_1\times1}
$$

Le calcul est :

$$
Z^{[1]}=W^{[1]}X+b^{[1]}
$$

Le biais est diffusé sur les $m$ colonnes. Le résultat contient un score par neurone et par exemple :

$$
Z^{[1]}=
\begin{bmatrix}
z_1^{[1](1)} & z_1^{[1](2)} & \dots & z_1^{[1](m)} \\
z_2^{[1](1)} & z_2^{[1](2)} & \dots & z_2^{[1](m)} \\
\vdots & \vdots & \ddots & \vdots \\
z_{n_1}^{[1](1)} & z_{n_1}^{[1](2)} & \dots & z_{n_1}^{[1](m)}
\end{bmatrix}
\in\mathbb{R}^{n_1\times m}
$$

## Activation

Avec la sigmoïde, l’activation est appliquée terme à terme :

$$
A^{[1]}=\frac{1}{1+e^{-Z^{[1]}}}
$$

## Couches suivantes

Pour toute couche $l\geq2$, on remplace les entrées initiales $X$ par les activations de la couche précédente :

$$
Z^{[l]}=W^{[l]}A^{[l-1]}+b^{[l]}
$$

$$
A^{[l]}=g^{[l]}\left(Z^{[l]}\right)
$$

où $g^{[l]}$ est la fonction d’activation choisie pour la couche. Avec $W^{[l]}\in\mathbb{R}^{n_l\times n_{l-1}}$, on obtient bien $Z^{[l]}\in\mathbb{R}^{n_l\times m}$.

## Pourquoi cette orientation compte

La [[AI/Architecures/0 Perceptron/Vectorisation des fonctions|note de vectorisation du perceptron]] présente aussi l’orientation équivalente où les exemples sont en lignes. Les deux sont correctes, mais ici les exemples restent en colonnes dans toutes les formules : $W^{[l]}A^{[l-1]}+b^{[l]}$.

Voir [[AI/Architecures/1 MLP/Forward Propagation|Propagation avant]] et [[AI/Architecures/1 MLP/Back-Propagation|Rétropropagation]].
