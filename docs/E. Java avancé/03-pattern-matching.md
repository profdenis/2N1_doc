# Guide complet : Pattern Matching en Java et bonnes pratiques OO

---

## 1. Introduction

Le **pattern matching** est une fonctionnalité puissante introduite en Java pour simplifier la manipulation des objets
en fonction de leur type ou de leur structure. Cependant, son utilisation doit être réfléchie pour respecter les
principes du **bon design orienté objet (OO)**. Ce guide explique quand et comment utiliser le pattern matching, ainsi
que ses alternatives et limites.

---

## 2. Historique et versions

| Version | Fonctionnalité introduite                                                                                      |
|---------|----------------------------------------------------------------------------------------------------------------|
| Java 16 | Pattern Matching pour `instanceof` (JEP 394)                                                                   |
| Java 17 | Pattern Matching pour `switch` (preview)                                                                       |
| Java 19 | Record Patterns (preview)                                                                                      |
| Java 21 | Pattern Matching pour `switch` (finalisé), Record Patterns (standard), Pattern Matching dans les boucles `for` |

---

## 3. Pattern Matching de base : `instanceof`

### a. Avant Java 16

Pour vérifier le type d’un objet et le caster, il fallait écrire :

```java
if(obj instanceof String){
    String s = (String) obj;
    System.out.println(s.length());
}
```

### b. Depuis Java 16 : Pattern Matching pour `instanceof`

La syntaxe est simplifiée et plus sûre :

```java
if(obj instanceofString s){
    System.out.println(s.length()); // s est automatiquement casté et disponible dans le bloc
}
```

- **Avantages** :
    - Pas besoin de caster manuellement.
    - La variable `s` est disponible uniquement dans le bloc `if`.
    - Moins de risques d’erreurs de cast.

---

### c. Exemple avec une hiérarchie de classes

```java
interface Shape {
}

record Circle(double radius) implements Shape {
}

record Rectangle(double length, double width) implements Shape {
}

void printArea(Shape shape) {
    if (shape instanceof Circle c) {
        System.out.println("Aire du cercle : " + Math.PI * c.radius() * c.radius());
    } else if (shape instanceof Rectangle r) {
        System.out.println("Aire du rectangle : " + r.length() * r.width());
    }
}
```

---

## 4. Pattern Matching avec `switch` (depuis Java 17+)

Le pattern matching étend la puissance de l’instruction `switch` en permettant de :

- Faire correspondre des types.
- Extraire des composants (notamment avec les `record`).
- Utiliser des motifs (`pattern`) directement dans les `case`.

### a. Syntaxe de base

```java
String description = switch (obj) {
    case Integer i -> "Nombre entier : " + i;
    case String s -> "Chaîne de caractères : " + s;
    case Double d -> "Nombre décimal : " + d;
    default -> "Type inconnu";
};
```

- **Points clés** :
    - Le type est vérifié et la variable est automatiquement castée.
    - La flèche (`->`) est utilisée pour les expressions (pas de `break` nécessaire si c’est une expression).
    - Le `default` reste obligatoire pour couvrir tous les cas.

---

### b. Utilisation avec des `record`

Le pattern matching brille particulièrement avec les `record`, car il permet de déconstruire directement leurs
composants :

```java
record Point(int x, int y) {
}

void printCoord(Object obj) {
    switch (obj) {
        case Point(int x, int y) -> System.out.printf("Point(%d, %d)%n", x, y);
        case null -> System.out.println("Objet null");
        default -> System.out.println("Type inconnu");
    }
}
```

- **Exemple avancé** :
  ```java
  record Person(String name, int age) {}

  void greet(Object obj) {
      switch (obj) {
          case Person p when p.age() >= 18 -> System.out.println("Bonjour, " + p.name() + " (adulte)");
          case Person p                    -> System.out.println("Bonjour, " + p.name() + " (mineur)");
          case null                        -> System.out.println("Aucune personne");
          default                          -> System.out.println("Type inconnu");
      }
  }
  ```

---

### c. Guarded Patterns (`when`)

On peut ajouter des conditions supplémentaires avec `when` :

