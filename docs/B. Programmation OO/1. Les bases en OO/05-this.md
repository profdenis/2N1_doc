# 🔸5🔸Le mot-clé `this`

Voici une version améliorée de la classe Personne utilisant la classe `LocalDate` de Java pour gérer les dates.

```java
import java.time.LocalDate;

public class Personne {
    private String nom;
    private String prenom;
    private LocalDate dateNaissance;

    // Constructeur complet
    public Personne(String nom, String prenom, LocalDate dateNaissance) {
        this.nom = nom;
        this.prenom = prenom;
        this.dateNaissance = dateNaissance;
    }

    // Constructeur qui appelle l'autre constructeur avec la date d'aujourd'hui
    public Personne(String nom, String prenom) {
        this(nom, prenom, LocalDate.now());
    }

    // Accesseurs et mutateurs
    public String getNom() {
        return nom;
    }

    public void setNom(String nom) {
        this.nom = nom;
    }

    public String getPrenom() {
        return prenom;
    }

    public void setPrenom(String prenom) {
        this.prenom = prenom;
    }

    public LocalDate getDateNaissance() {
        return dateNaissance;
    }

    public void setDateNaissance(LocalDate dateNaissance) {
        this.dateNaissance = dateNaissance;
    }

    // Méthode utilitaire pour calculer l'âge
    public int getAge() {
        return LocalDate.now().getYear() - dateNaissance.getYear();
    }
}
```

## Utilisation

```java
// Création avec date spécifique
LocalDate dateNaissance = LocalDate.of(2000, 1, 15);
Personne personne1 = new Personne("Dupont", "Jean", dateNaissance);

// Création sans date (utilisera la date d'aujourd'hui)
Personne personne2 = new Personne("Martin", "Marie");
```

Points importants dans cet exemple :

- L'utilisation de `this()` pour appeler un autre constructeur
- L'utilisation de `LocalDate` pour une gestion robuste des dates
- Les attributs sont privés avec leurs accesseurs et mutateurs
- Une méthode utilitaire `getAge()` qui calcule l'âge à partir de la date de naissance

!!! note "Note"
    Le calcul de l'âge dans cet exemple est simplifié. Pour un calcul plus précis, il faudrait tenir compte des mois
    et des jours.

## Le mot-clé `this`

`this` est une référence à l'objet courant, utilisable uniquement dans les méthodes d'instance (non-statiques). Il
représente l'instance de la classe qui exécute le code.

## Références et Objets

```java
public class Personne {
    private String nom;

    public void setNom(String nom) {
        this.nom = nom;  // this.nom réfère à l'attribut de l'instance
    }
}

// Utilisation avec plusieurs références
Personne p1 = new Personne();
Personne p2 = p1;  // p2 réfère au même objet que p1
```

## Différents Usages de `this`

**1. Distinguer les attributs des paramètres :**

```java
public class Personne {
    private String nom;

    public Personne(String nom) {
        this.nom = nom;  // Sans this, nom référerait au paramètre
    }
}
```

**2. Appeler un autre constructeur :**

```java
public class Personne {
    private String nom;
    private int age;

    public Personne(String nom) {
        this(nom, 0);  // Appelle l'autre constructeur
    }

    public Personne(String nom, int age) {
        this.nom = nom;
        this.age = age;
    }
}
```

## Références Multiples

```java
Personne p1 = new Personne("Alice");
Personne p2 = p1;  // Nouvelle référence au même objet
p2.setNom("Bob");  // Modifie l'objet via p2
System.out.println(p1.getNom());  // Affiche "Bob" car p1 et p2 réfèrent au même objet
```

## Comportement des Références

```java
public class ExempleReferences {
    public static void modifierPersonne(Personne p) {
        p.setNom("Charlie");  // Modifie l'objet original
        p = new Personne("David");  // Crée un nouvel objet, ne modifie pas la référence originale
    }

    public static void main(String[] args) {
        Personne p1 = new Personne("Alice");
        modifierPersonne(p1);
        System.out.println(p1.getNom());  // Affiche "Charlie"
    }
}
```

Dans cet exemple :

- La modification via une référence affecte l'objet pour toutes les références
- La réaffectation d'une référence n'affecte pas les autres références au même objet
- `this` reste toujours une référence à l'objet courant, peu importe le nombre de références externes

Cette compréhension des références est fondamentale en POO car elle explique comment les objets sont partagés et
modifiés à travers le programme.




-------

!!! note "Note"
    Page rédigée en partie avec l'aide d'un assistant IA, principalement à l'aide de Perplexity AI, avec le *LLM* 
    **Claude 3.5 Sonnet**. L'IA a été utilisée pour générer des explications, des exemples et/ou des suggestions de 
    structure. Toutes les informations ont été vérifiées, éditées et complétées par l'auteur.