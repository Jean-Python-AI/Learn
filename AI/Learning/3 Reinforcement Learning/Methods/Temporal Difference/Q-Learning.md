> Le **Q-learning** est un algorithme d’apprentissage par renforcement de la famille [[AI/Learning/3 Reinforcement Learning/Methods/Temporal Difference/0 Index|Temporal Difference]]. Il apprend la valeur des actions pour déterminer lesquelles choisir.

Il peut apprendre à partir de transitions observées, sans connaître les probabilités de transition ni la fonction de récompense du [[AI/Learning/3 Reinforcement Learning/MDP/0 Index|MDP]]. Il est donc *model-free*.

**Bonne source :** [vidéo](https://www.youtube.com/watch?v=nOBm4aYEYR4)
## Que représente Q ?

$Q(s,a)$ estime le return attendu en prenant l’action $a$ dans l’état $s$. Le Q-learning vise la fonction optimale $Q^*(s,a)$ : prendre cette première action, puis agir de façon optimale.

Dans un petit problème discret, on peut utiliser une **table Q** : une ligne par état et une colonne par action. Un réseau de neurones n’est pas nécessaire.

Par exemple, dans une case du labyrinthe :

| Action | Valeur Q estimée |
| --- | --- |
| Haut | $2$ |
| Bas | $-1$ |
| Gauche | $0$ |
| Droite | $5$ |

L’action actuellement préférée est « droite ». Ces nombres sont des estimations de retours, **pas des probabilités** : leur somme n’a pas à valoir $1$.

## Formule de mise à jour

Après avoir observé $(s_t,a_t,r_{t+1},s_{t+1})$ :

$$
\boxed{
Q(s_t,a_t)\leftarrow Q(s_t,a_t)+\alpha
\left[r_{t+1}+\gamma\max_{a'}Q(s_{t+1},a')-Q(s_t,a_t)\right]
}.
$$

- $Q(s_t,a_t)$ : valeur actuelle de l’action effectuée.
- $\alpha$ : taux d’apprentissage.
- $r_{t+1}$ : récompense reçue après cette action.
- $\gamma$ : facteur d’actualisation.
- $\max_{a'}Q(s_{t+1},a')$ : meilleure valeur estimée parmi les actions possibles dans l’état suivant.

La formule suit le schéma :

$$
\text{nouvelle estimation}
=\text{ancienne estimation}
+\alpha(\text{cible}-\text{ancienne estimation}).
$$

**Si l’état suivant est terminal**, il ne reste aucune récompense future : la cible est uniquement $r_{t+1}$. On n’applique pas le maximum à des actions inexistantes.

## Exemple numérique

L’agent choisit « droite » dans l’état $s$. Supposons :

- $Q(s,\text{droite})=2$ ;
- une récompense reçue de $1$ ;
- une meilleure valeur estimée de $5$ dans le nouvel état, non terminal ;
- $\gamma=0{,}9$ et $\alpha=0{,}1$.

La cible vaut :

$$
1+0{,}9\times5=5{,}5.
$$

La mise à jour donne :

$$
Q(s,\text{droite})\leftarrow2+0{,}1(5{,}5-2)=2{,}35.
$$

La valeur de cette action augmente, car la transition observée suggère un meilleur résultat que prévu.

## Explorer et exploiter

Choisir toujours la meilleure action connue peut empêcher de découvrir une meilleure option. Une policy **$\varepsilon$-greedy** permet de combiner :

- **Exploration** : avec une probabilité $\varepsilon$, choisir une action au hasard parmi les actions possibles.
- **Exploitation** : sinon, choisir une action qui maximise $Q(s,a)$.

Le maximum de la formule d’apprentissage n’impose donc pas l’action qui sera réellement effectuée au prochain pas : l’agent peut explorer.

## Pourquoi dit-on « off-policy » ?

Le Q-learning apprend la valeur d’une suite de décisions gloutonnes, qui choisissent les actions de valeur maximale, même lorsque les expériences proviennent d’une policy exploratoire.

La **policy qui produit les expériences** et la **policy visée par l’apprentissage** peuvent ainsi être différentes : c’est le sens de *off-policy*.

## Déroulement d’un épisode

Initialiser la table Q avant l’entraînement, puis, pour chaque épisode :

1. Observer l’état initial.
2. Choisir une action, par exemple avec une policy $\varepsilon$-greedy.
3. Exécuter l’action et observer la récompense et le nouvel état.
4. Mettre à jour la case $Q(s_t,a_t)$ avec la formule.
5. Recommencer depuis le nouvel état jusqu’à la fin de l’épisode.

La table est conservée d’un épisode au suivant. Les mises à jour répétées permettent aux récompenses obtenues en fin de parcours d’influencer progressivement les valeurs des actions précédentes.

## Limites et prolongement

Une table devient peu pratique lorsque les états ou les actions sont très nombreux ou continus. Un **DQN** utilise un réseau de neurones pour approximer les valeurs Q, généralement pour un ensemble discret d’actions.

Dans un MDP fini, le Q-learning tabulaire converge vers $Q^*$ sous des conditions précises, notamment des récompenses bornées, un facteur $\gamma<1$, une exploration de chaque paire état-action indéfiniment et des taux d’apprentissage adaptés. Avec un réseau de neurones, cette garantie ne s’applique pas automatiquement.

Retour : [[AI/Learning/3 Reinforcement Learning/Methods/0 Index|Méthodes d’apprentissage]]. Comparaison : [[AI/Learning/3 Reinforcement Learning/Methods/Monte Carlo|Monte Carlo]] utilise un return complet observé ; le Q-learning utilise une récompense et une estimation de la suite.
