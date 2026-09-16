La fonction **SoftMax** est une fonction qui permet de prendre toutes les sorties d'un réseau et de les convertir en sortie entre 0 et 1, qui toutes additionné donne 1.

$$
\begin{bmatrix}
	-3 \\
	2 \\
	-0.9 \\
	-4.2 \\
	3.1
\end{bmatrix}
\longrightarrow
\begin{bmatrix}
	0.0016 \\
	0.2458 \\
	0.0135 \\
	0.0005 \\
	0.7385
\end{bmatrix}
$$
Ce qui donne $\longrightarrow 0.0016 + 0.2458 + 0.0135 + 0.0005 + 0.7385 = 1$ 

Grâce à cela, lorsque l'ont sélectionne la plus haute possibilité, ont connait le pourcentage de cette possibilité attribué par l'IA.

### Formule mathématique
$$
\text{softMax}(z_i) = \frac{e^{z_i}}{\sum_{n=0}^{m} e^{z_n}}
$$
où
- $z_i$ : le score de la classe $i$
- $m$ : nombre de classe

