# Policy déterministe

> Une policy déterministe renvoie toujours la même action pour un même état, contrairement à une [[2 Stochastic Policy|policy stochastique]].

Elle s'écrit :

$$
a_t=\pi(s_t).
$$

Pour trois passages dans le même état $s$, elle produit donc la même action :

$$
\begin{aligned}
\pi(s) &= \text{action(droite)} \\
\pi(s) &= \text{action(droite)} \\
\pi(s) &= \text{action(droite)}.
\end{aligned}
$$

## Exploration

« Déterministe » ne signifie pas que l'agent n'explore jamais. Pendant l'entraînement, on peut exécuter une action bruitée, par exemple $a_t=\pi(s_t)+\varepsilon$, tout en conservant une policy cible déterministe. Il faut alors distinguer la policy apprise du comportement utilisé pour explorer.
