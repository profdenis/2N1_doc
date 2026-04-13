---
icon: material/file-document-outline
---

# 1. Interfaces

Une interface en Java est un contrat qui définit un ensemble de méthodes qu'une classe doit implémenter. Elle permet de
définir un comportement commun que plusieurs classes non liées peuvent partager.

## Exemple

```java
// Définition de l'interface
public interface Animal {
    void faireBruit();

    void seDeplacer();
}

// Implémentation de l'interface
public class Chat implements Animal {
    @Override
    public void faireBruit() {
        System.out.println("Miaou!");
    }

    @Override
    public void seDeplacer() {
        System.out.println("Le chat marche silencieusement");
    }
}

// Une autre implémentation
public class Chien implements Animal {
    @Override
    public void faireBruit() {
        System.out.println("Wouf!");
    }

    @Override
    public void seDeplacer() {
        System.out.println("Le chien court joyeusement");
    }
}
```

## Comparaison entre Interfaces et Classes Abstraites

| Caractéristique   | Interface                                                     | Classe Abstraite                                            |
|-------------------|---------------------------------------------------------------|-------------------------------------------------------------|
| Méthodes          | Uniquement abstraites (par défaut) et statiques               | Peut avoir des méthodes abstraites et concrètes             |
| Attributs         | Constants uniquement (public static final)                    | Peut avoir des variables d'instance                         |
| Héritage multiple | Une classe peut implémenter plusieurs interfaces              | Une classe ne peut hériter que d'une seule classe abstraite |
| Constructeur      | Ne peut pas avoir de constructeur                             | Peut avoir des constructeurs                                |
| Implémentation    | Ne peut pas contenir d'implémentation (sauf méthodes default) | Peut contenir des implémentations partielles                |

### **Les méthodes par défaut dans les interfaces (Java 8 et +)**

Depuis Java 8, les interfaces peuvent contenir des **méthodes par défaut** (ou *default methods*), qui permettent
d’ajouter une implémentation concrète à une méthode sans forcer les classes qui implémentent l’interface à la redéfinir.
Cela répond à un besoin crucial : **faire évoluer une interface sans casser le code existant**.

#### **Pourquoi utiliser des méthodes par défaut ?**

- **Compatibilité ascendante** : Avant Java 8, ajouter une nouvelle méthode à une interface obligeait toutes les classes
  l’implémentant à fournir une implémentation, sous peine de ne plus compiler. Les méthodes par défaut résolvent ce
  problème en fournissant une implémentation "par défaut".
- **Réutilisation de code** : Elles permettent de factoriser du code commun à plusieurs implémentations, directement
  dans l’interface.
- **Flexibilité** : Les classes peuvent choisir de redéfinir la méthode par défaut si nécessaire, ou d’utiliser
  l’implémentation fournie.

#### **Syntaxe et exemple**

Une méthode par défaut est déclarée avec le mot-clé `default` :

```java
public interface Volant {
    void voler(); // Méthode abstraite

    default void atterrir() { // Méthode par défaut
        System.out.println("Atterrissage standard en cours...");
    }
}
```

Ici, toute classe implémentant `Volant` **héritera automatiquement** de l’implémentation d’`atterrir()`, mais pourra la
redéfinir si besoin.

#### **Cas d’usage typique**

Les méthodes par défaut sont souvent utilisées pour :

- Ajouter des fonctionnalités optionnelles à une interface (ex : `Iterator.forEach`).
- Fournir des comportements génériques (ex : `Collection.stream()`).

#### **Conflits et règles de résolution**

Si une classe implémente deux interfaces contenant une méthode par défaut de même signature, elle **doit redéfinir**
cette méthode pour lever l’ambiguïté. Par exemple :

```java
interface A {
    default void faireQuelqueChose() {
        System.out.println("A");
    }
}

interface B {
    default void faireQuelqueChose() {
        System.out.println("B");
    }
}

class MaClasse implements A, B {
    @Override
    public void faireQuelqueChose() {
        A.super.faireQuelqueChose(); // Appel explicite à l’implémentation de A
    }
}
```

---

### **Le concept de contrat dans les interfaces**

En programmation orientée objet, une **interface** définit un **contrat** que toute classe l’implémentant **doit
respecter**. Ce contrat est un ensemble de :

- **Méthodes abstraites** (signatures sans implémentation).
- **Constantes** (`public static final`).
- **Comportements attendus** (via les méthodes par défaut ou statiques).

#### **Pourquoi parler de "contrat" ?**

- **Garantie de comportement** : Une interface garantit que toute classe qui l’implémente **fournira** les méthodes
  déclarées, ce qui permet aux autres parties du code de s’y fier sans connaître les détails d’implémentation.
- **Polymorphisme** : Le contrat permet de traiter des objets de classes différentes de manière uniforme, tant qu’ils
  implémentent la même interface. Par exemple :
  ```java
  List<String> maListe = new ArrayList<>(); // ArrayList implémente List
  ```
  Ici, `maListe` peut être utilisée comme une `List`, peu importe son implémentation concrète.

#### **Exemple de contrat**

Prenons l’interface `List` en Java :

```java
public interface List<E> {
    void add(E element); // Contrat : toute List doit permettre d’ajouter un élément

    E get(int index);    // Contrat : toute List doit permettre de récupérer un élément par index
    // ...
}
```

Toute classe implémentant `List` (comme `ArrayList` ou `LinkedList`) **doit** fournir une implémentation de `add` et
`get`, sinon elle ne compilera pas.

#### **Avantages du contrat**

1. **Découplage** : Le code utilisant l’interface n’a pas besoin de connaître les détails d’implémentation.
2. **Extensibilité** : On peut ajouter de nouvelles implémentations sans modifier le code client.
3. **Testabilité** : Les interfaces facilitent l’utilisation de *mocks* ou de *stubs* pour les tests unitaires.

#### **Différence avec l’héritage**

- **Héritage (classe abstraite)** : Définit une relation "est-un" (ex : un `Chien` **est un** `Animal`).
- **Interface (contrat)** : Définit une relation "peut-faire" (ex : un `Oiseau` **peut voler**, donc il implémente
  `Volant`).

---

### **Synthèse pédagogique**

- **Méthodes par défaut** : Outils pour faire évoluer les interfaces sans casser le code existant, tout en permettant
  une personnalisation.
- **Contrat** : Fondement des interfaces, assurant que les classes offrent un comportement prévisible et
  interchangeable.

---


## Points Clés à Retenir

Les interfaces sont particulièrement utiles pour:

- Définir un contrat que plusieurs classes doivent respecter
- Permettre le polymorphisme sans créer une hiérarchie d'héritage
- Créer des systèmes faiblement couplés

Les classes abstraites sont préférables quand:

- On veut partager du code entre plusieurs classes étroitement liées
- On a besoin de déclarer des attributs non constants
- On souhaite fournir une implémentation partielle d'une classe


-------

??? info "Utilisation de l'IA"
    Page rédigée en partie avec l'aide d'un assistant IA. L'IA a été utilisée pour générer des 
    explications, des exemples et/ou des suggestions de structure. Toutes les informations ont 
    été vérifiées, éditées et complétées par l'auteur.
