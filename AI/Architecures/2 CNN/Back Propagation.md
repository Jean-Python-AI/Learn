Pour comprendre d'où vienne les formules de la Back Propagation, il faut s'assurer de comprendre la [[AI/Architecures/2 CNN/Forward Propagation|Forward Propagation]] et le fonctionement d'un [[AI/Architecures/1 MLP/0 Index|MLP]].

$$
\frac{\partial\mathcal{L}}{\partial F_{w,h}^{[l]}}
= \frac{\partial\mathcal{L}}{\partial X_{x,y}^{[l]}} \cdot \frac{\partial X_{x,y}^{[l]}}{\partial F_{w,h}^{[l]}}
$$
où $w$ correspond à la position sur l'axe $x$ de la valeur de la case du filtre et $h$ correspond à la position de la case du filtre sur l'axe $y$.


$$
\frac{\partial\mathcal{L}}{\partial X_{x,y}^{[l]}}
= dZ^{[l]} \cdot \frac{\partial Z^{[l]}}{\partial X_{x,y}^{[l]}}
= dZ^{[l]} \cdot W_{x,y}^{[l]}
$$
où $W_{x,y}^{[l]}$ correspond juste aux $W$ qui sont lier à ce $X$ précis, à noté que les $x,y$ doivent être converti en juste un $p$ (par exemple) car toute l'image sera aplati en 1 vecteur avant de rentrer dans le MLP.


$$
\frac{\partial X_{x,y}^{[l]}}{\partial F_{w,h}^{[l]}}
= I_{x+w, y+h}
$$
où $I$ correspond à l'image d'input.

