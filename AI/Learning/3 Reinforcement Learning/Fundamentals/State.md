# État

> L'état $s_t$ est l'information utilisée par l'agent pour décider à l'instant $t$.

Selon le problème, il peut contenir une position, une vitesse, des mesures de capteurs ou des pixels. Par exemple, la position seule d'un pendule ne suffit généralement pas : sa vitesse angulaire est aussi nécessaire pour prédire son mouvement.

Dans un [[AI/Learning/3 Reinforcement Learning/MDP/0 Index|MDP]], un état est **markovien** si, une fois $s_t$ et $a_t$ connus, le passé n'apporte pas d'information supplémentaire pour prédire la distribution de la transition suivante.

## État et observation

L'agent ne voit pas toujours l'état complet du monde. Ce qu'il reçoit peut être une **observation** $o_t$ partielle ou bruitée. Dans ce cas, la policy agit sur $o_t$ (et parfois sur une mémoire de l'historique) plutôt que sur un état parfaitement observable.
