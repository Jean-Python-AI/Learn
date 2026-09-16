# Espace d'actions continu

> Un espace d'actions continu contient une infinité de valeurs possibles. La policy détermine une action en fonction de l'état $s$, contrairement à une [[3 Discrete Action Space|policy à espace discret]].

Par exemple :

$$
\mathcal A=[-1,1].
$$

Les actions possibles peuvent donc être :

$$
\begin{aligned}
-0.8345 \\
0.3215 \\
0.9873 \\
-0.1479 \\
\dots
\end{aligned}
$$

Une [[1 Deterministic Policy|policy déterministe]] retourne une valeur précise :

$$
a_t=\pi(s_t)=0.3781.
$$

Une [[2 Stochastic Policy|policy stochastique]] peut produire les paramètres d'une distribution, par exemple :

$$
s_t \rightarrow \pi \rightarrow
\begin{bmatrix}
\mu=0.2 \\
\sigma=0.3
\end{bmatrix}.
$$

On construit alors une distribution gaussienne à partir de ces deux éléments, $\mu$ et $\sigma$ :

![[Continuous_Stochastic.svg|479]]

On y échantillonne enfin une action. Pour le même état, cela peut donner différentes actions :

$$
\begin{aligned}
a_t &= 0.18 \\
a_t &= 0.23 \\
a_t &= 0.39 \\
a_t &= 0.15 \\
a_t &= \dots
\end{aligned}
$$

## Attention aux bornes

Une Gaussienne a un support non borné : elle peut échantillonner une valeur hors de $[-1,1]$. Lorsqu'une action doit respecter des bornes physiques, il faut utiliser une distribution bornée ou transformer un échantillon, par exemple $a_t=\tanh(u_t)$ avec $u_t\sim\mathcal N(\mu,\sigma)$. Cette transformation doit aussi être prise en compte lorsqu'on calcule la log-probabilité de l'action en policy gradient.
