Lorsqu'une policy est défini par **Discrete action space**, cela signifie que la policy détermine l'action en fonction de $s$ en choisissant parmis un ensemble fini d'actions (contrairement à une [[4 Continuous Action Space|policy Continuous]]).

Par exemple:
$$
Actions = [left, nothing, right]
$$

Une policy [[1 Deterministic Policy|determinisitc]] ferais donc :
$state = left$

Alors qu'une policy [[2 Stochastic Policy|stochastic]] ferais :
$state = \begin{bmatrix} left && 0.6 \\ nothing && 0.3 \\ right && 0.1 \end{bmatrix}$

