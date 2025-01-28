# Solutions : exercices partie 2

## Question 1

### Version avec Tableau

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;

public class LectureNombresTableau {
    /**
     * Lit les nombres d'un fichier et les stocke dans un tableau
     * @param nomFichier le chemin du fichier à lire
     * @return un tableau contenant les nombres lus
     * @throws IOException si une erreur de lecture survient
     * @throws NumberFormatException si le fichier contient des données non numériques
     */
    public static int[] lireFichierNombres(String nomFichier) throws IOException {
        // Compte d'abord le nombre de lignes pour dimensionner le tableau
        Path path = Paths.get(nomFichier);
        int nombreLignes = (int) Files.lines(path).count();
        int[] nombres = new int[nombreLignes];

        try (BufferedReader reader = new BufferedReader(new FileReader(nomFichier))) {
            String ligne;
            int index = 0;
            while ((ligne = reader.readLine()) != null) {
                nombres[index] = Integer.parseInt(ligne.trim());
                index++;
            }
        }
        return nombres;
    }

    /**
     * Affiche les nombres du tableau
     * @param nombres le tableau de nombres à afficher
     */
    public static void afficherNombres(int[] nombres) {
        if (nombres == null) {
            throw new IllegalArgumentException("Le tableau ne peut pas être null");
        }

        for (int i = 0; i < nombres.length; i++) {
            System.out.printf("Nombre %d: %d%n", i + 1, nombres[i]);
        }
    }

    public static void main(String[] args) {
        try {
            int[] nombres = lireFichierNombres("nombres.txt");
            afficherNombres(nombres);
        } catch (IOException e) {
            System.err.println("Erreur lors de la lecture du fichier: " + e.getMessage());
        } catch (NumberFormatException e) {
            System.err.println("Le fichier contient des données non numériques: " + e.getMessage());
        }
    }
}
```

### Version avec ArrayList

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;
import java.util.ArrayList;

public class LectureNombresArrayList {
    /**
     * Lit les nombres d'un fichier et les stocke dans une ArrayList
     * @param nomFichier le chemin du fichier à lire
     * @return une ArrayList contenant les nombres lus
     * @throws IOException si une erreur de lecture survient
     * @throws NumberFormatException si le fichier contient des données non numériques
     */
    public static ArrayList<Integer> lireFichierNombres(String nomFichier) throws IOException {
        ArrayList<Integer> nombres = new ArrayList<>();

        try (BufferedReader reader = new BufferedReader(new FileReader(nomFichier))) {
            String ligne;
            while ((ligne = reader.readLine()) != null) {
                nombres.add(Integer.parseInt(ligne.trim()));
            }
        }
        return nombres;
    }

    /**
     * Affiche les nombres de l'ArrayList
     * @param nombres l'ArrayList de nombres à afficher
     */
    public static void afficherNombres(ArrayList<Integer> nombres) {
        if (nombres == null) {
            throw new IllegalArgumentException("La liste ne peut pas être null");
        }

        for (int i = 0; i < nombres.size(); i++) {
            System.out.printf("Nombre %d: %d%n", i + 1, nombres.get(i));
        }
    }

    public static void main(String[] args) {
        try {
            ArrayList<Integer> nombres = lireFichierNombres("nombres.txt");
            afficherNombres(nombres);
        } catch (IOException e) {
            System.err.println("Erreur lors de la lecture du fichier: " + e.getMessage());
        } catch (NumberFormatException e) {
            System.err.println("Le fichier contient des données non numériques: " + e.getMessage());
        }
    }
}
```

### Comparaison des Versions

**Avantages de la version tableau**:

- Utilisation mémoire fixe et prévisible
- Accès direct aux éléments plus rapide
- Performance légèrement meilleure pour les opérations de lecture séquentielle

**Avantages de la version ArrayList**:

- Pas besoin de connaître la taille à l'avance
- Taille dynamique qui s'adapte automatiquement
- Code plus simple et plus lisible
- Plus flexible pour les modifications futures

**Points communs aux deux versions**:

- Gestion des exceptions (IOException, NumberFormatException)
- Validation des entrées (vérification null)
- Documentation JavaDoc complète
- Structure de code similaire

Pour tester ces implémentations, créez un fichier `nombres.txt` contenant des nombres entiers, un par ligne, comme:

```
42
17
123
456
789
```

## Question 2

### Version avec Tableau

