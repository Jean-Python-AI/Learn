Une **deterministic policy** défini une policy qui pour un état donné va toujour retourner la même action (contrairement à une policy [[2 Stochastic Policy|stochastic]]).
$$
\begin{aligned}
s_a = action(right) \\
s_a = action(right) \\
s_a = action(right)
\end{aligned}
$$

**Attention** deterministic ne signifie pas que l'agent n'explore jamais. Il est possible d'utiliser du bruit lors de l'entrainement pour explorer.

