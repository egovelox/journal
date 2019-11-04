# Base de donn�es: Mod�lisation d'un domaine fonctionnel.

Le domaine fonctionnel est vu comme une composition d'objets. 

On peut tr�s bien utilister UML et le diagramme de classes.
Bien qu'UML soit destin� � d�crire l'organisation d'un syst�me avec une approche orient�e objet (AOO), et non une base de donn�es relationnelle, il peut servir de base � sa conception en mod�lisant le domaine fonctionnel (gr�ce au diagramme de classes).

## Rappels
Une base de donn�es relationnelle est un ensemble de tableaux (appel�s � tables �). 

Ces tables correspondent globalement aux classes en AOO.

Chaque colonne d'une table repr�sente un attribut.

Chaque ligne (appel�e tuple ou n-uplet) repr�sente une instance donnant ainsi la valeur de chaque attribut de l'objet.

Une base de donn�es relationnelle est donc compos�e d'un ensemble de tables, pouvant �tre li�es entre elles. 
Cette mani�re d'organiser les �l�ments s'appuie sur ce que l'on appelle un mod�le relationnel.

## M�thode

Vous commencez par identifier les concepts ou entit�s de votre domaine fonctionnel. => Vous listez ainsi les classes.

Pour chaque classe, vous identifiez ensuite les informations � enregistrer et leur type (texte, nombre...). => Vous obtenez ainsi un diagramme de classes avec leurs attributs.

Vous cr�ez le mod�le physique de donn�es � partir du diagramme de classes en :
* cr�ant une table pour chaque classe ;
* cr�ant, dans chaque table, une colonne pour chaque attribut de la classe correspondante.

## Nommage en UML
* Pour le nom des classes :
	* au singulier
	* avec des lettres non accentu�es
	* commen�ant par une majuscule
	* utilisant Pascal Case (chaque mot commence avec une majuscule)
	* Ex : PierrePrecieuse

* Pour les attributs :
	* au singulier
	* avec des lettres non accentu�es
	* commen�ant par une minuscule
	* utilisant Camel Case (chaque mot commence avec une majuscule sauf le premier)
	* Ex : couleurYeux

* Dans le MPD :
	* Pour le nom des tables et des attributs :
	* au singulier
	* avec des lettres non accentu�es
	* en minuscules
	* utilisant Underscore Case (_)
	* Ex : pierre_precieuse, couleur_yeux


## Relations entre entit�s
NB: on parle d'association entre classes en UML, en AOO il s'agit en fait d'associations entre objets, entre instances de ces classes.

En UML, la relation entre deux classes s'appelle une association.

Les multiplicit�s servent � apposer des contraintes num�riques sur l'association, ou plus pr�cis�ment, combien d'instances d'une classe peuvent �tre li�es � une instance de la classe de l'autre c�t� de l'association. En d'autres termes, elles bornent les cardinalit�s des instances li�es entre elles.


```
Classe A Ax/Ay	______	Bx/By Classe B

Ax/Ay Combien de A **POUR 1 B**
Bx/By Combien de B **POUR 1 A**

```

Il est important de noter que les multiplicit�s imposent des limites de cardinalit�s � un **instant t**.

**Il n'y a pas de notion d'historique dans les associations.**

* Exemple: Musicien / Groupe
Classe Musicien 2/10 _____CONSTITUER_______ 0/5 Classe Groupe

Au min 2, au max 10 musiciens POUR UN GROUPE
Au min 0, au max 5 groupes POUR UN MUSICIEN


## CATEGORIES D'ASSOCIATIONS
Les associations sont class�es en 3 cat�gories, en fonction des multiplicit�s appos�es sur celles-ci.
* ONE TO ONE
* ONE TO MANY
* MANY TO MANY

## TRADUCTION EN UN MPD
Traduire les associations entre classes (UML) dans un mod�le relationnel.

On le sait, une cl� primaire (PK) sert d'identifiant pour chaque n-uplet ou tuple.

� quoi va bien servir cet identifiant ?

Avant de faire un lien entre les tuples de diff�rentes tables (ou instances de classes), il faut pouvoir les identifier de mani�re unique et certaine.

**C'est ce que fait la cl� primaire.**

Et c'est cette cl� qui va servir de r�f�rence pour relier les tuples de la table � ceux d'une autre table !

Le principe g�n�ral: cr�er un attribut qui contient une r�f�rence vers le tuple li�.

**C'est la cl� �trang�re.**
La valeur de cet attribut est toujours la valeur de la cl� primaire du tuple li�.


### Traduction ONE TO ONE : 
choix possible de la table o� d�clarer la cl� �trang�re

    (voiture 1 ______ 0/1 conducteur)

Soit dans la table voiture (plus �vident, une voiture accueille un conducteur)

Soit dans la table conducteur (moins intuitif)

### Traduction ONE TO MANY: 
choix impossible.

    (journal 1 ________  0/* article)

La cl� �trang�re est un forc�ment attribut de la table article.

### Traduction MANY TO MANY:
il n'est plus possible de faire ce lien d'une table � l'autre.

    (musicien 1/* _________ * groupe)

La solution consiste � cr�er une table ad hoc, mat�rialisant les liens multiples, en cr�ant une **CLE PRIMAIRE COMPOSEE** des cl�s �trang�res pointant vers les tables musicien et groupe

```
	musicien             __________         composition                  __________       groupe
    _id: INTEGER [PK]                     musicien_id: INTEGER [PK, FK]                   _id: INTEGER [PK]
     prenom: VARCHAR                       groupe_id: INTEGER [PK, FK]			    nom : VARCHAR
       nom: VARCHAR

```

## LES CLASSES D'ASSOCIATION 

Au niveau du mod�le conceptuel, lorsque l'association est MANY TO MANY, il arrive qu'on cr�e une classe d'association, rendant possible l'ajout d'attribut propre � cette association.

Imaginons l'association repr�sentant les concerts donn�s par un groupe de musique dans des lieux de spectacle. 

A chaque fois que j'ai un lieu entre un Groupe et un Lieu, cela donne lieu de repr�senter un Concert. 

En cr�ant la classe d'association Concert, je peux ajouter, par exemple, un attribut date, qui sp�cifie la date du concert.

```
	
	Groupe  * _______________________  * Lieu
      nom: String	     |               nom : String
			     |               ville: String
			  Concert
			 date: Date

```

Traduction en MPD: une CLASSE D'ASSOCIATION donne lieu � une TABLE de m�me nom, avec une CLE PRIMAIRE COMPOSEE, et les attributs de cette classe.

```

	groupe 		    __________         concert			   __________       lieu
    _id: INTEGER [PK]                     groupe_id: INTEGER [PK, FK]                   _id: INTEGER [PK]
      nom: VARCHAR		           lieu_id: INTEGER [PK, FK]			  nom : VARCHAR
					       date: DATE			         ville: VARCHAR

```

Il y a de nombreux cas o� les classes d'association sont utiles, par exemple enregistrer le num�ro de si�ge dans une relation Passager/Vol, etc.

