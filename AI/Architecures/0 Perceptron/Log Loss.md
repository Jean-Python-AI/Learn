![[log_loss.svg|515]]
La *Log Loss* function permet de mesurer la vraisemblance d'un modèle.

**Log Loss function :**
$$
\mathcal{L} = -\frac{1}{m} * \sum_{i = 1}^{m} y_i \log(a_i) + (1-y_i)\log(1-a_i)
$$
- $\mathcal{L}$ : Log Loss
- $m$ : nombre d'éléments (pour le graphique d'exemple $\Rightarrow$ 6 )
- $\log(...)$ : logarithme naturel donc logarithme en base $e$ qui s'écrit en parfois $\ln(...)$



**ATTENTION** en programation, on utilise des vecteurs au lieux d'éxecuter plusieurs fois les mêmes calculs.
Pour retrouver la fonction *Log Loss* vectoriser => [[Vectorisation des fonctions]]

La fonction *Log Loss* vectorisée
$$
\mathcal{L} = -\frac{1}{m} * \sum_{i = 1}^{m} y_i \log(A) + (1-y_i)\log(1-A)
$$
on remplace juste les $a_1, a_2, \dots a_i$ par une matrice $A$