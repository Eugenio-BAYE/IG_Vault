---
title: Entrepots_BDD_Entrepots_FR
author: Eugénio BAYE
lecture author: Anne LAURENT
lecture: Entrepôts de Données
date: 2024-11-17
update: 2024-11-17
copyright: Polytech Montpellier, Anne LAURENT
---
## Entrepôts de données
> [!abstract] Fonctionnement Général d'un Entrepôt de Données
> - Données provenant de sources hétérogènes.
> - Passage par des processus **ETL** (Extraction, Transformation, Chargement).
> - Magasin de données multidimensionnelles pour l'analyse.

### Types de systèmes de gestion de bases de données

> [!important] OLAP
> **OLAP (On-Line Analytical Processing)** : Analyser de grandes quantités de données pour des *rapports complexes* ou des *analyses décisionnelles*.
>- Requêtes complexes
>- Optique *décisionnelle*
>- Vision ensembliste (tendances ...)
>- Destiné aux analystes et décideurs (peu nombreux)

> [!important] OLTP
> **OLTP (On-Line Transaction Processing)** : Traiter un *grand nombre de transactions* rapides et courantes
>- Requêtes simples
>- Production et Mise à jour des données
>- Vision au niveau individuel
>- Destiné aux agents *opérationnels* (nombreux)

### Représentation Multidimensionnelle

![[BDD_ENTR_FIG1.png]]
> Ce cube nous permet de visualiser des données multidimensionnelles et d'analyser les ventes selon trois dimensions principales : les produits, les villes, et les mois. En d'autres termes, on peut suivre combien de produits ont été vendus dans différentes villes au cours de plusieurs mois.


Les données dans les entrepôts sont organisées autour de **dimensions**, permettant une analyse multidimensionnelle.

> [!important] Types de dimensions :
> - **Dimensions plates** : Pas de sous-niveaux, chaque élément est *isolé*.
> - **Dimensions hiérarchisées** : Les données sont *structurées* en plusieurs niveaux d'analyse.

> [!important] Hiérarchies :
>- **Hiérarchies simples** : Organisation arborescente avec un *seul parent* par niveau (ex : Jour > Mois > Trimestre).
>- **Hiérarchies complexes** : Plus flexible, un élément peut avoir *plusieurs parents* ou appartenir à plusieurs niveaux.

> Pour la dimension hiérarchisée **Temps** :
>- **Jour > Semaine > Mois > Trimestre**
>- Graphique inexact


![[BDD_ENTR_FIG2.png]]

> [!important] **ETL (Extract, Transform, Load)**  
> - **Extract** : Extraction des données depuis diverses sources (bases de données, fichiers).  
> - **Transform** : Nettoyage et harmonisation des données (formats, valeurs invalides).  
> - **Load** : Chargement des données transformées dans l'entrepôt.  
> _L'ETL représente 80% du travail dans un projet décisionnel, car il assure que les données sont prêtes à être analysées._

> [!important] **Table de faits**  
> Contient les mesures ou événements à analyser, souvent volumineuse. Exemples : ventes, transactions.

> [!important] **Tables de dimensions**  
> Fournissent des informations contextuelles aux faits (ex : produits, clients). Moins volumineuses que la table de faits.  


> [!important] Table de faits normalisée
> Une table est **BCNF** (Boyce-Codd Normal Form) si elle est déjà *3-NF* (Troisième Forme Normale) et si pour chaque dépendance fonctionnelle non triviale $X \rightarrow Y$, l'attribut $X$ est une *clé candidate* (attribut ou ensemble qui identifie chaque ligne de la table)

### Types de schémas multidimensionnels

> [!important] **Schéma en étoile**  
> - Simple, table de faits centrale reliée à des dimensions non normalisées.  
> - Facile à comprendre, mais redondance possible dans les dimensions.  

> [!important] **Schéma en flocon**  
> - Dimensions normalisées (sans redondance), reliées indirectement à la table de faits.  
> - Moins de redondance, mais requêtes plus complexes et coûteuses en termes de navigation.  

