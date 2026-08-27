
### Inputs

- $\theta$ : angle du pendule par apport à l'objectif (qui est $90°$) normaliser entre $-1$ et $1$
- $a_\theta$ : accélération angulaire du pendule normaliser entre $-1$ et $1$ (ou $-1$ et $1$ correspondent aux $max$ et $min$ pris en compte, au dessus, ont reste à $-1$ et $1$)
- $a$ : accélération actuelle sur l'axe $x$ de l'origine normaliser entre $-1$ et $1$
- $x$ : position du pendule sur l'axe $x$ normaliser entre $-1$ et $1$

**Normaliser entre $-1$ et $1$**
$$
x_{normaliser} = 2 \cdot \frac{x - x_{min}}{x_{max} - x_{min}} -1
$$


### RL (entrainement)
