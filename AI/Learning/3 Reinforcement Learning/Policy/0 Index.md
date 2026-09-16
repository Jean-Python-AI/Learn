# Policy

> Une **policy** $\pi$ est la règle utilisée par l'agent pour choisir une action à partir de l'état (ou de l'observation) courant.

Une policy déterministe associe directement une action à un état :

$$
a_t=\pi(s_t).
$$

Une policy stochastique associe une **distribution** d'actions à un état, puis une action est échantillonnée :

$$
a_t\sim\pi(\cdot\mid s_t).
$$

## Policy $\ne$ agent

- **Agent** : le système complet qui interagit avec l'environnement et peut apprendre, mémoriser ou planifier.
- **Policy** : la partie qui décide de l'action, parfois appelée le « cerveau » décisionnel de l'agent.

Une policy n'est pas nécessairement un réseau de neurones. Elle peut être une règle très simple :

```python
if angle > 0:
    action = "left"
else:
    action = "right"
```

## Deux axes de description

On distingue une policy par la manière dont elle choisit, puis par le type d'action qu'elle manipule :

- [[1 Deterministic Policy|déterministe]] ou [[2 Stochastic Policy|stochastique]] ;
- [[3 Discrete Action Space|espace d'actions discret]] ou [[4 Continuous Action Space|espace d'actions continu]].

| | **Discret** | **Continu** |
| --- | --- | --- |
| **Déterministe** | une action précise | une valeur précise ou un vecteur précis |
| **Stochastique** | une probabilité par action | une distribution de probabilité sur les actions |