> [!example] Schéma en flocon
> ![[BDD_ENTR_FIG3.png]]
> ![[BDD_ENTR_FIG4.png]]
>> Sales est la table de faits
>> Les autres sont les tables de dimensions. Cela veut dire qu'on va analyser les ventes en fonction des autres facteurs comme le temps, les produits et les magasins

> [!example] Schéma en flocon
> ![[BDD_ENTR_FIG5.png]]
>> Moins redondant -> Les produits sont divisés par catégories, mais nécessite plus de jointures pour obtenir toutes les informations, donc perte d'efficacité

> [!example] Schéma normalisé
> ![[BDD_ENTR_FIG6.png]]
>> Les informations sont divisées en plusieurs tables pour éviter la redondance, le schéma est normalisé (Les stores vont souvent avoir les mêmes départements... Donc on crée une table département)

## Hypercube
### Calcul du cube
Questions à se poser pour faire le calcul du cube:
> [!important] Quel cube construire
> Réfléchir aux dimensions et aux mesures nécessaires pour construire le cube (OLAP)
>> [!example]
>> Pour l'analyse des ventes, on prend `sales` en table de faits et `products`, `time`, `store`... En table de dimensions.
>> Il faut aussi penser à la **granularité**, c'est à dire veut on le time par Mois? Semaine? Jour?

> [!important] Comment le construire
> Comprendre la structure du cube, c'est à dire les mesures, les "unités" qu'on va utiliser, et comment les agrégations ou conversions seront calculées.
>> [!example]
>> Si on veut les ventes totales par mois, on utilisera un `GROUP BY` pour avoir des $ventes/mois$
>
> L'agrégation de toutes les données dimensions choisies se fait par le `GROUP BY`

> [!important] Treillis des Cuboïdes
> Les **treillis** sont toutes les combinaisons possibles d'agrégations des dimensions.
>> [!example]
>> Pour l'analyse des ventes, on peut faire
>>- **0D** (Aucune Dimension): Nombre de vente total dans nos données
>>- **1D** (1 Dimension): On va agréger une seule dimensions :
>>	- Ventes par Mois
>>	- Ventes par Produits
>>	- Ventes par Ville
>>- **2D** (2 Dimensions): On agrège 2 dimensions:
>>	- Ventes par Mois par Villes
>>	- ...

> [!failure] Ajouter nouveau cours sur le treillis
### Stockage du cube
Types de stockage de cube :
> [!important] ROLAP (Relational OLAP)
> Les données sont stockées dans une base de données relationnelle classique. On ne stocke pas le cube, il n'est pas matérialise.
> Les calculs sont effectués dynamiquement au moment de la requête
> Avantages:
>- Gestion de très gros volumes de données
> 
> Inconvénients:
>- Requêtes plus lentes car il faut recalculer le cube 

> [!important] MOLAP (Multidimensional OLAP)
> Les données sont stockées sous forme de cubes multidimensionnels matérialisés. Les agrégations nécessaires (la formation du cube) sont pré-calculées.
> Avantages:
>- Calculs très rapides
>- Optimisé pour les analyses complexes
>
> Inconvénients:
>- Consomme beaucoup d'espace de stockage donc limité en capacité

> [!important] HOLAP (Hybrid OLAP)
> Combinaison hybride entre ROLAP et MOLAP.
> Une partie des données est *matérialisée* (MOLAP) et l'autre partie reste stockée de manière relationnelle (ROLAP)
> C'est un compromis entre les 2 types de stockage, à optimiser en fonction des besoins.

> [!important] Sparsity
> Dans un cube OLAP, un grand nombre de cellules du cube sont vides ou ne contiennent pas de données. Un cube a plusieurs dimensions n'aura pas toujours de données significative pour toutes les combinaisons possibles de dimensions.

### Mise à jour des données

