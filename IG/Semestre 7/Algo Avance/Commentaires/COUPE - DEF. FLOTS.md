Les **coupes** dans un réseau permettent de séparer un réseau en deux parties, afin de mesurer le flux qui traverse cette séparation.

### Définition
Une **coupe** $S$ dans un réseau $R = (G, s, t)$ est un sous-ensemble de sommets où :
- $s \in S$ (la source est dans $S$)
- $t \notin S$ (le puits n'est pas dans $S$)

### Arcs Sortants et Entrants
- **Arcs sortants** $\delta^+(S)$ : arcs quittant le groupe $S$ vers l’extérieur ($v \notin S$).
- **Arcs entrants** $\delta^-(S)$ : arcs venant de l'extérieur vers le groupe $S$ (non pris en compte pour la coupe).

### Valeur de la Coupe
La **valeur** de la coupe est la somme des capacités des arcs sortants $\delta^+(S)$ :
$$ c(S) = \sum_{a \in \delta^+(S)} c(a) $$

### Exemple
Imaginons un réseau de canalisations d’eau :
- $s$ est une station de pompage, et $t$ un réservoir.
- La coupe coupe les canalisations entre ces deux points.
- Si les capacités des canalisations coupées sont 50 et 30 L/s, la valeur de la coupe est 80 L/s.

### Utilité
Les coupes sont utilisées pour analyser les goulots d’étranglement d’un réseau. Le **théorème du flot maximal et de la coupe minimale** affirme que la valeur du **flot maximum** est égale à la valeur de la **coupe minimum**. 
