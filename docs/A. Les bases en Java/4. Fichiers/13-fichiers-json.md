---
icon: material/file-document-outline
---

# 13. Gestion des fichiers JSON

## Exemple avec `com.google.gson.Gson`

Voici les classes `Personne` et `JsonUtils` :

??? note "Code `Personne`"

    ```java
    public class Personne {
        private String nom;
        private int age;
    
        public Personne(String nom, int age) {
            this.nom = nom;
            this.age = age;
        }
    
        // Getters et setters optionnels avec Gson
        public String getNom() {
            return nom;
        }
    
        public int getAge() {
            return age;
        }
    
        @Override
        public String toString() {
            return "Personne{nom='" + nom + "', age=" + age + "}";
        }
    }
    ```

??? note "Code `JsonUtils`"

    ```java
    import com.google.gson.Gson;
    import java.io.FileReader;
    import java.io.FileWriter;
    import java.io.IOException;
    
    public class JsonUtils {
        // Fonction de sérialisation
        public static void sauvegarderEnJson(Personne personne, String cheminFichier) throws IOException {
            Gson gson = new Gson();
            try (FileWriter writer = new FileWriter(cheminFichier)) {
                gson.toJson(personne, writer);
            }
        }
    
        // Fonction de désérialisation
        public static Personne chargerDeJson(String cheminFichier) throws IOException {
            Gson gson = new Gson();
            try (FileReader reader = new FileReader(cheminFichier)) {
                return gson.fromJson(reader, Personne.class);
            }
        }
    
        // Exemple d'utilisation
        public static void main(String[] args) {
            try {
                // Sérialisation
                Personne p1 = new Personne("Alice", 30);
                sauvegarderEnJson(p1, "fichiers/personne.json");
    
                // Désérialisation
                Personne p2 = chargerDeJson("fichiers/personne.json");
                System.out.println(p2.getNom() + ", " + p2.getAge());
    
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
    ```

Le code de la classe utilitaire nommée `JsonUtils` est conçue pour faciliter la sérialisation et la désérialisation
d'objets Java vers et depuis le format JSON en utilisant la bibliothèque Gson. Ceci est couramment utilisé pour la
persistance des données ou l'échange avec d'autres systèmes.

### Composants clés

1. **Dépendances :**
    - `com.google.gson.Gson`: la bibliothèque principale gérant la conversion JSON.
    - `java.io.*`: Fournit des classes pour les opérations d'entrée/sortie de fichiers.

2. **Classe `JsonUtils` :**
   Cette classe contient deux méthodes principales : `sauvegarderEnJson` et `chargerDeJson`.

3. **`sauvegarderEnJson` (Sérialisation) :**
    - `public static void sauvegarderEnJson(Personne personne, String cheminFichier)`: Cette méthode prend un objet
      `Personne` et un chemin de fichier en entrée. Le modificateur `public static` permet un accès direct sans
      instanciation de classe. Le type de retour `void` indique qu'aucune valeur n'est renvoyée.
    - `Gson gson = new Gson();`: Instancie un objet `Gson`.
    - `try (FileWriter writer = new FileWriter(cheminFichier))`: Crée un `FileWriter` pour écrire dans le fichier
      spécifié dans un bloc *try-with-resources* pour la gestion automatique des ressources.
    - `gson.toJson(personne, writer);`: Sérialise l'objet `Personne` en JSON et l'écrit dans le fichier via le `writer`.

4. **`chargerDeJson` (Désérialisation) :**
    - `public static Personne chargerDeJson(String cheminFichier)`: Cette méthode prend un chemin de fichier et renvoie
      un objet `Personne` désérialisé.
    - `Gson gson = new Gson();`: Instancie un objet `Gson`.
    - `try (FileReader reader = new FileReader(cheminFichier))`: Crée un `FileReader` pour lire le fichier JSON.
    - `return gson.fromJson(reader, Personne.class);`: Désérialise le JSON du fichier en un objet `Personne` et le
      renvoie.

