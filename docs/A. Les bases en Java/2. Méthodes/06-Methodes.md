# 🔸6🔸Méthodes

## Déclaration de méthodes

La syntaxe de base d'une méthode :

```java
typeRetour nomMethode(typeParam1 param1, typeParam2 param2) {
    // Corps de la méthode
    return valeur; // si nécessaire
}
```

Exemples simples :

```java
public class ExemplesMethodes {
    // Méthode sans paramètre et sans retour
    void afficherBonjour() {
        System.out.println("Bonjour!");
    }

    // Méthode avec paramètres et retour
    int additionner(int a, int b) {
        return a + b;
    }

    // Méthode avec plusieurs paramètres
    double calculerMoyenne(double... notes) {
        double somme = 0;
        for (double note : notes) {
            somme += note;
        }
        return somme / notes.length;
    }
}
```

## Passage de paramètres

En Java, les paramètres sont toujours passés **par valeur**. Cependant, pour les objets, c'est la référence qui est
passée par valeur.

**Exemple avec types primitifs** :

```java
public class ExempleSwap {
    // Cette méthode ne fonctionne PAS
    void swapQuiNeMarchePas(int a, int b) {
        int temp = a;
        a = b;
        b = temp;
    }

    public static void main(String[] args) {
        int x = 5;
        int y = 10;

        ExempleSwap exemple = new ExempleSwap();
        exemple.swapQuiNeMarchePas(x, y);

        // x est toujours 5, y est toujours 10
        System.out.printf("x=%d, y=%d%n", x, y);
    }
}
```

**Solution avec une classe wrapper** :

```java
public class ExempleSwapFonctionnel {
    // Classe pour contenir une valeur modifiable
    class Nombre {
        int valeur;

        Nombre(int valeur) {
            this.valeur = valeur;
        }
    }

    void swap(Nombre a, Nombre b) {
        int temp = a.valeur;
        a.valeur = b.valeur;
        b.valeur = temp;
    }

    public static void main(String[] args) {
        ExempleSwapFonctionnel exemple = new ExempleSwapFonctionnel();

        Nombre x = exemple.new Nombre(5);
        Nombre y = exemple.new Nombre(10);

        System.out.printf("Avant: x=%d, y=%d%n", x.valeur, y.valeur);
        exemple.swap(x, y);
        System.out.printf("Après: x=%d, y=%d%n", x.valeur, y.valeur);
    }
}
```

## Exemple pratique complet

```java
public class ManipulationTableaux {
    // Méthode qui modifie un tableau (le tableau est modifié car c'est une référence)
    void doubleElements(int[] tableau) {
        for (int i = 0; i < tableau.length; i++) {
            tableau[i] *= 2;
        }
    }

    // Méthode qui retourne un nouveau tableau
    int[] creerTableauDouble(int[] original) {
        int[] resultat = new int[original.length];
        for (int i = 0; i < original.length; i++) {
            resultat[i] = original[i] * 2;
        }
        return resultat;
    }

    // Méthode avec plusieurs paramètres de types différents
    String formaterNote(String nomEtudiant, double note, boolean afficherMention) {
        String mention = "";
        if (afficherMention) {
            mention = note >= 60 ? " (Réussite)" : " (Échec)";
        }
        return String.format("%s a obtenu %.1f%s", nomEtudiant, note, mention);
    }

    public static void main(String[] args) {
        ManipulationTableaux manip = new ManipulationTableaux();

        // Test avec tableau (passage par référence)
        int[] nombres = {1, 2, 3, 4, 5};
        System.out.println("Avant modification:");
        for (int n : nombres) System.out.print(n + " ");
        System.out.println();

        manip.doubleElements(nombres);

        System.out.println("Après modification:");
        for (int n : nombres) System.out.print(n + " ");
        System.out.println();

        // Test avec création d'un nouveau tableau
        int[] original = {1, 2, 3};
        int[] double1 = manip.creerTableauDouble(original);

        System.out.println("\nTableau original inchangé:");
        for (int n : original) System.out.print(n + " ");
        System.out.println();

        System.out.println("Nouveau tableau:");
        for (int n : double1) System.out.print(n + " ");
        System.out.println();

        // Test du formatage de note
        String resultat = manip.formaterNote("Alice", 85.5, true);
        System.out.println("\n" + resultat);
    }
}
```

## Points clés à retenir

1. Les types primitifs sont toujours passés par valeur
2. Les objets sont passés par référence (techniquement, la référence est passée par valeur)
3. Pour modifier des valeurs primitives, il faut :
    - Soit retourner la nouvelle valeur
    - Soit encapsuler la valeur dans un objet
    - Soit utiliser un tableau
4. Les tableaux et les objets peuvent être modifiés à l'intérieur des méthodes
5. Une méthode peut avoir :
    - Aucun paramètre
    - Un ou plusieurs paramètres
    - Un nombre variable de paramètres (varargs)
    - Un type de retour ou void



-------

!!! note "Note"
    Page rédigée en partie avec l'aide d'un assistant IA, principalement à l'aide de Perplexity AI, avec le *LLM* 
    **Claude 3.5 Sonnet**. L'IA a été utilisée pour générer des explications, des exemples et/ou des suggestions de 
    structure. Toutes les informations ont été vérifiées, éditées et complétées par l'auteur.