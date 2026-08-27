![[a(z).svg|460]]
$a(z)$ = sortie final du perceptron
cela correspond à une probabilité qui se trouve entre 0 et 1 de faire partie d'une des deux cathégories.

**Formule mathématique pour trouver $a(z)$ en fonction de $z$ :**
$$
a(z) = \frac{1}{1+e^{-z}}
$$

**ATTENTION** en programation, on utilise des vecteurs au lieux d'éxecuter plusieurs fois les mêmes calculs.
Pour retrouver la fonction $a(z)$ vectoriser => [[Vectorisation des fonctions]]