```java
void checkObject(Object obj) {
    switch (obj) {
        case String s when s.length() > 5 -> System.out.println("Longue chaîne");
        case String s -> System.out.println("Chaîne courte");
        case Integer i when i > 100 -> System.out.println("Grand nombre");
        case Integer i -> System.out.println("Petit nombre");
        default -> System.out.println("Autre type");
    }
}
```

---

## 5. Pattern Matching dans les boucles `for` (depuis Java 21)

On peut utiliser le pattern matching directement dans les boucles `for` pour filtrer et caster les éléments :

```java
List<Object> objects = List.of("hello", 42, new Point(1, 2), "world");

for (Object obj : objects) {
    if(obj instanceof String s && s.length() > 3) {
        System.out.println("Long string: "+s);
    } else if(obj instanceof Point p) {
        System.out.println("Point: "+p);
    }
}
```

---

## 6. Record Patterns (depuis Java 19+)

Les `record` et le pattern matching sont faits pour s’entendre. On peut déconstruire un `record` directement dans un
`switch` ou un `instanceof` :

### a. Avec `instanceof`

```java
record Person(String name, int age) {
}

void printPersonInfo(Object obj) {
    if (obj instanceof Person(String name, int age)) {
        System.out.println(name + " a " + age + " ans.");
    }
}
```

### b. Avec `switch`

```java
void printPersonDetails(Object obj) {
    switch (obj) {
        case Person(var name, var age) when age >= 18 -> System.out.println(name + " est adulte.");
        case Person(var name, var age) -> System.out.println(name + " est mineur.");
        default -> System.out.println("Pas une personne.");
    }
}
```

---

## 7. Exercices pratiques

### Exercice 1 : Pattern Matching avec `instanceof`

Écrivez une méthode qui prend un `Object` et affiche :

- La longueur si c’est une `String`.
- La valeur si c’est un `Integer`.
- Un message par défaut sinon.

**Solution attendue** :

```java
void printInfo(Object obj) {
    if (obj instanceof String s) {
        System.out.println("Longueur : " + s.length());
    } else if (obj instanceof Integer i) {
        System.out.println("Valeur : " + i);
    } else {
        System.out.println("Type non géré");
    }
}
```

---

### Exercice 2 : `switch` avec Pattern Matching

Écrivez un `switch` qui :

- Affiche l’aire si l’objet est un `Circle` (`record Circle(double radius)`).
- Affiche le périmètre si l’objet est un `Rectangle` (`record Rectangle(double length, double width)`).
- Affiche un message par défaut sinon.

**Solution attendue** :

```java
void printShapeInfo(Shape shape) {
    switch (shape) {
        case Circle c -> System.out.println("Aire : " + Math.PI * c.radius() * c.radius());
        case Rectangle r -> System.out.println("Périmètre : " + 2 * (r.length() + r.width()));
        default -> System.out.println("Forme inconnue");
    }
}
```

---

### Exercice 3 : Record Patterns

Créez un `record` `Book(String title, int year)` et écrivez une méthode qui utilise le pattern matching pour afficher :

- "Livre récent" si l’année est >= 2000.
- "Livre ancien" sinon.

**Solution attendue** :

```java
record Book(String title, int year) {
}

void printBookInfo(Object obj) {
    if (obj instanceof Book(var title, var year) && year >= 2000) {
        System.out.println(title + " (récent)");
    } else if (obj instanceof Book(var title, var year)) {
        System.out.println(title + " (ancien)");
    }
}
```

---

### Exercice 4 : `switch` avec `when`

Utilisez un `switch` avec `when` pour afficher :

- "Long" si la `String` a plus de 10 caractères.
- "Court" sinon.
- "Nombre pair" si l’`Integer` est pair.
- "Nombre impair" sinon.

**Solution attendue** :

```java
void printDetails(Object obj) {
    switch (obj) {
        case String s when s.length() > 10 -> System.out.println("Long");
        case String s -> System.out.println("Court");
        case Integer i when i % 2 == 0 -> System.out.println("Nombre pair");
        case Integer i -> System.out.println("Nombre impair");
        default -> System.out.println("Type inconnu");
    }
}
```

---

## 8. Pattern Matching vs Polymorphisme : Quand utiliser quoi ?

### a. Principe de design OO : Privilégier le polymorphisme

Dans un **bon design OO**, on privilégie généralement le **polymorphisme** pour modéliser des comportements variables.
Par exemple, pour calculer l’aire de différentes formes géométriques, il est préférable de définir une méthode abstraite
dans une interface ou une classe de base, et de l’implémenter dans chaque sous-classe :

