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
Ce principe énonce qu'il est préférable d'utiliser plusieurs petites interfaces plutôt qu'une grande. Ces petites interfaces sont dites "client-specific" ce qui signifie qu'elles ne sont faites que   composant implémentant  les interfaces d'un projet soient "client-specific" ce qui signifie qu'un composant ne doit pas proposer 


#TODO Interface Segregation Principle
### DIP : Dependency Inversion Principle
#TODO Dependency Inversion Principle