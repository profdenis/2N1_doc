# 🔸1🔸Programmation OO

La programmation orientée objet (POO) est une approche de programmation qui organise le code autour du concept d'objets,
qui sont des instances de classes.

## Classes et Objets

Une **classe** est un modèle qui définit la structure et le comportement d'un type d'objet. Elle contient des
attributs (données) et des méthodes (comportements). Par exemple, la classe `String` en Java définit la structure d'une
chaîne de caractères.

Un **objet** est une instance concrète d'une classe. Par exemple :

```java
String message = new String("Bonjour");
```

Dans cet exemple :

- `String` est la classe
- `message` est une variable qui référence l'objet
- `new String("Bonjour")` crée une nouvelle instance

## Constructeurs

Un **constructeur** est une méthode spéciale qui est appelée lors de la création d'un objet avec le mot-clé `new`. Il
porte le même nom que la classe et initialise les attributs de l'objet.

## Exemple Pratique avec la Classe Personne

Voici un exemple simple d'une classe `Personne` :

```java
public class Personne {
    // Attributs
    public String nom;
    public String prenom;
    public int age;

    // Constructeur
    public Personne(String nom, String prenom, int age) {
        this.nom = nom;
        this.prenom = prenom;
        this.age = age;
    }

    // Méthode supplémentaire
    public void sePresenter() {
        System.out.println("Je m'appelle " + prenom + " " + nom +
                " et j'ai " + age + " ans");
    }
}
```

Pour utiliser cette classe, on peut créer des instances comme ceci :

```java
Personne etudiant = new Personne("Dupont", "Jean", 20);
etudiant.sePresenter();
```

Dans cet exemple :

- Les attributs `nom`, `prenom` et `age` sont publics (nous verrons plus tard pourquoi c'est généralement déconseillé)
- Le constructeur prend trois paramètres pour initialiser les attributs
- La méthode `sePresenter()` affiche les informations de la personne

Cette introduction aux concepts de base de la POO permet de comprendre comment les classes servent de modèles pour créer
des objets qui contiennent à la fois des données (attributs) et des comportements (méthodes).



-------

!!! note "Note"
    Page rédigée en partie avec l'aide d'un assistant IA, principalement à l'aide de Perplexity AI, avec le *LLM* 
    **Claude 3.5 Sonnet**. L'IA a été utilisée pour générer des explications, des exemples et/ou des suggestions de 
    structure. Toutes les informations ont été vérifiées, éditées et complétées par l'auteur.
