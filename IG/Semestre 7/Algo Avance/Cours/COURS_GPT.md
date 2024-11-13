# Algorithmique Avancée

> [!abstract] **Auteur**: Marin Bougeret  
> **Date**: 10 septembre 2024  
> Ce document traite de l'algorithmique avancée avec un focus particulier sur la **programmation dynamique**.

## Plan du module S1

- **Volume**: 
    - 5 cours magistraux (CM): 
        - 2 sur la programmation dynamique (DP)
        - 2 sur la réduction/flots
        - 1 de révisions.
    - 8 séances de travaux dirigés (TD) ou travaux pratiques (TP) par groupe.
  
- **Notation**:
    - Contrôle continu (CC) pour chacune des deux parties du cours (questions de cours et exercices simples).
    - Feuille A4 recto-verso autorisée pour les contrôles et l'examen final.
    - Note finale: 30% CC, 70% examen final.

- **Organisation**:
    - Ressources pédagogiques accessibles sur l’ENT.

## Marche à suivre face à un problème combinatoire

1. **Phase 1**: Formulation mathématique.
    - Exemple 1: **Problème Chim**
        - *Objectif*: Transporter le maximum de produits chimiques non dangereux ensemble.
        - **Entrée**: Une matrice booléenne D où D[i][j] est vrai si les produits i et j sont dangereux ensemble.
        - **Sortie**: Maximiser un ensemble de produits sûrs à transporter.
        - Ce problème est un **maximum Independent Set**.

    - Exemple 2: **Problème ParcourS**
        - *Objectif*: Affecter le maximum d’étudiants à des universités selon leurs préférences.
        - **Entrée**: Deux tableaux d’ensembles, e pour les préférences des étudiants, u pour les admissions des universités.
        - **Sortie**: Maximiser le nombre d'appariements entre étudiants et universités.
        - Ce problème est un **Maximum Matching** dans les graphes bipartis.

2. **Phase 2**: 
    - Prouver que le problème est **polynomial** ou **NP-difficile**.
  
3. **Phase 3**: 
    - Si NP-difficile, chercher des **heuristiques** ou des **approximations**.

## Problème d’optimisation vs Problème de décision

> [!important] **Problème de décision**  
> *Définition*: Une instance I et une question "I vérifie-t-elle la propriété p ?".  
> Exemple: **3-SAT**, où on décide si une formule 3-SAT est satisfiable.

> [!important] **Problème d’optimisation**  
> *Définition*: Trouver une solution S faisable qui maximise ou minimise une fonction objectif.  
> Exemple: **Vertex Cover (VC)**, où on cherche à minimiser le nombre de sommets couvrant tous les arcs d’un graphe.

## Histoire et contexte de la Programmation Dynamique

> [!abstract] **Programmation dynamique**  
> Technique permettant de réduire la complexité d’un algorithme récursif (typiquement d’exponentiel à polynomial). Utilisée dans de nombreux contextes (algorithmes polynomiaux, FPT, heuristiques).

- **Origine**: Introduite par Richard Bellman dans les années 50.

## Exemple 1: Fibonacci avec Programmation Dynamique

1. **Définition**:
    - F(0) = 1, F(1) = 1, F(n) = F(n-1) + F(n-2).
  
2. **Problème**: Complexité exponentielle de l'algorithme récursif naïf dû aux calculs redondants.

3. **Solution**: Utilisation de la **mémoïsation** pour éviter de recalculer des valeurs déjà connues, en stockant les résultats intermédiaires dans un tableau.

> [!example] **Code: Mémoïsation pour Fibonacci**
```c
int FibClient(n){
    t = new int[n];
    pour tout i, t[i] = -infini;
    return FibDP(n);
}

int FibDP(n){
    if (t[n] == -infini){
        int res;
        if (n <= 1) res = 1;
        else res = FibDP(n-1) + FibDP(n-2);
        t[n] = res;
    }
    return t[n];
}
```


Complexité: O(n) en temps et en mémoire.

Exemple 2: Problème du Sac à Dos (Knapsack Problem)

    Définition:
        Entrée: Un entier C et deux tableaux p (poids) et v (valeurs) de taille n.
        Objectif: Maximiser la valeur des objets sélectionnés sans dépasser la capacité du sac à dos.

    Complexité: Ce problème est NP-difficile, mais on peut le résoudre en O(nC) avec la programmation dynamique (pseudo-polynomial).

    [!example] Code: Résolution DP du Knapsack

c

int sacDP(int c, int i){
    if (t[c, i] == -infini){
        int res;
        if (i == n) res = 0;
        else {
            if (p[i] > c) res = sacDP(c, i + 1);
            else res = max(v[i] + sacDP(c - p[i], i + 1), sacDP(c, i + 1));
        }
        t[c, i] = res;
    }
    return t[c, i];
}

Conclusion

    [!important] Points clés sur la Programmation Dynamique

    DP = Récursivité + Tableau.
    Complexité: Dépend du nombre de cases du tableau et du temps de chaque appel.
    Cas d’usage: La DP est utile lorsque plusieurs trajectoires peuvent aboutir au même état.

    [!abstract] En résumé, la programmation dynamique permet de résoudre efficacement des problèmes où de nombreuses solutions partielles peuvent être réutilisées, en particulier dans les problèmes d'optimisation combinatoire.


![[Réduction]]