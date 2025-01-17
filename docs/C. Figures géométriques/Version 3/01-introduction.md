# Introduction

Dans cette version, la classe `Shape` est une classe de base abstraite pour toutes les formes. Elle centralise les
propriétés et les comportements communs à toutes les formes. Dans cet exemple, la propriété commune est la couleur de
dessin (`drawColor`).

Elle est déclarée abstraite pour deux raisons principales :

1. **Impossibilité d'instancier directement :** Une forme "générique" n'a pas de sens en soi. On ne peut pas dessiner
   une "forme" sans plus de précisions. L'abstraction empêche la création d'objets `Shape` directement. On doit créer
   des instances de classes concrètes comme `Point` ou `Circle`.

2. **Définition d'un contrat :** La méthode `draw` est déclarée abstraite dans `Shape`. Cela oblige toutes les classes
   dérivées (comme `Point` et `Circle`) à fournir leur propre implémentation de la méthode `draw`. Chaque forme doit
   savoir se dessiner elle-même. C'est ce qu'on appelle un "contrat" : toute classe qui hérite de `Shape` s'engage à
   implémenter `draw`.

En résumé, `Shape` fournit un modèle commun pour les formes, gère les propriétés partagées, et impose aux formes
concrètes de définir comment elles se dessinent.



-------

!!! note "Note"
      Page rédigée en partie avec l'aide d'un assistant IA, principalement à l'aide de Perplexity AI, avec le *LLM*
      **Claude 3.5 Sonnet**. L'IA a été utilisée pour générer des explications, des exemples et/ou des suggestions de
      structure. Toutes les informations ont été vérifiées, éditées et complétées par l'auteur.