Explication des formules mathématique de simulation du Pendule

Pour calculer l’angle du pendule, on utilise un algorithme qui se base sur des équations
différentielle.

Les équations vont se résoudre chaque frame en prenant en entrée l'état du pendule pour calculer sont état prochain.

## Différentes étapes de calcul de l'angle du pendule
#### 1. Calcul de l'accélération angulaire du pendule

$$
Aa = - \frac{g}{l} \cdot \sin(\theta - \theta_0)
$$
- $Aa$ : Accélération angulaire
- $g$ et $l$ : gravité ($9.8$) et longeur du pendule
- $\theta$ : Angle du pendule la frame précédente
- $\theta_0$ : Angle d'équilibre du pendule

**Pour calculer $\theta_0$**
$$
\theta_0 = -1.52 - \tan(\frac{a}{g})
$$
- $-1.52$ : correspond à $-90°$ et sert à réajuster le pendule vers le bas
- $a$ : accélération du point d'accroche du pendule sur l'axe $x$
- $g$ : gravité ($9.8$)

#### 2. Calcul de la vitesse angulaire du pendule

$$
Va = Va_{-1} + Aa \cdot \Delta t
$$

- $Va$ = vitesse Angulaire
- $Va_{-1}$ = vitesse angulaire de la frame précédente
- $Aa$ = Acceleration angulaire (qui viens d'être caclulé)
- $\Delta t$ = temps en seconde entre les deux états (entre la frame précédente et celle ci)

On ajoute la force de frottement à cette vitesse angulaire.
$$
Va = Va \cdot \exp(-f \cdot \Delta t)
$$
- $f$ = force du frottement

#### 3. Calcul de l'angle du pendule
$$
A = A_{-1} + Va \cdot \Delta t
$$
- $A$ = nouvelle angle du pendule
- $A_{-1}$ = angle de la frame précédente
- $Va$ = vitesse Angulaire
- $\Delta t$ = temps en seconde de la frame


## Dessin du pendule sur un graphique

#### 1. Calcul de la position du point d'accroche
Caclule de l'origine du pendule.
Le $y$ de l'origine reste toujours identique, toujours $0$.

**Calcule de la vitesse de l'origine**
$$
Vo = Vo_{-1} + a \cdot \Delta t
$$
Frottement du sol
$$
Vo = Vo \cdot e^{-f \cdot \Delta t}
$$
- $Vo$ : Vitesse de l'origine sur l'axe $x$
- $Và_{-1}$ : Vitesse de l'origine à la frame précédente
- $a$ : accélération de l'origine du pendule
- $\Delta t$ : temps d'une frame
- $f$ : force du frottement

**Calcul de la nouvelle position avec la vitesse**
$$
xOrigin = xOrigin_{-1} + Vo \cdot \Delta t
$$


#### 2. Calcul de la position de l'extrémité du pendule
Là où se trouve le poids.
$$
x = l \cdot \cos(A) + xOrigin
$$
$$
y = l \cdot \sin(A)
$$
- $A$ : Angle du pendule
- $l$ : longueur du pendule