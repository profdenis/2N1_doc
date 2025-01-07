# La classe `Image`

La classe `Image` est une encapsulation simplifiée de la classe `java.awt.image.BufferedImage` pour faciliter le dessin
de formes géométriques et leur sauvegarde dans un fichier. Elle offre une interface plus intuitive pour manipuler une
image en mémoire.

Voici les principaux aspects de la classe :

* **Dimensions et couleur de fond :** Elle définit la largeur (`width`), la hauteur (`height`) et la couleur de fond
  (`backgroundColor`) de l'image. Des valeurs par défaut sont fournies (`defaultWidth`, `defaultHeight`,
  `defaultBackgroundColor`). Plusieurs constructeurs permettent de créer une image avec différentes combinaisons de ces
  paramètres.

* **`BufferedImage` :** L'attribut `bufferedImage` est une instance de `java.awt.image.BufferedImage`, qui est la
  représentation sous-jacente de l'image en mémoire.

* **`Clear()` :** Cette méthode remplit l'image avec la couleur spécifiée, permettant d'effacer le contenu précédent.

* **`GetPixel()` et `SetPixel()` :** Ces méthodes permettent respectivement de lire et de modifier la couleur d'un pixel
  spécifique de l'image. La méthode `GetPixel()` retourne la couleur de fond par défaut si les coordonnées sont hors
  limites, au lieu de générer une erreur.

* **`Save()` :** Cette méthode enregistre l'image dans un fichier au format PNG. Elle gère les exceptions `IOException`
  qui pourraient survenir lors de l'écriture du fichier.

En résumé, la classe `Image` simplifie l'utilisation de `BufferedImage` en fournissant une interface plus simple pour
créer, manipuler et enregistrer des images. Elle masque la complexité de `BufferedImage` et offre des fonctionnalités de
base pour le dessin, comme la définition de pixels et l'effacement de l'image.



-------

!!! note "Note"
    Page rédigée en partie avec l'aide d'un assistant IA, principalement à l'aide de Perplexity AI, avec le *LLM* 
    **Claude 3.5 Sonnet**. L'IA a été utilisée pour générer des explications, des exemples et/ou des suggestions de 
    structure. Toutes les informations ont été vérifiées, éditées et complétées par l'auteur.