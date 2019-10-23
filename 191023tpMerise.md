# MERISE

#### Comprendre la notion de clé dans une SGBD
* deux types de clés: primaire ou étrangère.

La clé primaire (composée d'un ou plusieurs champs de la table) permet d'identifier de façon unique chaque entrée de la table. Par csq, la valeur du champ "clé primaire" est toujours unique, dans une table donnée.

Une clé étrangère permet d'établir, pour une entrée unique donnée, une relation avec une entrée unique d'une autre table. Car elle a pour valeur celle du champ "clé primaire" d'une autre table. **Contrairement à une clé primaire", une même valeur, dans une table donnée, du champ "clé étrangère" peut être présente dans plusieurs entrées de cette table. Car la clé étrangère ne sert plus à identifier, elle sert à relier.

Cependant, qu'une clé étrangère soit aussi primaire, cela est tout à fait possible.
De même que plusieurs clés étrangères peuvent former ensemble une clé primaire. Celle-ci est alors constituée du n-uplet de valeurs de ces clés étrangères.

#### L'exemple de la base de données textuelles cf PDF BD-CleRelations.pdf

* Considérons la base constituée de 4 tables : documents, phrases, mots, occurences

La première DOCUMENTS recense des livres(titre, auteur). 
* clé primaire: le champ ENTIER num_doc

La seconde PHRASES des phrases issues de ces livres (phrase explicite)
* clé primaire: le champ ENTIER num_phrase,
* #clé étrangère: le champ doc_source  (sa valeur est donc celle du champ num-doc, clé primaire de DOCUMENTS) 

La troisième MOTS recense les mots issus des diverses phrases de ces livres (mot explicite)
* clé primaire: le champ ENTIER num_mot

La quatrième OCCURENCES recense les occurences dans les phrases des divers mots (pour une phrase donnée, le nombre de fois que le mot apparait)
* clé primaire constituée du couple de champs ENTIERS: les clés étrangères di-dessous
* #clé étrangère 1: le champ phrase (sa valeur est celle du champ num_phrase, clé primaire de PHRASES)
* #clé étrangère 2: le champ mot (sa valeur est celle du champ num_mot, clé primaire de MOTS)

#### Exercice
 
```
Voici le modèle relationnel:

DESTINATION (**codepost,** libelle)
SEJOUR (**numsej,** duree, nbplacemax, codedest#)
CLIENT (**numcli,** nomcli, prenomcli, ruecli, cplcli, villecli, telcli, mailcli)
DEPARTS  (**numsej#,** date-depart, prix)
RESERVATION ( **numcli#, numsej#,** date_res, nb_personnes, tx_remise)

```

Pour une destination, plusieurs séjours (1 à plusieurs)

Pour un séjour, un départ (1 à 1)

Dans la table RESERVATION, plusieurs entrées peuvent avoir le même numcli, plusieurs entrées peuvent avoir le même numsej,mais une entrée ne peut avoir le même couple (numcli, numsej) qu'une autre. 

Ce qui veut dire: un client peut avoir plusieurs reservations. un séjour aussi peut avoir plusieurs réservations. Mais un client, pour un séjour donné, ne peut avoir qu'une réservation (éventuellement pour plusieurs personnes). 
