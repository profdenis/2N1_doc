---
icon: material/file-document-outline
---

# 2. Variables et types

## Déclaration de variables

En Java, la déclaration de variables suit une syntaxe stricte :

```java
// Déclaration simple
type nomVariable;

// Déclaration avec initialisation
type nomVariable = valeur;

// Exemples concrets
int age = 25;
String nom;
nom = "Alice";
```

## Types de variables

**Types primitifs** :

- `byte` : entier sur 8 bits (-128 à 127)
- `short` : entier sur 16 bits (-32,768 à 32,767)
- `int` : entier sur 32 bits (-2^31 à 2^31-1)
- `long` : entier sur 64 bits (-2^63 à 2^63-1)
- `float` : décimal sur 32 bits
- `double` : décimal sur 64 bits
- `boolean` : true ou false
- `char` : caractère Unicode sur 16 bits

**Classes wrapper** :

| Type primitif | Classe wrapper | Exemple d'utilisation    |
|---------------|----------------|--------------------------|
| int           | Integer        | Integer nombre = 42;     |
| double        | Double         | Double prix = 19.99;     |
| boolean       | Boolean        | Boolean estActif = true; |
| char          | Character      | Character lettre = 'A';  |

Les classes wrapper offrent des fonctionnalités supplémentaires :

```java
// Conversion String vers int
String nombreTexte = "123";
int nombrePrimitif = Integer.parseInt(nombreTexte);

// Valeurs min/max
int maximum = Integer.MAX_VALUE;
int minimum = Integer.MIN_VALUE;
```

## Formatage des chaînes

**Concaténation simple** :

```java
String nom = "Alice";
int age = 25;
System.out.println("Je m'appelle "+nom +" et j'ai "+age+" ans");
```

**String.format()** :

```java
String message = String.format("Je m'appelle %s et j'ai %d ans", nom, age);
System.out.println(message);
```

**printf** :

```java
System.out.printf("Je m'appelle %s et j'ai %d ans%n", nom, age);
```

**Text blocks (Java 15+)** :

```java
String texteMultiLigne = """
        Bonjour,
        Je m'appelle %s
        J'ai %d ans
        """.formatted(nom, age);
```

**Spécificateurs de format courants** :

- `%s` : chaînes
- `%d` : entiers
- `%f` : nombres décimaux
- `%n` : saut de ligne
- `%.2f` : décimal avec 2 chiffres après la virgule

Exemple complet :

```java
public class ExempleFormatage {
    public static void main(String[] args) {
        String nom = "Alice";
        int age = 25;
        double taille = 1.68;
        boolean estEtudiant = true;

        // Formatage avec différentes méthodes
        System.out.printf("Nom: %s, Âge: %d%n", nom, age);
        System.out.printf("Taille: %.2f m%n", taille);

        // Utilisation de text blocks avec formatage
        String profil = """
                Profil de l'utilisateur:
                Nom: %s
                Âge: %d ans
                Taille: %.2f m
                Statut étudiant: %b
                """.formatted(nom, age, taille, estEtudiant);

        System.out.println(profil);

        // Formatage de nombres
        double prix = 1234.5678;
        System.out.printf("Prix formaté: %,.2f €%n", prix);  // Affiche: 1 234,57 €
    }
}
```

-------

??? info "Utilisation de l'IA"
    Page rédigée en partie avec l'aide d'un assistant IA. L'IA a été utilisée pour générer des 
    explications, des exemples et/ou des suggestions de structure. Toutes les informations ont 
    été vérifiées, éditées et complétées par l'auteur.