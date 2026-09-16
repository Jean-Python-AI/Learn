# Markov Decision Process (MDP)

> Un **processus de décision markovien** est le cadre mathématique le plus courant pour modéliser un problème de reinforcement learning. Un MDP n'est pas l'enregistrement d'une session : c'est le modèle qui décrit les états, les actions, les transitions et les récompenses.

On le note généralement :

$$
(\mathcal S,\mathcal A,P,R,\gamma),
$$

où :

- $\mathcal S$ est l'ensemble des états ;
- $\mathcal A$ est l'ensemble des actions ;
- $P(s'\mid s,a)$ décrit la transition vers l'état suivant ;
- $R$ décrit la récompense ;
- $\gamma$ est le facteur d'actualisation.

## Trajectoire d'un épisode

Lors d'une session d'entraînement, on peut enregistrer une trajectoire générée dans le MDP :

$$
s_0, a_0, r_0, s_1, a_1, r_1, s_2, a_2, r_2, \dots
$$

Cette note utilise la convention où $r_t$ est la récompense obtenue après l'action $a_t$. Une autre convention fréquente écrit $r_{t+1}$ pour cette même récompense ; l'essentiel est de rester cohérent dans toutes les formules.
A noter que souvent, on enregistre en plus de l'action $a_t$, la probabilité d'avoir fait cette action $p_t$ (si il y a des probabilité qui rentre en jeu).

## Policy $\pi$

La **policy** est la règle ou le modèle qui fait passer d'un état à une action — ou, dans le cas stochastique, à une distribution d'actions.

[[AI/Learning/3 Reinforcement Learning/Policy/0 Index|policy]]

## Return $G_t$

Le return à l'instant $t$ est la somme pondérée des récompenses présentes et futures :

$$
G_t = r_t + \gamma r_{t+1} + \gamma^2 r_{t+2} + \gamma^3 r_{t+3} + \dots
$$

avec $0\leq\gamma\leq1$. Plus $\gamma$ est grand, plus l'agent tient compte des conséquences à long terme ; plus il est faible, plus il privilégie les récompenses immédiates.

## Objectif

Apprendre une policy qui maximise le **return attendu** :

$$
\pi^*=\arg\max_\pi\;\mathbb E_\pi[G_t].
$$
