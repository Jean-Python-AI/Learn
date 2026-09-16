# Entraînement d’un MLP

Entraîner un MLP consiste à répéter trois opérations sur des mini-batches : produire une prédiction, mesurer son erreur, puis modifier tous les paramètres pour réduire cette erreur.

## 1. Propagation avant et loss

La [[AI/Architecures/1 MLP/Forward Propagation|propagation avant]] calcule les activations jusqu’à la dernière couche :

$$
A^{[0]}=X,
\qquad
Z^{[l]}=W^{[l]}A^{[l-1]}+b^{[l]},
\qquad
A^{[l]}=g^{[l]}\left(Z^{[l]}\right)
$$

Pour une classification binaire avec une sigmoïde en sortie, on calcule ensuite la [[AI/Architecures/0 Perceptron/Log Loss|log-loss]] à partir de $A^{[L]}$, la sortie de la dernière couche $L$.

## 2. Calculer les dérivées partielles

Chaque poids et chaque biais influence la loss. La [[AI/Architecures/1 MLP/Back-Propagation|rétropropagation]] applique la règle de chaîne de la dernière couche vers la première afin d’obtenir :

$$
\frac{\partial\mathcal{L}}{\partial W^{[L]}},
\quad
\frac{\partial\mathcal{L}}{\partial b^{[L]}},
\quad
\ldots,
\quad
\frac{\partial\mathcal{L}}{\partial W^{[1]}},
\quad
\frac{\partial\mathcal{L}}{\partial b^{[1]}}
$$

Pour une couche $l$, les gradients d’un batch de $m$ exemples sont :

$$
\frac{\partial\mathcal{L}}{\partial W^{[l]}}
=\frac{1}{m}dZ^{[l]}\left(A^{[l-1]}\right)^T
$$

$$
\frac{\partial\mathcal{L}}{\partial b^{[l]}}
=\frac{1}{m}\sum_{\text{exemples}}dZ^{[l]}
$$

où $dZ^{[l]}$ est le gradient de la loss par rapport à la sortie linéaire de la couche $l$.

## 3. Mettre à jour $W$ et $b$

Une fois les gradients calculés, chaque paramètre est modifié avec le pas d’apprentissage $\alpha$ :

$$
W^{[l]}\leftarrow W^{[l]}-\alpha\frac{\partial\mathcal{L}}{\partial W^{[l]}}
$$

$$
b^{[l]}\leftarrow b^{[l]}-\alpha\frac{\partial\mathcal{L}}{\partial b^{[l]}}
$$

Ces mises à jour s’appliquent à toutes les couches, de $l=1$ à $l=L$.

## Boucle complète

1. Choisir un mini-batch $(X,Y)$.
2. Calculer $A^{[L]}$ par propagation avant.
3. Calculer la loss.
4. Calculer tous les gradients par rétropropagation.
5. Mettre à jour $W^{[1]},b^{[1]},\ldots,W^{[L]},b^{[L]}$.
6. Recommencer pour les autres mini-batches et les époques suivantes.
