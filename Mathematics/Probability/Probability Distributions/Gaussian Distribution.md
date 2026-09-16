---
type: concept
domaine: probabilités
aliases:
  - Loi normale
  - Distribution gaussienne
---

# Loi normale (distribution gaussienne)

La **distribution gaussienne**, aussi appelée **loi normale**, est une loi continue en forme de cloche. Elle sert souvent à modéliser une quantité qui fluctue autour d'une valeur centrale.

## Paramètres et notation

La convention usuelle est :

$$
X\sim\mathcal N(\mu,\sigma^2),
\qquad \sigma>0.
$$

Par exemple :

$$
X\sim\mathcal N(3,2^2)=\mathcal N(3,4).
$$

Cela signifie que :

- $\mu=3$ est la moyenne et le centre de la distribution ;
- $\sigma^2=4$ est la variance ;
- $\sigma=2$ est l'écart-type.

> [!important] Correction de vocabulaire
> L'écart-type ne correspond pas exactement à « l'écart moyen autour de la moyenne ». Il est défini par $\sigma=\sqrt{\mathbb E[(X-\mu)^2]}$ : il mesure une dispersion quadratique autour de la moyenne. L'idée intuitive de dispersion autour de $\mu$ reste correcte.

![[distributionGausienne.png|442]]

## Densité de probabilité

La courbe rouge est la densité :

$$
f(x)=\frac{1}{\sigma\sqrt{2\pi}}\exp\!\left(-\frac{(x-\mu)^2}{2\sigma^2}\right).
$$

Pour une variable continue, $f(x)$ n'est pas la probabilité d'obtenir exactement $x$. Une probabilité est une aire sous la courbe, par exemple :

$$
\mathbb P(a\le X\le b)=\int_a^b f(x)\,dx.
$$

## Tirer une valeur selon une loi normale

### En Python

```python
import numpy as np

x = np.random.normal(loc=2, scale=0.6)

print(x)
```

Dans cet exemple :

- $\mu=2$ (`loc`) ;
- $\sigma=0{,}6$ (`scale`).

La fonction attend l'écart-type, et non la variance. Autrement dit, `scale=0.6` correspond à une variance de $0{,}6^2$.

### En mathématiques — transformation de Box–Muller

Si $U_1$ et $U_2$ sont deux variables aléatoires indépendantes, uniformes sur $]0,1[$, alors :

$$
Z=\sqrt{-2\ln(U_1)}\cos(2\pi U_2)
$$

suit une loi normale standard $\mathcal N(0,1)$. On obtient ensuite une loi normale quelconque par :

$$
X=\mu+\sigma Z.
$$

Ici, $\ln$ est le logarithme naturel, de base $e$.

## À retenir

- Dans $\mathcal N(\mu,\sigma^2)$, le second paramètre est la **variance**.
- Une grande valeur de $\sigma$ rend la courbe plus étalée ; une petite valeur la rend plus concentrée autour de $\mu$.
- La loi normale standard est $\mathcal N(0,1)$.
