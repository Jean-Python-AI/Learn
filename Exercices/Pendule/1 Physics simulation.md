---
type: note-de-projet
projet: "[[0 Index]]"
---

# Simulation physique du pendule

Cette note explique les formules utilisées pour simuler le pendule du projet [[0 Index]]. À chaque image (*frame*), l'algorithme part de l'état actuel, calcule les accélérations, puis produit l'état suivant. C'est une résolution numérique d'équations différentielles.

## Conventions et état simulé

On note :

- $A$ ou $\theta$ : angle du pendule ; dans cette note, $A=\theta$ ;
- $Va$ ou $\omega$ : vitesse angulaire ;
- $Aa$ ou $\alpha$ : accélération angulaire ;
- $xOrigin$ : position horizontale du point d'accroche ;
- $Vo$ : vitesse horizontale de ce point ;
- $a$ : accélération horizontale du point d'accroche ;
- $l$ : longueur du pendule ;
- $g \simeq 9{,}8\ \mathrm{m\,s^{-2}}$ : accélération de la pesanteur ;
- $\Delta t$ : durée, en secondes, entre deux états.

Les indices $t$ et $t+1$ désignent respectivement l'état courant et l'état calculé pour l'image suivante. Les notations originales $A_{-1}$, $Va_{-1}$ et $Vo_{-1}$ correspondent donc aux valeurs de l'image précédente.

## 1. Mettre à jour l'angle du pendule

### 1.1 Accélération angulaire

Le pendule est dessiné avec les coordonnées

$$
x=xOrigin+l\cos(\theta),
\qquad
y=l\sin(\theta).
$$

Avec cette convention, le pendule suspendu vers le bas a $\theta=-\frac{\pi}{2}$. Si le point d'accroche n'a pas d'accélération horizontale ($a=0$), l'équation est :

$$
Aa=\ddot\theta=-\frac{g}{l}\sin(\theta-\theta_0),
\qquad
\theta_0=-\frac{\pi}{2}.
$$

Ici, $Aa$ est l'accélération angulaire, $g$ la gravité, $l$ la longueur du pendule, $\theta$ l'angle de l'image précédente et $\theta_0$ l'angle d'équilibre.

Lorsque le point d'accroche accélère horizontalement, une formulation cohérente avec les mêmes coordonnées est :

$$
Aa=\frac{a\sin(\theta)-g\cos(\theta)}{l}
=-\frac{\sqrt{g^2+a^2}}{l}\sin(\theta-\theta_0),
$$

avec

$$
\theta_0=-\frac{\pi}{2}-\arctan\!\left(\frac{a}{g}\right).
$$

> [!important] Correction de la formule d'équilibre
> La formule précédente utilisait $-1{,}52-\tan(a/g)$. Il faut employer $-\frac{\pi}{2}$ (l'angle exact de $-90^\circ$) et $\arctan(a/g)$, non $\tan(a/g)$. La différence est importante dès que $a$ n'est pas négligeable. La forme $-\frac{g}{l}\sin(\theta-\theta_0)$ reste une bonne expression lorsque $a=0$ ; avec une accélération horizontale, le facteur exact est $\sqrt{g^2+a^2}/l$.

### 1.2 Vitesse angulaire et amortissement

On intègre d'abord l'accélération angulaire :

$$
Va_{t+1}=Va_t+Aa_t\,\Delta t.
$$

Puis on applique l'amortissement :

$$
Va_{t+1}\leftarrow Va_{t+1}\exp(-f_\theta\Delta t).
$$

Le symbole $f_\theta$ désigne un **coefficient d'amortissement** (en $\mathrm{s^{-1}}$), plutôt qu'une force de frottement. L'exponentielle réduit progressivement la vitesse angulaire sans dépendre fortement de la taille de $\Delta t$.

### 1.3 Nouvel angle

Enfin, l'angle est mis à jour avec la vitesse nouvellement calculée :

$$
A_{t+1}=A_t+Va_{t+1}\,\Delta t.
$$

Ces trois étapes constituent une intégration d'Euler semi-implicite : l'accélération met à jour la vitesse, puis cette nouvelle vitesse met à jour la position angulaire.

## 2. Dessiner le pendule

### 2.1 Position du point d'accroche

Le point d'accroche est l'origine du pendule. Sa coordonnée verticale reste fixe à $y=0$ ; seule sa position horizontale est intégrée.

La vitesse horizontale est calculée à partir de l'accélération :

$$
Vo_{t+1}=Vo_t+a_t\,\Delta t.
$$

On applique ensuite le frottement du sol :

$$
Vo_{t+1}\leftarrow Vo_{t+1}\exp(-f_x\Delta t).
$$

Ici, $Vo$ est la vitesse de l'origine sur l'axe $x$, $a$ son accélération, $\Delta t$ le temps d'une image et $f_x$ un coefficient d'amortissement. La note initiale utilisait le même symbole $f$ pour les deux amortissements ; les distinguer ($f_\theta$ et $f_x$) évite de confondre leurs rôles si leurs valeurs diffèrent.

La nouvelle position est alors :

$$
xOrigin_{t+1}=xOrigin_t+Vo_{t+1}\,\Delta t.
$$

### 2.2 Position de l'extrémité du pendule

L'extrémité est le point où se trouve le poids. À partir de l'angle et de la longueur :

$$
x=l\cos(A)+xOrigin,
$$

$$
y=l\sin(A).
$$

Ainsi, avec $A=-\frac{\pi}{2}$, le poids est à $(xOrigin,-l)$. Ces équations supposent donc que l'axe $y$ positif pointe vers le haut ; si la bibliothèque graphique utilise $y$ vers le bas, il faut convertir la coordonnée au moment du dessin.

## Résumé d'une image

1. Lire $\theta_t$, $Va_t$, $xOrigin_t$, $Vo_t$ et l'accélération horizontale $a_t$.
2. Calculer $Aa_t$, puis $Va_{t+1}$ et $\theta_{t+1}$.
3. Calculer $Vo_{t+1}$ et $xOrigin_{t+1}$.
4. Convertir $(xOrigin_{t+1},\theta_{t+1})$ en position $(x,y)$ de l'extrémité.
