# Méthodes d’apprentissage par renforcement

> Un **MDP décrit un problème de décision**. Une **méthode d’apprentissage** utilise l’expérience de l’agent pour estimer quelles décisions rapportent le plus de récompenses à long terme.

## Cadre, politique et apprentissage

- Le [[AI/Learning/3 Reinforcement Learning/MDP/0 Index|MDP]] décrit les états, les actions, les transitions et les récompenses de l’environnement.
- La [[AI/Learning/3 Reinforcement Learning/Policy/0 Index|policy]] décrit comment l’agent choisit ses actions.
- La méthode d’apprentissage indique comment l’agent améliore ses estimations ou sa policy à partir de son expérience.

Dans un labyrinthe, le MDP décrit les déplacements possibles et leurs conséquences ; la policy choisit un déplacement ; l’apprentissage exploite les parcours pour améliorer les décisions.

## Notation utilisée dans ces fiches

Après l’action $a_t$ dans l’état $s_t$, l’agent reçoit $r_{t+1}$ et arrive dans $s_{t+1}$ :

$$
s_t \xrightarrow{a_t} (r_{t+1},s_{t+1}).
$$

Cette convention est celle de l’index général du RL. La fiche MDP note actuellement cette même récompense $r_t$ : seul le décalage des indices change.

Pour un épisode qui se termine à l’instant $T$, le **return** est :

$$
G_t=\sum_{k=0}^{T-t-1}\gamma^k r_{t+k+1}.
$$

Le facteur $\gamma$ pondère les récompenses futures. On prend généralement $0\leq\gamma<1$ pour une tâche continue ; $\gamma=1$ est aussi possible pour des épisodes finis lorsque les retours sont bien définis.

## Qu’apprend-on ?

Deux fonctions de valeur sont courantes :

- $V^\pi(s)$ : le return moyen attendu en partant de l’état $s$, puis en suivant la policy $\pi$.
- $Q^\pi(s,a)$ : le return moyen attendu en choisissant d’abord l’action $a$ dans l’état $s$, puis en suivant $\pi$.

**Évaluer une policy** consiste à estimer ses valeurs. **Améliorer la policy**, ou faire du *contrôle*, consiste à rechercher de meilleures décisions à l’aide de ces valeurs, par exemple.

## Deux familles à découvrir

| Méthode                                                                                                  | Cible utilisée pour apprendre                         | Attend la fin de l’épisode ?              |
| -------------------------------------------------------------------------------------------------------- | ----------------------------------------------------- | ----------------------------------------- |
| [[AI/Learning/3 Reinforcement Learning/Methods/Monte Carlo\|Monte Carlo]]                                | Le return observé jusqu’à la fin                      | Oui, dans la version épisodique classique |
| [[AI/Learning/3 Reinforcement Learning/Methods/Temporal Difference/0 Index\|Différence temporelle — TD]] | Une récompense observée et une estimation de la suite | Non, pour les méthodes à un pas           |

Le [[AI/Learning/3 Reinforcement Learning/Methods/Temporal Difference/Q-Learning|Q-learning]] est un **algorithme de contrôle de la famille TD**. Il vise à apprendre $Q^*$, la valeur des actions lorsque la suite des décisions est optimale.

Ces méthodes peuvent apprendre à partir de transitions observées **sans connaître les probabilités de transition du MDP** : on parle de méthodes *model-free*. Cela ne signifie pas que le problème n’est pas un MDP.

## Ordre de lecture

1. [[AI/Learning/3 Reinforcement Learning/Methods/Monte Carlo|Monte Carlo]] : apprendre à partir d’un résultat complet.
2. [[AI/Learning/3 Reinforcement Learning/Methods/Temporal Difference/0 Index|Différence temporelle]] : apprendre avec une estimation du futur.
3. [[AI/Learning/3 Reinforcement Learning/Methods/Temporal Difference/Q-Learning|Q-learning]] : utiliser cette idée pour apprendre quelles actions choisir.
