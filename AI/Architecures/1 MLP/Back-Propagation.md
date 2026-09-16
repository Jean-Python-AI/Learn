# Rétropropagation

La rétropropagation (*backpropagation*) remonte l’effet de la [[AI/Architecures/0 Perceptron/Log Loss|log-loss]] de la dernière couche vers la première. Elle calcule les dérivées de la loss par rapport à tous les poids $W^{[l]}$ et biais $b^{[l]}$.

Elle réutilise la règle de chaîne déjà rencontrée dans la [[AI/Architecures/0 Perceptron/Descante de gradients|descente de gradient]].

## Idée de la règle de chaîne

Pour la dernière couche $L$, un poids influence la loss selon le chemin :

$$
\frac{\partial\mathcal{L}}{\partial W^{[L]}}
=
\frac{\partial\mathcal{L}}{\partial A^{[L]}}
\frac{\partial A^{[L]}}{\partial Z^{[L]}}
\frac{\partial Z^{[L]}}{\partial W^{[L]}}
$$

Pour un poids de la couche $c$, l’effet traverse toutes les couches suivantes :

$$
\frac{\partial\mathcal{L}}{\partial W^{[c]}}
=
\frac{\partial\mathcal{L}}{\partial A^{[L]}}
\frac{\partial A^{[L]}}{\partial Z^{[L]}}
\frac{\partial Z^{[L]}}{\partial A^{[L-1]}}
\cdots
\frac{\partial A^{[c]}}{\partial Z^{[c]}}
\frac{\partial Z^{[c]}}{\partial W^{[c]}}
$$

> [!note]
> Cette écriture décrit le chemin conceptuel. Avec des matrices, les dérivées sont des gradients et des Jacobiennes ; les formules ci-dessous donnent les produits matriciels corrects.

## Le raccourci $dZ^{[l]}$

Pour ne pas réécrire toute la chaîne, on définit :

$$
dZ^{[l]}=\frac{\partial\mathcal{L}}{\partial Z^{[l]}}
$$

À la dernière couche :

$$
dZ^{[L]}
=
\frac{\partial\mathcal{L}}{\partial A^{[L]}}
\odot
\frac{\partial A^{[L]}}{\partial Z^{[L]}}
$$

Dans le cas important « sigmoïde + log-loss binaire », cette expression se simplifie :

$$
dZ^{[L]}=A^{[L]}-Y
$$

Pour une couche cachée $l$, le gradient est ramené depuis la couche suivante puis traverse l’activation :

$$
dZ^{[l]}
=
\left(W^{[l+1]}\right)^T dZ^{[l+1]}
\odot
g'^{[l]}\left(Z^{[l]}\right)
$$

Avec une sigmoïde :

$$
g'^{[l]}\left(Z^{[l]}\right)
=A^{[l]}\odot\left(1-A^{[l]}\right)
$$

## Gradients des poids et des biais

Pour chaque couche $l$ et un batch de $m$ exemples :

$$
\frac{\partial\mathcal{L}}{\partial W^{[l]}}
=\frac{1}{m}dZ^{[l]}\left(A^{[l-1]}\right)^T
$$

$$
\frac{\partial\mathcal{L}}{\partial b^{[l]}}
=\frac{1}{m}\sum_{\text{colonnes}}dZ^{[l]}
$$

Le symbole $\odot$ désigne un produit terme à terme. Les autres juxtapositions sont des produits matriciels, et $T$ indique une transposée.

## Exemple : réseau à deux couches

Pour une couche cachée $1$ et une couche de sortie $2$ :

$$
dZ^{[2]}=A^{[2]}-Y
$$

$$
\frac{\partial\mathcal{L}}{\partial W^{[2]}}
=\frac{1}{m}dZ^{[2]}\left(A^{[1]}\right)^T
\qquad
\frac{\partial\mathcal{L}}{\partial b^{[2]}}
=\frac{1}{m}\sum_{\text{colonnes}}dZ^{[2]}
$$

$$
dZ^{[1]}
=\left(W^{[2]}\right)^TdZ^{[2]}
\odot
A^{[1]}\odot\left(1-A^{[1]}\right)
$$

$$
\frac{\partial\mathcal{L}}{\partial W^{[1]}}
=\frac{1}{m}dZ^{[1]}X^T
\qquad
\frac{\partial\mathcal{L}}{\partial b^{[1]}}
=\frac{1}{m}\sum_{\text{colonnes}}dZ^{[1]}
$$

> [!warning] Correction de la dérivée sigmoïde
> Le terme de la couche cachée est $A^{[1]}\odot(1-A^{[1]})$. Omettre le facteur $A^{[1]}$ donne un gradient incorrect.

La chaîne de la dernière couche part bien de $\frac{\partial\mathcal{L}}{\partial A^{[L]}}$ avant de passer par $Z^{[L]}$ ; cette dépendance est indispensable.

Une fois ces gradients obtenus, [[AI/Architecures/1 MLP/Entrainement du réseau|l’entraînement]] met les paramètres à jour.
