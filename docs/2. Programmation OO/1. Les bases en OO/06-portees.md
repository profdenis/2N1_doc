# Mots-clés de portée

## Résumé des Portées

| Modificateur | Classe | Package | Sous-classe | Partout |
|--------------|--------|---------|-------------|---------|
| private      | ✓      | ✗       | ✗           | ✗       |
| (default)    | ✓      | ✓       | ✗           | ✗       |
| protected    | ✓      | ✓       | ✓           | ✗       |
| public       | ✓      | ✓       | ✓           | ✓       |

## Détails des Modificateurs d'Accès

**private**

- Accès limité uniquement à l'intérieur de la classe déclarante
- Utilisé principalement pour les attributs afin d'assurer l'encapsulation

```java
public class Compte {
    private double solde;  // Accessible uniquement dans Compte
}
```

**default (pas de modificateur)**

- Accès limité au package (aussi appelé "package-private")
- C'est la portée par défaut quand aucun modificateur n'est spécifié

```java
class Utilitaire {  // Accessible uniquement dans le même package
    int valeur;     // Également accessible uniquement dans le package
}
```

**protected**

- Accessible dans le package et par les sous-classes
- Utile pour permettre l'héritage tout en limitant l'accès public

```java
public class Animal {
    protected void respirer() {  // Accessible aux sous-classes
        // code
    }
}
```

**public**

- Accessible partout
- Utilisé pour les interfaces publiques des classes

```java
public class Client {
    public String getNom() {  // Accessible de partout
        return nom;
    }
}
```

## Bonnes Pratiques

- Utiliser `private` pour les attributs (encapsulation)
- Utiliser `public` pour les méthodes qui font partie de l'interface publique
- Utiliser `protected` avec parcimonie, seulement quand l'héritage le justifie
- La portée par défaut est utile pour les classes utilitaires internes au package

## Exemple Complet

```java
public class Employe {
    private String nom;           // Accessible uniquement dans cette classe
    protected double salaire;     // Accessible dans les sous-classes
    String departement;          // Accessible dans le package

    public String getId();       // Accessible partout
}
```

Cette hiérarchie de portées permet de contrôler précisément la visibilité des éléments et de maintenir un bon niveau
d'encapsulation dans le code.