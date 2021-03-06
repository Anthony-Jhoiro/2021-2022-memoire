# Qu'est ce qu'un niveau d'abstraction ?

Aujourd’hui, il est important qu’un programme puisse s’adapter aux différents changements qui proviendront. Une des clefs de cette adaptation est l’abstraction. On définit souvent l’abstraction en parlant de couche ou de niveau d’abstraction (ou en anglais “abstraction layer”). Une couche d’abstraction permet à deux entités de communiquer entre elles sans avoir d’informations sur leur implémentation. Souvent ce principe passe par un système d’interface ou équivalents ne définissant que la structure attendue. 

Prenons un composant d'une application s'occupant de la gestion des utilisateurs et un autre composant qui lui s'occupe du stockage des utilisateur dans une base de donnée.

![[Cours/M1/S2/Mémoire/abstraction/abstraction-example1.excalidraw]]

Ici, le composant "UserManager" a besoin du composant "UserPostgresStorage" afin de stocker et récupérer les informations de l'utilisateur. Le problème de cette approche est qu'en cas de modification du mode stockage, dû par exemple à un changement de base de donnée ou d'externalisation des données, le composant "UserPostgresStorage" ne sera peut être plus utilisé. Dans ce cas le "UserManager" devra lui aussi changer pour s'adapter au nouveau mode de stockage. 

Dans notre exemple, il n'y a que deux composants donc le changement sera rapide mais que se passe t'il quand nous en avons 10, 100 ou 500 ? Et bien ce genre de modification risque d'avoir un énorme impacte ! Afin d'éviter ce problème, nous pouvons placer une interface entre nos deux composants. 

![[Cours/M1/S2/Mémoire/abstraction/abstraction-example1-solution.excalidraw]]

Dans la figure ci-dessus, nous avons ajouté l'interface "UserStorage" à notre model. Cette interface est un "contrat" entre nos deux composants. "UserManager" *annonce* qu'elle a besoin d'un composant qui **implémente** cette "UserStorage" et c'est ce que fait "UserPostgresStorage" en implémentant les méthodes définies dans "UserStorage". Maintenant si nous changeons le mode de stockage de nos utilisateurs, nous pouvons simplement créer un nouveau composant qui implémentera l'interface et le composant "UserManager" n'aura pas besoin de savoir comment les utilisateurs sont stockés.

La notion d'interface et d'abstraction est souvent présentée comme une notion phare de la programmation orienté objet cependant elle n'y est pas restreinte. Si on prend un langage comme le C, les fichiers headers (avec l'extension .h) peuvent tout à fait ajouter une couche d'abstraction. Conventionnellement ces fichiers ne contiennent que les déclarations des fonctions et non leur définition. Quand un de ces fichiers est importé, il n'est pas nécessaire de savoir comment ces fonctions sont implémentées. C'est alors le rôle du compilateur de dire quel fichier implémentera les fonction du header et quelles implémentations seront donc utilisées.
