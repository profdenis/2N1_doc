# 7. La méthode `equals`

En Java, la redéfinition de la méthode `equals()` est souvent nécessaire pour comparer des objets selon leur contenu
plutôt que leur référence mémoire. Voici une explication détaillée avec exemples :

## Comparaison avec la classe String

Avec les chaînes de caractères, la différence entre `==` et `equals()` est cruciale :

```java
String s1 = new String("hello");
String s2 = new String("hello");

System.out.println(s1 == s2);    // false (comparaison de références)
System.out.println(s1.equals(s2)); // true (comparaison de contenu)
```

- **`==`** vérifie si les références pointent vers le même objet en mémoire[2][5][7]
- **`equals()`** (redéfini dans String) compare les caractères un par un[2][5]

## Cas d'une classe Personnalisée : Point

Considérons une classe `Point` avec des coordonnées x et y :

```java
public class Point {
    private int x;
    private int y;

    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
```

**Sans redéfinition de equals()** :

```java
Point p1 = new Point(3, 5);
Point p2 = new Point(3, 5);

System.out.println(p1.equals(p2)); // false (utilise l'implémentation Object)
```

**Avec redéfinition correcte** :

```java

@Override
public boolean equals(Object obj) {
    if (this == obj) return true;
    if (obj == null || getClass() != obj.getClass()) return false;

    Point other = (Point) obj;
    return x == other.x && y == other.y;
}
```

Maintenant `p1.equals(p2)` retournera `true` lorsque les coordonnées sont identiques[3][6][8].

## Pourquoi redéfinir equals() ?

1. **Égalité sémantique** : Comparer l'état des objets plutôt que leur identité mémoire[1][4][9]
2. **Compatibilité avec les collections** : Fonctionnement correct des `HashSet`, `HashMap`, etc.[1][4]
3. **Respect du contrat** : Nécessité de redéfinir `hashCode()` conjointement[1][4][8]

**Règles à respecter** (contrat equals) :

- **Réflexivité** : `x.equals(x)` = true
- **Symétrie** : `x.equals(y)` ⇨ `y.equals(x)`
- **Transitivité** : `x.equals(y)` ∧ `y.equals(z)` ⇨ `x.equals(z)`
- **Consistance** : Résultat stable si objets non modifiés
- **Non-nullité** : `x.equals(null)` = false[3][4]

## Impact de la non-redéfinition

```java
Set points = new HashSet<>();
points.add(new Point(1,2));
System.out.println(points.contains(new Point(1,2))); // false sans redéfinition
```

Ce code retournerait `false` car `HashSet` utilise à la fois `equals()` et `hashCode()` pour identifier les
éléments[1][4].

Pour une implémentation complète, il faut aussi redéfinir `hashCode()` de manière cohérente avec `equals()`[1][4][8].

Il est possible de générer le code des méthodes `equals` et `hashCode` à l'aide d'IntelliJ, qu'on pourra modifier au
besoin.

??? note "Citations"

      - [1] https://invivoo.com/blog/reussir-entretien-technique-java-equals-hashcode
      - [2] https://www.scaler.com/topics/difference-between-equals-method-in-java/
      - [3] https://dept-info.labri.fr/~baudon/Enseirb/2008/point.html
      - [4] https://jmdoudoux.developpez.com/cours/developpons/java/chap-techniques_java.php
      - [5] https://stackoverflow.com/questions/7520432/what-is-the-difference-between-and-equals-in-java
      - [6] https://docs.oracle.com/javase/6/docs/api/java/awt/Point.html
      - [7] https://stackoverflow.com/questions/8180430/how-to-override-equals-method-in-java
      - [8] https://byjus.com/gate/difference-between-operator-and-equals-method-in-java/
      - [9] https://www.jmdoudoux.fr/java/dej/chap-techniques_java.htm

## La méthode `hashCode`

La méthode hashCode() est une méthode fondamentale en Java, héritée de la classe Object et présente dans toutes les
classes Java. Voici ses principales caractéristiques :

### Définition et rôle

- Elle retourne un entier signé de 32 bits qui représente le code de hachage de l'objet[1][3].
- Ce code est une représentation numérique de l'objet, censée être représentative de son contenu[5].

### Fonctionnement

- Par défaut, l'implémentation de Object.hashCode() retourne généralement une valeur basée sur l'adresse mémoire de
  l'objet[5].
- Les classes peuvent redéfinir cette méthode pour fournir un code de hachage plus approprié à leurs données
  spécifiques[1].

### Importance

1. **Collections** : Utilisée par les structures de données basées sur le hachage (comme HashMap, HashSet) pour stocker
   et récupérer efficacement les objets[7].
2. **Performance** : Un bon hashCode() permet une distribution uniforme des objets dans ces structures, améliorant les
   performances[6].

### Contrat avec equals()

- Si deux objets sont égaux selon equals(), ils doivent avoir le même hashCode()[1][7].
- Deux objets avec le même hashCode() ne sont pas nécessairement égaux[7].

### Implémentation

Une implémentation typique combine les codes de hachage des champs significatifs de l'objet :

```java

@Override
public int hashCode() {
    int result = 17; // Nombre premier arbitraire
    result = 31 * result + (field1 != null ? field1.hashCode() : 0);
    result = 31 * result + field2;
    // ... autres champs
    return result;
}
```

Cette méthode est cruciale pour le bon fonctionnement des collections basées sur le hachage et doit être soigneusement
implémentée en conjonction avec la méthode equals().

??? note "Citations"

      - [1] https://fr.wikipedia.org/wiki/Java_hashCode()
      - [2] https://stackoverflow.com/questions/113511/best-implementation-for-hashcode-method-for-a-collection
      - [3] https://codegym.cc/fr/groups/posts/fr.210.code-de-hachage-java-
      - [4] https://www.w3schools.com/java/ref_string_hashcode.asp
      - [5] https://blog.paumard.org/cours/java/chap03-object-string-object.html
      - [6] https://www.sitepoint.com/how-to-implement-javas-hashcode-correctly/
      - [7] https://www.digitalocean.com/community/tutorials/java-equals-hashcode
      - [8] https://www.youtube.com/watch?v=6YXiy9JavDc
      - [9] https://javarush.com/fr/groups/posts/fr.1340.surcharge-des-mthodes-equals-et-hashcode-en-java

