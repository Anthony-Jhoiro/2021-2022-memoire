# It's probably time to stop recommending Clean Code

> 2020-06-28 by qntm
> https://qntm.org/clean

## Notes

### About functions

#### Agree with
- functions shouldn't have low level and high level tasks
- functions name descriptives, consistent, verb phrases and should be chosen carrefully
- functions do exactly one thing
- avoid output arguments in favor of functions return
- functions must "do" something (queries) or "answer" something (query) but not both
- no functions side effects


il faut nuancer le "one function, one thing"
> provided that we aren't too dogmatic about how we define "one thing", and we understand that in plenty of cases this can be highly impractical.

#### Disagree with

> Martin says that a code file should be readable from top to bottom in a way that a function only usess functions defined above. This is an old practice as todays IDE allows developpers to jump from a function to another with a simple click or a keyboard shortcut depite its location. 


Ensuite il y a un exemple de code en java écrit par Martin selon ses standarts. 

- le nom de la classe n'est pas bonne (phrase verbale)
- imports non standarts
- 13 / 15 méthodes ont des effets de bords => la règles sur les effets de bords ne s'applique pas en POO ?

#### Agree with
> Side effects are lies. Your function promises to do one thing, but it also does other hidden things. **Sometimes it will make unexpected changes to the variables of its own class.** Sometimes it will make them to the parameters passed into the function or to system globals. In either case they are devious and damaging mistruths that often result in strange temporal couplings and order dependencies.

#### L'explication autour de l'analyse de la méthode est vraiment interessante : 

> Let's just look at one private method.
```java
private String render(boolean isSuite) throws Exception {
   this.isSuite = isSuite;
  if (isTestPage())
    includeSetupAndTeardownPages();
  return pageData.getHtml();
}
```
>
So... imagine that someone enters a kitchen, because they want to show you how to make a cup of coffee. As you watch carefully, they flick a switch on the wall. The switch looks like a light switch, but none of the lights in the kitchen turn on or off. Next, they open a cabinet and take down a mug, set it on the worktop, and then tap it twice with a teaspoon. They wait for thirty seconds, and finally they reach behind the refrigerator, where you can't see, and pull out a _different_ mug, this one full of fresh coffee.
>
...What just happened? What was flicking the switch for? Was tapping the empty mug part of the procedure? Where did the coffee come from?
>
> That's what this code is like. Why does `render` have a side effect of setting the value of `this.isSuite`? When is `this.isSuite` read back, in `isTestPage`, in `includeSetupAndTeardownPages`, in both, in neither? If it does get read back, why not just pass `isSuite` in as a Boolean? Or perhaps the caller reads it back?

=> impossible à tester

---
>_Clean Code_ mixes together a disarming combination of strong, timeless advice and advice which is highly questionable or dated or both.

**focus on OOP et valorise les valeurs de SOLID**

Martin a créé 3/5 des principes fondateurs de SOLID

=> pas de programmation fonctionnelle
=> pas de code procédurale

SOLID n'est plus vraiment d'actualité auourd'hui, la popularité et l'adoration baissent avec le temps

=> Le livre se concentre sur l'utilisation du Java mais dans une version outdated Justification :
> This kind of thing is unavoidable — programming books date legendarily poorly. That's part of the reason why _Clean Code_ was a recommended read at one time, and I now think that the pendulum is swinging back in the opposite direction.

### Les tests unitaires
#### D'accord avec
- tests rapides à l'execution
- tests indépendants
- test répétables
- de la même taille que la fonction testée
- beaucoup plus simple que la fonction testée

#### Pas d'accord
- Pour l'auteur, il ne faut pas ajouter de logique métier à part pour les tests unitaires !

---

### TDD loop

Rappel :
- **First Law** You may not write production code until you have written a failing unit test.
- **Second Law** You may not write more of a unit test than is sufficient to fail, and not compiling is failing.
- **Third Law** You may not write more production code than is sufficient to pass the currently failing test.

Pour l'auteur le TDD n'est pas une solution, tester tous les cas possibles demande beaucoup de temps et résulte en la présence d'une multitude de cas impossibles à tester et surtout à des tests innutiles.

---
#### Object and data structures
La définition d'une data structure de Martin diffère de la définition courante. Une datastructure classique  : liste, array, binary tree... mais Pour martin une data structure est un objet avec des attributs publiques là où un objet va mettre à dispositions des méthodes.

---

#### Un autre exemple :
En soit l'exemple montre juste que Martin ne respecte pas ses propres principes dans son code

#TODO : retrouver le contexte de l'exemple


#### Global
Les booleens devraient être utiliser avec beaucoup de précaution car soubvent moins clairs que des enumérations

Le gars est salé quand même :
> If this is the quality of code which this programmer produces — at his own leisure, under ideal circumstances, with none of the pressures of real production software development, _as a teaching example_ — then why should you pay any attention at all to the rest of his book? Or to his other books?


## Résumé
#TODO Trouver le vrai nom de l'auteur

L'objectif de l'article de <ins>Qntm</ins> est très clair dès son titre. L'auteur tente de démontrer les éléments de Clean Architecture ([[Bibliographie/Clean Architecture Martin]]) ne concordant pas à sa vision d'une bonne architecture de code. 

### Les fonctions
Pour commencer il est sujet des fonctions. Les deux auteurs concordent sur des points universels comme les règles de nommage, la nécessité d'écrire autant que possible des fonctions ne faisant q'une seule chose chacune, éviter de modifier les les paramètres au profit de retourner une valeur et la différence entre les fonction de type **Query** qui demande demandent et les fonction de type **Answer** qui répondent au query.

Par la suite, il va montrer son désaccord avec un concept de Martin qui est qu'un fichier de code doit pouvoir être lu de haut en bas avec au fur et à mesure des définitions de fonctions de moins en moins abstraite. Il défend que ce principe est souvent innaplicable et ne s'impose plus avec les éditeurs de code modernes. Une grande majorité des développeurs aujourd'hui utilisent des éditeurs comme VsCode ou IntelliJ qui permettent de passer d'une fonction à l'autre d'un simple clique, peu importe où elle est définie. 

### Les exemples de code
Ensuite l'auteur expose différents exemples de code écrit par <ins>Robert C Martin</ins> en précisant les cas dans lesquels les principes de Clean Architecture ne sont pas bien mis en place.

#TODO Est ce qu'il est pertinent de s'attarder dessus dans le mémoire ?

### Ce qui ne va pas au global dans le livre
Un point mis en avant par <ins>Qntm</ins> qui m'avait aussi dérangé pendant la lecture de Clean Architecture est que l'auteur se concentre sur la programmation orientée objet en laissant de côté les autres paradigmes. C'est un problème car des langages très populaires ne sont pas orientés objet comme le **Go** ou le **Rust**, voire mettent l'objet au second plan come le **Python** ou le **Typescript**. De plus l'auteur met un accent important sur l'utilisation du principe [[SOLID]] qui n'est pas forcément adaptés à nos façon de programmer modernes. 

Certes Robert C Martin a de nombreuses années d'experiences dans le développement mais les technologies (que ce soit les langages ou bien les frameworks) ont grandement évoluées depuis ses débuts. La problématique est que les 




