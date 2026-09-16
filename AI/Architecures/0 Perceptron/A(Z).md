# Fonction d’activation sigmoïde — $A(Z)$

![[a(z).svg|460]]

Après le calcul linéaire $z$, le perceptron produit une sortie $a(z)$. Pour une classification binaire, la fonction sigmoïde transforme ce score en une valeur comprise entre 0 et 1.

$$
a(z)=\frac{1}{1+e^{-z}}
$$

Lorsque le modèle est entraîné pour estimer une classe binaire, $a(z)$ peut être interprété comme une estimation de la probabilité de la classe positive :

$$
a(z)\approx P(y=1\mid x)
$$

## Entrée et sortie

- $z$ : sortie linéaire du perceptron, par exemple $z=w^T x+b$ ;
- $a(z)$ : activation transmise à la suite du réseau ou utilisée comme probabilité binaire.

## Dérivée utile pour l’apprentissage

La dérivée de la sigmoïde peut s’écrire à partir de sa propre sortie :

$$
\frac{da}{dz}=a(z)\bigl(1-a(z)\bigr)
$$

Cette relation est utilisée lors de la [[AI/Architecures/1 MLP/Back-Propagation|rétropropagation]].

## Vectorisation

En programmation, on applique la sigmoïde à tous les éléments d’un tableau en une opération :

$$
A=\frac{1}{1+e^{-Z}}
$$

Voir [[AI/Architecures/0 Perceptron/Vectorisation des fonctions|Vectorisation du perceptron]].
