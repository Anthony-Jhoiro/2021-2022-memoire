# Introduction

Depuis les débuts de l'informatique modernes, les évolutions en terme de technologies et de bonnes pratiques n'ont cessé de s'accélérer de façon exponentielles. Dans ce contexte en constante évolution, il est en parallèle devenu important que les application gagne en fonctionnalités. Le problème arrivé rapidement est que l'ajout des fonctionnalité d'une application est souvent complexe car une nouvelle fonctionnalité peut changer (directement ou indirectement) le comportement des autres créant ainsi des applications de plus en plus complexes à étendre et la plus simple des fonctionnalité qui aurait pu prendre quelques heures en début de projet fini par prendre plusieurs semaines à développer dans une application avec un plus fort historique. 

Voyez ici la construction d'application comme une tour dont la construction ne sera jamais terminée. Vous ne savez pas s'il faudra qu'elle grandisse en largeur ou en hauteur, sur combien d'étages, quel type de fenêtre... Il est alors nécessaire d'établir une solution dans laquelle il sera simple d'ajouter ou de modifier les éléments sans voir tout s'effondrer et devoir recommencer à zéro. Ainsi vous pourrez facilement vous **adapter** aux nouveaux changements.

Avant de nous intéresser à comment rendre notre code plus adaptable aux modifications, il est important de préciser la nature de notre code.

## Langage de programmation
Un langae de programmation est un ensemble de règles et de symboles permettant de formuler des algorithe et de produire des programmes. (https://www.linternaute.fr/dictionnaire/fr/definition/langage-de-programmation)

## Paradigme de programmation
Nous comptons aujourd'hui plusieurs méthodes de programmation principales que l'on appelle paradigme. Ces paradigmes sont utilisés par des langages ou frameworks et permettent de garder une cohérence dans la logique d'un langage à un autre. Certain langages sont dit multi-paradigm, ce qui signifie que l'on peut les utiliser avec un ou plusieurs paradigmes comme le Javascript ou le Python. Nous dénombrons aujourd'hui trois paradigmes de développement. 

### Programmation procédurale

Premièrement la **programmation procédurale**, comme décrite dans cet article https://www.techno-science.net/definition/11446.html est un paradigme de développement contré sur l’utilisation des procédures. Une procédure est une suite d'instruction ordonnée,"incluant d'autres procédures, voire la procédure elle-même" (https://www.techno-science.net/definition/11446.html ), nous parlons alors de récursivité. Nous retrouvons ce paradigme dans des langages comme le C ou le Go.

### Programmation orientée objet

Ensuite nous avons la **programmation orienté objet** souvent abrégée en OOP (Object-Oriented Programming) qui place l'objet au centre. Un objet est une brique logique représentant "un concept, une idée ou toute entité du monde physique, comme une voiture, une personne ou encore une page d'un livre." (https://www.techno-science.net/definition/5393.html). Nous retrouvons ce paradigme entre autre en Java ou en Dart.

### Programmation fonctionnelle

Enfin il existe le paradigme de **programmation fonctionnelle**, décrit entre autre dans cet article https://www.techno-science.net/glossaire-definition/Programmation-fonctionnelle.html, dans lequel l'élément central est la fonction qui ici reprend la logique d'une des fonctions mathématique . Il impose le principe d'immutabilité et rejette les changements d'état. La programmation fonctionnelle a été imaginé avant même le début de la programmation elle même et est fortement basée par le lambda-calcul inventé par Alonzo Church dans les années 1930 comme décrit par Robert C. Martin dans le chapitre 6 de Clean Architecture. Nous retrouvons ce paradigme dans des langages comme Clojure ou Haskell.



