**M**arkov **D**ecision **P**rocess

Dans le MDP, on enregistre tous les états d'une "session" d'entrainement.

$$
s_0, a_0, r_0, s_1, a_1, r_1, s_2, a_2, r_2, \dots
$$

**Policy** $\pi$ : est le modèle, ce qui fait passer $s \rightarrow a$
$\pi(a|s)$ = probabilité de faire l'action $a$ en fonction de l'état $s$


**Return** $G_t$ : est le reward de l'action en fonction des rewards suivant
$$
G_t = r_t + \gamma r_{t+1} + \gamma^2 r_{t+2} + \gamma^3 r_{t+3} + \dots
$$
où $0 ≤ \gamma ≤ 1$ : plus gamma est grand plus le modèle apprendra à jouer long terme (et inversément)

**GOAL** : maximise policy that maximise return

