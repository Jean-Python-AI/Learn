# Monte Carlo

> En apprentissage par renforcement, les méthodes **Monte Carlo** classiques estiment la valeur des états ou des actions à partir de **retours observés sur des épisodes complets**.

Plus généralement, Monte Carlo désigne des méthodes d’estimation fondées sur des échantillons aléatoires. Cette fiche traite de leur application au RL.

## Intuition

Un agent traverse un labyrinthe. Il attend la fin du parcours, puis regarde combien chaque état visité lui a finalement rapporté. En répétant les parcours, il estime leur valeur moyenne.

On n’a pas besoin de connaître les probabilités de transition de l’environnement : on utilise l’expérience obtenue en suivant une [[AI/Learning/3 Reinforcement Learning/Policy/0 Index|policy]].

## Le return observé

On note $r_{t+1}$ la récompense reçue après l’action $a_t$. Si l’épisode se termine à l’instant $T$ :

$$
G_t=r_{t+1}+\gamma r_{t+2}+\cdots+\gamma^{T-t-1}r_T.
$$

Ce return constitue la **cible** : la valeur observée vers laquelle on ajuste l’estimation.

Pour estimer la valeur d’un état sous une policy fixée $\pi$ :

$$
V(s_t)\leftarrow V(s_t)+\alpha\bigl[G_t-V(s_t)\bigr].
$$

- $V(s_t)$ : estimation actuelle de $V^\pi(s_t)$.
- $G_t$ : return réellement observé après cette visite.
- $\alpha$ : taux d’apprentissage, avec $0<\alpha\leq1$.

Avec $\alpha=1/N(s)$, où $N(s)$ compte les retours retenus pour l’état $s$, cette mise à jour calcule leur moyenne arithmétique. Un taux constant donne davantage de poids aux expériences récentes.

## Exemple

Depuis un état $s$, l’agent reçoit successivement $0$, $0$, puis $10$, et l’épisode se termine. Avec $\gamma=0{,}9$ :

$$
G_t=0+0{,}9\times0+0{,}9^2\times10=8{,}1.
$$

Si $V(s)=4$ et $\alpha=0{,}1$ :

$$
V(s)\leftarrow4+0{,}1(8{,}1-4)=4{,}41.
$$

L’agent rapproche son estimation du résultat obtenu ; une seule expérience ne suffit pas à connaître la valeur moyenne réelle.

## Si un état apparaît plusieurs fois

- **First-visit Monte Carlo** : on retient uniquement le return suivant la première visite de cet état dans chaque épisode.
- **Every-visit Monte Carlo** : on retient le return suivant chaque visite.

## Apprendre à choisir des actions

On peut estimer $Q(s,a)$ de la même manière :

$$
Q(s_t,a_t)\leftarrow Q(s_t,a_t)+\alpha\bigl[G_t-Q(s_t,a_t)\bigr].
$$

Pour améliorer la policy, l’agent favorise ensuite les actions dont la valeur estimée est élevée, tout en continuant à **explorer**. Sans exploration suffisante, certaines bonnes actions risquent de ne jamais être découvertes.

## Forces et limites

- La cible utilise les récompenses observées jusqu’à la fin, sans estimer la valeur d’un état futur : il n’y a pas de *bootstrapping*.
- Il faut attendre la fin de l’épisode ; la méthode classique ne convient donc pas directement à une tâche qui ne se termine jamais.
- Les retours peuvent varier fortement entre épisodes, ce qui rend les estimations parfois lentes à stabiliser.

Voir [[AI/Learning/3 Reinforcement Learning/Methods/Temporal Difference/0 Index|Différence temporelle]] pour apprendre avant la fin d’un épisode, et [[AI/Learning/3 Reinforcement Learning/Methods/0 Index|Méthodes d’apprentissage]] pour la vue d’ensemble.
