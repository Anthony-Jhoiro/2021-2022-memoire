# Qu'est ce qu'un niveau d'abstraction ?

Aujourd’hui, il est important qu’un programme puisse s’adapter aux différents changements qui proviendront. Une des clefs de cette adaptation est l’abstraction. On définit souvent l’abstraction en parlant de couche ou de niveau d’abstraction (ou en anglais “abstraction layer”). Une couche d’abstraction permet à deux entités de communiquer entre elles sans avoir d’informations sur leur implémentation. Souvent ce principe passe par un système d’interface ou équivalents ne définissant que la structure attendue. 

Prenons un composant d'une application s'occupant de la gestion des utilisateurs et un autre composant qui lui s'occupe du stockage des utilisateur dans une base de donnée.

![[Cours/M1/S2/Mémoire/abstraction/abstraction-example1.excalidraw]]

Ici, le composant UserManager a besoin du composant UserPostgresStorage afin de stocker et récupérer les informations de l'utilisateur. Le problème de cette approche est qu'en cas de modification du mode stockage, dû par exemple à un changement de base de donnée ou d'externalisation des données, le composant UserPostgresStorage ne sera 


Le niveau d’abstraction est présent ç différentes échelles en informatique. Bien sûr, on le retrouve dans les architectures de code mais auŝsi dans les architectures comportant plusirus applications ou les architectures réseaux. En effet,nous pouvons 
