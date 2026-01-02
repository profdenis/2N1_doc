# La classe `Shapes`

- Github: [Shapes.java](https://github.com/profdenis/Shapes/tree/master/src/v1/Shapes.java)

??? note "Code"

    ```java
    package v1;
    
    import java.awt.Color;
    
    public class Shapes {
        public static Color defaultColor = Color.BLACK;
        public static Image image = new Image(400);
    
        public static void drawPoint(int x, int y) {
            drawPoint(x, y, defaultColor);
        }
    
        public static void drawPoint(int x, int y, Color color) {
            image.SetPixel(x, y, color);
        }
    
        public static void drawHorizontalLine(int x1, int y1, int width) {
            drawHorizontalLine(x1, y1, width, defaultColor);
        }
    
        public static void drawHorizontalLine(int x1, int y1, int width, Color color) {
            for (int i = 0; i < width; i++) {
                drawPoint(x1 + i, y1, color);
            }
        }
    
        public static void drawVerticalLine(int x1, int y1, int height) {
            for (int j = 0; j < height; j++) {
                drawPoint(x1, y1 + j, defaultColor);
            }
        }
    
        public static void drawVerticalLine(int x1, int y1, int height, Color color) {
            for (int j = 0; j < height; j++) {
                drawPoint(x1, y1 + j, color);
            }
        }
    
        public static void drawLine(int x1, int y1, int x2, int y2) {
            drawLine(x1, y1, x2, y2, defaultColor);
        }
    
        public static void drawLine(int x1, int y1, int x2, int y2, Color color) {
    
            // ligne verticale, il faut éviter une division par 0
            if (x1 == x2) {
                drawVerticalLine(x1, Math.min(y1, y2), Math.abs(y2 - y1) + 1, color);
                return;
            }
    
            // éviter une division int/int qui entraînerait une imprécision
            double slope = (y2 - y1) / (double) (x2 - x1);
            double intercept = y2 - slope * x2;
    
            if (Math.abs(slope) < 1) {
                drawCloserToHorizontal(x1, x2, slope, intercept, color);
            } else {
                drawCloserToVertical(y1, y2, intercept, slope, color);
            }
        }
    
        private static void drawCloserToVertical(int startY, int endY, double intercept, double slope, Color color) {
            int minY = Math.min(startY, endY);
            int maxY = Math.max(startY, endY);
    
            for (int y = minY; y <= maxY; y++) {
                int x = (int) Math.round((y - intercept) / slope);
                image.SetPixel(x, y, color);
            }
        }
    
        private static void drawCloserToHorizontal(int startX, int endX, double slope, double intercept, Color color) {
            int minX = Math.min(startX, endX);
            int maxX = Math.max(startX, endX);
    
            for (int x = minX; x <= maxX; x++) {
                int y = (int) Math.round(slope * x + intercept);
                image.SetPixel(x, y, color);
            }
        }
    
        public static void drawTriangle(int x1, int y1, int x2, int y2, int x3, int y3) {
            drawTriangle(x1, y1, x2, y2, x3, y3, defaultColor);
        }
    
        public static void drawTriangle(int x1, int y1, int x2, int y2, int x3, int y3, Color color) {
            drawLine(x1, y1, x2, y2, color);
            drawLine(x2, y2, x3, y3, color);
            drawLine(x3, y3, x1, y1, color);
        }
    
        public static void drawRectangle(int x, int y, int width, int height) {
            drawRectangle(x, y, width, height, defaultColor);
        }
    
        public static void drawRectangle(int x, int y, int width, int height, Color color) {
            drawLine(x, y, x + width, y, color);
            drawLine(x + width, y, x + width, y + height, color);
            drawLine(x + width, y + height, x, y + height, color);
            drawLine(x, y + height, x, y, color);
        }
    
        public static void drawSquare(int x, int y, int width) {
            drawSquare(x, y, width, defaultColor);
        }
    
        public static void drawSquare(int x, int y, int width, Color color) {
            //noinspection SuspiciousNameCombination
            drawRectangle(x, y, width, width, color);
        }
    
        public static void drawPolyLine(int[] x, int[] y) {
            drawPolyLine(x, y, defaultColor);
        }
    
        public static void drawPolyLine(int[] x, int[] y, Color color) {
            for (int i = 1; i < x.length; i++) {
                drawLine(x[i - 1], y[i - 1], x[i], y[i], color);
            }
        }
    
    
        public static void drawPolygon(int[] x, int[] y) {
            drawPolygon(x, y, defaultColor);
        }
    
        public static void drawPolygon(int[] x, int[] y, Color color) {
            drawPolyLine(x, y, color);
            drawLine(x[0], y[0], x[x.length - 1], y[y.length - 1], color);
    
        }
    
        public static void drawCircle(int x, int y, int radius) {
            drawCircle(x, y, radius, defaultColor);
        }
    
        public static void drawCircle(int x, int y, int radius, Color color) {
            int cos45 = (int) Math.round(radius * Math.cos(Math.PI / 4));
    
            for (int i = 0; i <= cos45; i++) {
                int j = (int) Math.round(Math.sqrt(radius * radius - i * i));
                image.SetPixel(x + i, y + j, color); // point 1
                image.SetPixel(x - i, y + j, color); // point 2: symétrie du point 1 par rapport à l'axe Y
    
                image.SetPixel(x + i, y - j, color); // point 3: symétrie du point 1 par rapport à l'axe X
                image.SetPixel(x - i, y - j, color); // point 4: symétrie du point 3 par rapport à l'axe Y
    
                image.SetPixel(x + j, y + i, color); // point 5: symétrie du point 1 par rapport à la diagonale 45°
                image.SetPixel(x + j, y - i, color); // point 6: symétrie du point 5 par rapport à l'axe X
    
                image.SetPixel(x - j, y + i, color); // point 7: symétrie du point 5 par rapport à l'axe Y
                image.SetPixel(x - j, y - i, color); // point 8: symétrie du point 7 par rapport à l'axe X
            }
        }
    }
    ```


La classe `Shapes` fournit des méthodes statiques pour dessiner différentes formes sur une image. Elle utilise une image
`Image` de taille 400x400 pixels et une couleur par défaut `Color.BLACK`.

Voici une explication des méthodes :

* **Méthodes de dessin de points et de lignes :**
    * `drawPoint(x, y)` et `drawPoint(x, y, color)` : Dessine un point aux coordonnées `(x, y)` avec la couleur
      spécifiée
      ou la couleur par défaut.
    * `drawHorizontalLine(x1, y1, width)` et `drawHorizontalLine(x1, y1, width, color)` : Dessine une ligne horizontale
      à
      partir de `(x1, y1)` sur une largeur donnée.
    * `drawVerticalLine(x1, y1, height)` et `drawVerticalLine(x1, y1, height, color)` : Dessine une ligne verticale à
      partir de `(x1, y1)` sur une hauteur donnée.
    * `drawLine(x1, y1, x2, y2)` et `drawLine(x1, y1, x2, y2, color)` : Dessine une ligne entre les points `(x1, y1)` et
      `(x2, y2)`. Elle gère les cas particuliers des lignes verticales et optimise le dessin en fonction de la pente de
      la
      ligne.

* **Méthodes de dessin de formes :**
    * `drawTriangle(x1, y1, x2, y2, x3, y3)` et `drawTriangle(x1, y1, x2, y2, x3, y3, color)` : Dessine un triangle en
      reliant les trois points donnés.
    * `drawRectangle(x, y, width, height)` et `drawRectangle(x, y, width, height, color)` : Dessine un rectangle avec le
      coin supérieur gauche à (x, y), la largeur et la hauteur spécifiées.
    * `drawSquare(x, y, width)` et `drawSquare(x, y, width, color)` : Dessine un carré avec le coin supérieur gauche à
      `(x, y)` et le côté de longueur `width`.
    * `drawPolyLine(x[], y[])` et `drawPolyLine(int[] x, int[] y, Color color)` : Dessine une ligne brisée en reliant
      les
      points spécifiés par les tableaux `x` et `y`.
    * `drawPolygon(x[], y[])` et `drawPolygon(int[] x, int[] y, Color color)` : Dessine un polygone en reliant les
      points
      spécifiés par les tableaux x et y et en fermant le polygone.
    * `drawCircle(x, y, radius)` et `drawCircle(x, y, radius, color)` : Dessine un cercle de centre `(x, y)` et de rayon
      `radius`. Il utilise une méthode optimisée pour dessiner des points sur le cercle en utilisant la symétrie et les
      propriétés du cercle.

Chaque méthode de dessin a une version avec et sans le paramètre `color`. Si la couleur n'est pas spécifiée, la couleur
par défaut (`Color.BLACK`) est utilisée. Toutes les méthodes modifient directement l'image `image` statique.

## Méthode `drawLine`

La méthode `drawLine(int x1, int y1, int x2, int y2, Color color)` dessine une ligne entre les points `(x1, y1)` et
`(x2, y2)` avec la couleur spécifiée. Voici une explication détaillée :

### Cas particulier : ligne verticale

Si `x1` est égal à `x2`, la ligne est verticale. Dans ce cas, la méthode `drawVerticalLine` est appelée pour
dessiner la ligne. Ceci est important, car le calcul de la pente dans le cas général impliquerait une division par
zéro.

### Calcul de la pente et de l'ordonnée à l'origine

Si la ligne n'est pas verticale, la pente (`slope`) et
l'ordonnée à l'origine (`intercept`) sont calculées. Le calcul de la pente est effectué avec un cast en `double` pour
l'un des termes afin d'éviter une division entière qui pourrait entraîner une perte de précision.

### Optimisation basée sur la pente

La méthode utilise une optimisation pour minimiser l'effet d'escalier (*aliasing*) :

- **Si la valeur absolue de la pente est inférieure à 1**, la ligne est plus proche de l'horizontale. Dans ce cas, la
  méthode `drawCloserToHorizontal` est appelée. Cette méthode itère sur les coordonnées x et calcule la coordonnée y
  correspondante en utilisant l'équation de la droite : `y = slope * x + intercept`.
- **Si la valeur absolue de la pente est supérieure ou égale à 1**, la ligne est plus proche de la verticale. Dans ce
  cas, la méthode `drawCloserToVertical` est appelée. Cette méthode itère sur les coordonnées y et calcule la coordonnée
  x correspondante en utilisant l'équation : `x = (y - intercept) / slope`.

### `drawCloserToHorizontal`

Cette méthode parcourt les valeurs de x entre `minX` et `maxX` (les valeurs minimales et maximales de x1 et x2). Pour
chaque valeur de x, elle calcule la valeur de y correspondante à l'aide de l'équation de la droite et arrondit à
l'entier le plus proche. Ensuite, elle appelle `image.SetPixel(x, y, color)` pour dessiner le point.

### `drawCloserToVertical`

Cette méthode est similaire à `drawCloserToHorizontal`, mais elle itère sur les valeurs de y entre `minY` et `maxY`.
Pour chaque valeur de y, elle calcule la valeur de x, l'arrondit et dessine le point.

### Résumé

En résumé, la méthode `drawLine` gère les cas particuliers des lignes verticales, calcule la pente et l'ordonnée à
l'origine, puis choisit la méthode de dessin la plus appropriée en fonction de la pente pour minimiser l'effet
d'escalier et dessiner une ligne plus lisse.

## Méthodes `drawCloserToHorizontal` et `drawCloserToVertical`

### `drawCloserToHorizontal`

Cette méthode parcourt les valeurs de x entre `minX` et `maxX` (les valeurs minimales et maximales de x1 et x2). Pour
chaque valeur de x, elle calcule la valeur de y correspondante à l'aide de l'équation de la droite et arrondit à
l'entier le plus proche. Ensuite, elle appelle `image.SetPixel(x, y, color)` pour dessiner le point.

### `drawCloserToVertical`

Cette méthode est similaire à `drawCloserToHorizontal`, mais elle itère sur les valeurs de y entre `minY` et `maxY`.
Pour chaque valeur de y, elle calcule la valeur de x, l'arrondit et dessine le point.

Les variables `minX`, `maxX`, `minY` et `maxY` dans les méthodes `drawCloserToHorizontal` et `drawCloserToVertical` sont
essentielles pour déterminer les bornes de l'itération et garantir que la ligne est dessinée correctement, quel que soit
l'ordre des points fournis.

Voici pourquoi elles sont utiles :

- **Indépendance de l'ordre des points :** L'utilisateur peut appeler `drawLine` avec `(x1, y1)` et `(x2, y2)` dans
  n'importe quel ordre.  `minX` et `maxX` (ou `minY` et `maxY`) garantissent que la boucle `for` itère toujours du plus
  petit au plus grand, quel que soit l'ordre des points d'entrée. Sans ces variables, si `x1 > x2`, la boucle `for` dans
  `drawCloserToHorizontal` ne s'exécuterait pas, et aucune ligne ne serait dessinée.

- **Détermination des bornes de la ligne :** Ces variables définissent les limites du segment de droite à dessiner.
  Elles garantissent que tous les pixels entre les deux points spécifiés sont parcourus et potentiellement colorés. Sans
  ces limites, la ligne pourrait être dessinée au-delà des points d'extrémité souhaités ou être incomplète.

- **Optimisation des performances :** En déterminant les bornes minimales et maximales, la boucle `for` itère uniquement
  sur les valeurs nécessaires pour dessiner la ligne. Cela évite des itérations inutiles et optimise les performances du
  dessin, en particulier pour les longues lignes.

En résumé, ces variables locales permettent de gérer l'ordre des points d'entrée, de définir les bornes correctes du
segment de droite et d'optimiser les performances du dessin. Elles sont donc cruciales pour le bon fonctionnement des
méthodes `drawCloserToHorizontal` et `drawCloserToVertical`.

## Méthode `drawPolyLine`

La méthode `drawPolyLine(int[] x, int[] y, Color color)` dessine une ligne brisée en reliant les points spécifiés par
les tableaux `x` et `y` avec la couleur donnée. La boucle `for` dans cette méthode est au cœur de son fonctionnement :

```java
for(int i = 1; i<x.length;i++) {
    drawLine(x[i-1], y[i-1], x[i], y[i], color);
}
```

Voici une explication détaillée :

1. **Initialisation :** `int i = 1;`

       La boucle commence à l'indice 1, et non à 0.

2. **Condition :** `i < x.length;` 

       La boucle continue tant que `i` est strictement inférieur à la longueur du tableau `x`. Ceci est important, car la 
       boucle accède aux éléments `x[i]` et `x[i-1]`.

3. **Incrémentation :** `i++;`

       À chaque itération, `i` est incrémenté de 1.

4. **Corps de la boucle :** `drawLine(x[i - 1], y[i - 1], x[i], y[i], color);`  

       Le corps de la boucle appelle la méthode `drawLine` pour tracer un segment entre deux points consécutifs de la 
       ligne brisée. Plus précisément :

    - `x[i-1]` et `y[i-1]` sont les coordonnées du point précédent.
    - `x[i]` et `y[i]` sont les coordonnées du point actuel.

En résumé, la boucle itère sur les tableaux de coordonnées `x` et `y` et dessine des segments de droite entre chaque
paire de points consécutifs, créant ainsi la ligne brisée.

### Utilisation de `drawPolyLine` dans `drawPolygon`

La méthode `drawPolygon(int[] x, int[] y, Color color)` utilise `drawPolyLine` pour dessiner un polygone fermé. Voici
comment :

```java
drawPolyLine(x, y, color);
drawLine(x[0], y[0], x[x.length-1], y[y.length-1], color);
```

1. **Appel à `drawPolyLine` :** 

       La méthode appelle d'abord `drawPolyLine` pour dessiner les côtés du polygone, sauf le
       dernier côté qui ferme le polygone.

2. **Fermeture du polygone :** 

       Ensuite, elle appelle `drawLine` pour dessiner le dernier segment entre le dernier point
       `(x[x.length - 1], y[y.length - 1])` et le premier point `(x[0], y[0])`, fermant ainsi le polygone.

En combinant ces deux appels, `drawPolygon` dessine efficacement un polygone fermé en utilisant la fonctionnalité de
`drawPolyLine` pour dessiner la majorité des côtés.

## Méthode drawCircle

La méthode `drawCircle(int x, int y, int radius, Color color)` dessine un cercle de centre (x, y) et de rayon `radius`
avec la couleur spécifiée. Elle utilise une approche optimisée basée sur la symétrie des cercles pour dessiner les
points.

Voici une explication détaillée :

1. **Calcul de `cos45` :**
   ```java
   int cos45 = (int) Math.round(radius * Math.cos(Math.PI / 4));
   ```
   Cette ligne calcule la valeur de x (ou y) lorsqu'on est à 45 degrés sur le cercle. Elle est utilisée pour optimiser
   la boucle, en itérant seulement sur le premier octant du cercle (0 à 45 degrés). Les autres points sont calculés par
   symétrie.

2. **Boucle principale :**
   ```java
   for (int i = 0; i <= cos45; i++) {
       // ...
   }
   ```
   La boucle itère de 0 jusqu'à `cos45`.  `i` représente la coordonnée x par rapport au centre du cercle.

3. **Calcul de `j` :**
   ```java
   int j = (int) Math.round(Math.sqrt(radius * radius - i * i));
   ```
   À chaque itération, `j` est calculé.  `j` représente la coordonnée y par rapport au centre du cercle. Le calcul est
   basé sur le théorème de Pythagore ($x^2 + y^2 = r^2$), où `i` est la coordonnée x, `j` est la coordonnée y et 
   `radius` est le rayon.

4. **Dessin des points par symétrie :**
   Les lignes suivantes dessinent 8 points à chaque itération en exploitant la symétrie du cercle :
   ```java
   image.SetPixel(x + i, y + j, color); // point 1
   image.SetPixel(x - i, y + j, color); // point 2: symétrie du point 1 par rapport à l'axe Y
   image.SetPixel(x + i, y - j, color); // point 3: symétrie du point 1 par rapport à l'axe X
   image.SetPixel(x - i, y - j, color); // point 4: symétrie du point 3 par rapport à l'axe Y
   image.SetPixel(x + j, y + i, color); // point 5: symétrie du point 1 par rapport à la diagonale 45°
   image.SetPixel(x + j, y - i, color); // point 6: symétrie du point 5 par rapport à l'axe X
   image.SetPixel(x - j, y + i, color); // point 7: symétrie du point 5 par rapport à l'axe Y
   image.SetPixel(x - j, y - i, color); // point 8: symétrie du point 7 par rapport à l'axe X
   ```
   En dessinant 8 points à la fois, la méthode optimise le processus de dessin du cercle.

En résumé, la méthode `drawCircle` utilise une approche efficace pour dessiner un cercle en itérant sur un seul octant
et en utilisant la symétrie pour calculer et dessiner les autres points. Cela minimise les calculs et améliore les
performances.



-------

??? info "Utilisation de l'IA"
    Page rédigée en partie avec l'aide d'un assistant IA. L'IA a été utilisée pour générer des 
    explications, des exemples et/ou des suggestions de structure. Toutes les informations ont 
    été vérifiées, éditées et complétées par l'auteur.