```java
import java.io.PrintWriter;
import java.io.IOException;
import java.util.Random;

public class GenerateurNombresTableau {
    /**
     * Génère N nombres aléatoires entre MIN et MAX inclus
     * @param n nombre de nombres à générer
     * @param min valeur minimum
     * @param max valeur maximum
     * @return tableau contenant les nombres générés
     * @throws IllegalArgumentException si n < 0 ou min > max
     */
    public static int[] genererNombres(int n, int min, int max) {
        if (n < 0) {
            throw new IllegalArgumentException("Le nombre de valeurs à générer doit être positif");
        }
        if (min > max) {
            throw new IllegalArgumentException("La valeur minimum doit être inférieure ou égale à la valeur maximum");
        }

        Random random = new Random();
        int[] nombres = new int[n];

        for (int i = 0; i < n; i++) {
            nombres[i] = random.nextInt(max - min + 1) + min;
        }

        return nombres;
    }

    /**
     * Sauvegarde les nombres dans un fichier
     * @param nombres tableau de nombres à sauvegarder
     * @param nomFichier nom du fichier de destination
     * @throws IOException si une erreur d'écriture survient
     */
    public static void sauvegarderNombres(int[] nombres, String nomFichier) throws IOException {
        if (nombres == null) {
            throw new IllegalArgumentException("Le tableau ne peut pas être null");
        }

        try (PrintWriter writer = new PrintWriter(nomFichier)) {
            for (int nombre : nombres) {
                writer.println(nombre);
            }
        }
    }

    public static void main(String[] args) {
        try {
            int[] nombres = genererNombres(10, 1, 100);
            sauvegarderNombres(nombres, "nombres_aleatoires.txt");
            System.out.println("Génération et sauvegarde réussies!");
        } catch (IOException e) {
            System.err.println("Erreur lors de la sauvegarde: " + e.getMessage());
        } catch (IllegalArgumentException e) {
            System.err.println("Erreur de paramètres: " + e.getMessage());
        }
    }
}
```

### Version avec ArrayList

```java
import java.io.PrintWriter;
import java.io.IOException;
import java.util.ArrayList;
import java.util.Random;

public class GenerateurNombresArrayList {
    /**
     * Génère N nombres aléatoires entre MIN et MAX inclus
     * @param n nombre de nombres à générer
     * @param min valeur minimum
     * @param max valeur maximum
     * @return ArrayList contenant les nombres générés
     * @throws IllegalArgumentException si n < 0 ou min > max
     */
    public static ArrayList<Integer> genererNombres(int n, int min, int max) {
        if (n < 0) {
            throw new IllegalArgumentException("Le nombre de valeurs à générer doit être positif");
        }
        if (min > max) {
            throw new IllegalArgumentException("La valeur minimum doit être inférieure ou égale à la valeur maximum");
        }

        Random random = new Random();
        ArrayList<Integer> nombres = new ArrayList<>();

        for (int i = 0; i < n; i++) {
            nombres.add(random.nextInt(max - min + 1) + min);
        }

        return nombres;
    }

    /**
     * Sauvegarde les nombres dans un fichier
     * @param nombres ArrayList de nombres à sauvegarder
     * @param nomFichier nom du fichier de destination
     * @throws IOException si une erreur d'écriture survient
     */
    public static void sauvegarderNombres(ArrayList<Integer> nombres, String nomFichier) throws IOException {
        if (nombres == null) {
            throw new IllegalArgumentException("La liste ne peut pas être null");
        }

        try (PrintWriter writer = new PrintWriter(nomFichier)) {
            for (Integer nombre : nombres) {
                writer.println(nombre);
            }
        }
    }

    public static void main(String[] args) {
        try {
            ArrayList<Integer> nombres = genererNombres(10, 1, 100);
            sauvegarderNombres(nombres, "nombres_aleatoires.txt");
            System.out.println("Génération et sauvegarde réussies!");
        } catch (IOException e) {
            System.err.println("Erreur lors de la sauvegarde: " + e.getMessage());
        } catch (IllegalArgumentException e) {
            System.err.println("Erreur de paramètres: " + e.getMessage());
        }
    }
}
```

### Comparaison des Versions

**Avantages de la version tableau**:

- Allocation mémoire en une seule fois
- Performance légèrement meilleure pour un nombre fixe d'éléments
- Moins de surcharge mémoire car pas de structure de données dynamique

**Avantages de la version ArrayList**:

- Plus flexible si on veut modifier le nombre d'éléments après la génération
- Syntaxe plus claire avec les méthodes add()
- Plus facile à modifier si on veut ajouter des fonctionnalités

