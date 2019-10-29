Rappel HEXA
2 lettres ou chiffres = 1 octet


* une norme associant à **tout caractère visuel** un nombre (le point de code) et une dénomination uniques. 

* La norme ASCII et les normes ISO8859 font la même chose, en retenant une étendue de caractères moins importante.
**ASCII was the first character encoding standard (also called character set or charset).**

ASCII utilise comme point de code un nombre binaire de 7 chiffres, donc 2exp7 "points de code" (de 0 à 127), les ISO8859 utilisent un nombre binaire de 8 chiffres donc 2exp8 points de code (de 0 à 255).

Unicode utilise un nombre binaire à 21 chiffres, soit 2 097 152 points de code. Il parvient ainsi à décrire UCS (Universal Character Set).



* Dans chacune de ces normes, chaque "point de code" doit encore être encodé.

Pour ASCII ou ISO8859, un point de code est facilement représenté par un octet (un nombre de 7 bits ou de 8 bits rentrent dans un octet). Le type associé, en C, est le char (lui aussi codé sur 1 octet).


Pour l'Unicode, on emploiera soit l'UTF32, consistant à exprimer le point de code (de 21bits) par un mot de 32bits (4 bytes souvent représentés ainsi 0000001cb). Le type de l'encodage est un entier 32 bits. (depuis C11 on dispose du type char32_t). 

On emploiera aussi des encodages optant pour un type plus petit en taille que 21 bits. L'UTF16 et l'UTF8 emploient ainsi des entiers de 16 et de 8 bits. 