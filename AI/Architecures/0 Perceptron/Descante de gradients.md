L'algorithme de la descante de gradients vas modifier les différents poids ($w_1$, $w_2$, ...) et le biais ($b$) du modèle dans l'objectif de  maximiser la vraisemblance de $\mathcal{L}$ en minimisant la fonction "$-\log{\mathcal{L}}$".
Car en mathématique ont ne peut pas maximiser mais uniquement minimiser.

Pour minimiser le *Log Loss*, l'algorithme de *descente de gradients* vas calculer les $w$ et le $b$ qu'il faut au perceptron.

Pour cela, ont doit calculer le *gradient* (dit autrement, la dérivée) de notre fonction coût.

On utilise cette formule pour calculer le nouveau paramètre $w$ :
$$
W_{t+1} = W_t - \alpha \frac{d \mathcal{L}}{d W_t}
$$
- $W_{t+1}$ : paramètre $w$ à l'instant $t+1$
- $W_t$ : paramètre $w$ à l'instant $t$
- $\alpha$ : pas d'apprentissage positif
- $\frac{d \mathcal{L}}{d W_t}$ : Gradient à l'instant $t$

![[logLoss_by_W.svg|385]]

**Attention :** ce qu'il faut pour que la *descente de gradients* fonctionne correctement, c'est que la fonction soit convexe, c'est a dire quelle ne contienne pas de minimum local. Juste un minimum global.


---

#### Calcul de ce que vaut $\frac{d \mathcal{L}}{d W}$

On peut dérivé le *Log Loss* comme ceci
$$
\frac{d \mathcal{L}}{d w_1} = \frac{d \mathcal{L}}{d a} * \frac{d a}{d z} * \frac{d z}{d w_1}
$$
Où
$$
\frac{d \mathcal{L}}{d a} = \frac{-1}{m} \sum_{i=1}^{m} \frac{y}{a} - \frac{1-y}{1-a}
$$
$$
\frac{d a}{d z} = a (1 - a)
$$
$$
\frac{d z}{d w_1} = x_1
$$
et donc

**Pour $w_1$ :**
$$
\frac{d \mathcal{L}}{d w_1} = \frac{1}{m} \sum_{i=1}^{m} (y - a) x_1
$$
**Pour $w_n$ :**
$$
\frac{d \mathcal{L}}{d w_n} = \frac{1}{m} \sum_{i=1}^{m} (y - a) x_n
$$

**Pour le biais $b$ :**
$$
\frac{d \mathcal{L}}{d b} = \frac{1}{m} \sum_{i=1}^{m} (y - a)
$$


**ATTENTION** en programation, on utilise des vecteurs au lieux d'éxecuter plusieurs fois les mêmes calculs.
Pour retrouver les différentes fonctions de la descente de gradiant vectorisées => [[Vectorisation des fonctions]]