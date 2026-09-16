---
type: note-de-projet
projet: "[[0 Index]]"
domaines:
  - apprentissage-par-renforcement
  - réseaux-de-neurones
---

# Agent d'IA — pendule inversé

Cette note décrit l'agent du projet [[0 Index]] : il observe l'état issu de la [[1 Physics simulation|simulation physique]], choisit une accélération horizontale et apprend, par renforcement, à maintenir le pendule près de son objectif.

## 1. État observé par l'agent

À l'instant $t$, le réseau reçoit l'état $s_t$ composé de quatre entrées normalisées dans $[-1,1]$ :

- $e_\theta$ : erreur d'angle du pendule par rapport à l'objectif ;
- $\omega$ : vitesse angulaire du pendule ; les valeurs hors des limites prévues sont ramenées à $-1$ ou $1$ ;
- $v$ : vitesse actuelle de l'origine sur l'axe $x$ ;
- $x$ : position du chariot sur l'axe $x$.

> [!important] État causal et markovien
> La liste ci-dessus conserve les variables initialement prévues, mais $a$ est aussi l'action que l'agent choisit et $a_\theta$ dépend de l'état et de cette action. Sans convention temporelle explicite, cela crée une circularité. Un état plus directement markovien est par exemple $s_t=(e_{\theta,t},\omega_t,x_t,v_t)$, où $e_\theta$ est l'erreur d'angle, $\omega$ la vitesse angulaire et $v$ la vitesse du chariot. L'agent choisit ensuite $a_t$. Si le projet conserve $a_\theta$ ou l'action précédente, les noter $a_{\theta,t-1}$ et $a_{t-1}$.

### Normaliser entre $-1$ et $1$

Pour une grandeur bornée entre $x_{\min}$ et $x_{\max}$, la normalisation est :

$$
x_{\text{normalisé}}
=2\frac{x-x_{\min}}{x_{\max}-x_{\min}}-1.
$$

La valeur est ensuite limitée à $[-1,1]$ si elle dépasse les bornes prévues.

> [!warning] Convention d'angle
> La [[1 Physics simulation|simulation physique]] utilise $-90^\circ$ comme position verticale vers le bas, tandis que cette note indique un objectif de $90^\circ$. Il faut documenter dans le code la convention effectivement utilisée et normaliser l'**erreur d'angle** par rapport à l'objectif, pas un angle brut qui pourrait changer de signe selon la convention.

## 2. Réseau de neurones et politique

