https://marekdec.wordpress.com/2011/12/06/explicit-interface-per-class-antipattern/

Bien que se basant sur le framework Java EE, cet article s'applique à n'importe quel langage ou paradigme. L'auteur développe son point de vue sur l'utilisation d'une interface par classe. 

=> problèmes remontes du début de java (début de l'injection de dépendance)
=> en java chaque classe implemente par défaut une interface.

=> On retourne au problème de la comprehension du role de l'interface. L'interface est un contrat qui doit être définit par les classes l'utilisant. Le problème de l'interface explicite rendant ceci complexe dans des langages comme le Java, les développeurs ont commencés à les utiliser dans l'autre sens et donnant à chaque classe une interface ce qui n'est pas une inver.