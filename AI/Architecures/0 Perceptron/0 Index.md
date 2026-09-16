# Perceptron

Un perceptron est un neurone artificiel simple. Dans le cas d’une classification binaire, il apprend une frontière de décision linéaire : dans un plan, il peut par exemple placer une ligne droite entre deux catégories.

![[perceptronShema.svg|494]]

Le perceptron est la brique de base des réseaux de neurones. Un [[AI/Architecures/1 MLP/0 Index|MLP]] assemble plusieurs perceptrons en couches.

## 1. Calcul linéaire : $z$

À partir des entrées $x_1,x_2,\ldots,x_n$, le neurone calcule un score :

$$
z(x_1,x_2,\ldots,x_n)
=w_1x_1+w_2x_2+\ldots+w_nx_n+b
$$

- $w_j$ : poids associé à l’entrée $x_j$ ;
- $b$ : biais du perceptron ;
- $z$ : score qui détermine de quel côté de la frontière de décision se trouve l’exemple.

## 2. Activation : $a(z)$

Pour convertir le score en une sortie entre 0 et 1, on utilise la sigmoïde :

$$
a(z)=\frac{1}{1+e^{-z}}
$$

Dans un problème binaire, cette sortie peut être interprétée comme la probabilité estimée d’appartenir à la classe positive. Voir [[AI/Architecures/0 Perceptron/A(Z)|Fonction d’activation sigmoïde]].

## 3. Mesurer l’erreur

La [[AI/Architecures/0 Perceptron/Log Loss|log-loss]] compare la sortie $a$ à la bonne réponse $y$. Elle indique à quel point le modèle rend les données observées vraisemblables.

## 4. Apprendre les paramètres

La [[AI/Architecures/0 Perceptron/Descante de gradients|descente de gradient]] modifie progressivement les poids $w_1,\ldots,w_n$ et le biais $b$ pour diminuer la log-loss.

## 5. Calculer un batch efficacement

Au lieu de répéter en boucle les calculs de $z$, $a(z)$ et $\mathcal{L}$ pour chaque donnée, on les effectue avec des matrices. Cette [[AI/Architecures/0 Perceptron/Vectorisation des fonctions|vectorisation]] économise beaucoup de temps de calcul.

## Suite

- [[AI/Architecures/0 Perceptron/z Sources|Sources — Perceptron]]
- [[AI/Architecures/1 MLP/0 Index|Passer au MLP]]