**Points communs aux deux versions**:

- Même logique de génération de nombres aléatoires
- Validation similaire des paramètres d'entrée
- Gestion identique des exceptions
- Même approche pour la sauvegarde dans un fichier

Pour tester ces implémentations, exécutez simplement le main de l'une ou l'autre version. Le programme créera un
fichier "nombres_aleatoires.txt" contenant les nombres générés, un par ligne.

## Question 3

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class StatistiquesFichier {
    /**
     * Structure pour stocker les statistiques du fichier
     */
    public static class Statistiques {
        private int nombreLignes;
        private int nombreMots;
        private int nombreCaracteres;

        public Statistiques(int lignes, int mots, int caracteres) {
            this.nombreLignes = lignes;
            this.nombreMots = mots;
            this.nombreCaracteres = caracteres;
        }

        @Override
        public String toString() {
            return String.format("""
                            Statistiques du fichier:
                            Nombre de lignes: %d
                            Nombre de mots: %d
                            Nombre de caractères: %d""",
                    nombreLignes, nombreMots, nombreCaracteres);
        }
    }

    /**
     * Analyse un fichier texte et retourne ses statistiques
     * @param nomFichier le nom du fichier à analyser
     * @throws IOException si une erreur de lecture survient
     * @throws IllegalArgumentException si le nom du fichier est null ou vide
     */
    public static void analyserFichier(String nomFichier) throws IOException {
        if (nomFichier == null || nomFichier.trim().isEmpty()) {
            throw new IllegalArgumentException("Le nom du fichier ne peut pas être null ou vide");
        }

        int lignes = 0;
        int mots = 0;
        int caracteres = 0;

        try (BufferedReader reader = new BufferedReader(new FileReader(nomFichier))) {
            String ligne;
            while ((ligne = reader.readLine()) != null) {
                lignes++;

                // Compte les caractères (sans les retours à la ligne)
                caracteres += ligne.length();

                // Compte les mots (en ignorant les espaces multiples)
                if (!ligne.trim().isEmpty()) {
                    mots += ligne.trim().split("\\s+").length;
                }
            }
        }

        Statistiques stats = new Statistiques(lignes, mots, caracteres);
        System.out.println(stats);
    }

    /**
     * Version alternative qui retourne les statistiques au lieu de les afficher
     */
    public static Statistiques obtenirStatistiques(String nomFichier) throws IOException {
        if (nomFichier == null || nomFichier.trim().isEmpty()) {
            throw new IllegalArgumentException("Le nom du fichier ne peut pas être null ou vide");
        }

        int lignes = 0;
        int mots = 0;
        int caracteres = 0;

        try (BufferedReader reader = new BufferedReader(new FileReader(nomFichier))) {
            String ligne;
            while ((ligne = reader.readLine()) != null) {
                lignes++;
                caracteres += ligne.length();
                if (!ligne.trim().isEmpty()) {
                    mots += ligne.trim().split("\\s+").length;
                }
            }
        }

        return new Statistiques(lignes, mots, caracteres);
    }

    public static void main(String[] args) {
        try {
            // Test avec un fichier exemple
            analyserFichier("test.txt");

            // Test avec la version alternative
            Statistiques stats = obtenirStatistiques("test.txt");
            System.out.println("\nStatistiques obtenues via la méthode alternative:");
            System.out.println(stats);

        } catch (IOException e) {
            System.err.println("Erreur lors de la lecture du fichier: " + e.getMessage());
        } catch (IllegalArgumentException e) {
            System.err.println("Erreur de paramètre: " + e.getMessage());
        }
    }
}
```

### Points Importants de l'Implémentation

**Caractéristiques principales**:

- Utilisation d'une classe interne `Statistiques` pour encapsuler les résultats
- Deux versions de la méthode d'analyse : une qui affiche directement et une qui retourne un objet
- Gestion appropriée des espaces multiples dans le comptage des mots
- Prise en compte des lignes vides

**Gestion des cas particuliers**:

- Validation du nom de fichier
- Gestion des lignes vides dans le comptage des mots
- Traitement correct des espaces multiples

**Tests**

Pour tester cette implémentation, créez un fichier `test.txt` avec du contenu varié, par exemple:

```text
Ceci est une ligne de test
avec des    espaces   multiples

Et une ligne après une ligne vide
```

### Améliorations Possibles

1. **Comptage plus précis des caractères**:

```java
// Version améliorée du comptage des caractères
caracteres +=ligne.

