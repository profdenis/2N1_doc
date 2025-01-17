# Polymorphisme

Regrouper les similarités entre les classes de formes (comme dans la v3 avec `Shape`) offre plusieurs avantages :

- **Réduction de la redondance de code :** Au lieu de répéter le code pour la couleur et potentiellement d'autres
  propriétés communes dans chaque classe de forme (`Point`, `Circle`, `Rectangle`, etc.), on les définit une seule fois
  dans `Shape`. Cela simplifie la maintenance et l'évolution du code.
- **Cohérence :**  Toutes les formes partagent un comportement et des propriétés communs, assurant une cohérence dans
  leur utilisation.
- **Extensibilité :**  L'ajout de nouvelles formes est simplifié, car elles héritent automatiquement des propriétés et
  méthodes de `Shape`. Il suffit d'implémenter les spécificités de la nouvelle forme.
- **Polymorphisme :**  C'est le point clé pour utiliser des collections de formes. On peut manipuler un ensemble de
  formes différentes (points, cercles, etc.) de manière générique, sans se soucier de leur type spécifique.

## Polymorphisme avec une `ArrayList` de `Shape`

L'intérêt principal de `Shape` est de permettre le polymorphisme. On peut créer une `ArrayList` de `Shape` et y stocker
des objets de types différents qui héritent de `Shape` (comme `Point`, `Circle`, etc.). Ensuite, on peut parcourir cette
liste et appeler la méthode `draw()` sur chaque élément. Grâce au polymorphisme, la bonne version de `draw()` sera
appelée automatiquement en fonction du type réel de l'objet.

### Exemple

```java
import v3.shapes.*;

import java.awt.Color;
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        ArrayList<Shape> shapes = new ArrayList<>();
        shapes.add(new Point(10, 20, Color.RED));
        shapes.add(new Circle(new Point(50, 50), 30, Color.BLUE));
        // ... ajouter d'autres formes ...

        Image image = new Image(200, 200); // Supposons une classe Image pour le dessin

        for (Shape shape : shapes) {
            shape.draw(image); // Appel polymorphe de draw()
        }

        // ... afficher l'image ...
    }
}
```

Dans cet exemple, même si `shapes` contient des objets de types différents, l'appel à `shape.draw(image)` appelle la
méthode `draw()` appropriée pour chaque forme (celle de `Point`, celle de `Circle`, etc.). C'est la puissance du
polymorphisme.





-------

!!! note "Note"
    Page rédigée en partie avec l'aide d'un assistant IA, principalement à l'aide de Perplexity AI, avec le *LLM*
    **Claude 3.5 Sonnet**. L'IA a été utilisée pour générer des explications, des exemples et/ou des suggestions de
    structure. Toutes les informations ont été vérifiées, éditées et complétées par l'auteur.