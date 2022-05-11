---
articles:
  - https://medium.com/dailyjs/the-state-of-immutability-169d2cd11310
---

## Une solution pour éviter les effets de bord : l'immutabilité

Le principe d'immutabilité définit que toutes les entités (variables, fonctions, ...) doivent se comporter de façon immutable. Ce qui veut dire que pour modifier ces entités, il faut en faire une copie. 

Comme expliqué dans l'article "The State of Immutability de Maciej Sikora", l'immutabilité permet de supprimer les effets de bords dues aux mutations des valeurs ou des structures de données. Il est présenté deux approches très semblables, PLOP (PLace Oriented Programming) et VOP (Value Oriented Programming). PLOP pro

L'immutabilité est très utilisé dans la programmation fonctionnelle et est simple à utiliser dans un concept de programmation procédural cependant, son approche peut paraître déroutante en programmation orienté objet. 

Prenons le type `String` en Java. 

Nous apprenons en `C` qu'une chaîne de caractère, ou string, est un tableau de caractère de taille fixe. Cependant en Java ce code est totalement valide :

```java
String sentence = "Hello ";
sentence += "World !";
```

Est ce que le tableau a changé de taille ? Non. Un nouveau tableau a été créé pour contenir la nouvelle valeur de la chaîne de caractère. Le principe d'immutabilité est donc respecté car la chaîne de caractère de départ n'a pas été modifié. Un exemple un peu plus concret :

```java
public class Main {  
    public static void change(String sentence) {  
        sentence.toUpperCase();  
	}  
	public static void main(String[] args) {  
	    String a = "hello";  
	    change(a);  
	    System.out.println(a);  // Output : hello
	}
}
```

Ici le programme n'affiche que "hello" et non pas "HELLO" car une nouvelle chaîne de caractère a bien été crée dans la fonction `change`.

En reprenant le code de notre classe `Dockerfile` et en appliquant le principe d'immutabilité seul, nous obtenons ceci.

```java
class Dockerfile {  
	public static String addFrom(String content, String from) {  
		return content + "FROM " + from + "\n";  
	}  
	public static  String addCommand(String content, String command) {  
		return content + "CMD " + command + "\n";  
	}  
	public static String render(String content) {  
		return content;  
	}
}
```

Ou bien en gardant une approche objet
```java
class Dockerfile {  
	private final String content;
	
	public Dockerfile(String content) {
		this.content = content;
	}
	
	public Dockerfile addFrom(String from) {  
		return new Dockerfile(content + "FROM " + from + "\n");  
	}  
	public Dockerfile addCommand(String command) {  
		return new Dockerfile(content + "CMD " + command + "\n");  
	}  
	public Dockerfile render(String content) {  
		return content;  
	}
}
```