> [!important] Incrémentale
> On met à jour uniquement les données qui ont changé depuis le dernier rafraîchissement.
> Plus rapide et efficace mais nécessite une gestion complexe pour identifier précisément les changements.


> [!important] Recalcul Total
> On recalcule l'intégralité du cube en rechargeant toutes les données, même celles qu'on avait déjà précédemment.
> Assure des données toujours cohérentes et à jour, mais très coûteux en ressources.

### Opération OLAP
#### Visualisation
> [!important] Rotation (`PIVOT`)
> Permets de tourner le cube de données pour examiner les informations sous un angle différent. 
> 
> ($ventes/produits/mois\rightarrow ventes/mois/produits$)

> [!important] Inversion (`SWITCH`)
> Interversion des axes du cubes. 
> 
> Villes en fonction de produits devient produits en fonction de villes.
#### Modification
> [!important] Sélection sur les cellules (`SLICE`)
> Extraction d'une tranche de données en fixant une seule dimension
> 
> Cube avec Produit, Mois, Ville : On peut obtenir une sélection uniquement sur les données de ventes pour le moi de janvier

> [!important] Sélection sur les tranches (`DICE`)
> Extraction d'un sous-ensemble de cellules en fixant plusieurs dimensions
> 
> Ventes pour la ville de Clermont Férrand en Janvier et Février

> [!important] Spécialisation (`DRILL-DOWN`)
> Descente dans la hiérarchie (concept de granularité) pour obtenir des données plus détaillées.
> 
> On passe des ventes par ans aux ventes par mois ...

> [!important] Généralisation (`ROLL-UP`)
> Montée dans la hiérarchie (concept de granularité) pour obtenir des données agrégées
> 
> On passe des ventes par jour aux ventes par semaine

Spécialisation et Généralisation sont l'inverse l'un de l'autre

## Outils Commerciaux pour OLAP
Moteurs:
- Traitement et analyse des données, execution des requêtes...
Reporting:
- Création de rapports basés sur les analyses OLAP, présentation des données analysées de manière compréhensible pour les utilisateurs métiers.

> [!abstract] Example d'outils
> Microsoft SQL SSAS
> Oracle OLAP
> IBM Cognos
> SAP BusinessObjects
> Tableau Software
> Zendesk

## Oracle OLAP

> [!important] Options et Outils
> - **OLAP OPTION** : Oracle fournit des fonctionnalités dédiées à l'analyse OLAP, intégrées dans ses bases de données.
> - **Analytic Workspace et OLAP DML (Data Manipulation Language)** : Outils permettant de créer et de gérer des cubes multidimensionnels.
> - **Requêtes de partitionnement** : Optimisent les performances des analyses en divisant les données.
> - **Fonctions d'analyse** : Calculs avancés pour des insights précis, comme le rang, la proportion, et d'autres mesures analytiques.
> - **Outils ETL** : Pour extraire, transformer, et charger les données dans les entrepôts.
> - **Outils d'analyse** : Rapports et visualisations pour faciliter la prise de décision.

Gestion des cubes de différents types :
![[BDD_ENTR_FIG7.png]]

### Création de BD
> [!failure] Explications sur la configuration ?
> TODO: Expliquer 

### Partitionnement de données
> [!failure] Stratégies de gestion
> TODO: Expliquer


## Opérations de calcul de cube OLAP

> [!important] `GROUP BY`
> *Requête*:
> ```sql
> SELECT ville, etat, COUNT(*)
> FROM abonne, emprunt, exemplaire
> WHERE abonne.num_ab = emprunt.num_ab
>   AND exemplaire.numero = emprunt.num_ex
> GROUP BY ville, etat;
> ```
> *Résultat*:
> - La requête regroupe les données par `ville` et `etat`, comptant le nombre d'occurrences pour chaque combinaison.
> - Exemple de sortie :
>   - BEZIER, BON : 4
>   - BEZIER, ABIME : 2
>   - MONTPELLIER, BON : 18
>   - MONTPELLIER, ABIME : 2

