Consiste à retracer comment le [[Log Loss]] évolue de la dernière couche du réseau jusqu'à la première.

En réutilisant à peut près les mêmes principes qui ont été utilisé pour trouver $\frac{d \mathcal{L}}{d W}$ dans [[Descante de gradients]], ont vas devoir trouver $\frac{d \mathcal{L}}{d W^{[2]}}$, $\frac{d \mathcal{L}}{d b^{[2]}}$, $\frac{d \mathcal{L}}{d W^{[1]}}$, $\frac{d \mathcal{L}}{d b^{[1]}}$, ...

$n$ = numéro de la dernière couche
Pour la dernière couche du réseau
$$
\frac{d \mathcal{L}}{d W^{[n]}} = \frac{d \mathcal{L}}{d A^{[n]}} \frac{d A^{[n]}}{d Z^{[n]}} \frac{d Z^{[n]}}{d W^{[n]}}
$$

$c$ = numéro d'une couche du réseau
Ce qui donne:
$$
\frac{d \mathcal{L}}{d W^{[c]}} = \frac{d \mathcal{L}}{d A^{[n]}} . \frac{d A^{[n]}}{d Z^{[n]}} . \frac{d Z^{[n]}}{d A^{[n-1]}} . \frac{d A^{[n-1]}}{d Z^{[n-1]}} . \frac{d Z^{[n-1]}}{d A^{[n-2]}} \dots \frac{d A^{[c]}}{d Z^{[c]}} . \frac{d Z^{[c]}}{d W^{[c]}}
$$


**Mais** pour simplifier les calculs, on créer $dZj$
où $j$ = couche du $dZ$

Pour la dernière couche
$$
dZn = \frac{d \mathcal{L}}{d W^{[n]}} \frac{d A^{[n]}}{d Z^{[n]}}
$$
Pour les autres
$$
dZ3 = dZn \cdot \dots dZ4 \cdot \frac{d Z^{[4]}}{d A^{[3]}} \frac{d A^{[3]}}{d Z^{[3]}}
$$

Ce qui nous permet de faire
$$
\frac{d \mathcal{L}}{d W^{[c]}} = dZc \cdot \frac{d Z^{[c]}}{d W^{[c]}}
$$
$$
\frac{d \mathcal{L}}{d b^{[c]}} = dZc \cdot \frac{d Z^{[c]}}{d b^{[c]}}
$$

---

$$
dZ2 = (A^{[2]} - y)
$$
$$
\frac{d \mathcal{L}}{d W^{[2]}} = \frac{1}{m} \cdot dZ2 \times A^{[1]T} 
$$
- $\times$ : produit matriciel
- $X^T$ : Transposée de la matrice $X$
$$
\frac{d \mathcal{L}}{d b^{[2]}} = \frac{1}{m} \sum_{axe 1} dZ2
$$
- $\sum_{axe 1}$ : somme sur les axes 1 des matrices

$$
dZ1 = W^{[2]T} \times dZ2 \cdot A^{[1]} (1 - A^{[1]})
$$
$$
\frac{d \mathcal{L}}{d W^{[1]}} = \frac{1}{m} \cdot dZ1 \times X^T 
$$
$$
\frac{d \mathcal{L}}{d b^{[1]}} = \frac{1}{m} \sum_{axe 1} dZ1
$$

