# Propagation avant

La propagation avant (*forward propagation*) fait passer les entrées du réseau jusqu’à sa sortie. À chaque couche, le MLP calcule une transformation linéaire, puis une activation.

## 1. Initialisation du batch

Les exemples sont placés en colonnes :

$$
X=A^{[0]}=
\begin{bmatrix}
x_1^{(1)} & x_1^{(2)} & \dots & x_1^{(m)} \\
\vdots & \vdots & \ddots & \vdots \\
x_{n_0}^{(1)} & x_{n_0}^{(2)} & \dots & x_{n_0}^{(m)}
\end{bmatrix}
\in\mathbb{R}^{n_0\times m}
$$

- $n_0$ : nombre total d’entrées par exemple ;
- $m$ : nombre de cas dans le batch ;
- $x_j^{(i)}$ : entrée $j$ de l’exemple $i$.

Pour un problème binaire, les sorties attendues peuvent être rangées ainsi :

$$
Y=
\begin{bmatrix}
y^{(1)} & y^{(2)} & \dots & y^{(m)}
\end{bmatrix}
$$

$Y$ n’est pas nécessaire pour produire une prédiction, mais il est nécessaire ensuite pour mesurer l’erreur.

## 2. Calcul des couches

### Couche 1

$$
Z^{[1]}=W^{[1]}X+b^{[1]}
$$

$$
A^{[1]}=\frac{1}{1+e^{-Z^{[1]}}}
$$

### Couche 2

$$
Z^{[2]}=W^{[2]}A^{[1]}+b^{[2]}
$$

$$
A^{[2]}=\frac{1}{1+e^{-Z^{[2]}}}
$$

### Jusqu’à la dernière couche

La même règle se répète pour chaque couche $l$ :

$$
Z^{[l]}=W^{[l]}A^{[l-1]}+b^{[l]}
\qquad\text{puis}\qquad
A^{[l]}=g^{[l]}\left(Z^{[l]}\right)
$$

Quand on atteint la dernière couche $L$, $A^{[L]}$ est la sortie du réseau. La fonction d’activation finale dépend du problème ; les exemples de classification binaire ci-dessous utilisent une sigmoïde.

## 3. Log-loss du modèle

Pour $m$ exemples binaires et une sortie sigmoïde, la loss est :

$$
\mathcal{L}
=-\frac{1}{m}\cdot\sum_{i=1}^{m}
\left[
y^{(i)}\log\left(A^{[L](i)}\right)
+\left(1-y^{(i)}\right)\log\left(1-A^{[L](i)}\right)
\right]
$$

- $L$ : numéro de la dernière couche ;
- $A^{[L](i)}$ : prédiction de la dernière couche pour l’exemple $i$.

> [!note] Correction de parenthèses
> Les deux termes de la log-loss sont inclus dans la somme et dans la moyenne du batch.

La notation avec $\cdot$ conserve la multiplication explicite dans la moyenne de la loss.

Voir [[AI/Architecures/1 MLP/Vectorisation|Vectorisation du MLP]], [[AI/Architecures/0 Perceptron/Log Loss|Log-loss binaire]] et [[AI/Architecures/1 MLP/Back-Propagation|Rétropropagation]].
