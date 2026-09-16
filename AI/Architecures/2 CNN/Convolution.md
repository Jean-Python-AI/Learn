Une **convolution**, est un mécanisme dans le quelle on vas faire coulisser une petite fenêtre sur les pixels de l'image et à chaque fois on vas multiplier ça par un kernel (ou filtre cela se dit des deux manières) pour obtenir la valeur d'un pixel.
Puis, ont vas décaler la fenêtre et recommencer les calculs.

**Exemple :**
![[convolution.png|700]]
$$
\begin{bmatrix}
	5 & 2 & 1 \\
	4 & 3 & 2 \\
	0 & 2 & 1
\end{bmatrix}
\otimes
\begin{bmatrix}
	1 & 0 & 1 \\
	0 & 1 & 0 \\
	1 & 0 & 1
\end{bmatrix}
= 5\cdot1 + 2\cdot0 + 1\cdot1 + 4\cdot0 + ... + 2\cdot0 + 1\cdot1 = 10
$$
Puis, on décale la fenêtre:
![[convolutionSteps.png|292]]

Voici la **formule mathématique pour calculer la valeur de chaque pixel**:
$$
O_{x,y} = \sum^{h-1}_{u=0} \sum^{w-1}_{v=0} I_{x+v,y+u} \cdot F_{v,u}
$$
où
- $h$ et $w$ corresponde à la hauteur et la largeur du filtre
- $O_{x,y}$ correspond au pixel de l'image au niveau $x,y$
- $I$ correspond à l'image d'input qui ici est en 2D (noir et blanc)
- $F$ correspond au filtre (2D aussi)



**On peut aussi effectuer des convolutions sur des images en couleurs (3D)**
Simplement, le kernel doit aussi être en 3D.
![[convolution3D.png|586]]



>[!attention]
>La convolution ne s'applique pas uniquement aux images, elle s'applique dans pleins d'autres domaines où le voisinage et la position relative des éléments ont un sens.
>Comme:
>1D => Dans les audios, données de capteurs, ...
>2D => Les images mais aussi les jeux de plateaux, les cartes, ...
>3D => Les volumes médicaux comme les scanners, ...
>Bref, laisse libre court à ton imagination pour les utiliser



Il y a deux paramètres important lorsque l'ont fait de la convolution.
### Le Padding
Sert à avoir une image en sortie qui correspond à la taille de l'image en entrée.
Pour cela, on ajoute un padding sur les contour de l'image.
![[padding.png|287]]

### Strides
Le stride correspond au pas au quelle on vas déplacer la fenêtre sur l'image.
Pour l'exemple ci dessous, le stride correspond à 2.
![[strides.png|154]]

