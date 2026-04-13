---
icon: material/file-document-outline
---

# 5. Corrigé exercices : Classes abstraites et interfaces

## **Corrigé : Partie 1 – Compréhension**

---

### **Exercice 1 : Questions théoriques**

#### **1. Différence fondamentale entre une classe abstraite et une interface en Java**

- **Classe abstraite** : Peut contenir des champs d’instance, des méthodes abstraites et des méthodes concrètes. Elle
  est utilisée pour factoriser du code commun à plusieurs classes apparentées.
- **Interface** : Ne peut contenir que des constantes (`public static final`) et des déclarations de méthodes (
  abstraites, par défaut ou statiques). Elle définit un contrat que les classes doivent respecter.

#### **2. Quand utiliser une classe abstraite plutôt qu’une interface, et vice versa ?**

- **Classe abstraite** : Utilisée lorsque plusieurs classes partagent une logique commune (méthodes concrètes) et une
  relation "est-un" (héritage).
- **Interface** : Utilisée pour définir un comportement commun à des classes non apparentées (relation "peut-faire").
  Permet l’héritage multiple de comportements.

#### **3. Peut-on implémenter plusieurs interfaces dans une classe ? Peut-on hériter de plusieurs classes abstraites ? Pourquoi ?**

- **Interfaces** : Oui, une classe peut implémenter plusieurs interfaces (héritage multiple de contrats).
- **Classes abstraites** : Non, Java ne supporte pas l’héritage multiple de classes (problème du diamant).

#### **4. Méthode par défaut dans une interface**

Une méthode par défaut permet d’ajouter une implémentation à une interface sans casser les classes existantes qui
l’implémentent.
Exemple :

```java
interface Volant {
    void voler();

    default void atterrir() {
        System.out.println("Atterrissage en cours...");
    }
}
```

#### **5. Concept de "contrat" dans les interfaces**

Un contrat est un ensemble de méthodes que toute classe implémentant l’interface doit fournir. Cela garantit que les
objets répondent à un comportement attendu.

---

### **Exercice 2 : Vrai ou Faux**

1. **Vrai** : Une classe abstraite peut contenir des champs non statiques et non finals.
2. **Faux** : Une interface ne peut pas contenir d’implémentations de méthodes (sauf méthodes par défaut et statiques).
3. **Vrai** : Une classe peut implémenter plusieurs interfaces mais ne peut hériter que d’une seule classe abstraite.
4. **Vrai** : Les méthodes d’une interface sont implicitement `public` et `abstract`.
5. **Faux** : Une classe abstraite ne peut pas être instanciée directement.

---

## **Corrigé : Partie 2 – Pratique**

---

### **Exercice 3 : Implémentation de classes abstraites et d’interfaces**

#### **Classe abstraite `Forme`**

```java
public abstract class Forme {
    protected String nom;

    public Forme(String nom) {
        this.nom = nom;
    }

    public abstract double calculerAire();

    public abstract double calculerPerimetre();

    public void afficherDetails() {
        System.out.println("Nom : " + nom);
        System.out.println("Aire : " + calculerAire());
        System.out.println("Périmètre : " + calculerPerimetre());
    }
}
```

#### **Interface `Deplacable`**

```java
public interface Deplacable {
    void deplacer(double dx, double dy);
}
```

#### **Classe `Cercle`**

```java
public class Cercle extends Forme implements Deplacable {
    private double rayon;

    public Cercle(String nom, double rayon) {
        super(nom);
        this.rayon = rayon;
    }

    @Override
    public double calculerAire() {
        return Math.PI * rayon * rayon;
    }

    @Override
    public double calculerPerimetre() {
        return 2 * Math.PI * rayon;
    }

    @Override
    public void deplacer(double dx, double dy) {
        System.out.println(nom + " se déplace de (" + dx + ", " + dy + ")");
    }
}
```

#### **Classe `Rectangle`**

```java
public class Rectangle extends Forme implements Deplacable {
    private double longueur;
    private double largeur;

    public Rectangle(String nom, double longueur, double largeur) {
        super(nom);
        this.longueur = longueur;
        this.largeur = largeur;
    }

    @Override
    public double calculerAire() {
        return longueur * largeur;
    }

    @Override
    public double calculerPerimetre() {
        return 2 * (longueur + largeur);
    }

    @Override
    public void deplacer(double dx, double dy) {
        System.out.println(nom + " se déplace de (" + dx + ", " + dy + ")");
    }
}
```

#### **Classe `Main`**

```java
public class Main {
    public static void main(String[] args) {
        Cercle cercle = new Cercle("Cercle 1", 5.0);
        cercle.afficherDetails();
        cercle.deplacer(2.0, 3.0);

        Rectangle rectangle = new Rectangle("Rectangle 1", 4.0, 6.0);
        rectangle.afficherDetails();
        rectangle.deplacer(1.0, 1.0);
    }
}
```

---

### **Exercice 4 : Correction et amélioration de code**

#### **Erreurs et mauvaises pratiques**

1. Le champ `nom` n’est pas initialisé dans `Oiseau`.
2. La méthode `manger()` n’est pas déclarée `public` (or, les méthodes de classe abstraite sont implicitement `public`).
3. Pas de constructeur pour initialiser `nom`.

#### **Version corrigée**

```java
abstract class Animal {
    protected String nom;

    public Animal(String nom) {
        this.nom = nom;
    }

    public abstract void manger();
}

interface Volant {
    void voler();
}

class Oiseau extends Animal implements Volant {
    public Oiseau(String nom) {
        super(nom);
    }

    @Override
    public void manger() {
        System.out.println(nom + " mange des graines.");
    }

    @Override
    public void voler() {
        System.out.println(nom + " vole dans le ciel.");
    }
}

public class Main {
    public static void main(String[] args) {
        Oiseau pigeon = new Oiseau("Pigeon");
        pigeon.manger();
        pigeon.voler();
    }
}
```


-------

??? info "Utilisation de l'IA"
    Page rédigée en partie avec l'aide d'un assistant IA. L'IA a été utilisée pour générer des 
    explications, des exemples et/ou des suggestions de structure. Toutes les informations ont 
    été vérifiées, éditées et complétées par l'auteur.