replaceAll("\\s","").

length(); // Ignore les espaces
```

2. **Support de différents types de séparateurs de mots**:

```java
// Version plus robuste du comptage des mots
mots +=ligne.

trim().

split("[\\s,;.]+").length;
```

3. **Ajout de statistiques supplémentaires**:

- Nombre de paragraphes
- Nombre de caractères sans espaces
- Longueur moyenne des mots
- Nombre de phrases

Cette implémentation offre une base solide pour l'analyse de fichiers texte, avec une bonne gestion des erreurs et une
structure de code claire et maintenable.

## Question 4

### Version avec Tableau

```java
import java.io.*;
import java.nio.file.*;
import java.util.Arrays;

public class TriFichierTableau {
    /**
     * Lit toutes les lignes d'un fichier dans un tableau
     * @param nomFichier le nom du fichier à lire
     * @return un tableau contenant toutes les lignes du fichier
     * @throws IOException si une erreur de lecture survient
     */
    public static String[] lireLignesFichier(String nomFichier) throws IOException {
        if (nomFichier == null || nomFichier.trim().isEmpty()) {
            throw new IllegalArgumentException("Le nom du fichier ne peut pas être null ou vide");
        }

        Path path = Paths.get(nomFichier);
        return Files.readAllLines(path).toArray(new String[0]);
    }

    /**
     * Supprime les lignes vides d'un tableau de chaînes
     * @param lignes le tableau de lignes à traiter
     * @return un nouveau tableau sans les lignes vides
     */
    public static String[] supprimerLignesVides(String[] lignes) {
        if (lignes == null) {
            throw new IllegalArgumentException("Le tableau de lignes ne peut pas être null");
        }

        return Arrays.stream(lignes)
                .filter(ligne -> ligne != null && !ligne.trim().isEmpty())
                .sorted()
                .toArray(String[]::new);
    }

    /**
     * Sauvegarde un tableau de lignes dans un fichier
     * @param lignes le tableau de lignes à sauvegarder
     * @param nomFichier le nom du fichier de destination
     * @throws IOException si une erreur d'écriture survient
     */
    public static void sauvegarderLignes(String[] lignes, String nomFichier) throws IOException {
        if (lignes == null) {
            throw new IllegalArgumentException("Le tableau de lignes ne peut pas être null");
        }
        if (nomFichier == null || nomFichier.trim().isEmpty()) {
            throw new IllegalArgumentException("Le nom du fichier ne peut pas être null ou vide");
        }

        try (PrintWriter writer = new PrintWriter(new FileWriter(nomFichier))) {
            for (String ligne : lignes) {
                writer.println(ligne);
            }
        }
    }

    public static void main(String[] args) {
        try {
            // Lecture du fichier
            String[] lignes = lireLignesFichier("input.txt");

            // Traitement et tri
            String[] lignesTriees = supprimerLignesVides(lignes);

            // Sauvegarde
            sauvegarderLignes(lignesTriees, "output.txt");

            System.out.println("Traitement terminé avec succès!");
        } catch (IOException e) {
            System.err.println("Erreur d'entrée/sortie: " + e.getMessage());
        } catch (IllegalArgumentException e) {
            System.err.println("Erreur de paramètre: " + e.getMessage());
        }
    }
}
```

### Version avec ArrayList

```java
import java.io.*;
import java.nio.file.*;
import java.util.ArrayList;
import java.util.Collections;

public class TriFichierArrayList {
    /**
     * Lit toutes les lignes d'un fichier dans une ArrayList
     * @param nomFichier le nom du fichier à lire
     * @return une ArrayList contenant toutes les lignes du fichier
     * @throws IOException si une erreur de lecture survient
     */
    public static ArrayList<String> lireLignesFichier(String nomFichier) throws IOException {
        if (nomFichier == null || nomFichier.trim().isEmpty()) {
            throw new IllegalArgumentException("Le nom du fichier ne peut pas être null ou vide");
        }

        Path path = Paths.get(nomFichier);
        return new ArrayList<>(Files.readAllLines(path));
    }

    /**
     * Supprime les lignes vides d'une ArrayList de chaînes
     * @param lignes l'ArrayList de lignes à traiter
     * @return une nouvelle ArrayList sans les lignes vides
     */
    public static ArrayList<String> supprimerLignesVides(ArrayList<String> lignes) {
        if (lignes == null) {
            throw new IllegalArgumentException("La liste de lignes ne peut pas être null");
        }

        ArrayList<String> resultat = new ArrayList<>();

        for (String ligne : lignes) {
            if (ligne != null && !ligne.trim().isEmpty()) {
                resultat.add(ligne);
            }
        }

        Collections.sort(resultat);
        return resultat;
    }