5. **Méthode `main` (Exemple d'utilisation) :**
   La méthode `main` illustre l'utilisation de base : créer un objet `Personne`, le sérialiser en JSON, puis le
   désérialiser à partir du fichier.  `System.out.println` confirme le processus en affichant le nom et l'âge.

En résumé, `JsonUtils` fournit une interface simple pour la conversion entre les objets Java et JSON à l'aide de la
bibliothèque Gson. La classe `Personne`, bien que non affichée, contient vraisemblablement des attributs tels que `nom`
et `âge`. La fonctionnalité principale s'articule autour de l'utilisation de Gson pour la sérialisation (`toJson`) et la
désérialisation (`fromJson`).

### Résultat dans `personne.json`

```json
{"nom":"Alice","age":30}
```

### Résultat reformatté

```json
{
  "nom": "Alice",
  "age": 30
}
```

## Exemple avec `com.google.gson.Gson` et une `ArrayList`

??? note "Code"

      ```java
      import com.google.gson.Gson;
      import com.google.gson.reflect.TypeToken;
      import java.io.FileReader;
      import java.io.FileWriter;
      import java.io.IOException;
      import java.lang.reflect.Type;
      import java.util.ArrayList;
      import java.util.List;
      
      public class JsonUtilsList {
          // Fonction de sérialisation de la liste
          public static void sauvegarderListeEnJson(List<Personne> personnes, String cheminFichier) throws IOException {
              Gson gson = new Gson();
              try (FileWriter writer = new FileWriter(cheminFichier)) {
                  gson.toJson(personnes, writer);
              }
          }
      
          // Fonction de désérialisation de la liste
          public static List<Personne> chargerListeDeJson(String cheminFichier) throws IOException {
              Gson gson = new Gson();
              try (FileReader reader = new FileReader(cheminFichier)) {
                  // Création d'un Type pour ArrayList<Personne>
                  Type typeListePersonnes = new TypeToken<ArrayList<Personne>>(){}.getType();
                  return gson.fromJson(reader, typeListePersonnes);
              }
          }
      
          // Exemple d'utilisation
          public static void main(String[] args) {
              try {
                  // Création d'une liste de personnes
                  ArrayList<Personne> personnes = new ArrayList<>();
                  personnes.add(new Personne("Alice", 30));
                  personnes.add(new Personne("Bob", 25));
                  personnes.add(new Personne("Charlie", 35));
      
                  // Sérialisation
                  sauvegarderListeEnJson(personnes, "fichiers/personnes.json");
      
                  // Désérialisation
                  List<Personne> personnesChargees = chargerListeDeJson("fichiers/personnes.json");
      
                  // Affichage des personnes chargées
                  for (Personne p : personnesChargees) {
                      System.out.println(p);
                  }
      
              } catch (IOException e) {
                  e.printStackTrace();
              }
          }
      }
      ```

Le code définit une classe utilitaire `JsonUtilsList` pour sérialiser et désérialiser des listes d'objets `Personne`
vers et depuis des fichiers JSON en utilisant la bibliothèque Gson. Voici une explication, soulignant les différences
avec `JsonUtils`:

### `JsonUtilsList`

- **`sauvegarderListeEnJson(List<Personne> personnes, String cheminFichier)`:** Cette méthode sérialise une `List`
  d'objets `Personne` dans un fichier JSON spécifié par `cheminFichier`. Elle utilise `Gson.toJson()` pour effectuer la
  sérialisation.

- **`chargerListeDeJson(String cheminFichier)`:** Cette méthode désérialise une `List` d'objets `Personne` à partir d'un
  fichier JSON spécifié par `cheminFichier`. Il est crucial qu'elle utilise
  `TypeToken<ArrayList<Personne>>(){}.getType()` pour obtenir la représentation correcte du type pour la désérialisation
  avec Gson. Ceci est nécessaire, car Gson doit connaître le type spécifique de la `List` (dans ce cas,
  `ArrayList<Personne>`) pour désérialiser correctement.

- **Méthode `main`:** Démontre l'utilisation des deux méthodes de sérialisation et de désérialisation. Elle crée une
  liste d'objets `Personne`, les sérialise dans "fichiers/personnes.json", puis les désérialise à partir du fichier,
  affichant les objets chargés.

### Principales différences avec `JsonUtils`

- **Gestion des listes :** `JsonUtilsList` fonctionne avec `List<Personne>`, tandis que `JsonUtils` fonctionne avec des
  objets `Personne` individuels.
- **Utilisation de TypeToken :** `JsonUtilsList` utilise `TypeToken` pour désérialiser correctement les listes.
  `JsonUtils` n'en a pas besoin, car il désérialise vers une classe connue (`Personne.class`).
- **Noms de fichiers :** L'exemple d'utilisation dans `JsonUtilsList` utilise "fichiers/personnes.json" tandis que
  `JsonUtils` utilise "fichiers/personne.json". Cela reflète la différence de traitement entre les listes et les objets
  individuels.

En résumé, `JsonUtilsList` étend les fonctionnalités de `JsonUtils` pour gérer les collections d'objets `Personne`, en
utilisant le mécanisme `TypeToken` nécessaire pour une désérialisation correcte avec Gson.

### Résultat dans `personnes.json`

```json
[{"nom":"Alice","age":30},{"nom":"Bob","age":25},{"nom":"Charlie","age":35}]
```

### Résultat reformatté

```json
[
  {
    "nom": "Alice",
    "age": 30
  },
  {
    "nom": "Bob",
    "age": 25
  },
  {
    "nom": "Charlie",
    "age": 35
  }
]
```


-------

??? info "Utilisation de l'IA"
    Page rédigée en partie avec l'aide d'un assistant IA. L'IA a été utilisée pour générer des 
    explications, des exemples et/ou des suggestions de structure. Toutes les informations ont 
    été vérifiées, éditées et complétées par l'auteur.