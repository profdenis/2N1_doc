---
icon: material/file-document-outline
---

# 4. Exercices : Classes abstraites et interfaces

## **Partie 1 : Compréhension**

### **Exercice 1 : Questions théoriques**

Répondez aux questions suivantes en justifiant vos réponses avec des exemples de code si nécessaire.

1. **Quelle est la différence fondamentale entre une classe abstraite et une interface en Java ?**
2. **Quand utiliseriez-vous une classe abstraite plutôt qu’une interface, et vice versa ?**
3. **Peut-on implémenter plusieurs interfaces dans une classe ? Peut-on hériter de plusieurs classes abstraites ?
   Pourquoi ?**
4. **Qu’est-ce qu’une méthode par défaut dans une interface ? Donnez un exemple d’utilisation.**
5. **Expliquez le concept de "contrat" dans le contexte des interfaces.**

---

### **Exercice 2 : Vrai ou Faux**

Indiquez si les affirmations suivantes sont vraies ou fausses, et corrigez celles qui sont fausses.

1. Une classe abstraite peut contenir des champs non statiques et non finals.
2. Une interface peut contenir des implémentations de méthodes (hors méthodes par défaut et statiques).
3. Une classe peut implémenter plusieurs interfaces mais ne peut hériter que d’une seule classe abstraite.
4. Les méthodes d’une interface sont implicitement `public` et `abstract`.
5. Une classe abstraite peut être instanciée directement.

---

## **Partie 2 : Pratique**

### **Exercice 3 : Implémentation de classes abstraites et d’interfaces**

Créez un programme Java qui modélise un système de gestion de formes géométriques.

1. **Définissez une classe abstraite `Forme`** avec :
    - Un champ `nom` (de type `String`).
    - Une méthode abstraite `double calculerAire()`.
    - Une méthode abstraite `double calculerPerimetre()`.
    - Une méthode concrète `void afficherDetails()` qui affiche le nom de la forme, son aire et son périmètre.

2. **Définissez une interface `Deplacable`** avec :
    - Une méthode `void deplacer(double dx, double dy)` qui simule le déplacement de la forme.

3. **Créez deux classes concrètes** qui héritent de `Forme` et implémentent `Deplacable` :
    - `Cercle` (avec un champ `rayon`).
    - `Rectangle` (avec des champs `longueur` et `largeur`).

4. **Dans une classe `Main`**, créez des instances de `Cercle` et `Rectangle`, appelez leurs méthodes pour calculer
   l’aire et le périmètre, puis déplacez-les.

---

### **Exercice 4 : Correction et amélioration de code**

Le code suivant contient des erreurs ou des mauvaises pratiques. Corrigez-le et justifiez vos modifications.

```java
abstract class Animal {
    String nom;

    abstract void manger();
}

interface Volant {
    void voler();
}

class Oiseau extends Animal implements Volant {
    void manger() {
        System.out.println(nom + " mange des graines.");
    }

    public void voler() {
        System.out.println(nom + " vole dans le ciel.");
    }
}

public class Main {
    public static void main(String[] args) {
        Oiseau pigeon = new Oiseau();
        pigeon.manger();
        pigeon.voler();
    }
}
```

**Questions :**

1. Quelles erreurs ou mauvaises pratiques observez-vous ?
2. Proposez une version corrigée et améliorée du code.

-------

??? info "Utilisation de l'IA"
    Page rédigée en partie avec l'aide d'un assistant IA. L'IA a été utilisée pour générer des 
    explications, des exemples et/ou des suggestions de structure. Toutes les informations ont 
    été vérifiées, éditées et complétées par l'auteur.