    /**
     * Sauvegarde une ArrayList de lignes dans un fichier
     * @param lignes l'ArrayList de lignes à sauvegarder
     * @param nomFichier le nom du fichier de destination
     * @throws IOException si une erreur d'écriture survient
     */
    public static void sauvegarderLignes(ArrayList<String> lignes, String nomFichier) throws IOException {
        if (lignes == null) {
            throw new IllegalArgumentException("La liste de lignes ne peut pas être null");
        }
        if (nomFichier == null || nomFichier.trim().isEmpty()) {
            throw new IllegalArgumentException("Le nom du fichier ne peut pas être null ou vide");
        }

        try (PrintWriter writer = new PrintWriter(new FileWriter(nomFichier))) {
            for (String ligne : lignes) {
                writer.println(ligne);
            }
        }
    }

    public static void main(String[] args) {
        try {
            // Lecture du fichier
            ArrayList<String> lignes = lireLignesFichier("input.txt");

            // Traitement et tri
            ArrayList<String> lignesTriees = supprimerLignesVides(lignes);

            // Sauvegarde
            sauvegarderLignes(lignesTriees, "output.txt");

            System.out.println("Traitement terminé avec succès!");
        } catch (IOException e) {
            System.err.println("Erreur d'entrée/sortie: " + e.getMessage());
        } catch (IllegalArgumentException e) {
            System.err.println("Erreur de paramètre: " + e.getMessage());
        }
    }
}
```

### Comparaison des Versions

**Avantages de la version tableau**:

- Utilisation mémoire fixe
- Performance légèrement meilleure pour les opérations de lecture séquentielle
- Utilisation efficace de l'API Stream pour le filtrage et le tri

**Avantages de la version ArrayList**:

- Plus flexible pour les modifications dynamiques
- Code plus simple à comprendre
- Pas besoin de gérer la taille du tableau
- Plus facile à modifier si besoin d'ajouter des fonctionnalités

**Test de l'implémentation**

Créez un fichier `input.txt` avec le contenu suivant:

```text
Ligne 3
   
Ligne 1

Ligne 2

```

Le fichier `output.txt` devrait contenir:

```text
Ligne 1
Ligne 2
Ligne 3
```

Les deux versions produiront le même résultat, avec les lignes triées alphabétiquement et sans lignes vides.

## Question 5

### Version avec Tableau

```java
import java.io.*;
import java.nio.file.*;
import java.util.Arrays;

public class FusionFichiersTableau {
    /**
     * Fusionne deux fichiers triés en ordre croissant
     * @param fichier1 premier fichier source
     * @param fichier2 deuxième fichier source
     * @return tableau contenant tous les nombres fusionnés et triés
     * @throws IOException si une erreur de lecture survient
     */
    public static int[] fusionnerFichiers(String fichier1, String fichier2) throws IOException {
        if (fichier1 == null || fichier2 == null) {
            throw new IllegalArgumentException("Les noms de fichiers ne peuvent pas être null");
        }

        // Lecture des fichiers
        int[] nombres1 = lireFichierNombres(fichier1);
        int[] nombres2 = lireFichierNombres(fichier2);

        // Création du tableau résultat
        int[] resultat = new int[nombres1.length + nombres2.length];

        // Fusion des tableaux triés
        int i = 0, j = 0, k = 0;
        while (i < nombres1.length && j < nombres2.length) {
            if (nombres1[i] <= nombres2[j]) {
                resultat[k++] = nombres1[i++];
            } else {
                resultat[k++] = nombres2[j++];
            }
        }

        // Ajout des éléments restants
        while (i < nombres1.length) {
            resultat[k++] = nombres1[i++];
        }
        while (j < nombres2.length) {
            resultat[k++] = nombres2[j++];
        }

        return resultat;
    }

    /**
     * Lit un fichier de nombres et retourne un tableau trié
     */
    private static int[] lireFichierNombres(String nomFichier) throws IOException {
        return Files.lines(Paths.get(nomFichier))
                .map(String::trim)
                .filter(s -> !s.isEmpty())
                .mapToInt(Integer::parseInt)
                .sorted()
                .toArray();
    }

