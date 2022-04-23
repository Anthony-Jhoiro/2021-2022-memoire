## Principes de base

### SRP : Single Responsibility Principle

Le principe de responsabilité unique impose qu'une entité (une fonction, une classe, un composant, un package...) n'ait qu'une seule responsabilité ce qui signifie qu'il ne doit y a voir qu'une seule raison pour laquelle cette entité serait modifiée. 

Prenons un composant qui manipule les utilisateurs d'une application. Ce composant ne doit être modifié que si la stratégie de gestion des utilisateurs est modifiée. 

### OCP : Open-Closed Principle
> A software artifact should be open for extension but closed for modification.
*Bertrand Meyer. __Object Oriented Software Construction__, Prentice Hall, 1988, p.23*

Ce principe impose q'un ajout de fonctionnalité ne doit pas modifier le code existant d'un projet mais doit uniquement en ajouter. Ainsi, on réduit au minimum le risque de changer le comportement d'une entité qui utiliserait le code que l'on modifie. 

#TODO Better explanation for OCP for OOP
En programmation orienté objet, ce principe renvoie directement au polymorphisme de l'objet. 

En programmation fonctionnelle, ce principe peut aussi s'appliquer en utilisant la composition de fonction et les "high-order functions" (fonction pouvant prenant une fonction comme paramètre et / ou retournant une fonction).



### LSP : Liskov Substitution Principle
#TODO Liskov Substitution Principle
### ISP : Interface Segregation Principle
Ce principe énonce qu'il est préférable d'utiliser plusieurs petites interfaces plutôt qu'une grande. Ces petites interfaces sont dites "client-specific" ce qui signifie qu'elles ne sont faites que pour un seul client. Ce qui implique en toute logique que le client définit les interfaces dont il a besoin. 

En programmation orienté objet, il est courant de pouvoir implémenter plusieurs interface dans une  même classe. Cependant le concept d'interface n'est pas propre à la programmation orienté objet et ce concept existe très bien en programmation fonctionnelle ou en programmation procédurale. 

### DIP : Dependency Inversion Principle
Le principe d'inversion de dépendance dit qu'une entité ne doit jamais dépendre directement d'une autre mais doit toujours passer par une forme d'abstraction. Pour schématiser, prenons 

![[Cours/M1/S2/Mémoire/DIP-principle-example.excalidraw]]

Dans cet exemple, nous avons deux composants : "Users Service" et "Location Service". "Location Service" a besoin des données des utilisateurs pour fonctionner, il va donc utiliser le "Users Service". Pour respecter le principe d'inversion de dépendance, le Location Service doit passer par une interface ici appelée "Users Management interface" implémentée par le User Service.  Cette interface sert de contrat et permet de rendre abstrait la logique du "Users Service". 

Ce principe a un grand intérêt car il est très résistant au changement. Mettons que la gestion des utilisateurs soit déportée dans une autre application afin de rendre la gestion des utilisateurs globale au sein d'une entreprise. La logique du "Users Service" dans notre application de départ changerait alors complètement. Il faudrait donc implémenter une nouvelle entité qui serait chargée de communiquer avec 

#TODO Dependency Inversion Principle