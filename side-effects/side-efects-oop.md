## Les effets de bords dans la programmation orienté objet
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

Dans cet exemple, le contenu de l'attribut `content` est modifié par les méthodes `addFrom` et `addCommand` et lu par la méthode `render`.  Le comportement de la méthode `render` sera donc lourdement impacté par les méthodes précédentes et le sera encore plus si la classe est héritée par des classes modifiant de nouveau l'attribut. De plus en cas d'utilisation dans des processus parallèles, il se peut que les méthodes "addFrom" et "addCommand" soient appelées en même temps ce qui rendrait imprévisible leur comportement.


Dans [[It's probably time to stop recommending Clean Code]], l'auteur écrit en réponse à un code similaire écrit par <ins>Robert C. Martin</ins>, l'auteur de **Clean Architecture** :

> At this point you might reason that maybe Martin's definition of "side effect" doesn't include member variables of the object whose method we just called. If we take this definition, then the five member variables [...] are implicitly passed to _every_ private method call, and they are considered fair game; any private method is free to do anything it likes to any of these variables.

Il ajoute ensuite une citation de <ins>Robert C. Martin</ins> 

> Side effects are lies. Your function promises to do one thing, but it also does other hidden things. **Sometimes it will make unexpected changes to the variables of its own class.** Sometimes it will make them to the parameters passed into the function or to system globals. In either case they are devious and damaging mistruths that often result in strange temporal couplings and order dependencies.

Il existe donc une dualité concernant les attributs privés d'un objet. D'un côté certains considèrent qu'ils peuvent être modifiés et d'autres au contraire considèrent qu'ils doivent être constant et que toute modification devrait entraîner une modification de l'objet