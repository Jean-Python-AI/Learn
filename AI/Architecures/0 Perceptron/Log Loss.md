# Log-loss binaire / binary cross-entropy

![[log_loss.svg|515]]

La log-loss mesure l’écart entre la probabilité prédite par un modèle binaire et la bonne réponse. C’est la moyenne de la log-vraisemblance négative : la minimiser revient donc à rendre les observations plus vraisemblables selon le modèle.

## Pour un exemple

Pour une sortie attendue $y\in\{0,1\}$ et une prédiction $a\in(0,1)$ :

$$
\mathcal{L}(y,a)=-\left[y\log(a)+(1-y)\log(1-a)\right]
$$

- si $y=1$, une prédiction $a$ proche de $1$ donne une loss faible ;
- si $y=0$, une prédiction $a$ proche de $0$ donne une loss faible ;
- une prédiction très confiante mais fausse est fortement pénalisée.

## Pour un batch de $m$ exemples

$$
\mathcal{L}
=-\frac{1}{m}\cdot\sum_{i=1}^{m}
\left[
y^{(i)}\log\left(a^{(i)}\right)
+\left(1-y^{(i)}\right)\log\left(1-a^{(i)}\right)
\right]
$$

- $\mathcal{L}$ : log-loss moyenne ;
- $m$ : nombre d’exemples (6 dans le graphique d’exemple) ;
- $\log(\cdot)$ : logarithme naturel, aussi noté $\ln(\cdot)$ ;
- $a^{(i)}$ : sortie sigmoïde prédite pour l’exemple $i$ ;
- $y^{(i)}$ : réponse attendue pour l’exemple $i$.

> [!note] Correction de parenthèses
> Les deux termes doivent être inclus dans la somme. Sans les parenthèses, seul le premier terme serait moyenné sur les $m$ exemples.

## Version vectorisée

Si $A$ et $Y$ contiennent respectivement les prédictions et les réponses attendues du batch, la même formule s’écrit :

$$
\mathcal{L}
=-\frac{1}{m}
\sum\left[
Y\odot\log(A)
+(1-Y)\odot\log(1-A)
\right]
$$

$\odot$ représente une multiplication terme à terme et $\sum$ réduit tous les éléments concernés. En pratique, on évite aussi $\log(0)$ en bornant $A$ à un très petit intervalle ouvert autour de $[0,1]$.

Voir [[AI/Architecures/0 Perceptron/Vectorisation des fonctions|Vectorisation du perceptron]] et [[AI/Architecures/0 Perceptron/A(Z)|la fonction sigmoïde]].
