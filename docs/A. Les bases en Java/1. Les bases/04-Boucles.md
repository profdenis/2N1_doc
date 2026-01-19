---
icon: material/file-document-outline
---

# 4. Boucles

## Boucle while

La boucle `while` s'exécute tant que sa condition est vraie :

```java
public class ExempleWhile {
    public static void main(String[] args) {
        int compteur = 0;

        while (compteur < 5) {
            System.out.println("Compteur: " + compteur);
            compteur++;
        }

        // Exemple avec validation
        int nombre = 100;
        while (nombre > 1) {
            if (nombre % 2 == 0) {
                nombre = nombre / 2;
            } else {
                nombre = nombre * 3 + 1;
            }
            System.out.println("Nombre actuel: " + nombre);
        }
    }
}
```

## Boucle do-while

La boucle `do-while` s'exécute au moins une fois :

```java
public class ExempleDoWhile {
    public static void main(String[] args) {
        int compteur = 0;

        do {
            System.out.println("Itération: " + compteur);
            compteur++;
        } while (compteur < 3);

        // Exemple avec accumulation
        int somme = 0;
        int nombre = 1;
        do {
            somme += nombre;
            nombre++;
        } while (nombre <= 5);
        System.out.println("Somme finale: " + somme);
    }
}
```

## Boucle for

**Boucle for classique** :

```java
public class ExempleFor {
    public static void main(String[] args) {
        // Boucle simple
        for (int i = 0; i < 5; i++) {
            System.out.println("Index: " + i);
        }

        // Boucle avec pas différent
        for (int i = 0; i <= 10; i += 2) {
            System.out.println("Nombre pair: " + i);
        }

        // Boucle décroissante
        for (int i = 5; i > 0; i--) {
            System.out.println("Compte à rebours: " + i);
        }
    }
}
```

**Boucle for-each** :

```java
public class ExempleForEach {
    public static void main(String[] args) {
        // Avec un tableau
        int[] nombres = {1, 2, 3, 4, 5};
        for (int nombre : nombres) {
            System.out.println("Valeur: " + nombre);
        }

        // Avec une collection de chaînes
        String[] fruits = {"pomme", "banane", "orange"};
        for (String fruit : fruits) {
            System.out.println("Fruit: " + fruit);
        }
    }
}
```

## Exemple pratique combiné

```java
public class AnalyseNotes {
    public static void main(String[] args) {
        int[] notes = {85, 92, 78, 65, 88, 72};
        int somme = 0;
        int noteMax = Integer.MIN_VALUE;
        int noteMin = Integer.MAX_VALUE;

        // Utilisation de for-each pour le calcul
        for (int note : notes) {
            somme += note;
            noteMax = Math.max(noteMax, note);
            noteMin = Math.min(noteMin, note);
        }

        double moyenne = (double) somme / notes.length;

        // Utilisation de while pour l'analyse
        int i = 0;
        int notesSupMoyenne = 0;
        while (i < notes.length) {
            if (notes[i] > moyenne) {
                notesSupMoyenne++;
            }
            i++;
        }

        // Affichage des statistiques
        System.out.printf("Moyenne: %.2f%n", moyenne);
        System.out.printf("Note maximale: %d%n", noteMax);
        System.out.printf("Note minimale: %d%n", noteMin);
        System.out.printf("Nombre de notes supérieures à la moyenne: %d%n", notesSupMoyenne);

        // Utilisation de for pour afficher les notes avec leur statut
        for (int j = 0; j < notes.length; j++) {
            String statut = notes[j] >= moyenne ? "≥ moyenne" : "< moyenne";
            System.out.printf("Note %d: %d (%s)%n", j + 1, notes[j], statut);
        }
    }
}
```

## Instructions de contrôle de boucle

```java
public class ControleBoucles {
    public static void main(String[] args) {
        // Exemple de break
        for (int i = 0; i < 10; i++) {
            if (i == 5) {
                break; // Sort de la boucle
            }
            System.out.println("Valeur: " + i);
        }

        // Exemple de continue
        for (int i = 0; i < 5; i++) {
            if (i == 2) {
                continue; // Passe à l'itération suivante
            }
            System.out.println("Nombre: " + i);
        }

        // Exemple avec étiquette (label)
        exterieur:
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                if (i == 1 && j == 1) {
                    break exterieur; // Sort des deux boucles
                }
                System.out.printf("i=%d, j=%d%n", i, j);
            }
        }
    }
}
```



-------

??? info "Utilisation de l'IA"
    Page rédigée en partie avec l'aide d'un assistant IA. L'IA a été utilisée pour générer des 
    explications, des exemples et/ou des suggestions de structure. Toutes les informations ont 
    été vérifiées, éditées et complétées par l'auteur.