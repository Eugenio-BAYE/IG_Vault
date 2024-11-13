
> [!danger]- GPT SUMMARY
# Formalisation pour les problèmes d'optimisation
## Poly vs $NP$-hard pour les problèmes d'optimisation

> [!abstract] Un **problème d'optimisation** consiste à maximiser ou minimiser une fonction objectif tout en respectant des contraintes spécifiques à une instance donnée.

## Problème d'optimisation vs Problème de décision

- *Problème de décision* : Question de la forme "OUI ou NON".
- *Problème d'optimisation* : Trouver une solution réalisable qui maximise ou minimise une fonction objectif définie.

> [!example] - **Exemples** :
> - **3-SAT** : Problème de décision (existe-t-il une assignation vérifiant la formule ?).
> - **3-COL** : Problème de décision (le graphe est-il 3-colorable ?).

## Définition d’un problème d’optimisation

- **Entrée** : Une instance I ∈ I.
- **Sortie** : Une solution S réalisable (vérifiant les contraintes C).
- **Objectif** : Maximiser ou minimiser une fonction c(I, S).

### Remarque
- Il peut exister plusieurs solutions optimales, mais la valeur optimale elle-même est unique.

## Complexité des problèmes d'optimisation

- Un problème est **polynomial** s'il existe un algorithme capable de trouver une solution optimale en temps polynomial pour toute instance.
- Exemples :
  - **MAX-MATCHING** : Polynomial.
  - **Vertex Cover (VC)** : Pas de solution polynomiale connue, NP-hard.

> [!important] - **Complexité** :
> - Si un problème d'optimisation est NP-hard, cela signifie qu'il n'existe pas d'algorithme polynomial pour le résoudre, sauf si P = NP.

# Une réduction entre problèmes de décision

> [!abstract] Une **réduction** entre deux problèmes de décision consiste à transformer une instance d’un problème en une instance d’un autre, tout en préservant la réponse (OUI/NON). Cela permet de prouver la complexité relative des problèmes.

## Définition

- Une réduction de **Π₁ à Π₂** (notée Π₁ ≤ Π₂) signifie qu'il existe un **algorithme polynomial** \( f \) qui transforme une instance I₁ de Π₁ en une instance I₂ de Π₂.
- Cette transformation a la propriété suivante :
  - Si I₁ est une instance OUI de Π₁, alors I₂ est aussi une instance OUI de Π₂, et inversement pour les instances NON.

### Explication supplémentaire
*Cela permet de démontrer que si Π₂ est un problème facile (polynomial), alors Π₁ l'est également. Inversement, si Π₁ est difficile (NP-hard), cela implique que Π₂ l'est aussi.*

## Théorème

> [!important] Si Π₁ ≤ Π₂ et Π₂ peut être résolu en temps polynomial, alors Π₁ peut aussi être résolu en temps polynomial.

> [!example] - **Exemple** : Supposons que l’on sache résoudre Π₂ (par exemple 2-SAT) en temps polynomial. Si Π₁ (par exemple SAT) peut être réduit à Π₂, alors SAT est aussi polynomial, ce qui aurait des implications importantes sur la théorie de la complexité.

## Réduction pour prouver la difficulté (NP-hard)

- Dans la pratique, on utilise souvent cette technique **dans l'autre sens** pour montrer qu'un problème est difficile.
  - *On part d'un problème Π₀ connu pour être difficile* (NP-hard), et on montre que Π₀ se réduit à un autre problème Π₁. Cela prouve que Π₁ est aussi difficile que Π₀.

> [!example] - **Exemple** : Pour montrer que **Clique** est NP-hard, on peut partir de **3-SAT** (qui est NP-hard) et montrer qu’il existe une réduction de 3-SAT vers Clique.

# Réductions pour les problèmes d'optimisation

> [!abstract] Les **réductions** pour les problèmes d’optimisation permettent de transformer une instance d’un problème d’optimisation en une instance d’un autre problème, tout en préservant les propriétés de la solution optimale. Cela permet de prouver la complexité des problèmes d'optimisation.

## Définition d'une réduction (≤S)

