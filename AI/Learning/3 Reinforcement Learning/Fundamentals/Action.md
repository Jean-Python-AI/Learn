# Action

> Une action est une décision appliquée par l'agent à l'environnement à un instant donné.

Exemples : choisir une direction, sélectionner une vitesse de moteur, appliquer un couple ou cliquer sur un bouton. On la note généralement $a_t$.

L'ensemble des actions possibles est l'**espace d'actions** $\mathcal A$ :

- [[AI/Learning/3 Reinforcement Learning/Policy/3 Discrete Action Space|discret]] : une liste finie, par exemple $\{\text{gauche},\text{ne rien faire},\text{droite}\}$ ;
- [[AI/Learning/3 Reinforcement Learning/Policy/4 Continuous Action Space|continu]] : une ou plusieurs valeurs réelles, par exemple $a_t\in[-1,1]$.

Une [[AI/Learning/3 Reinforcement Learning/Policy/0 Index|policy]] choisit ou échantillonne l'action en fonction de l'état disponible.
