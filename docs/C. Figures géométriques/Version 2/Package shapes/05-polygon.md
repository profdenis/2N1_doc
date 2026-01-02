# Classes `PolyLine` et `Polygon`

## Classe `PolyLine`

??? note "Code"

    ```java
    package v2.shapes;
    
    import java.awt.Color;
    
    public class PolyLine {
        public static final Color defaultDrawColor = Color.BLACK;
    
        private Point[] points;
    
        private Color drawColor;
    
        public PolyLine(Point[] points) {
            this(points, defaultDrawColor);
        }
    
        public PolyLine(Point[] points, Color drawColor) {
            this.points = points;
            this.drawColor = drawColor;
        }
    
        public Color getDrawColor() {
            return drawColor;
        }
    
        public void setDrawColor(Color drawColor) {
            this.drawColor = drawColor;
        }
    
        public Point[] getPoints() {
            return points;
        }
    
        public void setPoints(Point[] points) {
            this.points = points;
        }
    
        public void draw(Image image) {
            for (int i = 1; i < points.length; i++) {
                new Line(points[i - 1], points[i], drawColor).draw(image);
            }
        }
    }
    ```

La classe `PolyLine` représente une série de segments de ligne connectés. Elle prend en entrée un tableau d'objets
`Point`, qui définissent les sommets de la *"polyligne"* (ligne brisée, ou segmentée). Elle possède également une
propriété `drawColor` pour spécifier la couleur des segments de ligne.

La méthode `draw` itère à travers le tableau `points`, dessinant un segment de `Line` entre chaque paire de points
consécutifs en utilisant la `drawColor` spécifiée. En effet, elle dessine une ligne de `points[0]` à `points[1]`, puis
de `points[1]` à `points[2]`, et ainsi de suite, jusqu'à ce que le dernier point soit atteint.

## Classe `Polygon`

??? note "Code"

    ```java
    package v2.shapes;
    
    import java.awt.*;
    
    public class Polygon {
        public static final Color defaultDrawColor = Color.BLACK;
    
        private Point[] points;
    
        private Color drawColor;
    
        public Polygon(Point[] points) {
            this(points, defaultDrawColor);
        }
    
        public Polygon(Point[] points, Color drawColor) {
            this.points = points;
            this.drawColor = drawColor;
        }
    
        public Color getDrawColor() {
            return drawColor;
        }
    
        public void setDrawColor(Color drawColor) {
            this.drawColor = drawColor;
        }
    
        public Point[] getPoints() {
            return points;
        }
    
        public void setPoints(Point[] points) {
            this.points = points;
        }
    
        public void draw(Image image) {
            new PolyLine(points, drawColor).draw(image);
            new Line(points[0], points[points.length - 1], drawColor).draw(image);
        }
    }
    ```

La classe `Polygon` représente un polygone fermé. Comme `PolyLine`, elle utilise un tableau de `Point` pour ses sommets
et une `drawColor` pour la couleur.

La principale différence réside dans la méthode `draw`.  `Polygon` dessine non seulement une ligne entre chaque paire de
points consécutifs (comme le fait `PolyLine`), mais elle dessine également une ligne fermant le polygone, entre le
dernier point (`points[points.length - 1]`) et le premier point (`points[0]`). Elle utilise `PolyLine` pour dessiner les
segments connectés et ensuite dessine explicitement la ligne fermante avec
`new Line(points[0], points[points.length - 1], drawColor).draw(image);`. Cela crée un polygone complet plutôt qu'une
simple ligne brisée.




-------

??? info "Utilisation de l'IA"
    Page rédigée en partie avec l'aide d'un assistant IA. L'IA a été utilisée pour générer des 
    explications, des exemples et/ou des suggestions de structure. Toutes les informations ont 
    été vérifiées, éditées et complétées par l'auteur.