---

> [!important] `GROUP BY CUBE`
> *Requête*:
> ```sql
> SELECT ville, etat, COUNT(*)
> FROM abonne, emprunt, exemplaire
> WHERE abonne.num_ab = emprunt.num_ab
>   AND exemplaire.numero = emprunt.num_ex
> GROUP BY CUBE(ville, etat);
> ```
> *Résultat*:
> - La clause `CUBE` génère toutes les combinaisons possibles d'agrégations, y compris les totaux globaux.
> - Exemple de sortie :
>   - BEZIER, BON : 4
>   - BEZIER, ABIME : 2
>   - BEZIER (tous états confondus) : 6
>   - MONTPELLIER, BON : 18
>   - MONTPELLIER, ABIME : 2
>   - MONTPELLIER (tous états confondus) : 20
>   - (Toutes les villes, tous les états) : 26

---

> [!important] `GROUP BY ROLLUP`
> *Requête*:
> ```sql
> SELECT ville, etat, COUNT(*)
> FROM abonne, emprunt, exemplaire
> WHERE abonne.num_ab = emprunt.num_ab
>   AND exemplaire.numero = emprunt.num_ex
> GROUP BY ROLLUP(ville, etat);
> ```
> *Résultat*:
> - La clause `ROLLUP` génère des totaux hiérarchiques, en regroupant d'abord par `ville`, puis en ajoutant des totaux pour chaque `etat`.
> - Exemple de sortie :
>   - BEZIER, BON : 4
>   - BEZIER, ABIME : 2
>   - BEZIER (tous états confondus) : 6
>   - MONTPELLIER, BON : 18
>   - MONTPELLIER, ABIME : 2
>   - MONTPELLIER (tous états confondus) : 20
>   - (Toutes les villes, tous les états) : 26

---

> [!important] `GROUP BY ROLLUP` avec `DECODE`
> *Requête*:
> ```sql
> SELECT DECODE(GROUPING(ville), 1, 'Toutes les villes', ville) AS ville,
>        DECODE(GROUPING(etat), 1, 'Tous états confondus', etat) AS etat,
>        COUNT(*)
> FROM abonne, emprunt, exemplaire
> WHERE abonne.num_ab = emprunt.num_ab
>   AND exemplaire.numero = emprunt.num_ex
> GROUP BY ROLLUP(ville, etat);
> ```
> *Résultat*:
> - La fonction `DECODE` est utilisée pour remplacer les valeurs nulles par des libellés comme "Toutes les villes" ou "Tous états confondus".
> - Exemple de sortie :
>   - BEZIER, BON : 4
>   - BEZIER, ABIME : 2
>   - BEZIER, Tous états confondus : 6
>   - MONTPELLIER, BON : 18
>   - MONTPELLIER, ABIME : 2
>   - MONTPELLIER, Tous états confondus : 20
>   - Toutes les villes, Tous états confondus : 26

---

> [!important] `GROUPING SETS`
> *Requête*:
> ```sql
> SELECT ville, etat, COUNT(*)
> FROM abonne, emprunt, exemplaire
> WHERE abonne.num_ab = emprunt.num_ab
>   AND exemplaire.numero = emprunt.num_ex
> GROUP BY GROUPING SETS ((ville, etat), (ville), (etat), ());
> ```
> *Résultat*:
> - La clause `GROUPING SETS` permet de spécifier explicitement les combinaisons d'agrégations souhaitées.
> - Exemple de sortie :
>   - BEZIER, BON : 4
>   - BEZIER (tous états confondus) : 6
>   - (Toutes les villes, BON) : 22
>   - (Toutes les villes, tous états confondus) : 26

---