    /**
     * Sauvegarde le résultat de la fusion dans un fichier
     * @param nombres tableau de nombres à sauvegarder
     * @param fichierSortie nom du fichier de destination
     * @throws IOException si une erreur d'écriture survient
     */
    public static void sauvegarderFusion(int[] nombres, String fichierSortie) throws IOException {
        if (nombres == null) {
            throw new IllegalArgumentException("Le tableau de nombres ne peut pas être null");
        }

        try (PrintWriter writer = new PrintWriter(new FileWriter(fichierSortie))) {
            for (int nombre : nombres) {
                writer.println(nombre);
            }
        }
    }

    public static void main(String[] args) {
        try {
            int[] nombresFusionnes = fusionnerFichiers("fichier1.txt", "fichier2.txt");
            sauvegarderFusion(nombresFusionnes, "fusion.txt");
            System.out.println("Fusion réussie!");
        } catch (IOException e) {
            System.err.println("Erreur d'entrée/sortie: " + e.getMessage());
        } catch (NumberFormatException e) {
            System.err.println("Format de nombre invalide: " + e.getMessage());
        }
    }
}
```

### Version avec ArrayList

```java
import java.io.*;
import java.nio.file.*;
import java.util.ArrayList;
import java.util.Collections;

public class FusionFichiersArrayList {
    /**
     * Fusionne deux fichiers triés en ordre croissant
     * @param fichier1 premier fichier source
     * @param fichier2 deuxième fichier source
     * @return ArrayList contenant tous les nombres fusionnés et triés
     * @throws IOException si une erreur de lecture survient
     */
    public static ArrayList<Integer> fusionnerFichiers(String fichier1, String fichier2) throws IOException {
        if (fichier1 == null || fichier2 == null) {
            throw new IllegalArgumentException("Les noms de fichiers ne peuvent pas être null");
        }

        // Lecture des fichiers
        ArrayList<Integer> nombres1 = lireFichierNombres(fichier1);
        ArrayList<Integer> nombres2 = lireFichierNombres(fichier2);

        // Création de la liste résultat
        ArrayList<Integer> resultat = new ArrayList<>();

        // Indices pour la fusion
        int i = 0, j = 0;

        // Fusion des listes triées
        while (i < nombres1.size() && j < nombres2.size()) {
            if (nombres1.get(i) <= nombres2.get(j)) {
                resultat.add(nombres1.get(i++));
            } else {
                resultat.add(nombres2.get(j++));
            }
        }

        // Ajout des éléments restants
        while (i < nombres1.size()) {
            resultat.add(nombres1.get(i++));
        }
        while (j < nombres2.size()) {
            resultat.add(nombres2.get(j++));
        }

        return resultat;
    }

    /**
     * Lit un fichier de nombres et retourne une ArrayList triée
     */
    private static ArrayList<Integer> lireFichierNombres(String nomFichier) throws IOException {
        ArrayList<Integer> nombres = new ArrayList<>();

        Files.lines(Paths.get(nomFichier))
                .map(String::trim)
                .filter(s -> !s.isEmpty())
                .mapToInt(Integer::parseInt)
                .forEach(nombres::add);

        Collections.sort(nombres);
        return nombres;
    }

    /**
     * Sauvegarde le résultat de la fusion dans un fichier
     * @param nombres ArrayList de nombres à sauvegarder
     * @param fichierSortie nom du fichier de destination
     * @throws IOException si une erreur d'écriture survient
     */
    public static void sauvegarderFusion(ArrayList<Integer> nombres, String fichierSortie) throws IOException {
        if (nombres == null) {
            throw new IllegalArgumentException("La liste de nombres ne peut pas être null");
        }

        try (PrintWriter writer = new PrintWriter(new FileWriter(fichierSortie))) {
            for (Integer nombre : nombres) {
                writer.println(nombre);
            }
        }
    }

    public static void main(String[] args) {
        try {
            ArrayList<Integer> nombresFusionnes = fusionnerFichiers("fichier1.txt", "fichier2.txt");
            sauvegarderFusion(nombresFusionnes, "fusion.txt");
            System.out.println("Fusion réussie!");
        } catch (IOException e) {
            System.err.println("Erreur d'entrée/sortie: " + e.getMessage());
        } catch (NumberFormatException e) {
            System.err.println("Format de nombre invalide: " + e.getMessage());
        }
    }
}
```

### Comparaison des Versions

**Avantages de la version tableau**:

- Performance mémoire optimale pour les grands ensembles de données
- Accès direct aux éléments plus rapide
- Meilleure performance pour la fusion elle-même

**Avantages de la version ArrayList**:

- Code plus flexible et maintenable
- Pas besoin de gérer la taille manuellement
- Plus facile à modifier pour ajouter des fonctionnalités

**Test de l'implémentation**

Créez deux fichiers de test:

`fichier1.txt`:

```text
1
3
5
7
9
```

`fichier2.txt`:

```text
2
4
6
8
10
```

Le fichier `fusion.txt` devrait contenir:

```text
1
2
3
4
5
6
7
8
9
10
```

Les deux versions produiront le même résultat, avec tous les nombres triés en ordre croissant.

## Question 6

### Version avec Tableau

```java
import java.io.*;
import java.nio.file.*;
import java.util.*;

