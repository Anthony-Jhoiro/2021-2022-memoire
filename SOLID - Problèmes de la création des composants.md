## Problèmes de la création des composants

Même si tous ces composants sont développés de façon isolés et respectent tous les concepts SOLID, un composant central devra quand même connaitre les autres afin de les initialiser. Ce composant est usuellement appelé `Main`, il a pour charge de créer, coordonner et oversees les autres (définition par Martin (Clean Architecture p232)).

La complexité du composant `Main` est donc très élevée et ne peut donc pas respecter les principes SOLID. Pour remédier à cela, Martin écrit :
> It is in this `Main` component that dependencies should be injected by a Dependency Injection framework. Once they are injected into `Main`, `Main` should distribute those dependencies normally, without using the framework.
*Clean Architecture p232*

D'après Clean Architecture de Robert C Martin, tous les composants doivent être injecté dans le composant "Main" qui a pour charge de les redistribuer. Ce composant utilise alors un framework d'injection de composant. Il en existe dans pratiquement tous les langages de programmation et permettent à chaque composant d'être créé avec ses dépendances sans en connaitre l'exacte implémentation. 


#TODO problème de la création de composant


L'utilisation d'un framework d'injection de dépendance permet de simplifier grandement cette partie du code mais n'est pas applicable dans tous les paradigmes. Elle est même grandement restreinte à la programmation orientée objet. Mais qu'en est il des autres paradigmes ? 

#TODO Trouver d'autres possibilités pours les autres paradigmes
#TOREAD [Implémentation de la DI en C](https://devmethodologies.blogspot.com/2012/07/dependency-injection.html)
