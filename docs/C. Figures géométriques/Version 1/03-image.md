# La classe `Image`

- Github: [Image.java](https://github.com/profdenis/Shapes/tree/master/src/v1/Image.java)

??? note "Code"

    ```java
    package v1;
    
    import javax.imageio.ImageIO;
    import java.awt.*;
    import java.awt.image.BufferedImage;
    import java.io.File;
    import java.io.IOException;
    
    public class Image {
    
        public static int defaultWidth = 100;
        public static int defaultHeight = 100;
        public static Color defaultBackgroundColor = Color.WHITE;
    
        public int width;
        public int height;
        public Color backgroundColor;
        public BufferedImage bufferedImage;
    
        public Image() {
            this(defaultWidth, defaultHeight, defaultBackgroundColor);
        }
    
        public Image(int width) {
            //noinspection SuspiciousNameCombination
            this(width, width, defaultBackgroundColor);
        }
    
        public Image(int width, int height) {
            this(width, height, defaultBackgroundColor);
        }
    
    
        public Image(int width, int height, Color backgroundColor) {
            this.width = width;
            this.height = height;
            this.backgroundColor = backgroundColor;
            bufferedImage = new BufferedImage(width, height, BufferedImage.TYPE_INT_ARGB);
            Clear(this.backgroundColor);
        }
    
        public void Clear(Color clearColor) {
            for (int i = 0; i < width; i++) {
                for (int j = 0; j < height; j++) {
                    SetPixel(i, j, clearColor);
                }
            }
        }
    
        public Color GetPixel(int x, int y) {
            if (x >= 0 && x < this.width && y >= 0 && y < this.height) {
                return GetPixel(x, y);
            }
            // throw exception?
            return backgroundColor;
        }
    
        public void SetPixel(int x, int y, Color drawColor) {
            if (x >= 0 && x < this.width && y >= 0 && y < this.height) {
                bufferedImage.setRGB(x, y, drawColor.getRGB());
            }
        }
    
        public void Save(String filename) {
            try {
                File outputFile = new File(filename);
                ImageIO.write(bufferedImage, "PNG", outputFile);
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
    ```

La classe `Image` est une encapsulation simplifiée de la classe `java.awt.image.BufferedImage` pour faciliter le dessin
de formes géométriques et leur sauvegarde dans un fichier. Elle offre une interface plus intuitive pour manipuler une
image en mémoire.

Voici les principaux aspects de la classe :

* **Dimensions et couleur de fond** 
      * Elle définit la largeur (`width`), la hauteur (`height`) et la couleur de fond
        (`backgroundColor`) de l'image. Des valeurs par défaut sont fournies (`defaultWidth`, `defaultHeight`,
        `defaultBackgroundColor`). Plusieurs constructeurs permettent de créer une image avec différentes combinaisons de ces
        paramètres.

* `BufferedImage` 
      * L'attribut `bufferedImage` est une instance de `java.awt.image.BufferedImage`, qui est la
        représentation sous-jacente de l'image en mémoire.

* `Clear()`
      * Cette méthode remplit l'image avec la couleur spécifiée, permettant d'effacer le contenu précédent.

* `GetPixel()` et `SetPixel()` 
      * Ces méthodes permettent respectivement de lire et de modifier la couleur d'un pixel
        spécifique de l'image. La méthode `GetPixel()` retourne la couleur de fond par défaut si les coordonnées sont hors
        limites, au lieu de générer une erreur.

* `Save()`
      * Cette méthode enregistre l'image dans un fichier au format PNG. Elle gère les exceptions `IOException`
        qui pourraient survenir lors de l'écriture du fichier.

En résumé, la classe `Image` simplifie l'utilisation de `BufferedImage` en fournissant une interface plus simple pour
créer, manipuler et enregistrer des images. Elle masque la complexité de `BufferedImage` et offre des fonctionnalités de
base pour le dessin, comme la définition de pixels et l'effacement de l'image.



-------

!!! note "Note"
    Page rédigée en partie avec l'aide d'un assistant IA, principalement à l'aide de Perplexity AI, avec le *LLM* 
    **Claude 3.5 Sonnet**. L'IA a été utilisée pour générer des explications, des exemples et/ou des suggestions de 
    structure. Toutes les informations ont été vérifiées, éditées et complétées par l'auteur.