public class RechercheMotsTableau {
    /**
     * Recherche toutes les occurrences d'un mot dans un fichier
     * @param mot le mot à rechercher
     * @param nomFichier le nom du fichier à analyser
     * @return tableau contenant les numéros des lignes où le mot apparaît
     * @throws IOException si une erreur de lecture survient
     */
    public static int[] rechercherMot(String mot, String nomFichier) throws IOException {
        if (mot == null || mot.trim().isEmpty()) {
            throw new IllegalArgumentException("Le mot à rechercher ne peut pas être null ou vide");
        }
        if (nomFichier == null || nomFichier.trim().isEmpty()) {
            throw new IllegalArgumentException("Le nom du fichier ne peut pas être null ou vide");
        }

        // Utilisation d'une liste temporaire pour stocker les numéros de ligne
        List<Integer> lignesTrouvees = new ArrayList<>();
        String motRecherche = mot.toLowerCase().trim();

        try (BufferedReader reader = new BufferedReader(new FileReader(nomFichier))) {
            String ligne;
            int numeroLigne = 1;

            while ((ligne = reader.readLine()) != null) {
                if (ligne.toLowerCase().contains(motRecherche)) {
                    lignesTrouvees.add(numeroLigne);
                }
                numeroLigne++;
            }
        }

        // Conversion de la liste en tableau
        return lignesTrouvees.stream().mapToInt(Integer::intValue).toArray();
    }

    /**
     * Affiche les résultats de la recherche
     * @param mot le mot recherché
     * @param lignes tableau des numéros de lignes où le mot a été trouvé
     */
    public static void afficherResultats(String mot, int[] lignes) {
        if (mot == null || lignes == null) {
            throw new IllegalArgumentException("Les paramètres ne peuvent pas être null");
        }

        if (lignes.length == 0) {
            System.out.printf("Le mot '%s' n'a pas été trouvé dans le fichier.%n", mot);
            return;
        }

        System.out.printf("Le mot '%s' a été trouvé %d fois:%n", mot, lignes.length);
        for (int ligne : lignes) {
            System.out.printf("- Ligne %d%n", ligne);
        }
    }

    public static void main(String[] args) {
        try {
            String motRecherche = "exemple";
            int[] lignesTrouvees = rechercherMot(motRecherche, "texte.txt");
            afficherResultats(motRecherche, lignesTrouvees);
        } catch (IOException e) {
            System.err.println("Erreur lors de la lecture du fichier: " + e.getMessage());
        } catch (IllegalArgumentException e) {
            System.err.println("Erreur de paramètre: " + e.getMessage());
        }
    }
}
```

### Version avec ArrayList

```java
import java.io.*;
import java.nio.file.*;
import java.util.ArrayList;

public class RechercheMotsArrayList {
    /**
     * Recherche toutes les occurrences d'un mot dans un fichier
     * @param mot le mot à rechercher
     * @param nomFichier le nom du fichier à analyser
     * @return ArrayList contenant les numéros des lignes où le mot apparaît
     * @throws IOException si une erreur de lecture survient
     */
    public static ArrayList<Integer> rechercherMot(String mot, String nomFichier) throws IOException {
        if (mot == null || mot.trim().isEmpty()) {
            throw new IllegalArgumentException("Le mot à rechercher ne peut pas être null ou vide");
        }
        if (nomFichier == null || nomFichier.trim().isEmpty()) {
            throw new IllegalArgumentException("Le nom du fichier ne peut pas être null ou vide");
        }

        ArrayList<Integer> lignesTrouvees = new ArrayList<>();
        String motRecherche = mot.toLowerCase().trim();

        try (BufferedReader reader = new BufferedReader(new FileReader(nomFichier))) {
            String ligne;
            int numeroLigne = 1;

            while ((ligne = reader.readLine()) != null) {
                if (ligne.toLowerCase().contains(motRecherche)) {
                    lignesTrouvees.add(numeroLigne);
                }
                numeroLigne++;
            }
        }

        return lignesTrouvees;
    }

