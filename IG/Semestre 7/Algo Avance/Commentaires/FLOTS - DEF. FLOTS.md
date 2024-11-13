Les **flots** dans un réseau représentent des quantités circulant d’un point à un autre, en respectant des règles spécifiques comme les limites de capacité et la conservation du flux. Ils modélisent des systèmes transportant des ressources, par exemple de l’eau dans des canalisations, des véhicules sur des routes, ou des données dans des réseaux informatiques.

### Principes de Base des Flots
Un flot est formalisé par une fonction $f : A \to \mathbb{R}^+$, où :
- **$A$** est l’ensemble des arcs (ou liens) dans le réseau.
- **$\mathbb{R}^+$** signifie que le flot est une valeur positive (ou nulle), correspondant à la quantité transportée par chaque arc.

### Propriétés des Flots
Deux règles principales régissent le comportement d'un flot dans un réseau :

1. **Contrainte de Capacité**
   - Chaque arc $a$ possède une capacité $c(a)$, le maximum de flot qu’il peut transporter.
   - La contrainte de capacité exige que, pour tout arc $a$, 
     $$ f(a) \leq c(a) $$

2. **Conservation du Flot**
   - Pour chaque nœud (ou sommet) $v$ du réseau, à l'exception de la source $s$ et du puits $t$, la quantité totale de flot entrant dans $v$ doit être égale à la quantité totale de flot sortant de $v$.
   - En termes mathématiques, si $f^+(v)$ représente le flot sortant de $v$ et $f^-(v)$ le flot entrant dans $v$, alors :
     $$ f^+(v) = f^-(v) $$
   - Plus formellement, cette conservation s'écrit :
     $$ \sum_{{vw \in A}} f(vw) = \sum_{{wv \in A}} f(wv) $$
   - Cela signifie que pour chaque sommet (autre que la source et le puits), le flot total entrant est égal au flot total sortant.

### Objectif : Maximisation du Flot
Dans un problème de **flot maximum**, l'objectif est de maximiser le flot total sortant de la source $s$ et atteignant le puits $t$, tout en respectant les contraintes de capacité et de conservation. Ce problème est crucial pour l’optimisation de réseaux dans divers domaines, comme les transports, la logistique et les communications.
