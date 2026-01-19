---
icon: material/file-document-outline
---

# 12. Gestion des fichiers texte

## *try-with-resources* vs. *try* classique

La différence est fondamentale et concerne la gestion des ressources. Comparons les deux approches :

### *Try-with-resources* (avec parenthèses)

```java
try (BufferedReader lecteur = new BufferedReader(new FileReader(fichier));
     PrintWriter ecrivain = new PrintWriter(destination)) {
    // Code utilisant lecteur et ecrivain
} catch (IOException e) {
    // Gestion des erreurs
}

```

**Avantages**

- Fermeture automatique des ressources, même en cas d'exception
- Les ressources sont fermées dans l'ordre inverse de leur création
- Plus concis et plus sûr
- Impossible d'oublier de fermer une ressource
- Les ressources sont fermées même si on quitte la méthode avec un `return`

### Try classique

```java
BufferedReader lecteur = null;
PrintWriter ecrivain = null;
try {
    lecteur = new BufferedReader(new FileReader(fichier));
    ecrivain = new PrintWriter(destination);
    // Code utilisant lecteur et ecrivain
} catch (IOException e) {
    // Gestion des erreurs
} finally {
    try {
        if (lecteur != null) lecteur.close();
        if (ecrivain != null) ecrivain.close();
    } catch (IOException e) {
        // Nouvelle exception pendant la fermeture
    }
}
```

**Inconvénients**

- Code plus verbeux
- Risque d'oublier de fermer une ressource
- Nécessite un bloc `finally` explicite
- Doit gérer les exceptions lors de la fermeture
- Risque de masquer l'exception originale si une exception survient pendant la fermeture

### Important à noter

Le *try-with-resources* (introduit en Java 7) :

- Ne fonctionne qu'avec les classes qui implémentent l'interface `AutoCloseable`
- Est considéré comme la meilleure pratique pour la gestion des ressources
- Réduit considérablement les risques de fuites de ressources
- Produit un code plus maintenable et plus sûr


## Lecture d'un fichier texte

La lecture d'un fichier texte en Java peut être réalisée de plusieurs manières. Voici un exemple simple utilisant
`BufferedReader` qui permet de lire le fichier ligne par ligne.

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class LectureFichier {
    public static void main(String[] args) {
        // Le chemin vers notre fichier, relativement au dossier du projet ou au dossier courant
        String cheminFichier = "fichiers/exemple1.txt";
        int nombreLignesNonVides = 0;

        // Utilisation de try-with-resources pour fermer automatiquement les ressources
        try (BufferedReader lecteur = new BufferedReader(new FileReader(cheminFichier))) {
            String ligne;

            // Lecture du fichier ligne par ligne
            while ((ligne = lecteur.readLine()) != null) {
                // On utilise trim() pour enlever les espaces au début et à la fin
                if (!ligne.trim().isEmpty()) {
                    nombreLignesNonVides++;
                }
            }

            System.out.println("Nombre de lignes non vides : " + nombreLignesNonVides);

        } catch (IOException e) {
            System.err.println("Erreur lors de la lecture du fichier : " + e.getMessage());
        }
    }
}
```

### Explications du code

**Importation des classes nécessaires**

- `BufferedReader` : classe qui permet de lire efficacement le texte ligne par ligne
- `FileReader` : classe de base pour lire des fichiers texte
- `IOException` : exception qui peut survenir lors des opérations de lecture

**Points importants à noter**

1. L'utilisation du bloc `try-with-resources` (avec les parenthèses après le try) permet de fermer automatiquement le
   fichier après utilisation.

2. La méthode `readLine()` retourne :
    - Une ligne de texte quand il y a du contenu à lire
    - `null` quand on arrive à la fin du fichier

3. La méthode `trim()` enlève les espaces au début et à la fin de la chaîne de caractères. Une ligne qui ne contient que
   des espaces sera considérée comme vide après le `trim()`.

4. La gestion des exceptions est importante, car plusieurs erreurs peuvent survenir :
    - Le fichier n'existe pas
    - Le fichier n'est pas accessible en lecture
    - Une erreur survient pendant la lecture.

Ce code représente la façon moderne et recommandée de lire un fichier en Java, car il :

- Gère correctement la fermeture des ressources
- Utilise une lecture efficace ligne par ligne
- Gère les exceptions de manière appropriée

## Copier le contenu d'un fichier

Voici un exemple qui utilise `BufferedReader` pour lire un fichier et `PrintWriter` pour écrire dans un nouveau fichier
avec des numéros de ligne :

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.PrintWriter;
import java.io.IOException;

public class AjoutNumeroLignes {
    public static void main(String[] args) {
        String fichierSource = "source.txt";
        String fichierDestination = "destination.txt";
        int numeroLigne = 1;

        try (BufferedReader lecteur = new BufferedReader(new FileReader(fichierSource));
             PrintWriter ecrivain = new PrintWriter(fichierDestination)) {

            String ligne;
            while ((ligne = lecteur.readLine()) != null) {
                // Format du numéro de ligne sur 3 caractères avec des zéros devant
                String numero = String.format("%03d", numeroLigne);
                ecrivain.println(numero + " | " + ligne);
                numeroLigne++;
            }

            System.out.println("Fichier traité avec succès");

        } catch (IOException e) {
            System.err.println("Erreur lors du traitement des fichiers : " + e.getMessage());
        }
    }
}
```

### Explications du code

**Éléments principaux**

- `BufferedReader` est utilisé pour la lecture efficace du fichier source
- `PrintWriter` permet d'écrire facilement dans le fichier de destination
- `String.format()` formate le numéro de ligne sur 3 caractères

**Particularités**

- Les numéros de ligne sont formatés avec des zéros devant (001, 002, etc.)
- Un séparateur " | " est ajouté entre le numéro et le contenu de la ligne
- Le `try-with-resources` ferme automatiquement les deux fichiers
- Si le fichier source contient "Bonjour" et "Monde", le fichier destination contiendra :
  ```txt
  001 | Bonjour
  002 | Monde
  ```

Cette approche est efficace, car elle :

- Lit et écrit les fichiers ligne par ligne
- Gère correctement les ressources
- Ajoute un formatage clair et lisible aux numéros de ligne.

??? note "Citations"
    - [1] https://www.digitalocean.com/community/tutorials/java-read-file-line-by-line
    - [2] https://howtodoinjava.com/java/io/linenumber-reader-example/
    - [3] https://stackoverflow.com/questions/23023472/how-to-add-line-numbers-to-a-text-file
    - [4] https://www.geeksforgeeks.org/java-program-to-read-content-from-one-file-and-write-it-into-another-file/
    - [5] https://www.reddit.com/r/golang/comments/jmc6ow/append_line_numbers_to_a_text_file/
    - [6] https://www.youtube.com/watch?v=IodQ6yhBbbU



-------

??? info "Utilisation de l'IA"
    Page rédigée en partie avec l'aide d'un assistant IA. L'IA a été utilisée pour générer des 
    explications, des exemples et/ou des suggestions de structure. Toutes les informations ont 
    été vérifiées, éditées et complétées par l'auteur.