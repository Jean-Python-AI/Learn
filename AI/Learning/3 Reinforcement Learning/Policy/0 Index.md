Une **Policy** est une règle utilisé par l'agent pour décider l'action qu'il va prendre.

$$
s_t​→a_t​
$$
La policy return une action ($a_t$) en fonction d'un état à l'instant $t$ ($s_t$).

**Attention**, Policy ≠ Agent
- Agent : système complet qui interagit avec l'environnement.
- Policy : a partie qui décide des actions, le "cerceau".


Une Policy n'est pas spécialement un réseau de neurones.
Il peut aussi être quelque chose de très simple comme:
```python
if angle > 0:
    action = left
else:
    action = right
```



Il y a différents types de Policy.
En fonction de *comment elle choisissent une action*:
    [[1 Deterministic Policy|Deterministic]] ou [[2 Stochastic Policy|Stochastic]]
Et en fonction de *Quelle type d'actions elle choisissent:*
    [[3 Discrete Action Space|Discrete]] ou [[4 Continuous Action Space|Continuous]]

|                   | **Discrete**               | **Continuous**                  |
| ----------------- | -------------------------- | ------------------------------- |
| **Deterministic** | une action précise         | une valeur précise              |
| **Stochastic**    | une probabilité par action | une distribution de probabilité |
