# Architectures de réseaux de neurones

Cette section regroupe les briques d’architecture et d’optimisation utilisées pour construire puis entraîner des réseaux de neurones. L’objectif est de comprendre les mécanismes avant d’utiliser des bibliothèques qui les automatisent.

## Parcours actuel

1. [[AI/Architecures/0 Perceptron/0 Index|Perceptron]] — un neurone, une frontière de décision et l’apprentissage binaire.
2. [[AI/Architecures/1 MLP/0 Index|MLP]] — plusieurs couches de perceptrons, propagation avant et rétropropagation.

## Convention de notation

Dans les notes sur le MLP, les exemples d’un mini-batch sont placés en colonnes :

$$
A^{[0]} = X \in \mathbb{R}^{n_0 \times m}
$$

- $m$ est le nombre d’exemples du batch ;
- $n_0$ est le nombre de caractéristiques d’entrée ;
- $A^{[l]}$ est la sortie (activation) de la couche $l$ ;
- $Z^{[l]}$ est la sortie linéaire, avant activation ;
- $W^{[l]}$ et $b^{[l]}$ sont les paramètres de la couche $l$.

Cette convention est rappelée dans les notes de [[AI/Architecures/1 MLP/Vectorisation|vectorisation du MLP]]. La note sur le perceptron indique aussi la convention équivalente où les exemples sont en lignes ; il ne faut pas mélanger les deux dans un même calcul.

## Sources

- [[AI/Architecures/0 Perceptron/z Sources|Sources — Perceptron]]
- [[AI/Architecures/1 MLP/z Sources|Sources — MLP]]
