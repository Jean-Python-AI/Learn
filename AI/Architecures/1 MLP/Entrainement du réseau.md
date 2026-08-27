## 1. Définir le Log Loss

Ont calcul le [[Log Loss]] avec la matrice du **dernier** $A^{[final]}$ du modèle

## 2. Calculer les dérivées partielles
**Pour chaque paramètres du réseau**
$n$ : numéro de la dernière couche du réseau
$$
\frac{d \mathcal{L}}{d \dots^{[n]}} = \dots
$$
$$
\frac{d \mathcal{L}}{d W^{[2]}} = \dots
$$
$$
\frac{d \mathcal{L}}{d b^{[2]}} = \dots
$$
$$
\frac{d \mathcal{L}}{d W^{[1]}} = \dots
$$
$$
\frac{d \mathcal{L}}{d b^{[1]}} = \dots
$$


## 3. Mettre à jour les différents paramètres $W$ et $b$

$n$ : numéro de la dernière couche du réseau
$$
\dots^{[n]} = \dots^{[n]} - \alpha \frac{d \mathcal{L}}{d \dots^{[n]}}
$$
$$
W^{[2]} = W^{[2]} - \alpha \frac{d \mathcal{L}}{d W^{[2]}}
$$
$$
b^{[2]} = b^{[2]} - \alpha \frac{d \mathcal{L}}{d b^{[2]}}
$$
$$
W^{[1]} = W^{[1]} - \alpha \frac{d \mathcal{L}}{d W^{[1]}}
$$
$$
b^{[1]} = b^{[1]} - \alpha \frac{d \mathcal{L}}{d b^{[1]}}
$$

