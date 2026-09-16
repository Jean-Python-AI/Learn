# Descente de gradient

La descente de gradient modifie les poids $w_1,w_2,\ldots,w_n$ et le biais $b$ afin de diminuer la [[AI/Architecures/0 Perceptron/Log Loss|log-loss]] du modèle.

## Objectif : minimiser la loss

On peut soit maximiser une vraisemblance, soit minimiser une loss : ce sont deux formulations équivalentes quand la loss est l’opposé de la log-vraisemblance. Ici, $\mathcal{L}$ désigne déjà la log-loss à minimiser.

> [!note] Correction de formulation
> Il est tout à fait possible de maximiser une fonction en mathématiques. La descente de gradient est simplement un algorithme conçu pour minimiser ; pour maximiser une fonction, on utiliserait une montée de gradient ou l’opposé de cette fonction.

Pour chaque paramètre $W$, une mise à jour est :

$$
W_{t+1}=W_t-\alpha\frac{\partial\mathcal{L}}{\partial W_t}
$$

- $W_t$ : valeur du paramètre à l’instant $t$ ;
- $W_{t+1}$ : nouvelle valeur ;
- $\alpha>0$ : pas d’apprentissage ;
- $\frac{\partial\mathcal{L}}{\partial W_t}$ : composante du gradient associée au paramètre.

![[logLoss_by_W.svg|385]]

## Quand la descente de gradient converge-t-elle ?

Pour la régression logistique (un perceptron avec log-loss), la loss est convexe par rapport aux paramètres : elle ne possède donc pas plusieurs minima locaux isolés. La situation est différente pour les réseaux de neurones profonds, dont la loss n’est généralement pas convexe ; la descente de gradient reste utile, mais n’offre pas la même garantie globale.

## Dériver la log-loss

Pour un poids $w_j$, la règle de chaîne donne :

$$
\frac{\partial\mathcal{L}}{\partial w_j}
=\sum_{i=1}^{m}
\frac{\partial\mathcal{L}}{\partial a^{(i)}}
\frac{\partial a^{(i)}}{\partial z^{(i)}}
\frac{\partial z^{(i)}}{\partial w_j}
$$

Les trois éléments à utiliser sont :

$$
\frac{\partial\mathcal{L}}{\partial a^{(i)}}
=-\frac{1}{m}
\left[
\frac{y^{(i)}}{a^{(i)}}
-\frac{1-y^{(i)}}{1-a^{(i)}}
\right]
$$

$$
\frac{\partial a^{(i)}}{\partial z^{(i)}}
=a^{(i)}\left(1-a^{(i)}\right)
$$

$$
\frac{\partial z^{(i)}}{\partial w_j}=x_j^{(i)}
$$

Après simplification :

$$
\frac{\partial\mathcal{L}}{\partial w_j}
=\frac{1}{m}\sum_{i=1}^{m}
\left(a^{(i)}-y^{(i)}\right)x_j^{(i)}
$$

Pour le biais :

$$
\frac{\partial\mathcal{L}}{\partial b}
=\frac{1}{m}\sum_{i=1}^{m}
\left(a^{(i)}-y^{(i)}\right)
$$

> [!warning] Correction importante : le signe
> Le gradient de la log-loss avec une sortie sigmoïde contient $(a-y)$, et non $(y-a)$. Avec la mise à jour $W\leftarrow W-\alpha\nabla_W\mathcal{L}$, inverser ce signe ferait évoluer les paramètres dans la mauvaise direction.

## Version vectorisée

Les mêmes calculs peuvent être effectués sur tout un batch avec des matrices, sans boucle explicite. Voir [[AI/Architecures/0 Perceptron/Vectorisation des fonctions|Vectorisation du perceptron]].
