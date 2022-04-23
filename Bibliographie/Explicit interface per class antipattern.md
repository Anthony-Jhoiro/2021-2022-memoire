https://marekdec.wordpress.com/2011/12/06/explicit-interface-per-class-antipattern/

Bien que se basant sur le framework Java EE, cet article s'applique à n'importe quel langage ou paradigme. L'auteur développe son point de vue sur l'utilisation d'une interface par classe. 

=> problèmes remontes du début de java (début de l'injection de dépendance)
=> en java chaque classe implemente par défaut une interface.

=> On retourne au problème de la comprehension du role de l'interface. L'interface est un contrat qui doit être définit par les classes l'utilisant. Le problème de l'interface explicite rendant ceci complexe dans des langages comme le Java, les développeurs ont commencés à les utiliser dans l'autre sens et donnant à chaque classe une interface ce qui pourrait sembler être une version du principe d'inversion de dépendance (DIP) mais n'en est pas. En effet si l'interface a pour but de refléter les données de l'entité, alors la dépendance ne va pas de la classe à l'interface mais de l'interface à la classe. 
![[Cours/M1/S2/Mémoire/interface-for-class-antipattern.excalidraw]]

Pour reprendre le schéma utilisé pour parler du DIP, on constate que l'inversion n'est pas faite et que l'interface n'a pas d'utilité.

=> L'auteur n'exlu pas l'utilisation des interfaces maos 