- Soit Π₁ et Π₂ deux problèmes de **maximisation**.
- Π₁ se **S-réduit** à Π₂ (noté Π₁ ≤S Π₂) s'il existe deux algorithmes polynomiaux \( f \) et \( g \) :
  - \( f \) crée une instance I₂ de Π₂ à partir d'une instance I₁ de Π₁.
  - Pour tout seuil \( t \), si Π₁ a une solution \( s₁ \) avec \( c₁(s₁) ≥ t \), alors Π₂ a une solution \( s₂ \) avec \( c₂(s₂) ≥ t \).
  - L'algorithme \( g \) permet de transformer la solution \( s₂ \) de Π₂ en une solution \( s₁ \) de Π₁, avec la garantie que \( c₁(s₁) ≥ c₂(s₂) \).

### Explication supplémentaire
*Cela signifie que si Π₂ peut être résolu efficacement (en temps polynomial), alors Π₁ peut également être résolu en temps polynomial.*

## Exemple de réduction pour les problèmes de minimisation

- La définition peut être adaptée pour les problèmes de **minimisation** de façon similaire :
  - On vérifie que \( c₁(s₁) ≤ t \) implique \( c₂(s₂) ≤ t \), et vice versa.

> [!important] La réduction entre problèmes d'optimisation est cruciale pour prouver qu’un problème d’optimisation est difficile, en montrant qu’il est au moins aussi difficile qu’un autre problème NP-hard.

# Exemple : Problème de réservation de terrain de tennis

> [!abstract] Ce problème consiste à accepter le maximum de réservations d’un terrain de tennis sans créer de chevauchements.

## Formulation

- **Entrée** : \( n \) intervalles \( r_i = [d_i, f_i] \), où \( d_i < f_i \) représente les heures de réservation.
- **Objectif** : Maximiser le nombre de réservations acceptées sans chevauchement.

### Interprétation en théorie des graphes

- Ce problème ressemble au problème de l’ensemble indépendant (IS).
  - Chaque réservation est un sommet.
  - Une arête existe entre deux réservations si elles se chevauchent.
  - L'objectif est de trouver un ensemble stable de réservations.

> [!important] La réduction consiste à montrer que le problème de réservation se réduit au problème de l’ensemble stable dans les graphes d'intervalles (IS-inter), qui peut être résolu en temps polynomial.

### Conclusion

> [!important] Cette réduction montre que le problème de réservation de terrain de tennis peut être résolu en temps polynomial, car **IS-inter** est polynomial.

# Quelques principes pour aider au P vs NP-hard

> [!abstract] Trouver des réductions efficaces entre problèmes peut être difficile. Voici quelques principes pour faciliter cette tâche.

## Principe 1 : Utiliser des objets mathématiques

- Formalisez votre problème avec des **objets mathématiques** (graphes, ensembles, tuples), plutôt que des structures informatiques comme des tableaux.
- Cela aide à identifier des problèmes similaires ou des réductions possibles.

> [!example] **Exemple** : Problème de stabilité chimique
> - **Entrée** : Une matrice booléenne indiquant si deux éléments sont dangereux ensemble.
> - **Sortie** : Un sous-ensemble d'éléments qui ne sont pas dangereux ensemble.
> - Ce problème correspond à un **ensemble stable** dans un graphe.

## Principe 2 : Identifier la catégorie du problème

- Devinez dans quelle **catégorie** de problèmes se trouve votre problème (par exemple, SAT, graphes, covering, partitioning).
- Consultez des ouvrages de référence comme **Garey & Johnson** pour identifier les problèmes classiques NP-hard ou polynomiaux.

## Principe 3 : Chercher des hypothèses supplémentaires

- Identifiez si des **hypothèses supplémentaires** simplifient votre problème.
  - Par exemple, si votre problème concerne un graphe, vérifiez s'il s'agit d’un graphe particulier (planaire, biparti, etc.).

> [!example] **Exemple** : Problème de réservation de tennis (RESA)
> - Le problème RESA peut sembler NP-hard, mais en fait, il est polynomial lorsqu'il est restreint aux **graphes d’intervalles**.
