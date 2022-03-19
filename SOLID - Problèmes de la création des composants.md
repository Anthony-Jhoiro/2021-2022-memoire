## Problèmes de la création des composants
#todo Problèmes de la création des composants

Même si tous ces composants sont développés de façon isolés et respectent tous les concepts SOLID, un composant central devra quand même connaitre les autres afin de les initialiser. Ce composant est usuellement appelé `Main`, il a pour charge de créer, coordonner et oversees les autres (définition par Martin (Clean Architecture p232)).

### Concept de Martin
=> Tous les composants doivent être injectés dans Main puis Main a pour charge de les redistribuer sans framework
=> Main est le composant le plus "crade" car il doit connaitre l’existence de tous les autres composants utilisés dan l'application et ne peut donc pas respecter les principes SOLID.

La complexité du composant `Main` est donc très élevée. Pour remédier à cela, Martin écrit :
> It is in this `Main` component that dependencies should be injected by a Dependency Injection framework. Once they are injected into `Main`, `Main` should distribute those dependencies normally, without using the framework.
*Clean Architecture p232*

L'utilisation d'un framework d'injection de dépendance permet de simplifier grandement cette partie du code mais n'est pas applicable dans tous les paradigmes. Elle est même grandement restreinte à la programmation orientée objet. Mais qu'en est il des autres paradigmes ? 

#TODO Trouver d'autres possibilités pours les autres paradigmes
#TOREAD [Implémentation de la DI en C](https://devmethodologies.blogspot.com/2012/07/dependency-injection.html)
