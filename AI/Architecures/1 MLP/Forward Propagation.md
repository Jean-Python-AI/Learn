Propagation vers l'avant dans le réseaux de neurones, ce sont les différentes étapes pour faire passée des inputs en outputs d'un réseau de neurones.

### 1. Initialisation
Ont pose $X$ et $Y$ qui corresponde aux inputs et au output attendu.
$$
X =
\begin{bmatrix}
	x_1^{(1)} && x_1^{(2)} && \dots x_1^{(m)} \\
	\dots && \dots \\
	x_i^{(1)} && x_i^{(2)} && \dots x_i^{(m)} 
\end{bmatrix}
$$
- $i$ : nombres total de inputs
- $m$ : nombre de cas que le réseaux aura

$$
Y =
\begin{bmatrix}
	y^{(1)} && y^{(2)} && \dots y^{(m)}
\end{bmatrix}
$$

### 2. Calculs des outputs des différentes couches de neurones
##### Couche 1 :
$$
Z^{[1]} = W^{[1]} X + b^{[1]}
$$
$$
A^{[1]} = \frac{1}{1 + e^{-Z^{[1]}}}
$$
##### Couche 2:

$$
Z^{[2]} = W^{[2]} A^{[1]} + b^{[2]}
$$
$$
A^{[2]} = \frac{1}{1 + e^{-Z^{[2]}}}
$$
##### ... Jusqu'à la dernière couche
Lorsque l'ont arrive à la dernière couche, ont prend le output du dernier $A$ et il correspond à la réponsse du réseau.


### 3. Log Loss du modèle
$$
\mathcal{L} = -\frac{1}{m} * \sum_{i = 1}^{m} y_i \log(A^{[n]}) + (1-y_i)\log(1-A^{[n]})
$$
- $n$ : nombre de couche totale ou plutôt, numéro de la dernière couche