Le réseau est un [[AI/Architecures/1 MLP/0 Index|MLP]] avec une [[AI/Learning/3 Reinforcement Learning/Policy/2 Stochastic Policy|politique stochastique]] dans un [[AI/Learning/3 Reinforcement Learning/Policy/4 Continuous Action Space|espace d'action continu]].

À partir de $s_t$, sa dernière couche produit deux sorties :

$$
z^{[m]}=
\begin{bmatrix}
z_\mu \\
z_o
\end{bmatrix},
\qquad
\mu=z_\mu,
\qquad
\sigma=e^{z_o}.
$$

$\mu$ est la moyenne de la distribution d'action et $z_o$ est son *log-écart-type*. L'exponentielle garantit que $\sigma>0$.

### Échantillonner puis borner l'action

La politique définit une loi normale sur une variable latente $u_t$ :

$$
u_t\sim\mathcal N(\mu_t,\sigma_t^2).
$$

On échantillonne $u_t$, puis on le transforme en accélération envoyée au chariot :

$$
a_t=5\tanh(u_t).
$$

L'action est donc strictement dans $(-5,5)$ et tend vers les bornes $-5$ et $5$. Cette transformation conserve l'idée initiale : l'échantillon gaussien n'est pas borné, alors que l'accélération du chariot doit l'être.

## 3. Récompense et objectif

Le *reward* mesure la qualité de l'état obtenu. Il pénalise l'écart angulaire, l'accélération angulaire, l'accélération du chariot et sa position :

$$
\tilde a_t=\frac{a_t}{5}\in(-1,1).
$$

$$
r_t=-\left(
\alpha\lvert\theta_t\rvert
+\beta\lvert a_{\theta,t}\rvert
+\gamma_a\lvert\tilde a_t\rvert
+\delta\lvert x_t\rvert
\right).
$$

Les termes ont la priorité suivante :

- $\alpha$ : importance de l'angle ($+++)$ ;
- $\beta$ : importance de l'accélération angulaire ($++)$ ;
- $\gamma_a$ : importance de l'accélération normalisée du chariot ($++)$ ;
- $\delta$ : importance de la position du chariot ($+)$.

Le signe négatif transforme ces écarts en pénalités. L'agent cherche donc à maximiser la somme de ses récompenses.

> [!important] Correction de notation
> La version précédente utilisait $\gamma$ à la fois pour le poids de $\lvert a\rvert$ dans la récompense et pour le facteur d'actualisation des *returns*. Ce sont deux rôles différents. Cette note utilise $\gamma_a$ pour le poids de l'action et réserve $\gamma$ au facteur d'actualisation.

## 4. Enregistrer un épisode

Pour chaque étape $t$, il faut conserver au minimum :

$$
\begin{aligned}
&\text{states}=[s_0,s_1,s_2,\ldots], \\
&\text{raw actions}=[u_0,u_1,u_2,\ldots], \\
&\text{actions}=[a_0,a_1,a_2,\ldots], \\
&\text{log probabilities}=[\log\pi_\phi(u_0\mid s_0),\log\pi_\phi(u_1\mid s_1),\ldots], \\
&\text{rewards}=[r_0,r_1,r_2,\ldots].
\end{aligned}
$$

Conserver aussi $\mu_t$ et $\sigma_t$ (ou les recalculer depuis $s_t$) est nécessaire pour calculer les gradients manuellement.

### Log-probabilité de l'action choisie

La densité normale s'applique à la variable latente $u_t$, avant le $\tanh$ :

$$
\log\pi_\phi(u_t\mid s_t)
=-\frac{1}{2}\left(\frac{u_t-\mu_t}{\sigma_t}\right)^2
-\log(\sigma_t)
-\frac{1}{2}\log(2\pi).
$$

Cette valeur est enregistrée pour chaque action prise.

> [!important] Correction liée au $\tanh$
> Écrire directement $a_t\sim\mathcal N(\mu_t,\sigma_t^2)$ serait incohérent, car l'action réellement envoyée est $a_t=5\tanh(u_t)$. Pour REINFORCE, enregistrer la log-probabilité du tirage $u_t$ est cohérent. Si une méthode a besoin de la densité exacte dans l'espace de l'action bornée, avec $u=\operatorname{atanh}(a/5)$, il faut utiliser :
> $$
> \log\pi_\phi(a\mid s)=\log\mathcal N(u;\mu,\sigma^2)-\log(5)-\log\!\left(1-\tanh^2(u)\right).
> $$

## 5. Calculer les returns

Le *return* $G_t$ est la somme des récompenses futures pondérées par le facteur d'actualisation $\gamma$ :

$$
G_t=r_t+\gamma r_{t+1}+\gamma^2r_{t+2}+\gamma^3r_{t+3}+\cdots,
$$

ou, de façon récursive :

$$
G_t=r_t+\gamma G_{t+1},
\qquad 0\le\gamma\le1.
$$

Plus $\gamma$ est grand, plus l'agent prend en compte les conséquences à long terme de ses actions.

## 6. Loss REINFORCE

Pour chaque étape $t$, la loss est :

$$
L_t=-G_t\log\pi_\phi(u_t\mid s_t).
$$

La loss totale de l'épisode est :

$$
L=\sum_tL_t.
$$

Le signe négatif transforme la maximisation de la performance en minimisation d'une loss. Les valeurs $G_t$ peuvent aussi être normalisées ou remplacées par un avantage pour réduire la variance, mais la formule ci-dessus est la version de base utilisée ici.

## 7. Dérivées à la sortie du MLP

On cherche le gradient du loss par rapport à chaque poids et biais du MLP. Un poids $W^{[n]}$ influence le loss par deux chemins :

$$
W^{[n]}\longrightarrow\mu\longrightarrow L,
\qquad
W^{[n]}\longrightarrow\sigma\longrightarrow L.
$$

### Dérivée par rapport à $\mu$

En traitant le tirage $u$ comme l'action choisie au moment du calcul du gradient :

$$
\frac{\partial\log\pi}{\partial\mu}
=\frac{u-\mu}{\sigma^2}.
$$

Donc :

$$
\frac{\partial L}{\partial\mu}
=-G\frac{u-\mu}{\sigma^2}.
$$

> [!important] Correction de dérivée
> Le terme $(u-\mu)/\sigma$ ne doit pas être mis au carré dans $\partial L/\partial\mu$. Le carré appartient à la log-probabilité elle-même ; sa dérivée par rapport à $\mu$ est linéaire en $(u-\mu)$.

### Dérivée par rapport à $\sigma$

$$
\frac{\partial\log\pi}{\partial\sigma}
=\frac{(u-\mu)^2}{\sigma^3}-\frac{1}{\sigma}.
$$

Donc :

$$
\frac{\partial L}{\partial\sigma}
=-G\left(
\frac{(u-\mu)^2}{\sigma^3}-\frac{1}{\sigma}
\right).
$$

### Propager vers les deux logits de sortie

Comme $\mu=z_\mu$ :

$$
\frac{\partial L}{\partial z_\mu}
=\frac{\partial L}{\partial\mu}.
$$

Comme $\sigma=e^{z_o}$ :

$$
\frac{\partial\sigma}{\partial z_o}=\sigma,
$$

et donc :

$$
\frac{\partial L}{\partial z_o}
=\frac{\partial L}{\partial\sigma}\sigma
=-G\left(
\frac{(u-\mu)^2}{\sigma^2}-1
\right).
$$

Le gradient de la dernière couche est alors :

$$
\delta^{[m]}
=\begin{bmatrix}
\dfrac{\partial L}{\partial z_\mu} \\
\dfrac{\partial L}{\partial z_o}
\end{bmatrix}.
$$

Ici, $m$ est le numéro de la dernière couche.

> [!important] Correction de chaîne de dérivation
> $z_o$ n'est pas égal à $\sigma$ : il produit $\sigma$ par $\sigma=e^{z_o}$. Le gradient de la seconde sortie doit donc être multiplié par $\sigma$. Cette étape était absente dans la formule précédente.

## 8. Backpropagation dans les couches cachées

Dans les couches cachées du MLP, l'activation utilisée est la sigmoïde :

$$
a^{[n]}=\frac{1}{1+e^{-z^{[n]}}}.
$$

Sa dérivée peut s'écrire de deux manières équivalentes :

$$
\frac{\partial a^{[n]}}{\partial z^{[n]}}
=\frac{e^{-z^{[n]}}}{(1+e^{-z^{[n]}})^2}
=a^{[n]}\left(1-a^{[n]}\right).
$$

On définit :

$$
\delta^{[n]}=\frac{\partial L}{\partial z^{[n]}}.
$$

Pour une couche cachée $n$, le gradient remontant de la couche suivante est $\left(W^{[n+1]}\right)^T\delta^{[n+1]}$. Il traverse ensuite la dérivée de la sigmoïde :

$$
\delta^{[n]}
=\left(\left(W^{[n+1]}\right)^T\delta^{[n+1]}\right)
\odot a^{[n]}\odot\left(1-a^{[n]}\right),
$$

où $\odot$ représente une multiplication élément par élément. Cette formule est répétée de la dernière couche vers la première.

> [!important] Correction de la dérivée sigmoïde
> La formule doit contenir les deux facteurs $a^{[n]}$ et $1-a^{[n]}$. Il ne suffit pas de multiplier par $1-a^{[n]}$, et l'activation concernée est celle de la couche courante $n$, non celle de la couche précédente.

## 9. Gradients et mise à jour des paramètres

Pour une couche :

$$
z^{[n]}=W^{[n]}a^{[n-1]}+b^{[n]},
$$

les gradients sont :

$$
\frac{\partial L}{\partial W^{[n]}}
=\delta^{[n]}\left(a^{[n-1]}\right)^T,
\qquad
\frac{\partial L}{\partial b^{[n]}}
=\delta^{[n]}.
$$

Ces expressions sont celles d'une étape. Comme la loss d'un épisode est une somme sur $t$, il faut accumuler les contributions de toutes les étapes avant une mise à jour :

$$
\frac{\partial L}{\partial W^{[n]}}
=\sum_t\delta_t^{[n]}\left(a_t^{[n-1]}\right)^T,
\qquad
\frac{\partial L}{\partial b^{[n]}}
=\sum_t\delta_t^{[n]}.
$$

Une fois les gradients calculés, les paramètres sont mis à jour avec un *learning rate* $\eta$ :

$$
W^{[n]}\leftarrow W^{[n]}-\eta\frac{\partial L}{\partial W^{[n]}},
$$

$$
b^{[n]}\leftarrow b^{[n]}-\eta\frac{\partial L}{\partial b^{[n]}}.
$$

## 10. Boucle complète

$$
\text{État}
\longrightarrow\text{Policy}
\longrightarrow\text{Action}
\longrightarrow\text{Reward}
\longrightarrow\text{Return}
\longrightarrow\text{Loss}
\longrightarrow\text{Backpropagation}
\longrightarrow\text{Mise à jour}.
$$

Un nouvel épisode est ensuite lancé avec les paramètres mis à jour.
