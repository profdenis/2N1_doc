---
icon: material/file-document-outline
---

# 6. La classe `Object`

La classe Object est la classe racine de la hiérarchie des classes en Java. Elle est la superclasse directe ou indirecte
de toutes les autres classes[1][8]. Voici les principales caractéristiques de la classe Object :

## Rôle fondamental

- Toute classe en Java hérite implicitement de Object si aucune autre superclasse n'est spécifiée[2][9].
- Elle fournit des méthodes de base communes à tous les objets Java.

## Méthodes importantes

La classe Object définit plusieurs méthodes essentielles[1][11] :

1. `toString()` : Retourne une représentation en chaîne de caractères de l'objet.
2. `equals(Object obj)` : Compare l'objet avec un autre pour déterminer l'égalité.
3. `hashCode()` : Retourne une valeur de hachage pour l'objet.
4. `getClass()` : Retourne un objet de type Class représentant la classe de l'objet.
5. `clone()` : Crée et retourne une copie de l'objet.
6. `finalize()` : Appelée par le ramasse-miettes avant que l'objet ne soit détruit.

## Utilisation

- Grâce à l'héritage de Object, toutes les classes Java peuvent utiliser ces méthodes de base[9].
- Il est courant de redéfinir certaines de ces méthodes (comme toString() ou equals()) dans les classes personnalisées
  pour adapter leur comportement[1].

## Polymorphisme

- Comme toutes les classes héritent de Object, une variable de type Object peut référencer n'importe quel objet
  Java[12].
- Cela permet une grande flexibilité dans la manipulation des objets, notamment pour les collections génériques.

En comprenant bien la classe Object et ses méthodes, les développeurs peuvent mieux exploiter les fonctionnalités de
base offertes à tous les objets en Java et améliorer la conception de leurs propres classes.

??? note "Citations"

      - [1] https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html
      - [2] https://fr.wikibooks.org/wiki/Programmation_Java/H%C3%A9ritage
      - [3] https://datascientest.com/programmation-orientee-objet-guide-ultime
      - [4] https://www.w3schools.com/java/java_classes.asp
      - [5] https://codegym.cc/fr/groups/posts/fr.942.hritage-en-java
      - [6] https://www.u-picardie.fr/ferment/java/cours/chap08_d.html
      - [7] https://miashs-www.u-ga.fr/prevert/Prog/Java/CoursJava/classes1.html
      - [8] https://blog.paumard.org/cours/java/chap07-heritage-interface-heritage.html
      - [9] https://www.jmdoudoux.fr/java/dej/chap-poo.htm
      - [10] https://www.digitalocean.com/community/tutorials/inheritance-java-example
      - [11] https://blog.paumard.org/cours/java/chap03-object-string-object.html
      - [12] https://gayerie.dev/epsi-b3-java/langage_java/heritage_composition.html



-------

??? info "Utilisation de l'IA"
      Page rédigée en partie avec l'aide d'un assistant IA, principalement à l'aide de Perplexity AI, avec le *LLM*
      **Claude 3.5 Sonnet**. L'IA a été utilisée pour générer des explications, des exemples et/ou des suggestions de
      structure. Toutes les informations ont été vérifiées, éditées et complétées par l'auteur.
     