Rappel HEXA
2 lettres ou chiffres = 1 octet


* une norme associant � **tout caract�re visuel** un nombre (le point de code) et une d�nomination uniques. 

* La norme ASCII et les normes ISO8859 font la m�me chose, en retenant une �tendue de caract�res moins importante.
**ASCII was the first character encoding standard (also called character set or charset).**

ASCII utilise comme point de code un nombre binaire de 7 chiffres, donc 2exp7 "points de code" (de 0 � 127), les ISO8859 utilisent un nombre binaire de 8 chiffres donc 2exp8 points de code (de 0 � 255).

Unicode utilise un nombre binaire � 21 chiffres, soit 2 097 152 points de code. Il parvient ainsi � d�crire UCS (Universal Character Set).



* Dans chacune de ces normes, chaque "point de code" doit encore �tre encod�.

Pour ASCII ou ISO8859, un point de code est facilement repr�sent� par un octet (un nombre de 7 bits ou de 8 bits rentrent dans un octet). Le type associ�, en C, est le char (lui aussi cod� sur 1 octet).


Pour l'Unicode, on emploiera soit l'UTF32, consistant � exprimer le point de code (de 21bits) par un mot de 32bits (4 bytes souvent repr�sent�s ainsi 0000001cb). Le type de l'encodage est un entier 32 bits. (depuis C11 on dispose du type char32_t). 

On emploiera aussi des encodages optant pour un type plus petit en taille que 21 bits. L'UTF16 et l'UTF8 emploient ainsi des entiers de 16 et de 8 bits. 