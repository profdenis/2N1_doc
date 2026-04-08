# Guide complet : Les `record` en Java

---

## 1. Introduction

Les `record` ont été introduits en Java 16 (en preview) et finalisés en Java 17. Ils permettent de déclarer des *
*classes de données immutables** de manière concise, en réduisant considérablement la quantité de code boilerplate (
constructeurs, getters, `equals`, `hashCode`, `toString`). Un `record` est idéal pour modéliser des données simples,
comme des coordonnées, des points, des paires clé-valeur, etc.

---

## 2. Pourquoi utiliser un `record` ?

- **Immutabilité** : Les champs sont implicitement `final`.
- **Concis** : Pas besoin d’écrire manuellement les getters, `equals`, `hashCode`, ou `toString`.
- **Clarté** : La déclaration est compacte et exprime clairement l’intention : stocker des données.
- **Sécurité** : Moins de risques d’erreurs dans les méthodes générées automatiquement.

---

## 3. Syntaxe de base

Un `record` se déclare ainsi :

```java
public record NomDuRecord(Type1 champ1, Type2 champ2, ...) {
    // Corps optionnel (constructeurs, méthodes, etc.)
}
```

- Java génère automatiquement :
    - Un constructeur canonique (qui initialise tous les champs).
    - Des méthodes d’accès (`champ1()`, `champ2()`, etc., **pas de `get**`).
    - `equals()`, `hashCode()`, et `toString()`.

---

## 4. Exemple : Conversion de `Coord` en `record`

### a. Classe originale (avec boilerplate)

```java
import java.util.Objects;

public class Coord {
    private final int x;
    private final int y;

    public Coord(int x, int y) {
        this.x = x;
        this.y = y;
    }

    public int getX() {
        return x;
    }

    public int getY() {
        return y;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Coord coord = (Coord) o;
        return x == coord.x && y == coord.y;
    }

    @Override
    public int hashCode() {
        return Objects.hash(x, y);
    }

    @Override
    public String toString() {
        return "(" + x + "," + y + ")";
    }
}
```

### b. Équivalent en `record`

```java
public record Coord(int x, int y) {
    // Aucun code supplémentaire n'est nécessaire !
}
```

- **Utilisation** :
  ```java
  Coord c = new Coord(10, 20);
  System.out.println(c.x()); // 10 (pas de getX !)
  System.out.println(c.y()); // 20
  System.out.println(c);     // (10,20) (toString généré)
  ```

---

## 5. Constructeurs personnalisés

Si vous voulez ajouter de la logique dans le constructeur (validation, calculs, etc.), vous pouvez définir un *
*constructeur compact** :

```java
public record Coord(int x, int y) {
    public Coord {
        if (x < 0 || y < 0) {
            throw new IllegalArgumentException("Les coordonnées doivent être positives.");
        }
    }
}
```

- **Remarque** : Le constructeur compact n’a pas de liste de paramètres explicite ; ils sont implicites (ceux du
  `record`).

---

## 6. Méthodes supplémentaires

Vous pouvez ajouter des méthodes comme dans une classe normale :

```java
public record Coord(int x, int y) {
    public double distanceFromOrigin() {
        return Math.sqrt(x * x + y * y);
    }
}
```

- **Utilisation** :
  ```java
  Coord c = new Coord(3, 4);
  System.out.println(c.distanceFromOrigin()); // 5.0
  ```

---

## 7. Immutabilité et sécurité

- Les champs d’un `record` sont `final` et ne peuvent pas être modifiés après la construction.
- Les `record` sont **thread-safe** par nature, car immutables.
- Ils sont particulièrement utiles pour les DTO (Data Transfer Objects), les clés de maps, ou les valeurs dans des
  collections.

---

## 8. Comparaison avec une classe classique

