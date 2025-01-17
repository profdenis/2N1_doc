# Classe `Circle`

??? note "Code"

    ```java
    package v2.shapes;
    
    import java.awt.*;
    
    @SuppressWarnings("DuplicatedCode")
    public class Circle {
        public static final Color defaultDrawColor = Color.BLACK;
    
        private Point center;
        private int radius;
    
        private Color drawColor;
    
        public Circle(Point center, int radius) {
            this(center, radius, defaultDrawColor);
        }
    
        public Circle(Point center, int radius, Color drawColor) {
            this.center = center;
            this.radius = radius;
            this.drawColor = drawColor;
        }
    
        public Point getCenter() {
            return center;
        }
    
        public void setCenter(Point center) {
            this.center = center;
        }
    
        public int getRadius() {
            return radius;
        }
    
        public void setRadius(int radius) {
            this.radius = radius;
        }
    
        public Color getDrawColor() {
            return drawColor;
        }
    
        public void setDrawColor(Color drawColor) {
            this.drawColor = drawColor;
        }
    
        public void draw(Image image) {
            int cos45 = (int) Math.round(radius * Math.cos(Math.PI / 4));
    
            for (int i = 0; i <= cos45; i++) {
                int j = (int) Math.round(Math.sqrt(radius * radius - i * i));
                image.setPixel(center.getX() + i, center.getY() + j, drawColor); // point 1
                image.setPixel(center.getX() - i, center.getY() + j, drawColor); // point 2: symétrie du point 1 par rapport à l'axe Y
    
                image.setPixel(center.getX() + i, center.getY() - j, drawColor); // point 3: symétrie du point 1 par rapport à l'axe X
                image.setPixel(center.getX() - i, center.getY() - j, drawColor); // point 4: symétrie du point 3 par rapport à l'axe Y
    
                image.setPixel(center.getX() + j, center.getY() + i, drawColor); // point 5: symétrie du point 1 par rapport à la diagonale 45°
                image.setPixel(center.getX() + j, center.getY() - i, drawColor); // point 6: symétrie du point 5 par rapport à l'acenter.getX()e X
    
                image.setPixel(center.getX() - j, center.getY() + i, drawColor); // point 7: symétrie du point 5 par rapport à l'axe Y
                image.setPixel(center.getX() - j, center.getY() - i, drawColor); // point 8: symétrie du point 7 par rapport à l'axe X
            }
        }
    }
    ```

La classe `Circle` représente un cercle et fournit des méthodes pour le dessiner sur une image. Détaillons la méthode
`Draw` :

```java
public void draw(Image image) {
    int cos45 = (int) Math.round(radius * Math.cos(Math.PI / 4));

    for (int i = 0; i <= cos45; i++) {
        int j = (int) Math.round(Math.sqrt(radius * radius - i * i));
        image.setPixel(center.getX() + i, center.getY() + j, drawColor); // point 1
        // ... autres points
    }
}
```

La méthode `draw` prend un objet `Image` en paramètre, sur lequel le cercle sera dessiné. Elle utilise un algorithme
simple pour dessiner le cercle point par point en exploitant les symétries du cercle :

1. **Calcul de `cos45`:**  `cos45` est utilisé pour optimiser la boucle. Il représente la distance horizontale ou
   verticale entre le centre du cercle et le point à 45 degrés. La boucle itère donc de 0 jusqu'à cette valeur pour
   couvrir un octant du cercle. Les autres points sont calculés par symétrie.

2. **Boucle principale :** La boucle `for` itère de `i = 0` à `cos45`.  `i` représente la distance horizontale par
   rapport au centre du cercle.

3. **Calcul de `j`:** À l'intérieur de la boucle, `j` est calculé.  `j` représente la distance verticale correspondante
   à `i` pour un point sur le cercle. L'équation du cercle est $x^2 + y^2 = r^2$, donc y = sqrt(r² - x²), où`i` joue le 
   rôle de x et `j` celui de y.

4. **Dessin des points :** Les lignes suivantes dessinent 8 points symétriques sur l'image en utilisant
   `image.setPixel()`. Chaque appel à `setPixel()` prend les coordonnées x et y du point et la couleur `drawColor` du
   cercle. Les 8 points sont calculés comme suit :
    * **Point 1:** `(x + i, y + j)` - Point initial dans le premier octant
    * **Point 2:** `(x - i, y + j)` - Symétrique du point 1 par rapport à l'axe Y
    * **Point 3:** `(x + i, y - j)` - Symétrique du point 1 par rapport à l'axe X
    * **Point 4:** `(x - i, y - j)` - Symétrique du point 3 par rapport à l'axe Y
    * **Point 5:** `(x + j, y + i)` - Symétrique du point 1 par rapport à la diagonale à 45°
    * **Point 6:** `(x + j, y - i)` - Symétrique du point 5 par rapport à l'axe X
    * **Point 7:** `(x - j, y + i)` - Symétrique du point 5 par rapport à l'axe Y
    * **Point 8:** `(x - j, y - i)` - Symétrique du point 7 par rapport à l'axe X

En dessinant ces 8 points à chaque itération, la méthode `draw` dessine efficacement un cercle complet.




-------

!!! note "Note"
    Page rédigée en partie avec l'aide d'un assistant IA, principalement à l'aide de Perplexity AI, avec le *LLM*
    **Claude 3.5 Sonnet**. L'IA a été utilisée pour générer des explications, des exemples et/ou des suggestions de
    structure. Toutes les informations ont été vérifiées, éditées et complétées par l'auteur.
