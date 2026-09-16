# Agent

> L'agent est le système qui reçoit de l'information sur son environnement et choisit les actions à y appliquer.

À l'instant $t$, il utilise l'état ou l'observation disponible pour sélectionner $a_t$. Son comportement peut inclure une [[AI/Learning/3 Reinforcement Learning/Policy/0 Index|policy]], de la mémoire, un modèle du monde ou un algorithme de planification.

L'agent n'est donc pas forcément un réseau de neurones. Une règle écrite à la main, une table de valeurs ou un réseau de neurones peuvent tous jouer ce rôle.

## Dans la boucle RL

$$
s_t \xrightarrow{\text{agent}} a_t.
$$

- Ce que l'agent **observe** : [[AI/Learning/3 Reinforcement Learning/Fundamentals/State|État]].
- Ce qu'il **choisit** : [[AI/Learning/3 Reinforcement Learning/Fundamentals/Action|Action]].
- Ce qui guide son apprentissage : [[AI/Learning/3 Reinforcement Learning/Fundamentals/Reward|Récompense]].
