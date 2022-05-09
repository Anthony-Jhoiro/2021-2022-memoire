## Les effets de bord
Dans une fonction, on parle d'effet de bord l’interaction avec des entités externes au contexte de la fonction. 

Attention: Selon les sources, on ne parle pas forcément d'effet de bord le fait d'utiliser des éléments externes en lecture seule.
#todo : présenter un article pour et un article contre

Exemple :
```go
//...

var a = 0

func addFive() {
	a += 5
}

func  main() {
	fct()
	log.Printf("%d\n", a)
}

```

Ici la fonction `fct` a un effet de bord car elle modifie la variable a qui se situe en dehors de sa définition. Une solution pour éviter ce comportement est :

```go
//...

func addFive(a int) int {
	return a + 5
}

func  main() {
	var a = 0
	a = fct(a)
	log.Printf("%d\n", a)
}

```

#TODO Vérifier que l'article est bien

Dans cet exemple, la fonction "addFive" ne présente aucun effet de bord car les seules éléments utilisés sont dans son scope directe. Nous pouvons alors parler de fonction pure comme définit dans cette article [https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-pure-function-d1c076bec976](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-pure-function-d1c076bec976) . 



### Applications dans les classes (POO)
La question des effets de bord se pose dan l'utilisation de la programmation orientée objet. 

Prenons une classe `Utilisateur` avec deux attributs privés `nom` et `age`. Si dans cette même classe nous avons une méthode `incrementerAge` ne prenant aucun paramètre et ajoutant 1 à l'âge de l'utilisateur. En Java, cela pourrait donner :
```java
class Utilisateur {
	private String nom;
	private int age;

	public void incrementerAge() {
		this.age += 1;
	}
}
```

*Cette situation présente-t-elle un effet de bord ? *

Une nouvelle fois, il y a deux possibilités. Soit on considère que l'objet avec ses attributs et méthodes ne forment q'une seule et même entité donc on exclus les effets de bords, tant que rien n'est modifié en dehors du scope de la classe. Soit on considère que c'est bien un effet de bord comme l'attribut age est définit en dehors de la méthode. 

Le problème de la deuxième vision est que chaque "setter", même au plus simple devient un effet de bord, ce qui s'oppose à une convention fondamentale de la Programmation orientée objet qui est que chaque attribut d'une fonction ne doit être accédé et modifié que par l'intermédiaire de méthode. 

Cependant, cette approche est plus pertinente dans d'autres cas.

```java
class Dockerfile {
	private StringBuilder content;
	
	public Dockerfile() {
		content  = new StringBuilder("");
	}

	public void addFrom(String from) {
		content
			.append("FROM ")
			.append(from)
			.append("\n");		
	}
	
	public void addCommand(String command) {
		content
			.append("CMD ")
			.append(command)
			.append("\n");		
	}

	public String render() {
		return content.toString();
	}
}
```

Dans cet exemple, le contenu de l'attribut `content` est modifié par les méthodes `addFrom` et `addCommand` et lu par la méthode `render`.  Le comportement de la méthode `render` sera donc lourdement impacté par les méthodes précédentes et le sera encore plus si la classe est héritée par des classes modifiant de nouveau l'attribut.

#TODO Trouver un moyen d'inclure la suite

Dans [[It's probably time to stop recommending Clean Code]], l'auteur écrit en réponse à un code similaire écrit par <ins>Robert C. Martin</ins>, l'auteur de **Clean Code** :

> At this point you might reason that maybe Martin's definition of "side effect" doesn't include member variables of the object whose method we just called. If we take this definition, then the five member variables [...] are implicitly passed to _every_ private method call, and they are considered fair game; any private method is free to do anything it likes to any of these variables.

Il ajoute ensuite une citation de <ins>Robert C. Martin</ins> 

> Side effects are lies. Your function promises to do one thing, but it also does other hidden things. **Sometimes it will make unexpected changes to the variables of its own class.** Sometimes it will make them to the parameters passed into the function or to system globals. In either case they are devious and damaging mistruths that often result in strange temporal couplings and order dependencies.


### Solutions envisageables

#### Principe d'immutabilité
Le principe d'immutabilité définit que tous les éléments (variables, fonctions, ...) doivent se comporter de façon immutable. Ce qui veut dire que pour modifier ces éléments, il faut en faire une copie. Ce principe est très utilisé dans la programmation fonctionnelle et est simple à utiliser dans un concept de programmation procédural cependant, son approche peut paraître déroutante en programmation orienté objet. 

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
  
 System.out.println(a);  // Log : hello
 }}
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