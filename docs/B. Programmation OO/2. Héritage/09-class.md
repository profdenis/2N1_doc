---
icon: material/file-document-outline
---

# 9. La classe `Class`

## La classe `Class` en Java

La classe `Class` (dans le package `java.lang`) est une classe fondamentale en Java qui représente les métadonnées d'une
classe à l'exécution. Voici ses caractéristiques principales :

- **Représentation des types** : Chaque classe, interface, enum ou annotation en Java a un objet `Class` correspondant
  qui décrit sa structure.
- **Accès aux métadonnées** : Permet d'obtenir des informations sur les champs, méthodes, constructeurs, etc.
- **Finale** : Ne peut pas être étendue (déclarée `final`).
- **Pas d'instanciation directe** : On obtient ses instances via :
    - La méthode `getClass()` des objets
    - Le littéral `.class` (ex: `String.class`)
    - `Class.forName()`

**Exemple d'utilisation** :

```java
Class stringClass = String.class;
System.out.println(stringClass.getName()); // "java.lang.String"
```

## La méthode `getClass()`

Définie dans `Object`, cette méthode retourne l'objet `Class` représentant le type réel d'un objet à l'exécution :

```java
public final Class getClass()
```

**Caractéristiques clés** :

- **Finale** : Ne peut pas être redéfinie.
- **Temps d'exécution** : Retourne toujours la classe concrète de l'objet, pas le type déclaré.
- **Utile pour** :
    - L'introspection (reflection)
    - Les comparaisons de type
    - Les opérations génériques

**Exemple** :

```java
Object obj = new ArrayList<>();
Class clazz = obj.getClass(); 
System.out.println(clazz.getName()); // "java.util.ArrayList"
```

## Différence entre `.class` et `getClass()`

| `.class`                                         | `getClass()`                      |
|--------------------------------------------------|-----------------------------------|
| Littéral utilisé à la **compilation**            | Méthode appelée à l'**exécution** |
| Fonctionne avec tous types (y compris primitifs) | Ne fonctionne qu'avec des objets  |
| Retourne le type déclaré                         | Retourne le type concret          |

**Exemple** :

```java
Number num = new Integer(5);
Class c1 = num.getClass();    // Integer.class
Class c2 = Number.class;      // Number.class
```

## Cas d'usage avancés

1. **Reflection** :

```java
Method[] methods = "hello".getClass().getDeclaredMethods();
```

2. **Comparaison dynamique** :

```java
if(obj1.getClass() == obj2.getClass()){
    // Même classe concrète
}
```

3. **Pattern Factory** :

```java
public static T createInstance(Class clazz) {
    return clazz.newInstance();
}
```

Cette combinaison (`Class` + `getClass()`) est au cœur de nombreux mécanismes avancés en Java comme la reflection, les
proxies dynamiques ou les annotations runtime.

??? note "Citations"

    - [1] https://www.scholarhat.com/tutorial/java/java-class-and-object
    - [2] https://www.scaler.com/topics/class-class-in-java/
    - [3] https://www.programiz.com/java-programming/reflection
    - [4] https://www.programiz.com/java-programming/library/object/getclass
    - [5] https://codegym.cc/groups/posts/java-object-getclass-method
    - [6] https://www.scaler.com/topics/getclass-in-java/
    - [7] https://www.tutorialspoint.com/java/lang/object_getclass.htm
    - [8] https://docs.vultr.com/java/standard-library/java/lang/Object/getClass
    - [9] https://docs.oracle.com/javase/tutorial/reflect/class/classNew.html
    - [10] https://learn.microsoft.com/en-us/dotnet/api/java.lang.class?view=net-android-35.0
    - [11] https://stackoverflow.com/questions/15078935/what-does-class-mean-in-java
    - [12] https://www.baeldung.com/java-reflection
    - [13] https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html
    - [14] https://stackoverflow.com/questions/2215843/using-reflection-in-java-to-create-a-new-instance-with-the-reference-variable-ty
    - [15] https://stackabuse.com/javas-object-methods-getclass/
    - [16] https://stackoverflow.com/questions/36233435/could-someone-explain-me-the-getclass-method-in-java
    - [17] https://www.w3schools.com/java/java_classes.asp
    - [18] https://www.oracle.com/technical-resources/articles/java/javareflection.html
    - [19] https://stackoverflow.com/questions/7398088/do-we-need-the-method-getclass-from-java-lang-object
    - [20] https://www.youtube.com/watch?v=_dIDcwIeOgI



-------

??? info "Utilisation de l'IA"
      Page rédigée en partie avec l'aide d'un assistant IA, principalement à l'aide de Perplexity AI, avec le *LLM*
      **Claude 3.5 Sonnet**. L'IA a été utilisée pour générer des explications, des exemples et/ou des suggestions de
      structure. Toutes les informations ont été vérifiées, éditées et complétées par l'auteur.
     