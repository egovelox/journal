# Base de données: Modélisation d'un domaine fonctionnel.

Le domaine fonctionnel est vu comme une composition d'objets. 

On peut très bien utilister UML et le diagramme de classes.
Bien qu'UML soit destiné à décrire l'organisation d'un système avec une approche orientée objet (AOO), et non une base de données relationnelle, il peut servir de base à sa conception en modélisant le domaine fonctionnel (grâce au diagramme de classes).

## Rappels
Une base de données relationnelle est un ensemble de tableaux (appelés « tables »). 

Ces tables correspondent globalement aux classes en AOO.

Chaque colonne d'une table représente un attribut.

Chaque ligne (appelée tuple ou n-uplet) représente une instance donnant ainsi la valeur de chaque attribut de l'objet.

Une base de données relationnelle est donc composée d'un ensemble de tables, pouvant être liées entre elles. 
Cette manière d'organiser les éléments s'appuie sur ce que l'on appelle un modèle relationnel.

## Méthode

Vous commencez par identifier les concepts ou entités de votre domaine fonctionnel. => Vous listez ainsi les classes.

Pour chaque classe, vous identifiez ensuite les informations à enregistrer et leur type (texte, nombre...). => Vous obtenez ainsi un diagramme de classes avec leurs attributs.

Vous créez le modèle physique de données à partir du diagramme de classes en :
* créant une table pour chaque classe ;
* créant, dans chaque table, une colonne pour chaque attribut de la classe correspondante.

## Nommage en UML
* Pour le nom des classes :
	* au singulier
	* avec des lettres non accentuées
	* commençant par une majuscule
	* utilisant Pascal Case (chaque mot commence avec une majuscule)
	* Ex : PierrePrecieuse

* Pour les attributs :
	* au singulier
	* avec des lettres non accentuées
	* commençant par une minuscule
	* utilisant Camel Case (chaque mot commence avec une majuscule sauf le premier)
	* Ex : couleurYeux

* Dans le MPD :
	* Pour le nom des tables et des attributs :
	* au singulier
	* avec des lettres non accentuées
	* en minuscules
	* utilisant Underscore Case (_)
	* Ex : pierre_precieuse, couleur_yeux


## Relations entre entités
NB: on parle d'association entre classes en UML, en AOO il s'agit en fait d'associations entre objets, entre instances de ces classes.

En UML, la relation entre deux classes s'appelle une association.

Les multiplicités servent à apposer des contraintes numériques sur l'association, ou plus précisément, combien d'instances d'une classe peuvent être liées à une instance de la classe de l'autre côté de l'association. En d'autres termes, elles bornent les cardinalités des instances liées entre elles.


```
Classe A Ax/Ay	______	Bx/By Classe B

Ax/Ay Combien de A **POUR 1 B**
Bx/By Combien de B **POUR 1 A**

```

Il est important de noter que les multiplicités imposent des limites de cardinalités à un **instant t**.

**Il n'y a pas de notion d'historique dans les associations.**

* Exemple: Musicien / Groupe
Classe Musicien 2/10 _____CONSTITUER_______ 0/5 Classe Groupe

Au min 2, au max 10 musiciens POUR UN GROUPE
Au min 0, au max 5 groupes POUR UN MUSICIEN


## CATEGORIES D'ASSOCIATIONS
Les associations sont classées en 3 catégories, en fonction des multiplicités apposées sur celles-ci.
* ONE TO ONE
* ONE TO MANY
* MANY TO MANY

## TRADUCTION EN UN MPD
Traduire les associations entre classes (UML) dans un modèle relationnel.

On le sait, une clé primaire (PK) sert d'identifiant pour chaque n-uplet ou tuple.

À quoi va bien servir cet identifiant ?

Avant de faire un lien entre les tuples de différentes tables (ou instances de classes), il faut pouvoir les identifier de manière unique et certaine.

**C'est ce que fait la clé primaire.**

Et c'est cette clé qui va servir de référence pour relier les tuples de la table à ceux d'une autre table !

Le principe général: créer un attribut qui contient une référence vers le tuple lié.

**C'est la clé étrangère.**
La valeur de cet attribut est toujours la valeur de la clé primaire du tuple lié.


### Traduction ONE TO ONE : 
choix possible de la table où déclarer la clé étrangère

    (voiture 1 ______ 0/1 conducteur)

Soit dans la table voiture (plus évident, une voiture accueille un conducteur)

Soit dans la table conducteur (moins intuitif)

### Traduction ONE TO MANY: 
choix impossible.

    (journal 1 ________  0/* article)

La clé étrangère est un forcément attribut de la table article.

### Traduction MANY TO MANY:
il n'est plus possible de faire ce lien d'une table à l'autre.

    (musicien 1/* _________ * groupe)

La solution consiste à créer une table ad hoc, matérialisant les liens multiples, en créant une **CLE PRIMAIRE COMPOSEE** des clés étrangères pointant vers les tables musicien et groupe

```
	musicien             __________         composition                  __________       groupe
    _id: INTEGER [PK]                     musicien_id: INTEGER [PK, FK]                   _id: INTEGER [PK]
     prenom: VARCHAR                       groupe_id: INTEGER [PK, FK]			    nom : VARCHAR
       nom: VARCHAR

```

## LES CLASSES D'ASSOCIATION 

Au niveau du modèle conceptuel, lorsque l'association est MANY TO MANY, il arrive qu'on crée une classe d'association, rendant possible l'ajout d'attribut propre à cette association.

Imaginons l'association représentant les concerts donnés par un groupe de musique dans des lieux de spectacle. 

A chaque fois que j'ai un lieu entre un Groupe et un Lieu, cela donne lieu de représenter un Concert. 

En créant la classe d'association Concert, je peux ajouter, par exemple, un attribut date, qui spécifie la date du concert.

```
	
	Groupe  * _______________________  * Lieu
      nom: String	     |               nom : String
			     |               ville: String
			  Concert
			 date: Date

```

Traduction en MPD: une CLASSE D'ASSOCIATION donne lieu à une TABLE de même nom, avec une CLE PRIMAIRE COMPOSEE, et les attributs de cette classe.

```

	groupe 		    __________         concert			   __________       lieu
    _id: INTEGER [PK]                     groupe_id: INTEGER [PK, FK]                   _id: INTEGER [PK]
      nom: VARCHAR		           lieu_id: INTEGER [PK, FK]			  nom : VARCHAR
					       date: DATE			         ville: VARCHAR

```

Il y a de nombreux cas où les classes d'association sont utiles, par exemple enregistrer le numéro de siège dans une relation Passager/Vol, etc.

