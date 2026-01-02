# 🔸2🔸Mot-clé `static`

Le mot-clé `static` est un modificateur qui permet de définir des éléments (attributs ou méthodes) qui appartiennent à
la classe elle-même plutôt qu'aux instances de cette classe[1].

## Attributs Statiques

Un attribut statique possède les caractéristiques suivantes :

- Une seule copie de la variable est créée et partagée entre tous les objets de la classe[1]
- Il existe dès que la classe est chargée en mémoire, avant même la création d'instances[2]
- Il est accessible directement par le nom de la classe, sans créer d'instance[1]

Par exemple :

```java
public class Compteur {
    public static int nombreTotal = 0;

    public Compteur() {
        nombreTotal++; // Incrémente le compteur partagé
    }
}
```

## Méthodes Statiques

Une méthode statique a plusieurs caractéristiques importantes :

- Elle appartient à la classe et non aux instances[3]
- Elle ne peut accéder qu'aux autres membres statiques de la classe[3]
- Elle ne peut pas utiliser les mots-clés `this` ou `super`[1]
- Elle est appelée directement sur la classe, sans créer d'instance[3]

## Pourquoi main() est Static

La méthode `main` doit être statique car elle doit pouvoir être exécutée par la JVM avant la création de toute instance
de classe[3]. Comme elle est le point d'entrée du programme, elle doit être accessible sans avoir besoin d'instancier la
classe qui la contient[2].

## Exemple d'Utilisation

```java
public class Exemple {
    public static int compteur = 0;  // Variable statique

    public static void incrementer() {  // Méthode statique
        compteur++;
    }
}
```

```java
// Utilisation
Exemple.incrementer();  // Appel sans instance
System.out.println(Exemple.compteur);  // Accès direct
```

??? note "Citations"
    - [1] https://waytolearnx.com/2018/11/le-mot-cle-static-en-java.html
    - [2] https://perso.telecom-paristech.fr/hudry/coursJava/avance/static.html
    - [3] https://www.guru99.com/fr/static-variable-in-java.html
    - [4] https://javarush.com/fr/groups/posts/fr.3874.pause-caf-142-quel-rle-le-mot-cl-static-joue-t-il-en-java-
    - [5] https://blog.paumard.org/cours/java/chap04-structure-classe-statique.html




-------

??? info "Utilisation de l'IA"
    Page rédigée en partie avec l'aide d'un assistant IA. L'IA a été utilisée pour générer des 
    explications, des exemples et/ou des suggestions de structure. Toutes les informations ont 
    été vérifiées, éditées et complétées par l'auteur.