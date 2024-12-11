# 11- ArrayList

## ArrayList en Java

Une ArrayList est une implémentation redimensionnable des tableaux qui fait partie du framework Collections.

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

Citations:
[1] https://beginnersbook.com/2013/12/java-arraylist/
[2] https://www.programiz.com/java-programming/arraylist
[3] https://www.geeksforgeeks.org/arraylist-in-java/
[4] https://www.w3schools.com/java/java_arraylist.asp