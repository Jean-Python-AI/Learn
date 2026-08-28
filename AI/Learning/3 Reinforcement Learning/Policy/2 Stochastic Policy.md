Une **Stochastic Policy** défini une policy qui pour un état donné vas retourner la liste des actions possible avec leurs probabilitées d'être faite (contrairement à une policy [[1 Deterministic Policy|Deterministic]] qui fera toujours la même chose).

$$
s→P(a∣s)
$$
La policy vas donné la probalité de prendre l'action $a$ en fonction de $s$.

Ce qui donnera par exemple:
$$
s → \pi →
\begin{bmatrix}
 left && 0.2 \\
 stay && 0.3 \\
 right && 0.5
\end{bmatrix}
→ sample → action(right)
$$
- $s$ : état (input)
- $\pi$ : policy
- $left$  $0.2$ = $20$% de chance de faire l'action $left$
- $sample$ : tirage au sort


Cela vas donc donné en sortie pour le même états répété plusieurs fois, ceci:
$$
\begin{aligned}
s_a = action(right) \\
s_a = action(stay) \\
s_a = action(right)
\end{aligned}
$$

