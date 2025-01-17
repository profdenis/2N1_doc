# Classe `Circle`

??? note "Code"

      ```java
      package v3.shapes;

      import java.awt.Color;
      
      public class Circle extends Shape {
          private Point center;
          private int radius;
      
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
      
          public Circle(Point center, int radius, Color drawColor)
          {
              super(drawColor);
              this.center = center;
              this.radius = radius;
          }
      
          public Circle(Point center, int radius)
          {
              this(center, radius, defaultDrawColor);
          }
      
          @Override
          public void draw(Image image) {
              int x = 0;
              int y = radius;
              int d = 3 - 2 * radius;
              drawCirclePoints(image, center.getX(), center.getY(), x, y);
              while (y >= x) {
                  x++;
                  if (d > 0) {
                      y--;
                      d = d + 4 * (x - y) + 10;
                  } else {
                      d = d + 4 * x + 6;
                  }
                  drawCirclePoints(image, center.getX(), center.getY(), x, y);
              }
          }
      
          private void drawCirclePoints(Image image, int x, int y, int x1, int y1) {
              image.setPixel(x + x1, y + y1, drawColor);
              image.setPixel(x - x1, y + y1, drawColor);
              image.setPixel(x + x1, y - y1, drawColor);
              image.setPixel(x - x1, y - y1, drawColor);
              image.setPixel(x + y1, y + x1, drawColor);
              image.setPixel(x - y1, y + x1, drawColor);
              image.setPixel(x + y1, y - x1, drawColor);
              image.setPixel(x - y1, y - x1, drawColor);
          }
      }
      ```

Les différences principales entre les versions 2 et 3 de `Circle` résident dans l'héritage, la gestion de la couleur et
l'algorithme de dessin :

### Version 2

- **Classe indépendante :** `Circle` est une classe autonome sans héritage.
- **Gestion des couleurs :** La couleur de dessin (`drawColor`) est gérée directement dans la classe`Circle`, avec une
  valeur par défaut (`defaultDrawColor`).
- **Algorithme de dessin :** Utilise un algorithme basé sur le calcul de points symétriques pour dessiner le cercle. Cet
  algorithme est relativement simple, mais peut être moins précis et performant pour les grands rayons.

### Version 3

- **Héritage de `Shape` :** `Circle` hérite de la classe `Shape`, héritant ainsi de la propriété `drawColor` et de ses
  méthodes associées. Cela réduit la redondance de code et améliore la cohérence.
- **Algorithme de dessin :** Utilise l'algorithme de Bresenham pour tracer le cercle. Cet algorithme est plus efficace et
  précis que celui utilisé dans la version 2, en particulier pour les grands cercles. Il utilise des opérations
  entières, ce qui le rend plus rapide. La logique est encapsulée dans la méthode privée `drawCirclePoints`.

En résumé, la version 3 de `Circle` bénéficie de l'héritage de `Shape` pour une meilleure structure du code.
L'utilisation de l'algorithme de Bresenham améliore significativement les performances et la précision du dessin.


-------

!!! note "Note"
    Page rédigée en partie avec l'aide d'un assistant IA, principalement à l'aide de Perplexity AI, avec le *LLM*
    **Claude 3.5 Sonnet**. L'IA a été utilisée pour générer des explications, des exemples et/ou des suggestions de
    structure. Toutes les informations ont été vérifiées, éditées et complétées par l'auteur.
