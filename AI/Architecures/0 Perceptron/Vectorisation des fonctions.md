
- $m$ : nombre de données
- $n$ : nombre de inputs

La matrice des entrées:
$$
X =
\begin{bmatrix}
  x_1^{(1)} & \dots & x_n^{(1)} \\
  x_1^{(2)} & \dots & x_n^{(2)} \\
  \vdots & \vdots & \vdots \\
  x_1^{(m)} & \dots & x_n^{(m)}
\end{bmatrix}
$$
La matrice des sorties attendue (bonnes réponsses)
$$
Y = 
\begin{bmatrix}
	y^{(1)} \\
	y^{(2)} \\
	\vdots \\
	y^{(m)}
\end{bmatrix}
$$

La matrice des poids du modèle
$$
W =
\begin{bmatrix}
	w_1 \\
	w_2 \\
	\vdots \\
	w_n
\end{bmatrix}
$$

---

### $Z(x_1, x_2, ..., x_n)$
**sous forme de matrice**

$$
Z =
\begin{bmatrix}
	z^{(1)} \\
	z^{(2)} \\
	\vdots \\
	z^{(m)}
\end{bmatrix}
=
\begin{bmatrix}
	w_1 x_1^{(1)} + \dots + w_n x_n^{(1)} + b \\
	w_1 x_1^{(2)} + \dots + w_n x_n^{(2)} + b \\
	\vdots \\
	w_1 x_1^{(m)} + \dots + w_n x_n^{(m)} + b
\end{bmatrix}
=
\begin{bmatrix}
  x_1^{(1)} & \dots & x_n^{(1)} \\
  x_1^{(2)} & \dots & x_n^{(2)} \\
  \vdots & \vdots & \vdots \\
  x_1^{(m)} & \dots & x_n^{(m)}
\end{bmatrix}
\begin{bmatrix}
	w_1 \\
	w_2 \\
	\vdots \\
	w_n
\end{bmatrix}
+
\begin{bmatrix}
	b \\
	b \\
	\vdots \\
	b
\end{bmatrix}
$$
En simplifier
$$
Z = XW + b
$$


---
### $a(z)$
**sous forme de matrice**
$$
A = \frac{1}{1 + e^{-Z}}
$$


---
### Calcul des nouveaux $w_1, w_2, ..., w_n$ avec la descente de gradients
**sous forme de matrices**
$$
w_n = w_n - \alpha \frac{d \mathcal{L}}{d w_n}
$$
 sauf que maintenant, au lieu de calculer les modifications pour chaque poids ($w_x$) séparément, ont peut tous calculer en une fois en remplacent $w_x$ par la matrice de tous les $w$.
 $$
 W = W - \alpha \frac{d \mathcal{L}}{d W}
 $$
**Ce que donne** $\frac{d \mathcal{L}}{d W}$
$$
\frac{d \mathcal{L}}{d W} =
\begin{bmatrix}
	\frac{d \mathcal{L}}{d w_1} \\
	\frac{d \mathcal{L}}{d w_2} \\
	\vdots \\
	\frac{d \mathcal{L}}{d w_n}
\end{bmatrix}
= \frac{1}{m}
\begin{bmatrix}
	\sum_{i=1}^m (a^{(i)} - y^{(i)}) x_1^{(i)} \\
	\sum_{i=1}^m (a^{(i)} - y^{(i)}) x_2^{(i)} \\
	\vdots \\
	\sum_{i=1}^m (a^{(i)} - y^{(i)}) x_n^{(i)}
\end{bmatrix}
= \frac{1}{m}
\begin{bmatrix}
	x_1^{(1)} && x_1^{(2)} && \dots && x_1^{(m)} \\
	x_2^{(1)} && x_2^{(2)} && \dots && x_2^{(m)} \\
	\vdots && \vdots && \vdots && \vdots \\
	x_n^{(1)} && x_n^{(2)} && \dots && x_n^{(m)}
\end{bmatrix}
(
\begin{bmatrix}
	a^{(1)} \\
	a^{(2)} \\
	\vdots \\
	a^{(m)}
\end{bmatrix}
-
\begin{bmatrix}
	y^{(1)} \\
	y^{(2)} \\
	\vdots \\
	y^{(m)}
\end{bmatrix}
)
$$
donc, en mieux écrit
$$
\frac{d \mathcal{L}}{d W} = \frac{1}{m} X^T (A - Y)
$$
Où
- $X^T$ : Matrice X transposée
- $A$ : matrice des $a$
- Y : matrice des $y$ attendue (bonnes réponsses)


**Pour le biais** ($b$), vus qu'il est inutile de le changer en vecteur, il reste $b$ simple.
$$
b = b -\alpha \frac{d \mathcal{L}}{d b}
$$
Où
$$
\frac{d \mathcal{L}}{d b} = \frac{1}{m} \sum_{i=1}^m (A - Y)
$$
- $A$ : matrice des $a$
- Y : matrice des $y$ attendue (bonnes réponsses)

