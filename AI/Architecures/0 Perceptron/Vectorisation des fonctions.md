# Vectorisation des fonctions du perceptron

La vectorisation remplace une boucle qui traite les exemples un par un par quelques opérations sur des matrices. Elle calcule en une fois les scores $Z$, les activations $A$, la loss et les gradients d’un batch entier.

## Les données d’un batch

On note :

- $m$ : nombre de données (exemples) ;
- $n$ : nombre d’entrées par exemple ;
- $x_j^{(i)}$ : entrée $j$ de l’exemple $i$ ;
- $y^{(i)}$ : sortie attendue de l’exemple $i$.

### Convention avec les exemples en lignes

Cette première convention correspond à la formulation initiale de la note. Chaque ligne de $X$ est un exemple :

$$
X=
\begin{bmatrix}
x_1^{(1)} & \dots & x_n^{(1)} \\
x_1^{(2)} & \dots & x_n^{(2)} \\
\vdots & \vdots & \vdots \\
x_1^{(m)} & \dots & x_n^{(m)}
\end{bmatrix}
\in\mathbb{R}^{m\times n}
$$

$$
Y=
\begin{bmatrix}
y^{(1)} \\
y^{(2)} \\
\vdots \\
y^{(m)}
\end{bmatrix}
\in\mathbb{R}^{m\times1}
\qquad
W=
\begin{bmatrix}
w_1 \\
w_2 \\
\vdots \\
w_n
\end{bmatrix}
\in\mathbb{R}^{n\times1}
$$

## Calcul de $Z$

Pour chaque exemple, le perceptron calcule $z^{(i)}=w_1x_1^{(i)}+\ldots+w_nx_n^{(i)}+b$. Pour tout le batch :

$$
Z=
\begin{bmatrix}
z^{(1)} \\
z^{(2)} \\
\vdots \\
z^{(m)}
\end{bmatrix}
=
\begin{bmatrix}
w_1x_1^{(1)}+\dots+w_nx_n^{(1)}+b \\
w_1x_1^{(2)}+\dots+w_nx_n^{(2)}+b \\
\vdots \\
w_1x_1^{(m)}+\dots+w_nx_n^{(m)}+b
\end{bmatrix}
$$

La même opération s’écrit simplement :

$$
Z=XW+b
$$

Ici, le scalaire $b$ est ajouté à chaque ligne de $XW$ par diffusion (*broadcasting*).

## Calcul de $A$

La sigmoïde s’applique terme à terme :

$$
A=\frac{1}{1+e^{-Z}}
$$

Ainsi, $A$ contient toutes les sorties $a^{(1)},\ldots,a^{(m)}$. Voir [[AI/Architecures/0 Perceptron/A(Z)|Fonction d’activation sigmoïde]] et [[AI/Architecures/0 Perceptron/Log Loss|Log-loss binaire]].

## Mettre à jour les paramètres

La descente de gradient reste la même pour chaque poids :

$$
w_j\leftarrow w_j-\alpha\frac{\partial\mathcal{L}}{\partial w_j}
$$

La vectorisation permet de mettre à jour tous les poids simultanément :

$$
W\leftarrow W-\alpha\frac{\partial\mathcal{L}}{\partial W}
$$

Avec la log-loss binaire et une sortie sigmoïde :

$$
\frac{\partial\mathcal{L}}{\partial W}
=\frac{1}{m}
\begin{bmatrix}
\sum_{i=1}^{m}\left(a^{(i)}-y^{(i)}\right)x_1^{(i)} \\
\sum_{i=1}^{m}\left(a^{(i)}-y^{(i)}\right)x_2^{(i)} \\
\vdots \\
\sum_{i=1}^{m}\left(a^{(i)}-y^{(i)}\right)x_n^{(i)}
\end{bmatrix}
=\frac{1}{m}X^T(A-Y)
$$

Pour le biais :

$$
b\leftarrow b-\alpha\frac{\partial\mathcal{L}}{\partial b}
\qquad\text{avec}\qquad
\frac{\partial\mathcal{L}}{\partial b}
=\frac{1}{m}\sum_{i=1}^{m}\left(a^{(i)}-y^{(i)}\right)
$$

> [!warning] Correction de signe
> Le gradient contient $A-Y$, et non $Y-A$. La règle de mise à jour soustrait déjà le gradient.

## Convention utilisée pour le MLP

Les notes du [[AI/Architecures/1 MLP/0 Index|MLP]] placent plutôt les exemples en colonnes. C’est exactement la transposée de la convention ci-dessus :

$$
X_{\text{colonnes}}=X^T\in\mathbb{R}^{n\times m}
$$

Dans cette convention, un perceptron s’écrit :

$$
Z=WX+b,
\qquad
A=\frac{1}{1+e^{-Z}},
\qquad
\frac{\partial\mathcal{L}}{\partial W}
=\frac{1}{m}(A-Y)X^T
$$

Les deux conventions sont correctes. L’essentiel est de choisir une orientation et de la conserver tout au long d’un calcul, pour éviter des transpositions ou des gradients incohérents.

Voir aussi [[AI/Architecures/0 Perceptron/Descante de gradients|Descente de gradient]] et [[AI/Architecures/1 MLP/Vectorisation|Vectorisation du MLP]].