    /**
     * Affiche les résultats de la recherche
     * @param mot le mot recherché
     * @param lignes ArrayList des numéros de lignes où le mot a été trouvé
     */
    public static void afficherResultats(String mot, ArrayList<Integer> lignes) {
        if (mot == null || lignes == null) {
            throw new IllegalArgumentException("Les paramètres ne peuvent pas être null");
        }

        if (lignes.isEmpty()) {
            System.out.printf("Le mot '%s' n'a pas été trouvé dans le fichier.%n", mot);
            return;
        }

        System.out.printf("Le mot '%s' a été trouvé %d fois:%n", mot, lignes.size());
        for (int ligne : lignes) {
            System.out.printf("- Ligne %d%n", ligne);
        }
    }

    /**
     * Version améliorée qui retourne aussi le contexte
     */
    public static ArrayList<String> rechercherMotAvecContexte(String mot, String nomFichier, int contexteLignes)
            throws IOException {
        ArrayList<String> resultats = new ArrayList<>();
        String motRecherche = mot.toLowerCase().trim();

        List<String> toutesLignes = Files.readAllLines(Paths.get(nomFichier));

        for (int i = 0; i < toutesLignes.size(); i++) {
            if (toutesLignes.get(i).toLowerCase().contains(motRecherche)) {
                StringBuilder contexte = new StringBuilder();

                // Ajout du contexte avant
                for (int j = Math.max(0, i - contexteLignes); j < i; j++) {
                    contexte.append(String.format("  %d: %s%n", j + 1, toutesLignes.get(j)));
                }

                // Ligne avec le mot trouvé
                contexte.append(String.format("→ %d: %s%n", i + 1, toutesLignes.get(i)));

                // Ajout du contexte après
                for (int j = i + 1; j <= Math.min(toutesLignes.size() - 1, i + contexteLignes); j++) {
                    contexte.append(String.format("  %d: %s%n", j + 1, toutesLignes.get(j)));
                }

                resultats.add(contexte.toString());
            }
        }

        return resultats;
    }

    public static void main(String[] args) {
        try {
            String motRecherche = "exemple";

            // Version simple
            ArrayList<Integer> lignesTrouvees = rechercherMot(motRecherche, "texte.txt");
            afficherResultats(motRecherche, lignesTrouvees);

            // Version avec contexte
            System.out.println("\nRecherche avec contexte (2 lignes avant/après):");
            ArrayList<String> resultatsAvecContexte = rechercherMotAvecContexte(motRecherche, "texte.txt", 2);
            for (String contexte : resultatsAvecContexte) {
                System.out.println(contexte);
            }

        } catch (IOException e) {
            System.err.println("Erreur lors de la lecture du fichier: " + e.getMessage());
        } catch (IllegalArgumentException e) {
            System.err.println("Erreur de paramètre: " + e.getMessage());
        }
    }
}
```

### Comparaison des Versions

**Avantages de la version tableau**:

- Performance mémoire légèrement meilleure
- Accès direct aux éléments plus rapide
- Plus simple pour les opérations de base

**Avantages de la version ArrayList**:

- Plus flexible pour ajouter/supprimer des résultats
- Facilité d'extension (comme montré avec la version avec contexte)
- Code plus lisible et maintenable

**Test de l'implémentation**

Créez un fichier `texte.txt` avec le contenu suivant:

```text
Ceci est un exemple de texte
pour tester notre programme.
Il contient plusieurs lignes
avec le mot exemple répété
à différents endroits du texte.
Voici un autre exemple.
```

Les deux versions produiront des résultats similaires, mais la version ArrayList offre plus de flexibilité pour des
fonctionnalités avancées comme l'affichage du contexte.

La version avec ArrayList inclut également une amélioration significative avec la méthode `rechercherMotAvecContexte`
qui montre les lignes avant et après chaque occurrence du mot recherché, ce qui est très utile pour comprendre le
contexte des résultats.


-------

??? info "Utilisation de l'IA"
      Page rédigée en partie avec l'aide d'un assistant IA, principalement à l'aide de Perplexity AI, avec le *LLM*
      **Claude 3.5 Sonnet**. L'IA a été utilisée pour générer des explications, des exemples et/ou des suggestions de
      structure. Toutes les informations ont été vérifiées, éditées et complétées par l'auteur.