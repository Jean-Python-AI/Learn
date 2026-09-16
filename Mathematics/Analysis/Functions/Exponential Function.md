![[Exponential_curve.svg|545]]

Une fonction exponentiel doit être égale à ça propre dérivée.

---
### Comment on a trouver le $e$ ?

Pour que $f(x) = f'(x)$ il faut :
![[expliationHow_e.svg|477]]
Donc, la fonction d'une exponentiel est:
$$
f(x) = 1 + x + \frac{x^2}{2} + \frac{x^3}{6} + \frac{x^4}{24} + \frac{x^5}{120} + \dots
$$
ce qui est égale à ça dérivée :
$$
f'(x) = 0 + 1 + x + \frac{x^2}{2} + \frac{x^3}{6} + \frac{x^4}{24} + \frac{x^5}{120} + \dots
$$

Cette fonction peut s'écrire différement:
$$
f(x) = \frac{x^0}{0!} + \frac{x^1}{1!} + \frac{x^2}{2!} + \frac{x^3}{3!} + \frac{x^4}{4!} + \frac{x^5}{5!} + \dots
$$
Si je ne me rappel plus ce que veut dire le $!$ il faut aller voir dans [[Factoriel]]

Si on simplifie la fonction:
$$
f(x) = \sum_{i=0}^∞ \frac{x^i}{i!}
$$

Mais, si on remplace $x$ par $1$ :
$$
1 + 1 + \frac{1}{2} + \frac{1}{6} + \frac{1}{24} + \frac{1}{120} + \dots = 2,718 = e
$$

Une fonction exponentiel s'écrit donc:
$$
f(x) = e^x
$$

---

### Dérivée une fonction exponentiel

$$
f'(x) = (e^{ax})' = a \cdot e^{ax}
$$

---

**L'inverse d'une exponentiel** est un *logartihme normal* [[Logarithm|Plus d'explications]]