| Fonctionnalité                   | Classe classique (ex: `Coord`)         | `record` (ex: `Coord`)                 |
|----------------------------------|----------------------------------------|----------------------------------------|
| Déclaration                      | Verbose (champs, constructeur, etc.)   | Concise (`record Coord(int x, int y)`) |
| Getters                          | `getX()`, `getY()`                     | `x()`, `y()`                           |
| `equals`, `hashCode`, `toString` | Doivent être implémentés manuellement  | Générés automatiquement                |
| Immutabilité                     | Doit être gérée manuellement (`final`) | Implicite                              |
| Constructeur personnalisé        | Possible                               | Possible (constructeur compact)        |

---

## 9. Exercices pratiques

### Exercice 1 : Conversion en `record`

Convertissez la classe suivante en `record` :

```java
public class Personne {
    private final String nom;
    private final int age;

    public Personne(String nom, int age) {
        this.nom = nom;
        this.age = age;
    }

    public String getNom() {
        return nom;
    }

    public int getAge() {
        return age;
    }

    @Override
    public boolean equals(Object o) { /* ... */ }

    @Override
    public int hashCode() { /* ... */ }

    @Override
    public String toString() { /* ... */ }
}
```

**Solution attendue** :

```java
public record Personne(String nom, int age) {
}
```

---

### Exercice 2 : Ajout de logique

Créez un `record` `Rectangle` avec des champs `largeur` et `hauteur` (tous deux `double`), et ajoutez une méthode
`aire()` qui retourne la surface du rectangle.

**Solution attendue** :

```java
public record Rectangle(double largeur, double hauteur) {
    public double aire() {
        return largeur * hauteur;
    }
}
```

---

### Exercice 3 : Validation dans le constructeur

Modifiez le `record` `Coord` pour que les coordonnées ne puissent pas être négatives (lancez une
`IllegalArgumentException` si c’est le cas).

**Solution attendue** :

```java
public record Coord(int x, int y) {
    public Coord {
        if (x < 0 || y < 0) {
            throw new IllegalArgumentException("Les coordonnées doivent être positives.");
        }
    }
}
```

---

### Exercice 4 : Utilisation dans une collection

Écrivez un programme qui crée une `List<Coord>`, y ajoute quelques `Coord`, puis les affiche en utilisant `toString()`
généré automatiquement.

**Solution attendue** :

```java
import java.util.List;

void main() {
    List<Coord> coords = List.of(
            new Coord(1, 2),
            new Coord(3, 4),
            new Coord(5, 6)
    );
    coords.forEach(System.out::println);
}
```

---

## 10. Points d’attention

- **Pas d’héritage** : Un `record` ne peut pas hériter d’une autre classe (mais peut implémenter des interfaces).
- **Champs implicites** : Tous les champs déclarés dans l’en-tête du `record` sont privés et finaux.
- **Constructeur par défaut** : Si vous définissez un constructeur personnalisé, le constructeur canonique n’est plus
  généré automatiquement (sauf si vous utilisez le constructeur compact).
- **Sérialisation** : Les `record` sont sérialisables par défaut (implémentent `Serializable`).

---

## 11. Pour aller plus loin

- **Pattern Matching** : Les `record` fonctionnent très bien avec le pattern matching (introduit en Java 16+).
  ```java
  Object obj = new Coord(1, 2);
  if (obj instanceof Coord c) {
      System.out.println("Coordonnées : " + c.x() + ", " + c.y());
  }
  ```
- **Imbrication** : Vous pouvez imbriquer des `record` ou les utiliser comme champs d’autres `record`.
- **Performance** : Les `record` sont optimisés par le compilateur pour être aussi performants que des classes
  équivalentes écrites manuellement.

---

## 12. Conclusion

Les `record` sont une avancée majeure pour Java, permettant de déclarer des classes de données de manière concise, sûre
et expressive. Ils réduisent le code boilerplate et rendent le code plus lisible et maintenable. En les utilisant, tes
étudiants pourront se concentrer sur la logique métier plutôt que sur les détails d’implémentation.

---

## 13. Ressources supplémentaires

- [JEP 395: Records (Java 16)](https://openjdk.org/jeps/395)
- [Tutoriel officiel sur les records](https://docs.oracle.com/en/java/javase/17/language/records.html)
- [Exemples avancés avec pattern matching](https://dev.java/learn/pattern-matching/)