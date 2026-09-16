# Récompense

> La récompense est un nombre qui évalue immédiatement la conséquence d'une transition ; elle est notée $r_{t+1}$ dans la convention la plus courante.

Une récompense positive encourage un comportement, une récompense négative le pénalise. Il ne s'agit pas d'une « bonne réponse » fournie à chaque étape : l'agent doit découvrir quelles suites d'actions conduisent à de bons résultats.

Le signal immédiat ne suffit pas toujours. L'objectif est de maximiser le **return attendu**, c'est-à-dire les récompenses futures pondérées :

$$
G_t = r_{t+1}+\gamma r_{t+2}+\gamma^2r_{t+3}+\cdots,
\qquad 0\leq\gamma\leq1.
$$

Voir [[AI/Learning/3 Reinforcement Learning/MDP/0 Index|MDP et return]] pour les conventions de notation et le rôle de $\gamma$.
