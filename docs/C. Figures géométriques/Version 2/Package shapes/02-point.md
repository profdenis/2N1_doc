# Classe `Point`

??? note "Code"

    ```java
    package v2.shapes;

    import java.awt.Color;
    
    public class Point {
    
        public static final Color defaultDrawColor = Color.BLACK;
    
        private int x;
        private int y;
    
        private Color drawColor;
    
    
        public Point(int x, int y) {
            this(x, y, defaultDrawColor);
        }
    
        public Point(int x, int y, Color color) {
            this.x = x;
            this.y = y;
            this.drawColor = color;
        }
    
        public int getX() {
            return x;
        }
    
        public void setX(int x) {
            this.x = x;
        }
    
        public int getY() {
            return y;
        }
    
        public void setY(int y) {
            this.y = y;
        }
    
        public Color getDrawColor() {
            return drawColor;
        }
    
        public void setDrawColor(Color drawColor) {
            this.drawColor = drawColor;
        }
    
        public void draw(Image image) {
            image.setPixel(x, y, drawColor);
        }
    }
    ```

La classe `Point` représente un point dans un espace bidimensionnel et possède des propriétés pour ses coordonnées x et
y, ainsi que pour sa couleur de dessin.

Voici une explication des différents éléments de la classe :

* **`defaultDrawColor`**: Une constante statique qui définit la couleur de dessin par défaut comme étant le noir.
* **`x`**: Une variable d'instance entière qui représente la coordonnée x du point.
* **`y`**: Une variable d'instance entière qui représente la coordonnée y du point.
* **`drawColor`**: Une variable d'instance de type `Color` qui représente la couleur utilisée pour dessiner le point.
* **`Point(int x, int y)`**: Un constructeur qui prend les coordonnées x et y en arguments et initialise le point avec
  la couleur de dessin par défaut.
* **`Point(int x, int y, Color color)`**: Un constructeur qui prend les coordonnées x et y et une couleur en arguments
  et initialise le point avec la couleur spécifiée.
* **`getX()`**: Une méthode getter qui renvoie la coordonnée x du point.
* **`setX(int x)`**: Une méthode setter qui définit la coordonnée x du point.
* **`getY()`**: Une méthode getter qui renvoie la coordonnée y du point.
* **`setY(int y)`**: Une méthode setter qui définit la coordonnée y du point.
* **`getDrawColor()`**: Une méthode getter qui renvoie la couleur de dessin du point.
* **`setDrawColor(Color drawColor)`**: Une méthode setter qui définit la couleur de dessin du point.
* **`draw(Image image)`**: Une méthode qui dessine le point sur une image donnée en utilisant la couleur de dessin
  spécifiée.

En résumé, la classe `Point` fournit une représentation simple d'un point avec des coordonnées et une couleur, ainsi que
des méthodes pour accéder à ces propriétés et dessiner le point sur une image.




-------

??? info "Utilisation de l'IA"
    Page rédigée en partie avec l'aide d'un assistant IA. L'IA a été utilisée pour générer des 
    explications, des exemples et/ou des suggestions de structure. Toutes les informations ont 
    été vérifiées, éditées et complétées par l'auteur.

