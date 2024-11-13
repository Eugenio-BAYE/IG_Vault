---
title: ALGO_Flots_FR
author: Eugénio BAYE
lecture author: Marin BOUGERET
lecture: Algorithmique Avancée, Polytech Montpellier
date: 2024-10-16
update: 2024-10-16
copyright: Polytech Montpellier, Marin BOUGERET
---
# Introduction aux Réseaux
> [!important] Définition
> Un **réseau** R est un triplet (G,s,T) où:
>- G=(V,A) est un graphe orienté
>- Chaque arc a$\in$A a une capacité c(a)>0
>- s(source) et t(puits) sont deux sommets particuliers de V
>
>> [!example] 
>> c(a) : limite de tonnes par jour sur autoroute dans deux villes.
>> ![[FLOTS - FIG1.png]]

> [!abstract] Application
> La notion de réseau modélise bien de nombreux "réseaux" du quotidien:
>- réseaux de communication
>- chaînes d’assemblage
>- réseaux électriques
>- liquides, réseaux transports
>
> .. mais (ce qui me touche plus personnellement ;) le problème du flot permet de résoudre en temps polynomial beaucoup d’autres problèmes

# Flots dans un réseau
> [!important] Définition
> Soit R = (G , s, t) un réseau. Un **flot** f dans le réseau R est une fonction $f : A \to \mathbb{R}^+$ vérifiant les propriétés suivantes:
>- *contrainte de capacité*: pour tout a ∈ A, f (a) ≤ c(a)
>- *conservation du flot*: pour tout u sauf s et t on a
>- $$f⁺(v)=f⁻(v),$$
>- $$avec f⁺(v)=\sum_{\substack{vw \in A}} f(vw) \\ f^-(v) = \sum_{\substack{wv \in A}} f(wv)$$
>
> ![[FLOTS - DEF. FLOTS]]
>> [!example]
>> Les capacites sont de 1
>> ![[FLOTS - FIG2.png]]

> [!important] Définition
> Étant donné un flot $f$, on définit :
> 
> - $f^+(v)$ et $f^-(v)$ (cf. slide précédent)
> - $\Delta(v) = f^+(v) - f^-(v)$ pour tout $v \in V$
> 
> Notation de graphes : pour $X \subseteq V$, on note
> 
> - $\delta^+(X) = \{ uv \in A \mid u \in X \text{ et } v \notin X \}$
> - $\delta^-(X) = \{ uv \in A \mid u \notin X \text{ et } v \in X \}$
> 
> Enfin, toutes les notations sont étendues aux sous-ensembles :  
> par exemple, $f^+(X) = \sum_{v \in X} f^+(v)$, de même pour $\Delta(X)$, et $c(A')$ (avec $A' \subseteq A$).
> 
>> [!example]
>> Les capacités sont de 1
>> ![[FLOTS - FIG3.png]]
>> - $f^+(X) = 1 + \frac{1}{4} + \frac{3}{4}$ 
>> - $\delta^+(X) = \{ bt, dt \}$ 
>> - $f(\delta^+(X)) = \frac{1}{4} + \frac{3}{4}$

> [!important] Observations importantes
> 
> - $\Delta(v) = 0$ pour tout $v$ différent de $s$ et $t$.
> - La valeur du flot est définie par $|f| = \Delta(s)$.
> 
> Exemple :
> 
> - Les deux flots de l’exemple précédent ont des valeurs respectives de $\frac{5}{4}$ et $0$.
> 
> **Problème central** :
> Le problème du flot maximum consiste, étant donné un réseau, à trouver un flot de valeur maximale.
> 
> - On note $MaxF(R)$ la valeur du flot maximum d’un réseau $R$.


# Coupe
> [!important] Définition : Coupe
> 
> Une **coupe** $S$ dans un réseau $R = (G, s, t)$ est un sous-ensemble de sommets tel que $s \in S$ et $t \notin S$.
> 
> - On rappelle que : 
>   - $\delta^+(S)$ est l'ensemble des arcs sortants de $S$.
>   - $\delta^-(S)$ est l'ensemble des arcs entrants dans $S$.
> 
> La **valeur** d'une coupe est donnée par :
> 
> $$ c(S) = c(\delta^+(S)) $$
> 
> *Attention* : on ne prend pas en compte les arcs entrants dans $S$ pour le calcul de la valeur de la coupe.
> 
> ![[COUPE - DEF. FLOTS]]
> 
>> [!example] 
>> ![[FLOTS - FIG4.png]]
>> c({s,a,c,d}) = 12 + 7 + 4
>> c({s,a,d}) = 12 + 10 + 13 + 7 + 4
>>> En premier on a la coupe (groupe s,a,c,d) qui contient donc le puits. Pour accéder à l'autre groupe (b,t) il faut donc passer par les arcs (a,b), (d,b) et (d,t) de valeurs respectives 12, 7 et 4. La valeur de la première coupe est donc de 23

> [!important] Problème Central
> 
> Le problème de la **coupe minimum** consiste, étant donné un réseau, à trouver une coupe de valeur minimale.
> 
> - On notera $MinC(R)$ la valeur de la coupe minimum d’un réseau $R$.

> [!important] Relations entre Coupes et Flots
> 
> **Théorème** :
> Pour tout réseau $R$, $MaxF(R) = MinC(R)$, et les deux problèmes **Max-FLOT** et **Min-CUT** sont polynomiaux.

# Conclusion

Les **extensions possibles** de ces concepts incluent plusieurs variantes qui restent polynomiales :
- Plusieurs sources et puits.
- Bornes inférieures sur les arcs : $l(a) \leq f(a) \leq c(a)$.
- Bornes inférieures et supérieures sur les sommets.
- Flot maximum de coût minimum (avec un prix par unité de flot pour chaque arc).

De plus, le fait que **Max-Flot = Min-Cut** entraîne de nombreux autres théorèmes et algorithmes polynomiaux, notamment pour :
- Le **théorème de Menger** (problème de trouver un maximum de chemins disjoints arc ou sommet).
- Le **théorème de Hall** (conditions nécessaires et suffisantes pour l’existence d’un couplage parfait dans un graphe biparti).
- Le **théorème de König-Egervary** (la taille d’un ensemble de couverture de sommets est égale à celle d’un couplage maximal dans un graphe biparti).