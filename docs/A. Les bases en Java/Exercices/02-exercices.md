# Exercices, partie 2

Pour chacun des exercices suivants, créez une ou plusieurs méthodes statiques qui font ce qui est décrit, et testez
vos méthodes dans un `main`. Vous pouvez créer une classe différente pour chaque question. Faites 2 versions de chaque
question : une avec des tableaux, l'autre avec des `ArrayList`.

Pour chaque exercice, vous devriez :

- Gérer les exceptions appropriées
- Valider les entrées
- Documenter le code
- Créer des tests unitaires simples (optionnel)
- Comparer les avantages/inconvénients des deux versions (tableau vs ArrayList)

## Questions

## Exercice 1 - Lecture de Nombres

Créez un programme qui lit un fichier contenant un nombre entier par ligne et qui stocke ces nombres dans un tableau ou
une `ArrayList`. Implémentez les méthodes suivantes :

```java
// Version tableau
public static int[] lireFichierNombres(String nomFichier)

public static void afficherNombres(int[] nombres)

// Version ArrayList
public static ArrayList<Integer> lireFichierNombres(String nomFichier)

public static void afficherNombres(ArrayList<Integer> nombres)
```

## Exercice 2 - Générateur Aléatoire

Développez un programme qui génère N nombres aléatoires entre MIN et MAX et les sauvegarde dans un fichier (un nombre
par ligne). Implémentez :

```java
// Version tableau
public static int[] genererNombres(int n, int min, int max)

public static void sauvegarderNombres(int[] nombres, String nomFichier)

// Version ArrayList
public static ArrayList<Integer> genererNombres(int n, int min, int max)

public static void sauvegarderNombres(ArrayList<Integer> nombres, String nomFichier)
```

## Exercice 3 - Statistiques Fichier

Créez un programme qui analyse un fichier texte et affiche le nombre de lignes, de mots et de caractères. Implémentez :

```java
public static void analyserFichier(String nomFichier)
```

## Exercice 4 - Tri de Fichier

Développez un programme qui lit un fichier texte, enlève les lignes vides, trie les lignes restantes et sauvegarde le
résultat dans un nouveau fichier. Implémentez :

```java
// Version tableau
public static String[] lireLignesFichier(String nomFichier)

public static String[] supprimerLignesVides(String[] lignes)

public static void sauvegarderLignes(String[] lignes, String nomFichier)

// Version ArrayList
public static ArrayList<String> lireLignesFichier(String nomFichier)

public static ArrayList<String> supprimerLignesVides(ArrayList<String> lignes)

public static void sauvegarderLignes(ArrayList<String> lignes, String nomFichier)
```

## Exercice 5 - Fusion de Fichiers**

Créez un programme qui fusionne deux fichiers triés en ordre croissant en gardant l'ordre. Implémentez :

```java
// Version tableau
public static int[] fusionnerFichiers(String fichier1, String fichier2)

public static void sauvegarderFusion(int[] nombres, String fichierSortie)

// Version ArrayList
public static ArrayList<Integer> fusionnerFichiers(String fichier1, String fichier2)

public static void sauvegarderFusion(ArrayList<Integer> nombres, String fichierSortie)
```

## Exercice 6 - Recherche de Mots

Développez un programme qui cherche toutes les occurrences d'un mot dans un fichier et retourne les numéros de lignes où
le mot apparaît. Implémentez :

```java
// Version tableau
public static int[] rechercherMot(String mot, String nomFichier)

public static void afficherResultats(String mot, int[] lignes)

// Version ArrayList
public static ArrayList<Integer> rechercherMot(String mot, String nomFichier)

public static void afficherResultats(String mot, ArrayList<Integer> lignes)
```
