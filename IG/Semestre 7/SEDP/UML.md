---
title: SEDP_UML_Complements_and_Practical_Aspects_EN
author: Eugénio BAYE
lecture author: Tiberiu STRATULAT
lecture: Fondamentaux du Machine Learning et Pattern Mining, Polytech Montpellier
date: 2024-10-15
update: 2024-10-15
copyright: Polytech Montpellier, Tiberiu STRATULAT
---
# Introduction to UML
> [!important] Unified Modeling Language ( #UML)
> Normalized graphic method to visualize software engineering models and object-oriented programming #OOP conception
> 
> Class diagrams
>- Describe classes and their relationships
>
> Interaction diagrams
>- show the behaviour of systems in terms of how objects interact with each other
>
> State diagrams and activity diagrams
>- show how systems behave internally
>
> Component and deployment diagrams
>- show how the various components of systems are arranged logically and physically


## What constitutes a good model ?

A model should :
- use a standard notation
- be understandable by clients and users
- lead software engineers to have insights about the system
- provide abstraction
Models are used :
- to help create designs
- to permit analysis and review of those designs.
- as the core documentation describing the system

## Class diagrams

> [!tip] Essentials of UML Class Diagrams
> The main symbols shown on class diagrams are:
>- Classes
>	- represent the types of data themselves
>- Associations
>	- represent linkages between instances of classes
>- Attributes
>	- are simple data found in classes and their instances
>- Operations
>	- represent the functions performed by the classes and their instances
>- Generalizations
>	- group classes into inheritance hierarchies


### Classes

A class is simply represented as a box with the name of the class inside
- The diagram may also show the attributes and operations
> [!example]
> ![[UML - FIG1.png]]

### Associations and Multiplicity
An **association** is used to show how two classes are related to each other.
- Symbols indicating multiplicity are shown at each end of the association

> [!example]
> ![[UML - FIG2.png]]

### Labelling associations
Each association can be labelled, to make explicit the nature of the association.
> [!example]
> ![[UML - FIG3.png]]

### Analyzing and validating associations
> [!tip] Many-to-one
>> [!example]
>> A company has many employees,
>> An employee can only work for one company.
>>- This company will not store data about the moonlighting activities of employees!
>> A company can have zero employees
>>- E.g. a ‘shell’ company
>> It is not possible to be an employee unless you work for a company
>> ![[UML - FIG4 1.png]]

> [!tip] Many-to-many
>> [!example]
>>- An assistant can work for many managers
>>- A manager can have many assistants
>>- Assistants can work in pools
>>- Managers can have a group of assistants
>>- Some managers might have zero assistants.
>>- Is it possible for an assistant to have, perhaps temporarily, zero managers?
>> ![[Semestre 7/SEDP/FIG FROM COURS/UML - FIG4.png]]

> [!tip] One-to-One
>> [!example]
>> For each company, there is exactly one board of directors
>> A board is the board of only one company
>> A company must always have a board
>> A board must always be of some company
>> ![[UML - FIG5.png]]

> [!warning]
> Avoid unnecessary one-to-one associations
> 
> Avoir this :
> ![[UML - FIG6.png]]
> 
> Do this instead :
> ![[UML - FIG7.png]]

### A more complex example
> [!example] 
> A booking is always for exactly one passenger
>- no booking with zero passengers
>- a booking could never involve more than one passenger.
>
> A Passenger can have any number of Bookings
>- a passenger could have no bookings at all
>- a passenger could have more than one booking
>
> ![[UML - FIG8.png]]
> 
> The frame around this diagram is an optional feature that any UML 2.0 may possess.

## Association classes
Sometimes, an attribute that concerns two associated classes cannot be placed in either of the classes
> [!example]
> The following are equivalent :
> ![[UML - FIG9.png]]

### Types of associations
> [!important] Directionality in associations
>- Associations are by default bi-directional
>- It is possible to limit the direction of an association by adding an arrow at one end.
>
>> [!example] 
>> ![[UML - FIG10.png]]

> [!important] Reflexive associations
>- It is possible for an association to connect a class to itself
>
>> [!example]
>> ![[UML - FIG11.png]]

> [!important] Generalization
> Specializing a superclass into two or more subclasses
>- A generalization set is a labeled group of generalizations with a common superclass
>- The label (sometimes called the discriminator) describes the criteria used in the specialization
>
> ![[UML - FIG12.png]]
> 
>> [!warning] Avoiding unnecessary generalizations
>> Inappropriate hierarchy of classes, which should be instances
>> Inappropriate example :
>> ![[Semestre 7/SEDP/FIG FROM COURS/UML - FIG13.png]]
>> 
>> Appropriate example :
>> ![[UML - FIG14.png]]

> [!important] Handling multiple discriminators
> Creating higher-level generalization
>> [!example]
>> ![[UML - FIG15.png]]
>
> Using multiple inheritance
> Using the Player-Role pattern
>> [!example]
>> ![[UML - FIG16.png]]

> [!warning] Avoiding having instances change class
> An instance should never need to change class
> ![[UML - FIG17.png]]

## Object Diagrams
> [!failure] Until 
>> Conception : Qqc qui n'existe pas
>> Modélisation : Représentation abstraite d'une réalité

