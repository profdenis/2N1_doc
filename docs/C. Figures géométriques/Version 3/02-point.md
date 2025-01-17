# Classe `Point`

??? note "Code"

    ```java
    package v3.shapes;
    
    import java.awt.Color;
    
    public class Point extends Shape {
        private int x;
        private int y;
    
        public int getX() {
            return x;
        }
    
        public void setX(int x) {
            if (x < 0) {
                throw new IllegalArgumentException("X cannot be negative");
            }
            this.x = x;
        }
    
        public int getY() {
            return y;
        }
    
        public void setY(int y) {
            if (y < 0) {
                throw new IllegalArgumentException("X cannot be negative");
            }
            this.y = y;
        }
    
    
        public Point(int x, int y, Color drawColor) {
            super(drawColor);
            setX(x);
            setY(y);
        }
    
        public Point(int x, int y) {
            this(x, y, Shape.defaultDrawColor);
        }
    
        public void draw(Image image) {
            image.setPixel(x, y, drawColor);
        }
    
        @Override
        public String toString() {
            return "Point{" +
                    "x=" + x +
                    ", y=" + y +
                    '}';
        }
    }
    ```



La nouvelle version de `Point` diffèrent principalement de la v2 par sa relation avec la classe `Shape` et la gestion
des coordonnées :

### Version 2

- **Classe indépendante :** `Point` est une classe autonome, sans héritage.
- **Gestion des couleurs :** La couleur de dessin (`drawColor`) est gérée directement dans la classe `Point`, avec une
  valeur par défaut (`defaultDrawColor`).
- **Pas de validation des coordonnées :** Les coordonnées `x` et `y` peuvent prendre n'importe quelle valeur entière, y
  compris des valeurs négatives.

### Version 3

- **Héritage de `Shape` :** `Point` hérite de la classe `Shape`, héritant ainsi de la propriété `drawColor` et de ses
  méthodes associées.
- **Validation des coordonnées :** Les méthodes `setX` et `setY` valident maintenant les coordonnées pour s'assurer 
  qu'elles ne sont pas négatives, levant une exception `IllegalArgumentException` si nécessaire. Ceci ajoute une 
  sécurité et une cohérence au code.

En résumé, la version 3 de `Point` est plus robuste et mieux intégrée à la hiérarchie des formes grâce à l'héritage de
`Shape`. La validation des coordonnées améliore également la qualité du code.



-------

!!! note "Note"
    Page rédigée en partie avec l'aide d'un assistant IA, principalement à l'aide de Perplexity AI, avec le *LLM*
    **Claude 3.5 Sonnet**. L'IA a été utilisée pour générer des explications, des exemples et/ou des suggestions de
    structure. Toutes les informations ont été vérifiées, éditées et complétées par l'auteur.