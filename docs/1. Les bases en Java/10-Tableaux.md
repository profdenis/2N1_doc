# 10- Tableaux

## Tableaux de types primitifs

```java
public class ExemplesTableauxPrimitifs {
    public static void main(String[] args) {
        // Déclaration et initialisation
        int[] nombres = new int[5];        // Tableau de 5 zéros
        int[] valeurs = {1, 2, 3, 4, 5};   // Initialisation directe

        // Accès et modification
        nombres[0] = 10;
        System.out.println("Premier nombre: " + nombres[0]);

        // Parcours avec for classique
        for (int i = 0; i < valeurs.length; i++) {
            System.out.println("Index " + i + ": " + valeurs[i]);
        }

        // Parcours avec for-each
        for (int valeur : valeurs) {
            System.out.println("Valeur: " + valeur);
        }
    }
}
```

## Tableaux de types références

```java
public class ExemplesTableauxReferences {
    public static void main(String[] args) {
        // Déclaration et initialisation
        String[] noms = new String[3];         // Tableau de 3 null
        String[] fruits = {"pomme", "banane", "orange"};

        // Accès et modification
        noms[0] = "Alice";
        noms[1] = "Bob";
        noms[2] = "Charlie";

        // Parcours et manipulation
        for (String nom : noms) {
            if (nom != null) {
                System.out.println(nom.toUpperCase());
            }
        }
    }
}
```

## Organisation en mémoire

**Variables simples** :

| Type   | Stockage                           | Taille                                                        |
|--------|------------------------------------|---------------------------------------------------------------|
| int    | Stack                              | 4 bytes fixes                                                 |
| String | Stack (référence) + Heap (contenu) | 4/8 bytes pour la référence + taille variable pour le contenu |

```java
public class ExempleMemoire {
    public static void main(String[] args) {
        // Sur la pile (stack)
        int nombre = 42;          // 4 bytes directement sur la pile

        // Référence sur la pile, objet sur le tas (heap)
        String texte = "Bonjour"; // 4/8 bytes (référence) + taille du contenu
    }
}
```

**Tableaux** :

```java
public class ExempleTableauxMemoire {
    public static void main(String[] args) {
        // Tableau de int
        int[] nombres = new int[5];

        // Tableau de String
        String[] textes = new String[5];

        // Remplissage
        nombres[0] = 42;
        textes[0] = "Bonjour";
    }
}
```

Organisation en mémoire pour `nombres` :

```
Stack:
nombres -> [référence vers le tableau]

Heap:
[42][0][0][0][0]  // Les valeurs sont stockées directement
```

Organisation en mémoire pour `textes` :

```
Stack:
textes -> [référence vers le tableau]

Heap:
[ref1][null][null][null][null]  // Tableau de références
    |
    v
"Bonjour"  // Objet String stocké séparément
```

## Exemple détaillé avec manipulation

```java
public class DemoMemoire {
    public static void main(String[] args) {
        // Tableau de int
        int[] nombres = new int[3];
        nombres[0] = 10;
        nombres[1] = 20;
        nombres[2] = 30;

        // Tableau de String
        String[] mots = new String[3];
        mots[0] = "Java";
        mots[1] = "Python";
        mots[2] = "C++";

        // Modification d'une valeur
        nombres[0] = 15;          // Modifie directement la valeur
        mots[0] = "JavaScript";   // Crée une nouvelle chaîne, met à jour la référence

        // Copie de tableaux
        int[] copieNombres = nombres.clone();      // Copie superficielle suffisante
        String[] copieMots = mots.clone();         // Copie superficielle (références)
    }
}
```

## Points clés à retenir

1. **Tableaux de types primitifs** :
    - Stockent directement les valeurs
    - Taille fixe en mémoire
    - Accès direct aux valeurs
    - Copie = duplication des valeurs

2. **Tableaux de types références** :
    - Stockent des références vers des objets
    - Double indirection pour accéder aux valeurs
    - Les objets référencés peuvent être de taille variable
    - Copie superficielle = duplication des références seulement

3. **Impact sur les performances** :

```java
public class PerformanceExample {
    public static void main(String[] args) {
        int[] nombres = new int[1000000];          // Allocation contiguë
        String[] textes = new String[1000000];     // Tableau de références

        // Plus efficace : accès direct
        for (int i = 0; i < nombres.length; i++) {
            nombres[i] = i;
        }

        // Moins efficace : création d'objets + gestion des références
        for (int i = 0; i < textes.length; i++) {
            textes[i] = String.valueOf(i);
        }
    }
}
```

4. **Implications pour le garbage collector** :

```java
public class GCExample {
    public static void main(String[] args) {
        int[] nombres = new int[100];      // Un seul objet à gérer
        String[] textes = new String[100];  // Jusqu'à 101 objets à gérer

        // Remplacement d'une valeur
        nombres[0] = 42;                    // Pas d'impact sur le GC
        textes[0] = "Nouveau";             // Ancien String peut être collecté
    }
}
```

La compréhension de ces différences est cruciale pour :

- L'optimisation des performances
- La gestion efficace de la mémoire
- Le choix des structures de données appropriées
- La prévention des fuites de mémoire