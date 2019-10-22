# Langage algo, une introduction



#### Principes
* �crire en majuscules
* commencer par `DEBUT`
* terminer par `FIN`
* d�clarer des variables typ�es `ENTIER I, J` `CHAINE S`, `ENTIER T[ 10]`
* `AFFICHER` et `SAISIR` au lieu de "�crire" et "lire".
* fermer les blocs, par exemple `SI...FINSI` ou `POUR...FINPOUR`

#### Le symbole d'affectation `<-`
```
I <- 0

J <- I / 3

A <- "Hello"
```

#### Les 6 op�rateurs de comparaison
```
< et >
<= et >=
= et != (ou <>)
```

#### Les diverses structures de contr�le 
```
SI (I>0) ALORS ... (SINON) FINSI
```

```
TANT QUE I<=100 ... FIN TANT QUE
```

```
FAIRE ... JUSQU'A (I>100)
```

```
POUR I ALLANT DE 1 A 100 ... FINPOUR
POUR I ALLANT DE 1 A 100 PAS 2 ... FINPOUR
POUR (I<-1 ; I<100 ; I<- I+1) ... FINPOUR
// et dans le cas d'une String ou d'un tableau
POUR I ALLANT DE 0 A LONGUEUR( A) ... FINPOUR
```
