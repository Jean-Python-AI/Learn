Lorsqu'une policy est défini par **continuous action space**, cela signifie que l'action déterminé par la policy en fonction de $s$ peut prendre une infinité de valeurs dans un intervalle (contrairement à une [[3 Discrete Action Space|policy discrete]]).

Par exemple:
$$
action∈[−1,1]
$$

les actions pourrais donc être:
$$
\begin{aligned}
-0.8345 \\
0.3215 \\
0.9873 \\
-0.1479 \\
\dots
\end{aligned}
$$

Une [[1 Deterministic Policy|policy déterministe]] ferais donc:
$state = 0.3781$


Alors qu'une [[2 Stochastic Policy|policy stochastic]] ferais:
$state → \pi → \begin{bmatrix}μ=0.2 \\ σ=0.2\end{bmatrix}$
pour ensuite créer la distribution gaussienne en fonction de ces deux éléments ($μ$ et $σ$)
![[Continuous_Stochastic.svg|479]]
Et enfin, on tire une action dans cette distribution.
Ce qui donnera pour le même state, différentes actions possible.
$$
\begin{aligned}
state = 0.18 \\
state = 0.23 \\
state = 0.39 \\
state = 0.15 \\
state = \dots
\end{aligned}
$$

