# Classes `VLine`, `HLine` et `Line`

## Classe `VLine`

??? note "Code"

    ```java
    package v2.shapes;
    
    import java.awt.Color;
    
    public class VLine {
        public static final Color defaultDrawColor = Color.BLACK;
    
        private Point start;
        private int height;
        private Color drawColor;
    
        public VLine(Point start, int height) {
            this(start, height, defaultDrawColor);
        }
    
        public VLine(Point start, int height, Color drawColor) {
            this.start = start;
            this.height = height;
            this.drawColor = drawColor;
        }
    
        public Point getStart() {
            return start;
        }
    
        public void setStart(Point start) {
            this.start = start;
        }
    
        public int getHeight() {
            return height;
        }
    
        public void setHeight(int height) {
            this.height = height;
        }
    
        public Color getDrawColor() {
            return drawColor;
        }
    
        public void setDrawColor(Color drawColor) {
            this.drawColor = drawColor;
        }
    
    
        public void draw(Image image) {
            for (int j = 0; j < height; j++) {
                new Point(start.getX(), start.getY() + j, drawColor).draw(image);
            }
        }
    }
    ```

La classe `VLine` représente une ligne verticale. Elle est conçue pour dessiner une ligne verticale d'une hauteur
spécifiée à partir d'un point donné. Voici une explication :

1. **Champs :**
    - `start`: Un objet `Point` représentant le point de départ de la ligne verticale. Ce point détermine les
      coordonnées x et y où la ligne commence.
    - `height`: Un entier représentant la longueur verticale de la ligne.
    - `drawColor`: Un objet `Color` spécifiant la couleur de la ligne. Par défaut, il est noir si aucune couleur n'est
      fournie.

2. **Constructeurs :**
    - `VLine(Point start, int height)`: Crée un `VLine` avec le point de départ et la hauteur spécifiés, en utilisant la
      couleur par défaut (noir).
    - `VLine(Point start, int height, Color drawColor)`: Crée un `VLine` avec le point de départ, la hauteur et la
      couleur spécifiés.

3. **Méthodes :**
    - `getStart()`: Renvoie le `Point` de départ de la ligne.
    - `setStart(Point start)`: Définit le `Point` de départ de la ligne.
    - `getHeight()`: Renvoie la hauteur de la ligne.
    - `setHeight(int height)`: Définit la hauteur de la ligne.
    - `getDrawColor()`: Renvoie la couleur de dessin de la ligne.
    - `setDrawColor(Color drawColor)`: Définit la couleur de dessin de la ligne.
    - `draw(Image image)`: Il s'agit de la méthode principale. Elle itère `height` fois, dessinant un seul `Point` à
      chaque position le long de la ligne verticale. La coordonnée x reste constante (à partir du point `start`), tandis
      que la coordonnée y est incrémentée à chaque itération. Chaque point est dessiné en utilisant la `drawColor`
      spécifiée sur l'`Image` fournie.

En résumé, `VLine` simplifie le dessin d'une ligne verticale en gérant l'itération et le dessin de points individuels
dans sa méthode `Draw`. Elle évite les calculs redondants en dessinant point par point verticalement.

## Classe `HLine`

??? note "Code"

    ```java
    package v2.shapes;
    
    import java.awt.Color;
    
    public class HLine {
        public static final Color defaultDrawColor = Color.BLACK;
    
        private Point start;
        private int width;
        private Color drawColor;
    
        public HLine(Point start, int width) {
            this(start, width, defaultDrawColor);
        }
    
        public HLine(Point start, int width, Color drawColor) {
            this.start = start;
            this.width = width;
            this.drawColor = drawColor;
        }
    
        public Point getStart() {
            return start;
        }
    
        public void setStart(Point start) {
            this.start = start;
        }
    
        public int getWidth() {
            return width;
        }
    
        public void setWidth(int width) {
            this.width = width;
        }
    
        public Color getDrawColor() {
            return drawColor;
        }
    
        public void setDrawColor(Color drawColor) {
            this.drawColor = drawColor;
        }
    
    
        public void draw(Image image) {
            for (int i = 0; i < width; i++) {
                new Point(start.getX() + i, start.getY(), drawColor).draw(image);
            }
        }
    }
    ```

La classe `HLine` est très similaire à `VLine`, mais elle dessine une ligne horizontale. La principale différence réside
dans la façon dont la méthode `Draw` fonctionne :

* **`HLine.draw(Image image)`:** Au lieu d'incrémenter la coordonnée y comme dans `VLine`, `HLine` incrémente la
  coordonnée x. La boucle `for` parcourt la `largeur` de la ligne :

```java
for(int i = 0; i<width; i++) {
        new Point(start.getX() + i, start.getY(),drawColor).draw(image);
}
```

À chaque itération, un nouveau `Point` est créé avec :

* `start.getX() + i`: La coordonnée x est incrémentée de `i` à chaque étape, déplaçant le dessin horizontalement vers
  la droite.
* `start.getY()`: La coordonnée y reste constante, maintenant le dessin sur la même ligne horizontale.
* `drawColor`: La couleur spécifiée pour la ligne.

Ce `Point` est ensuite dessiné sur l'`Image` fournie.

En résumé, la principale différence entre `HLine` et `VLine` est la direction dans laquelle la ligne est dessinée.
`HLine` dessine horizontalement en incrémentant x, tandis que `VLine` dessine verticalement en incrémentant y. Le reste
de la structure de la classe (champs, constructeurs, getters/setters) est quasiment identique.

