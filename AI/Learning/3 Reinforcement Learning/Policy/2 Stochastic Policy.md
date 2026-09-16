# Policy stochastique

> Une policy stochastique associe à un état une distribution de probabilité sur les actions possibles, contrairement à une [[1 Deterministic Policy|policy déterministe]] qui renvoie toujours la même action.

Elle se note :

$$
\pi(a\mid s)=P(A_t=a\mid S_t=s).
$$

La policy fournit une distribution, puis l'agent y effectue un tirage. Dans un espace discret :

$$
s \xrightarrow{\pi}
\begin{bmatrix}
\text{gauche} & 0.2 \\
\text{rester} & 0.3 \\
\text{droite} & 0.5
\end{bmatrix}
\xrightarrow{\text{échantillonnage}}
\text{action(droite)}.
$$

- $s$ : état en entrée ;
- $\pi$ : policy ;
- « gauche, $0.2$ » : $20\%$ de probabilité de choisir l'action gauche ;
- échantillonnage : tirage aléatoire suivant cette distribution.

Les probabilités des actions possibles doivent sommer à $1$. Pour le même état répété, les actions observées peuvent donc différer :

$$
\begin{aligned}
a_t &= \text{action(droite)} \\
a_t &= \text{action(rester)} \\
a_t &= \text{action(droite)}.
\end{aligned}
$$
Pour que les probabilité d'action somme à 1, il faut utiliser [[SoftMax]].



Voir aussi [[3 Discrete Action Space|espace discret]] et [[4 Continuous Action Space|espace continu]].