> [!important] `RANK`
> *Requête*:
> ```sql
> SELECT ville, etat, COUNT(*),
>        RANK() OVER (ORDER BY COUNT(*) DESC) AS rnk
> FROM emprunt, abonne, exemplaire
> WHERE emprunt.num_ab = abonne.num_ab
>   AND exemplaire.numero = emprunt.num_ex
> GROUP BY ville, etat;
> ```
> *Résultat*:
> - Classe les résultats selon le nombre d'occurrences, du plus élevé au plus faible.
> - Exemple de sortie :
>   - MONTPELLIER, BON : 18, RNK : 1
>   - BEZIER, BON : 4, RNK : 2
>   - BEZIER, ABIME : 2, RNK : 3
>   - MONTPELLIER, ABIME : 2, RNK : 3

---

> [!important] `TOP-N`
> *Requête*:
> ```sql
> SELECT *
> FROM (SELECT ville, etat, COUNT(*),
>              RANK() OVER (ORDER BY COUNT(*) DESC) AS rnk
>       FROM emprunt, abonne, exemplaire
>       WHERE emprunt.num_ab = abonne.num_ab
>         AND exemplaire.numero = emprunt.num_ex
>       GROUP BY ville, etat)
> WHERE rnk <= 2;
> ```
> *Résultat*:
> - Retourne les `N` premiers résultats selon le classement.
> - Exemple de sortie :
>   - MONTPELLIER, BON : 18, RNK : 1
>   - BEZIER, BON : 4, RNK : 2

---

> [!important] `BOTTOM-N`
> *Requête*:
> ```sql
> SELECT *
> FROM (SELECT ville, etat, COUNT(*),
>              RANK() OVER (ORDER BY COUNT(*)) AS rnk
>       FROM emprunt, abonne, exemplaire
>       WHERE emprunt.num_ab = abonne.num_ab
>         AND exemplaire.numero = emprunt.num_ex
>       GROUP BY ville, etat)
> WHERE rnk <= 2;
> ```
> *Résultat*:
> - Retourne les `N` derniers résultats selon le classement.
> - Exemple de sortie :
>   - BEZIER, ABIME : 2, RNK : 1
>   - MONTPELLIER, ABIME : 2, RNK : 1

---

> [!important] `RATIO_TO_REPORT`
> *Requête*:
> ```sql
> SELECT abonne.num_ab, ville, COUNT(*),
>        RATIO_TO_REPORT(COUNT(*)) OVER (PARTITION BY ville) AS ratio
> FROM emprunt, abonne
> WHERE emprunt.num_ab = abonne.num_ab
> GROUP BY ville, abonne.num_ab;
> ```
> *Résultat*:
> - Calcule la proportion de chaque valeur par rapport au total.
> - Exemple de sortie :
>   - 911007, BEZIER : 6, Ratio : 1
>   - 901001, MONTPELLIER : 4, Ratio : 0.2
>   - 902043, MONTPELLIER : 4, Ratio : 0.2
>   - 902075, MONTPELLIER : 2, Ratio : 0.1
>   - 911021, MONTPELLIER : 1, Ratio : 0.05
>   - 911023, MONTPELLIER : 6, Ratio : 0.3
>   - 921102 MONTPELLIER : 3, Ratio : 0.15

---

> [!important] `Création de BD`
> *Requête*:
> ```sql
> CREATE MATERIALIZED VIEW OLAPV_EMPRUNTS
> REFRESH START WITH SYSDATE NEXT SYSDATE+1
> ENABLE QUERY REWRITE
> AS
> SELECT VILLE, ETAT, COUNT(*)
> FROM EMPRUNT, EXEMPLAIRE, ABONNE
> WHERE EMPRUNT.NUM_AB = ABONNE.NUM_AB 
> AND EXEMPLAIRE.NUMERO = EMPRUNT.NUM_EX
> GROUP BY VILLE, ETAT;
> ```
> *Résultat*:
> - Crée une vue matérialisée OLAP qui peut être rafraîchie automatiquement chaque jour.

---

