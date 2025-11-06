Le Domain Driven Design (DDD) est une approche qui a pour but de centrer le développement logiciel autour du domaine métier
et d'un langage commun entre les experts métier et les développeurs.

Le DDD a été introduit et popularisé par Eric Evans dans son livre _Domain-Driven Design: Tackling Complexity in the Heart of Software_.

Le __domaine__ représente le cœur d'une application, ce pour quoi le logiciel est conçu. Dans le cadre d'une application d'entreprise,
c'est le business model de celle-ci, ce qui apporte de la valeur.

Par exemple:
- pour une banque, le domaine serait la gestion des comptes, des transactions, des prêts...
- pour une compagnie aérienne: les vols, les réservations, la gestion des passagers...

## Principes fondamentaux

### Langage universel entre tous les acteurs du logiciel (Ubiquitous Language)

Tous les acteurs doivent utiliser le même vocabulaire, et cela doit également se refléter dans le code métier.

### La modélisation du domaine

La modélisation du code métier doit être pilotée par l'Ubiquotous Language et ses définitions. 

### Séparation du domaine et du technique

Le code métier ne doit pas contenir de détails techniques (http, base de données...). Ces détails techniques doivent
être implémentés dans des modules séparés qui vont utiliser le domaine.

## Avantages

- Alignement entre le métier et le code, ce qui minimise, voire annule tout écart entre le besoin initial et la solution finale
- Réduction de la complexité accidentelle, qui est provoquée par une mauvaise compréhension du métier
- Code métier facilement testable et maintenable

## Inconvénients

- L'application du DDD peut être très chronophage, et demande beaucoup de rigueur
- Overkill pour les projets dont le métier n'est pas complexe

## Concepts

L'application du DDD s'articule autour de 2 étapes complémentaires: le design stratégique et le design tactique.

## Design stratégique

Le design stratégique est la phase de définition du domaine du point de vue métier. Après cette phase (qui va concerner
les experts et les développeurs), les développeurs devraient avoir une vue d'ensemble de toutes les définitions
du domaine et des relations entre elles.

### Event Storming

L'Event Storming est le moyen principal de réunir tous les acteurs, et définir le domaine dans sa globalité.
Après une session d'Event Storming, nous devons pouvoir définir notamment l'Ubiquitous Language, les Bounded Contexts,
les Context Maps, les entités, les value objects...

### Bounded Contexts

Un Bounded Context (contexte borné en français) délimite une frontière du métier. Les définitions dans cette frontière
peuvent évoluer indépendamment du reste du métier. Dans une architecture microservice, cela équivaut à un service.
Pour reprendre notre exemple d'une gestion de banque, nous pouvons avoir comme bounded contexts: `transaction`, `utilisateur`, `carte-bancaire` etc...

Un bounded context qui change ne doit PAS en affecter un autre.
Chaque contexte a son propre Ubiquitous Language et ses propres règles métier.

## Context Maps

Un context map représente tout simplement une dépendance entre deux bounded contexts. La liste des context maps définissent
comment les bounded contexts interagissent.

## Design tactique

### Entity

Une entité est un objet qui est défini par son identité et qui a un cycle de vie.

### Value Object

Un value object est un objet sans identité propre: il est défini par sa valeur.

### Repository

Un repository est une interface fournissant des méthodes qui interagiront avec un outil de stockage (base de données,
fichiers...)

### Service

Un service contient de la logique qui ne se trouve pas naturellement dans une entité ou un value object.
C'est une classe qui va utiliser des entités et des value objects pour communiquer avec des repositories.
