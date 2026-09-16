Voici un exemple de Forward Propagation.
![[forwardProp.png|700]]
En premier, il y a l'image RGB qui arrive en Input.
Puis, il y a plusieurs différentes [[Convolution|convolution]] qui lui sont appliqué, ce qui donne plusieurs résultat de convolutions (exemple 16 (sur l'image 4)).
Puis, un [[Pooling]] va être appliqué à ces nouvelle image résultant de la première série de convolution.
Ce qui donnera une série d'image plus petites qui vont à leur tour subir une séries de convolutions, exemple 8 ce qui donnera en sortie de cette convolution ($16\cdot8$) 128 images qui vont à leur tour subir un [[Pooling]], etc.

Pour à la fin, prendre toutes ces petites images transformer et les aplatir en un seul et long vecteur qui serra l'input d'un [[AI/Architecures/1 MLP/0 Index|MLP]] qui lui donnera les outups du modèle.
