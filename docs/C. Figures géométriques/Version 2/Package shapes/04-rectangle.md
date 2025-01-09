# Classes `Rectangle` et `Square`

## Classe `Rectangle`

??? note "Code"

    ```java
    package v2.shapes;
    
    import java.awt.*;
    
    public class Rectangle {
        public static final Color defaultDrawColor = Color.BLACK;
    
        private Point topLeft;
        private int width;
        private int height;
    
        private Color drawColor;
    
        public Rectangle(Point topLeft, int width, int height) {
            this(topLeft, width, height, defaultDrawColor);
        }
    
        public Rectangle(Point topLeft, int width, int height, Color drawColor) {
            this.topLeft = topLeft;
            this.width = width;
            this.height = height;
            this.drawColor = drawColor;
        }
    
        public Point getTopLeft() {
            return topLeft;
        }
    
        public void setTopLeft(Point topLeft) {
            this.topLeft = topLeft;
        }
    
        public int getWidth() {
            return width;
        }
    
        public void setWidth(int width) {
            this.width = width;
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
    
        public void Draw(Image image) {
            new VLine(topLeft, height, drawColor).Draw(image);
            new HLine(topLeft, width, drawColor).Draw(image);
            new VLine(new Point(topLeft.getX() + width, topLeft.getY()), height, drawColor).Draw(image);
            new HLine(new Point(topLeft.getX(), topLeft.getY() + height), width, drawColor).Draw(image);
        }
    }
    ```

La classe `Rectangle` représente un rectangle et fournit des méthodes pour le dessiner sur une image. Décomposons le
code :

**Champs :**

* `topLeft`: Un objet `Point` représentant le coin supérieur gauche du rectangle.
* `width`: Un entier représentant la largeur du rectangle.
* `height`: Un entier représentant la hauteur du rectangle.
* `drawColor`: Un objet `Color` représentant la couleur utilisée pour dessiner le rectangle. Par défaut, il est noir (
  `defaultDrawColor`).

**Constructeurs :**

* `Rectangle(Point topLeft, int width, int height)`: Ce constructeur prend le coin supérieur gauche, la largeur et la
  hauteur du rectangle. Il utilise la couleur de dessin par défaut (noir).
* `Rectangle(Point topLeft, int width, int height, Color drawColor)`: Ce constructeur prend le coin supérieur gauche, la
  largeur, la hauteur et la couleur de dessin du rectangle.

**Méthodes :**

* `getTopLeft()`: Renvoie le point du coin supérieur gauche du rectangle.
* `setTopLeft(Point topLeft)`: Définit le point du coin supérieur gauche du rectangle.
* `getWidth()`: Renvoie la largeur du rectangle.
* `setWidth(int width)`: Définit la largeur du rectangle.
* `getHeight()`: Renvoie la hauteur du rectangle.
* `setHeight(int height)`: Définit la hauteur du rectangle.
* `getDrawColor()`: Renvoie la couleur de dessin du rectangle.
* `setDrawColor(Color drawColor)`: Définit la couleur de dessin du rectangle.
* `Draw(Image image)`: Cette méthode dessine le rectangle sur l'image donnée. Pour ce faire, elle dessine quatre
  lignes :
  deux verticales et deux horizontales, à l'aide des classes `VLine` et `HLine` (probablement définies ailleurs dans le
  code). Elle utilise la `drawColor` du rectangle pour les lignes.

En résumé, la classe `Rectangle` encapsule les propriétés d'un rectangle et fournit un moyen de le dessiner sur une
image en utilisant ses dimensions et sa couleur définies.

## Classe `Square`

??? note "Code"

    ```java
    package v2.shapes;
    
    import java.awt.*;
    
    public class Square {
        public static final Color defaultDrawColor = Color.BLACK;
    
        private Point topLeft;
        private int width;
    
        private Color drawColor;
    
        public Square(Point topLeft, int width) {
            this(topLeft, width, defaultDrawColor);
        }
    
        public Square(Point topLeft, int width, Color drawColor) {
            this.topLeft = topLeft;
            this.width = width;
            this.drawColor = drawColor;
        }
    
        public Point getTopLeft() {
            return topLeft;
        }
    
        public void setTopLeft(Point topLeft) {
            this.topLeft = topLeft;
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
    
        public void Draw(Image image) {
            //noinspection SuspiciousNameCombination
            new Rectangle(topLeft, width, width, drawColor).Draw(image);
        }
    }
    ```

La classe `Square` représente un carré. Elle est similaire à la classe `Rectangle`, mais avec quelques différences
clés :

**Champs :**

* `topLeft`: Un objet `Point` représentant le coin supérieur gauche du carré. Identique à `Rectangle`.
* `width`: Un entier représentant la largeur du carré. Dans le cas d'un carré, la largeur est également la hauteur.
* `drawColor`: Un objet `Color` représentant la couleur utilisée pour dessiner le carré. Par défaut, il est noir
  (`defaultDrawColor`). Identique à `Rectangle`.

**Remarquez l'absence d'un champ `height`.** Puisqu'un carré a des côtés égaux, seule la `width` est nécessaire.

**Constructeurs :**

* `Square(Point topLeft, int width)`: Ce constructeur prend le coin supérieur gauche et la largeur du carré. Il utilise
  la couleur de dessin par défaut (noir).
* `Square(Point topLeft, int width, Color drawColor)`: Ce constructeur prend le coin supérieur gauche, la largeur et la
  couleur de dessin du carré.

**Similaire à `Rectangle`, mais sans la hauteur.**

**Méthodes :**

* `getTopLeft()`, `setTopLeft(Point topLeft)`, `getWidth()`, `setWidth(int width)`, `getDrawColor()`, et
  `setDrawColor(Color drawColor)`: Fonctionnent de la même manière que dans `Rectangle`.
* `Draw(Image image)`: Cette méthode dessine le carré sur l'image donnée. **Au lieu de dessiner quatre lignes
  individuelles, elle utilise la méthode `Draw()` de la classe `Rectangle` en lui passant la largeur pour à la fois la
  largeur et la hauteur, dessinant ainsi un carré.** C'est une différence importante dans l'implémentation.

En résumé, puisqu'un carré est un rectangle avec la contrainte supplémentaire que la hauteur et la largeur sont égales,
`Square` et `Rectangle` se ressemblent beaucoup. `Square` simplifie la représentation d'un carré en utilisant seulement
la largeur et en déléguant le dessin à la classe `Rectangle`.



-------

!!! note "Note"
    Page rédigée en partie avec l'aide d'un assistant IA, principalement à l'aide de Perplexity AI, avec le *LLM*
    **Claude 3.5 Sonnet**. L'IA a été utilisée pour générer des explications, des exemples et/ou des suggestions de
    structure. Toutes les informations ont été vérifiées, éditées et complétées par l'auteur.