> [!important] `Interrogation des Vues Matérialisées`
> *Requête*:
> ```sql
> SELECT * FROM olapv_emprunts;
> ```
> *Résultat*:
> - Interroge directement la vue matérialisée `olapv_emprunts` pour afficher les données agrégées stockées.
> - Exemple de sortie :
>   - BEZIER, BON : 4
>   - BEZIER, ABIME : 2
>   - MONTPELLIER, BON : 18
>   - MONTPELLIER, ABIME : 2

---

> [!important] `Rafraîchissement des Vues Matérialisées`
> *Requête*:
> ```sql
> BEGIN
>   dbms_mview.refresh('olapv_emprunts');
> END;
> ```
> *Résultat*:
> - Rafraîchit la vue matérialisée `olapv_emprunts` pour s'assurer que les données sont à jour.
> - Exemple de sortie après l'insertion de nouvelles données :
>   - BEZIER, BON : 5 (mise à jour)
>   - BEZIER, ABIME : 2
>   - MONTPELLIER, BON : 18
>   - MONTPELLIER, ABIME : 2

## Dimensions
### Clefs
On ajoute souvent une clef de substitution pour remplacer la combinaison d'attributs qui représente l'ancienne clef primaire.

### Domaines évolutifs

> [!important] Domaines à Rafraîchissement Lent (SCD)
> - *Définition* : Les domaines de données qui changent rarement, par exemple les données démographiques de clients ou les descriptions de produits.
> - *Exemple* : Des informations telles que le nom, l’adresse d’un client, ou la description d’un produit.
> - *Utilisation* : Ces données ne nécessitent pas des mises à jour fréquentes, et leur rafraîchissement peut être planifié de manière moins régulière.

---

> [!important] Domaines à Rafraîchissement Rapide (RCD)
> - *Définition* : Les domaines de données qui changent fréquemment, comme les transactions de vente, les inventaires ou les taux d’actualisation.
> - *Exemple* : Les ventes quotidiennes, le stock de produits, ou les flux financiers.
> - *Utilisation* : Ces données nécessitent des mises à jour en temps réel ou à des intervalles très courts pour garantir l’exactitude de l’analyse décisionnelle.

## Estimation des volumes

> [!important] Estimer le volume de l'entrepôt
> - *Étapes pour estimer le volume* :
>   - Identifier le nombre de tables et leur taille moyenne.
>   - Calculer la taille de chaque table en multipliant le nombre de lignes par la taille moyenne d'un enregistrement.
>   - Considérer les index, les métadonnées, et la redondance.
>   - Prendre en compte la croissance des données sur une période donnée (par exemple, sur 5 ans).
> - *Formule* : Volume total = (Taille des tables + Index + Redondance) x Facteur de croissance.

## Conclusion

> [!important]
> - L'analyse et le design d'un entrepôt de données nécessitent une estimation précise des volumes pour assurer la performance et la scalabilité.
> - La compréhension des types d'évolution des données (lentes ou rapides) est cruciale pour optimiser les opérations de rafraîchissement et la mise à jour des données.
> - Une planification minutieuse garantit que l'entrepôt pourra répondre aux besoins futurs sans compromettre la performance.

## Ajouts
> [!tip] Densité cube de donnée
> La **densité d'un cube de données** représente le pourcentage de cellules du cube qui contiennent des données réelles, par rapport au nombre total de cellules possibles.
> $$\text{Densité}=\frac{\text{Nombre de cellules avec données}}{\text{Nombre total de cellules possibles}}\times100$$
> 
> Donc souvent en pratique:
>  $$\frac{\text{Nombre de lignes affichées par GROUP BY CUBE}}{\text{Nombre théorique de lignes en multipliant le nombre de valeur pour chaque dimension}}$$


## Référence
- Ralph Kimball, Entrepôts de Données, Vuibert, 2002.
- Jiawei Han, Micheline Kamber, Data Mining: Concepts and Techniques, Morgan Kaufmann Publishers, 2000.
- http://www.oracle.com