## Classe `Line`

??? note "Code"

    ```java
    package v2.shapes;
    
    import java.awt.Color;
    
    public class Line {
        public static final Color defaultDrawColor = Color.BLACK;
    
        private Point start;
        private Point end;
        private Color drawColor;
    
        public Line(Point start, Point end) {
            this(start, end, defaultDrawColor);
        }
    
        public Line(Point start, Point end, Color drawColor) {
            this.start = start;
            this.end = end;
            this.drawColor = drawColor;
        }
    
        public Point getStart() {
            return start;
        }
    
        public void setStart(Point start) {
            this.start = start;
        }
    
        public Point getHeight() {
            return end;
        }
    
        public void setHeight(Point end) {
            this.end = end;
        }
    
        public Color getDrawColor() {
            return drawColor;
        }
    
        public void setDrawColor(Color drawColor) {
            this.drawColor = drawColor;
        }
    
        public void draw(Image image) {
            // ligne verticale, il faut éviter une division par 0
            if (start.getX() == end.getX()) {
                VLine vline = new VLine(start, Math.abs(end.getY() - start.getY()) + 1, drawColor);
                vline.Draw(image);
                return;
            }
    
            // éviter une division int/int qui entraînerait une imprécision
            double slope = (end.getY() - start.getY()) / (double) (end.getX() - start.getX());
            double intercept = end.getY() - slope * end.getX();
    
            if (Math.abs(slope) < 1) {
                drawCloserToHorizontal(image, start.getX(), end.getX(), slope, intercept, drawColor);
            } else {
                drawCloserToVertical(image, start.getY(), end.getY(), intercept, slope, drawColor);
            }
        }
    
        private static void drawCloserToVertical(Image image, int startY, int endY, double intercept, double slope, Color color) {
            int minY = Math.min(startY, endY);
            int maxY = Math.max(startY, endY);
    
            for (int y = minY; y <= maxY; y++) {
                int x = (int) Math.round((y - intercept) / slope);
                image.setPixel(x, y, color);
            }
        }
    
        private static void drawCloserToHorizontal(Image image, int startX, int endX, double slope, double intercept, Color color) {
            int minX = Math.min(startX, endX);
            int maxX = Math.max(startX, endX);
    
            for (int x = minX; x <= maxX; x++) {
                int y = (int) Math.round(slope * x + intercept);
                image.setPixel(x, y, color);
            }
        }
    
    }
    ```

La classe `Line` est plus générale que `HLine` et `VLine`, car elle peut dessiner des lignes dans n'importe quelle
direction, pas seulement horizontales ou verticales. Voici les principales différences :

1. **Champs :** Au lieu d'une `hauteur` ou d'une `largeur`, `Line` possède deux points : `start` et `end`, qui définissent
   les extrémités de la ligne.

2. **Méthode `draw` plus complexe :** La méthode `Draw` de `Line` est nettement plus sophistiquée. Elle gère plusieurs
   cas :

    * **Lignes verticales :** Si `start.getX()` est égal à `end.getX()`, la ligne est verticale. Dans ce cas, la méthode
      crée une instance de `VLine` et utilise sa méthode `draw` pour dessiner la ligne. Ceci est une optimisation pour
      éviter une division par zéro dans le calcul de la pente.

    * **Calcul de la pente et de l'ordonnée à l'origine :** Si la ligne n'est pas verticale, la méthode calcule la
      pente (`slope`) et l'ordonnée à l'origine (`intercept`) de la ligne à l'aide des coordonnées des points `start` et
      `end`. Le calcul de la pente est converti en `double` pour éviter les imprécisions liées à la division d'entiers.

    * **Optimisation du dessin :** Pour optimiser le dessin, la méthode choisit entre deux algorithmes en fonction de la
      pente :
        * Si la valeur absolue de la pente est inférieure à 1 (ligne plus proche de l'horizontale), la méthode
          `drawCloserToHorizontal` est utilisée. Cette méthode itère sur les coordonnées x et calcule la coordonnée y
          correspondante.
        * Si la valeur absolue de la pente est supérieure ou égale à 1 (ligne plus proche de la verticale), la méthode
          `drawCloserToVertical` est utilisée. Cette méthode itère sur les coordonnées y et calcule la coordonnée x
          correspondante.

    * **Méthodes `drawCloserToHorizontal` et `drawCloserToVertical`:** Ces méthodes parcourent l'intervalle des
      coordonnées x ou y, respectivement, et calculent l'autre coordonnée en utilisant la pente et l'ordonnée à
      l'origine. La fonction `Math.round` est utilisée pour arrondir les coordonnées calculées à l'entier le plus
      proche. Enfin, la méthode `SetPixel` de l'objet `Image` est appelée pour dessiner chaque point de la ligne.

En résumé, `Line` est une classe plus générale et flexible pour dessiner des lignes de toutes orientations. Sa méthode
`draw` utilise des optimisations et gère les cas particuliers pour garantir un dessin précis et efficace. L'utilisation
de `VLine` pour les lignes verticales est un bon exemple de réutilisation de code et de gestion des cas limites.



-------

??? info "Utilisation de l'IA"
    Page rédigée en partie avec l'aide d'un assistant IA. L'IA a été utilisée pour générer des 
    explications, des exemples et/ou des suggestions de structure. Toutes les informations ont 
    été vérifiées, éditées et complétées par l'auteur.