```java
interface Shape {
    double getArea(); // Méthode polymorphe
}

record Circle(double radius) implements Shape {
    @Override
    public double getArea() {
        return Math.PI * radius * radius;
    }
}

record Rectangle(double length, double width) implements Shape {
    @Override
    public double getArea() {
        return length * width;
    }
}

// Utilisation polymorphe
void printArea(Shape shape) {
    System.out.println("Aire : " + shape.getArea());
}
```

**Avantages du polymorphisme** :

- **Extensibilité** : Ajouter une nouvelle forme ne nécessite pas de modifier le code qui utilise `Shape`.
- **Respect du principe Open/Closed** : Le code est ouvert à l’extension mais fermé à la modification.
- **Lisibilité** : Le comportement est encapsulé dans chaque classe, ce qui rend le code plus clair et maintenable.

---

### b. Quand le pattern matching est-il justifié ?

Le pattern matching peut être utile dans les cas suivants, où le polymorphisme n’est **pas applicable** ou **peu
pratique** :

1. **Accès à des types externes ou non modifiables** :

   - Si vous utilisez des classes tierces (ex: `String`, `Integer`, `List`) ou des `record` que vous ne pouvez pas modifier
     pour y ajouter des méthodes polymorphes.

2. **Logique transversale ou temporaire** :

   - Pour des traitements ponctuels qui ne justifient pas une refactorisation en polymorphisme (ex: sérialisation, logging,
     validation).

3. **Traitement de types hétérogènes** :

   - Quand vous manipulez une collection d’objets de types différents sans hiérarchie commune (ex: `List<Object>` contenant
     des `String`, `Integer`, etc.).

4. **Déconstruction de `record**` :

   - Pour extraire et utiliser directement les composants d’un `record` sans avoir besoin de méthodes intermédiaires.

5. **Cas où le polymorphisme est trop lourd** :

   - Pour des petits projets, des scripts, ou des prototypes où la surcharge du polymorphisme n’est pas justifiée.

---

### c. Exemple : Quand le pattern matching est préférable

Supposons que vous deviez écrire une méthode qui affiche un message différent selon le type d’un objet **que vous ne
contrôlez pas** (ex: `String`, `Integer`, `List`) :

```java
void printTypeInfo(Object obj) {
    switch (obj) {
        case String s -> System.out.println("Chaîne de longueur " + s.length());
        case Integer i -> System.out.println("Nombre entier : " + i);
        case List<?> list -> System.out.println("Liste de taille " + list.size());
        default -> System.out.println("Type inconnu");
    }
}
```

- Ici, le polymorphisme n’est pas applicable car vous ne pouvez pas modifier `String`, `Integer`, ou `List`.

---

### d. Exemple : Quand le polymorphisme est préférable

Reprenons l’exemple des formes géométriques. Utiliser le pattern matching pour calculer l’aire **n’est pas recommandé**
si vous contrôlez les classes, car cela viole le principe de responsabilité unique et rend le code moins extensible :

```java
// À éviter si vous pouvez utiliser le polymorphisme
void printArea(Shape shape) {
    switch (shape) {
        case Circle c -> System.out.println("Aire : " + Math.PI * c.radius() * c.radius());
        case Rectangle r -> System.out.println("Aire : " + r.length() * r.width());
        // Si vous ajoutez un Triangle, il faut modifier cette méthode !
    }
}
```

---

## 9. Limites du polymorphisme

Il existe des cas où le polymorphisme **n’est pas applicable** ou **peu pratique** :

1. **Types finaux ou externes** :

   - Impossible d’étendre ou de modifier des classes comme `String`, `Integer`, ou des classes tierces.

2. **Logique dépendante du type concret** :

   - Certaines opérations (ex: sérialisation, clonage, comparaison) dépendent du type concret et ne peuvent pas être
     encapsulées dans une hiérarchie polymorphe.

3. **Hiérarchies complexes ou absentes** :

   - Si les objets proviennent de sources différentes sans hiérarchie commune, le polymorphisme n’est pas utilisable.

4. **Performances** :

   - Dans certains cas (ex: traitement de données en masse), le pattern matching peut être plus performant que des appels
     polymorphes (bien que cela soit rare en Java moderne).

