# Reinforcement Learning (RL)

> Le reinforcement learning apprend à un **agent** à prendre des décisions par interaction. On ne lui fournit pas la bonne action à chaque étape ; on lui fournit un signal de **récompense** qui indique si les conséquences de ses actions sont souhaitables.

## Boucle d'interaction

À l'instant $t$, l'agent observe un état (ou une observation) $s_t$, choisit une action $a_t$, puis l'environnement produit une récompense $r_{t+1}$ et un nouvel état $s_{t+1}$ :

$$
s_t \xrightarrow{\text{agent / policy}} a_t
\xrightarrow{\text{environnement}} (r_{t+1}, s_{t+1}).
$$

![[RL.svg|692]]

- **État** : par exemple une position, une vitesse ou la couleur de pixels ; voir [[AI/Learning/3 Reinforcement Learning/Fundamentals/State|État]].
- **Action** : par exemple une vitesse de moteur ou une direction ; voir [[AI/Learning/3 Reinforcement Learning/Fundamentals/Action|Action]].
- **Récompense** : un nombre qui peut être positif ou négatif ; une « punition » est simplement une récompense négative. Voir [[AI/Learning/3 Reinforcement Learning/Fundamentals/Reward|Récompense]].

L'objectif n'est pas de maximiser une récompense isolée, mais le **return attendu** : la somme pondérée des récompenses futures. Cette formalisation apparaît dans [[AI/Learning/3 Reinforcement Learning/MDP/0 Index|MDP et return]].

## Carte du sujet

- [[AI/Learning/3 Reinforcement Learning/Fundamentals/0 Index|Fondamentaux]] — agent, environnement, état, action et récompense.
- [[AI/Learning/3 Reinforcement Learning/Policy/0 Index|Policy]] — règle ou distribution qui transforme un état en action.
- [[AI/Learning/3 Reinforcement Learning/MDP/0 Index|MDP]] — cadre mathématique de la décision séquentielle.
- [[AI/Learning/3 Reinforcement Learning/Methods/0 Index|Méthodes d’apprentissage]] — Monte Carlo, différence temporelle et Q-learning.
- [[AI/Learning/3 Reinforcement Learning/z Sources|Sources]] — ressources utilisées.
