Lorsque l'ont vectorise un réseaux de neurones, ont utilise une matrice pour chaque couches du réseaux.

### $Z$
**vectorisé**
Pour la première couche du réseaux:
$$
Z^{[1]} =
\begin{bmatrix}
	w_{11}^{[1]} && w_{12}^{[1]} && \dots w_{1i}^{[1]} \\
	w_{21}^{[1]} && w_{22}^{[1]} && \dots w_{2i}^{[1]} \\
	\vdots && \vdots \\
	w_{n1}^{[1]} && w_{n2}^{[1]} && \dots w_{ni}^{[1]}
\end{bmatrix}
\begin{bmatrix}
	x_1^{(1)} && x_1^{(2)} && \dots x_1^{(m)} \\
	x_2^{(1)} && x_2^{(2)} && \dots x_2^{(m)} \\
	\vdots && \vdots \\
	x_i^{(1)} && x_i^{(2)} && \dots x_i^{(m)}
\end{bmatrix}
+
\begin{bmatrix}
	b_1^{[1]} \\
	b_2^{[1]} \\
	\vdots \\
	b_n^{[1]}
\end{bmatrix}
$$
$$
Z^{[1]} =
\begin{bmatrix}
	z_1^{[1](1)} && z_1^{[1](2)} && \dots z_1^{[1](m)} \\
	z_2^{[1](1)} && z_2^{[1](2)} && \dots z_2^{[1](m)} \\
	\vdots && \vdots \\
	z_n^{[1](1)} && z_n^{[1](2)} && \dots z_n^{[1](m)}
\end{bmatrix}
$$
Où
- $i$ : nombre de inputs (ex: $x_1, x_2, x_3$ => 3 inputs)
- $n$ : nombre de perceptrons dans la couche
- $m$ : nombre de 

Ce qui donne en visuellement simplifié
$$
Z^{[1]} = W^{[1]}X + b^{[1]}
$$

Pour les autres couche du réseaux, on remplace juste $X$ par la matrice des $a$ retourner par la précédente couche.
$$
X_{centre} = A^{[C-1]}
$$
et on doit aussi remplace les $^{[1]}$ par $^{[C]}$ où $C$ = numéro de la couche.
$Z^{[C]}, W^{[C]}, b^{[C]}$


### $a$
**vectorisé**
$$
A^{[C]} = \frac{1}{1 + e^{-Z^{[C]}}}
$$


