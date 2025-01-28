# 🔸11🔸ArrayList

## ArrayList en Java

Une `ArrayList` est une implémentation redimensionnable des tableaux qui fait partie du *framework* `Collections`.

```java
import java.util.ArrayList;

public class ExempleListes {
    public static void main(String[] args) {
        // Création d'une ArrayList typée
        ArrayList<String> noms = new ArrayList<>();

        // Ajout d'éléments
        noms.add("Alice");
        noms.add("Bob");
        noms.add("Charlie");

        // Ajout à un index spécifique
        noms.add(1, "David");    // Insère à l'index 1

        // Modification d'un élément
        noms.set(0, "Alicia");   // Remplace "Alice" par "Alicia"

        // Suppression d'éléments
        noms.remove("Bob");      // Par valeur
        noms.remove(0);          // Par index
    }
}
```

## Comparaison avec les tableaux

| Caractéristique | Tableau             | ArrayList               |
|-----------------|---------------------|-------------------------|
| Taille          | Fixe                | Dynamique               |
| Performance     | Plus rapide         | Plus lent               |
| Syntaxe         | nombres             | nombres.get(0)          |
| Types supportés | Primitifs et objets | Objets uniquement       |
| Mémoire         | Plus efficace       | Overhead supplémentaire |

## Avantages des tableaux

1. Performance optimale pour les opérations de lecture/écriture
2. Syntaxe plus simple et directe
3. Peuvent contenir des types primitifs
4. Moins de consommation mémoire

## Avantages des ArrayList

1. Taille dynamique
2. Méthodes utilitaires intégrées (add, remove, contains, etc.)
3. Facilité de manipulation des éléments
4. Conversion facile vers/depuis les tableaux

## Exemple pratique

```java
public class ComparaisonStructures {
    public static void main(String[] args) {
        // Tableau
        int[] tableauNombres = new int[3];
        tableauNombres[0] = 1;
        tableauNombres[1] = 2;
        tableauNombres[2] = 3;

        // ArrayList
        ArrayList<Integer> listeNombres = new ArrayList<>();
        listeNombres.add(1);
        listeNombres.add(2);
        listeNombres.add(3);

        // Conversion ArrayList vers tableau
        Integer[] tableauDepuisListe = listeNombres.toArray(new Integer[0]);

        // Conversion tableau vers ArrayList
        ArrayList<Integer> listeDepuisTableau =
                new ArrayList<>(Arrays.asList(tableauDepuisListe));

        // Parcours avec for-each (fonctionne pour les deux)
        for (int nombre : tableauNombres) {
            System.out.println(nombre);
        }

        for (Integer nombre : listeNombres) {
            System.out.println(nombre);
        }
    }
}
```

## Cas d'utilisation recommandés

**Utiliser un tableau quand** :

- La taille est fixe et connue
- Les performances sont critiques
- On travaille avec des types primitifs
- On fait beaucoup d'accès aléatoires

**Utiliser une ArrayList quand** :

- La taille est variable
- On a besoin d'ajouter/supprimer fréquemment
- On veut des méthodes utilitaires intégrées
- La flexibilité est plus importante que la performance

??? note "Citations"

    - [1] https://beginnersbook.com/2013/12/java-arraylist/
    - [2] https://www.programiz.com/java-programming/arraylist
    - [3] https://www.geeksforgeeks.org/arraylist-in-java/
    - [4] https://www.w3schools.com/java/java_arraylist.asp

## Convertir un `ArrayList` en tableau

Voici un exemple simple de programme Java qui utilise la méthode `toArray()` sur un `ArrayList` pour convertir vers un
tableau :

```java
import java.util.ArrayList;
import java.util.Arrays;

public class ExempleToArray {
    public static void main(String[] args) {
        // Création d'un ArrayList
        ArrayList<String> listeNoms = new ArrayList<>();

        // Ajout d'éléments
        listeNoms.add("Jean");
        listeNoms.add("Marie");
        listeNoms.add("Pierre");
        listeNoms.add("Colette");

        // Utilisation de toArray() pour obtenir un tableau
        Object[] tableauObjets = listeNoms.toArray();

        // Affichage du tableau
        System.out.println("Tableau obtenu via toArray():");
        System.out.println(Arrays.toString(tableauObjets));

        // Type casting pour obtenir un tableau de String
        String[] tableauStrings = listeNoms.toArray(new String[listeNoms.size()]);

        System.out.println("\nTableau de String après type casting:");
        System.out.println(Arrays.toString(tableauStrings));
    }
}
```

Ce programme crée un `ArrayList` de noms, ajoute quelques éléments, puis utilise `toArray()` pour obtenir un tableau
d'objets. Il montre ensuite comment effectuer un type casting pour obtenir un tableau de `String`.

## Possibilité de créer un ArrayList à partir d'un tableau

```java
import java.util.ArrayList;
import java.util.Arrays;

public class CreationArrayListFromArray {
    public static void main(String[] args) {
        // Tableau initial
        String[] tabInitial = {"A", "B", "C", "D"};

        // Création d'un ArrayList à partir du tableau
        ArrayList<String> liste = new ArrayList<>(Arrays.asList(tabInitial));

        // Affichage
        System.out.println("ArrayList créée à partir du tableau :");
        System.out.println(liste);
    }
}
```

Dans cet exemple, nous utilisons `Arrays.asList()` pour créer une liste à partir du tableau, puis passons cette liste au
constructeur d'`ArrayList`. Cela crée un nouveau `ArrayList` contenant tous les éléments du tableau original.

## Points clés à retenir

1. La méthode `toArray()` retourne un tableau d'objets (`Object[]`) par défaut.
2. Pour obtenir un tableau de type spécifique, il faut utiliser la signature `toArray(T[] a)` et passer un tableau vide
   du bon type.
3. On peut créer un `ArrayList` à partir d'un tableau en utilisant `Arrays.asList()` et en passant le résultat au
   constructeur d'`ArrayList`.
4. Cette approche permet de convertir facilement entre `ArrayList` et tableau standard.

En suivant ces méthodes, vous pouvez facilement convertir entre `ArrayList` et tableau dans Java, ce qui offre une
grande flexibilité dans vos programmes.

??? note "Citations"

      - [1] https://www.geeksforgeeks.org/arraylist-array-conversion-java-toarray-methods/
      - [2] https://stackoverflow.com/questions/32677003/how-to-convert-arraylist-to-array
      - [3] https://www.geeksforgeeks.org/arraylist-toarray-method-in-java-with-examples/
      - [4] https://www.codecademy.com/resources/docs/java/array-list/toArray    
      - [5] https://www.w3schools.com/java/ref_arraylist_toarray.asp
      - [6] https://docs.vultr.com/java/standard-library/java/util/ArrayList/toArray
      - [7] https://www.javatpoint.com/how-to-convert-arraylist-to-array-and-array-to-arraylist-in-java
      - [8] https://stackoverflow.com/questions/5061640/make-arraylist-toarray-return-more-specific-types/64137104
      - [9] https://howtodoinjava.com/java/collections/arraylist/convert-arraylist-to-array/
      - [10] https://forums.oracle.com/ords/apexds/post/convert-arraylist-into-array-7537


-------

??? info "Utilisation de l'IA"
      Page rédigée en partie avec l'aide d'un assistant IA, principalement à l'aide de Perplexity AI, avec le *LLM*
      **Claude 3.5 Sonnet**. L'IA a été utilisée pour générer des explications, des exemples et/ou des suggestions de
      structure. Toutes les informations ont été vérifiées, éditées et complétées par l'auteur.