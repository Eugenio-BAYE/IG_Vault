On prend un *algorithme récursif* **f()**
> [!important] Mémoisation : 
> 
> 1) *Initialiser* un tableau lors du *premier appel* de la **fDP()** à $-\infty$
> 2) Structurer **fDP()** avec :
> 	1) Résultat calculé? (Cas présent == $-\infty$)
> 	2) Cas de base
> 	3) Récursion
> 	4) Retour résultat

> [!example] Example of stamp coupling
> ``` Java
> public static int sac(int c, int i, int[] p, int[] v) {
>     if (i == p.length) {
>         return 0;
>         // Si toutes les tâches ont été traitées
>     } 
>     if (p[i] > c) {
>         return sac(c, i + 1, p, v); 
>         // Si l'objet est trop lourd, on le saute
>     } else {
>         return Math.max(v[i] + sac(c - p[i], i + 1, p, v), sac(c, i + 1, p, v)); 
>         // On choisit entre prendre ou ne pas prendre l'objet
>     }
> }
> ```
>  Puis en DP :
> ``` java
> public static int sacDP(int c, int i) {
>     // Si la solution pour la capacité c avec l'objet i a déjà été calculée
>     if (t[c][i] == -1) {  // -1 est utilisé pour indiquer que la case n'a pas été calculée
>         int res;
>         // Si tous les objets ont été traités, retourner 0 (valeur optimale atteinte)
>         if (i == n) {
>             res = 0;
>         } else {
>             // Si l'objet i est trop lourd pour être pris dans la capacité c
>             if (p[i] > c) {
>                 res = sacDP(c, i + 1);  // On ne peut pas prendre l'objet, on passe au suivant
>             } else {
>                 // Sinon, on choisit entre prendre l'objet ou ne pas le prendre
>                 res = Math.max(v[i] + sacDP(c - p[i], i + 1), sacDP(c, i + 1));
>             }
>         }
>         // On stocke le résultat dans t[c][i] pour éviter de recalculer
>         t[c][i] = res;
>     }
>     // Retourner la valeur mémoïsée
>     return t[c][i];
> }
> ```