5. **Code temporaire ou prototype** :

   - Pour des scripts ou des prototypes, le pattern matching peut être plus rapide à écrire.

---

## 10. Bonnes pratiques : Comment choisir ?

| Critère                            | Polymorphisme | Pattern Matching             |
|------------------------------------|---------------|------------------------------|
| Vous contrôlez les classes         | ✅ Recommandé  | ❌ À éviter                   |
| Vous ne contrôlez pas les classes  | ❌ Impossible  | ✅ Justifié                   |
| Logique extensible                 | ✅ Idéal       | ❌ Risque de duplication      |
| Logique ponctuelle ou transversale | ❌ Peu adapté  | ✅ Adapté                     |
| Respect des principes SOLID        | ✅ Oui         | ⚠️ Risque de violation (OCP) |
| Lisibilité et maintenabilité       | ✅ Meilleure   | ⚠️ Peut devenir complexe     |

---

## 11. Exemple complet : Combiner les deux approches

Parfois, une solution hybride est optimale. Par exemple, utilisez le polymorphisme pour les comportements principaux, et
le pattern matching pour des traitements spécifiques :

```java
interface Shape {
    double getArea(); // Polymorphisme pour le comportement principal
}

record Circle(double radius) implements Shape {
    @Override
    public double getArea() {
        return Math.PI * radius * radius;
    }
}

record Rectangle(double length, double width) implements Shape {
    @Override
    public double getArea() {
        return length * width;
    }
}

// Utilisation polymorphe pour l'aire
void printArea(Shape shape) {
    System.out.println("Aire : " + shape.getArea());
}

// Utilisation de pattern matching pour un traitement spécifique
void printShapeInfo(Object obj) {
    switch (obj) {
        case Circle c -> System.out.println("Cercle de rayon " + c.radius());
        case Rectangle r -> System.out.println("Rectangle " + r.length() + "x" + r.width());
        case Shape s -> System.out.println("Forme inconnue avec aire : " + s.getArea());
        default -> System.out.println("Pas une forme");
    }
}
```

---

## 12. Conclusion

- **Privilégiez le polymorphisme** pour modéliser des comportements variables dans une hiérarchie de classes que vous
  contrôlez.
- **Utilisez le pattern matching** pour des traitements ponctuels, des types externes, ou des cas où le polymorphisme
  n’est pas applicable.
- **Évitez le pattern matching** pour des logiques métiers centrales qui pourraient évoluer, afin de respecter les
  principes SOLID et de maintenir un code extensible.

En combinant judicieusement ces deux approches, vous pouvez écrire du code Java moderne, expressif et maintenable.

---

## 13. Exercice récapitulatif

### Exercice : Choisir la bonne approche

Pour chacun des cas suivants, indiquez si vous utiliseriez le **polymorphisme** ou le **pattern matching**, et justifiez
votre choix :

1. Calculer le périmètre de différentes formes géométriques (`Circle`, `Rectangle`, `Triangle`) que vous contrôlez.
2. Afficher un message différent selon qu’un objet est une `String`, un `Integer`, ou une `List` (types JDK).
3. Valider qu’un objet est soit un `User` soit un `Admin` (classes que vous contrôlez), et extraire leur nom.
4. Écrire un logger qui affiche des informations différentes selon le type d’une exception (`IOException`,
   `SQLException`, etc.).

??? info "Solutions suggérées"

    1. **Polymorphisme** : Ajoutez une méthode `getPerimeter()` dans l’interface `Shape`.
    2. **Pattern Matching** : Impossible d’utiliser le polymorphisme sur des types JDK.
    3. **Polymorphisme** : Ajoutez une méthode `getName()` dans une interface commune `Person`.
    4. **Pattern Matching** : Les exceptions sont des classes externes, et la logique est transversale (logging).

---

## 14. Ressources pour approfondir

- [Principe Open/Closed (SOLID)](https://en.wikipedia.org/wiki/Open%E2%80%93closed_principle)
- [Pattern Matching vs Polymorphism (Discussion)](https://stackoverflow.com/questions/67033250/when-to-use-pattern-matching-vs-polymorphism-in-java)
- [Java Language Architecture (JEP Index)](https://openjdk.org/jeps/0)