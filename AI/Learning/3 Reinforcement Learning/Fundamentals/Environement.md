# Environnement

> L'environnement est le système extérieur avec lequel l'agent interagit : un simulateur, un jeu, un robot et son monde physique, ou tout autre processus à contrôler.

Après l'action $a_t$, il fait évoluer la situation et renvoie un nouvel état ainsi qu'une récompense :

$$
(s_t, a_t) \xrightarrow{\text{environnement}} (r_{t+1}, s_{t+1}).
$$

Cette évolution peut être déterministe ou aléatoire. Dans un [[AI/Learning/3 Reinforcement Learning/MDP/0 Index|MDP]], elle est décrite par une dynamique de transition et une fonction ou distribution de récompense.

L'environnement ne « connaît » pas forcément la bonne action : il fournit seulement les conséquences de l'action de l'agent.
