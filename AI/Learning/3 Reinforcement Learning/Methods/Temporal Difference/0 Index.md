# Différence temporelle — Temporal Difference (TD)

> Les méthodes **TD** apprennent en comparant une estimation actuelle à une nouvelle cible construite à partir de récompenses observées et d’une estimation de la suite.

La version à un pas peut mettre à jour une valeur après chaque transition, sans attendre la fin de l’épisode.

## Intuition : apprendre à partir d’une estimation

Dans un labyrinthe, l’agent pense qu’une case vaut $4$. Il reçoit une récompense de $0$, puis arrive sur une case qu’il estime valoir $6$.

Même sans connaître la fin du parcours, il peut revoir la valeur de la première case : elle donne accès à une suite qui semble plus favorable que prévu.

Utiliser une estimation pour en mettre à jour une autre s’appelle le **bootstrapping**.

## TD(0) : évaluer une policy

L’agent suit une policy $\pi$ et observe une transition $(s_t,a_t,r_{t+1},s_{t+1})$. Pour estimer $V^\pi$, TD(0) utilise la cible :

$$
\text{cible TD}=r_{t+1}+\gamma V(s_{t+1}).
$$

L’**erreur de différence temporelle** est l’écart entre cette cible et la valeur actuelle :

$$
\delta_t=r_{t+1}+\gamma V(s_{t+1})-V(s_t).
$$

La mise à jour est :

$$
\boxed{V(s_t)\leftarrow V(s_t)+\alpha\delta_t}.
$$

- $\alpha$ contrôle la taille de la correction.
- $\gamma$ pondère la valeur future.
- Si $s_{t+1}$ est terminal, la valeur future vaut $0$ : la cible se réduit à $r_{t+1}$.

## Exemple numérique

Avec $V(s_t)=4$, $r_{t+1}=0$, $V(s_{t+1})=6$, $\gamma=0{,}9$ et $\alpha=0{,}1$ :

$$
\delta_t=0+0{,}9\times6-4=1{,}4,
$$

$$
V(s_t)\leftarrow4+0{,}1\times1{,}4=4{,}14.
$$

Cette correction dépend de la qualité de l’estimation du prochain état. Au fil des transitions, les estimations sont révisées à partir de nouvelles observations.

## Différence avec Monte Carlo

| | Monte Carlo classique | TD(0) |
| --- | --- | --- |
| Cible | $G_t$, le return complet observé | $r_{t+1}+\gamma V(s_{t+1})$ |
| Moment de la mise à jour | Après la fin de l’épisode | Après une transition |
| Utilise une estimation du futur | Non | Oui |
| Tâches sans fin d’épisode | Pas directement | Oui, avec un return bien défini |

La cible TD dépend d’une estimation qui peut être inexacte ; elle présente souvent moins de variabilité que le return complet de [[AI/Learning/3 Reinforcement Learning/Methods/Monte Carlo|Monte Carlo]]. Aucune de ces méthodes n’est systématiquement meilleure dans tous les problèmes.

## De l’évaluation au choix des actions

TD(0), présenté ci-dessus, évalue une policy avec $V(s)$. D’autres algorithmes TD apprennent des valeurs d’action $Q(s,a)$ pour améliorer les décisions :

- **SARSA** utilise la valeur de l’action effectivement choisie dans l’état suivant : $r_{t+1}+\gamma Q(s_{t+1},a_{t+1})$.
- Le **[[AI/Learning/3 Reinforcement Learning/Methods/Temporal Difference/Q-Learning|Q-learning]]** utilise la meilleure valeur estimée dans l’état suivant : $r_{t+1}+\gamma\max_{a'}Q(s_{t+1},a')$.

La famille TD comprend aussi des méthodes à plusieurs pas, qui utilisent plusieurs récompenses avant d’estimer la suite.

Retour : [[AI/Learning/3 Reinforcement Learning/Methods/0 Index|Méthodes d’apprentissage]].
