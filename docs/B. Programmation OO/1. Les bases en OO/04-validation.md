---
icon: material/file-document-outline
---

# 4. Validation dans les mutateurs

L'utilisation d'exceptions pour gérer les cas invalides est souvent préférable car elle force le code appelant à gérer
explicitement les erreurs, contrairement à un retour silencieux qui pourrait passer inaperçu.

## Version avec Exception

D'abord, définissons une exception personnalisée :

```java
public class AgeInvalideException extends Exception {
    public AgeInvalideException(String message) {
        super(message);
    }
}
```

Ensuite, modifions le setter pour utiliser cette exception :

```java
public class Personne {
    private int age;

    public void setAge(int age) throws AgeInvalideException {
        if (age < 0) {
            throw new AgeInvalideException("L'âge ne peut pas être négatif");
        }
        if (age > 125) {
            throw new AgeInvalideException("L'âge ne peut pas dépasser 125 ans");
        }
        this.age = age;
    }
}
```

## Utilisation

```java
Personne personne = new Personne();
try {
        personne.setAge(-5);
} catch(AgeInvalideException e) {
        System.out.println("Erreur : "+e.getMessage());
}
```

## Avantages de l'Approche par Exception

Cette approche est plus appropriée car :

- Elle rend explicite le fait qu'une erreur peut survenir
- Elle force le code appelant à gérer le cas d'erreur (soit avec try-catch, soit en propageant l'exception)
- Elle permet de transmettre des informations détaillées sur l'erreur
- Elle sépare clairement le code de gestion des erreurs du code normal
- Elle permet de traiter l'erreur à n'importe quel niveau de la pile d'appel

Cette version est particulièrement utile dans un système plus large où la validation des données est critique et où les
erreurs doivent être gérées de manière appropriée plutôt que d'être ignorées.

## Inconvénients Potentiels

L'utilisation d'exceptions dans la validation de l'âge présente quelques inconvénients :

- Le flot d'exécution devient non linéaire et plus complexe à suivre[1]
- La gestion des exceptions peut rendre le code plus verbeux avec les blocs `try-catch`
- Les exceptions peuvent impacter légèrement les performances si elles sont fréquemment lancées

## Pourquoi les Avantages l'Emportent

Malgré ces inconvénients, l'utilisation d'exceptions reste appropriée ici car :

- La validation de l'âge représente une condition exceptionnelle qui sort du flux normal d'exécution[3]
- Les exceptions permettent de séparer clairement le code de gestion des erreurs du code normal[3]
- Elles fournissent un mécanisme clair pour communiquer les erreurs aux niveaux supérieurs du programme[3]

## Alternative et Conclusion

Une approche alternative serait d'utiliser un système de validation de données avec des contraintes[5], mais pour un 
cas simple comme la validation de l'âge, les exceptions offrent une solution claire et efficace. Les inconvénients sont
mineurs comparés à l'avantage d'avoir un code plus robuste et plus explicite dans la gestion des erreurs.

L'utilisation d'exceptions est particulièrement pertinente ici car il s'agit d'une validation de données qui peut 
échouer en raison de facteurs externes (entrées utilisateur)[3], ce qui correspond exactement au cas d'usage recommandé
pour la gestion des exceptions.

??? note "Citations"
      - [1] https://www.osedea.com/fr/perspective/gerer-et-reduire-les-exceptions
      - [2] https://fr.wikipedia.org/wiki/Syst%C3%A8me_de_gestion_d'exceptions
      - [3] https://canada.lenovo.com/fr/ca/en/glossary/exception-handling/
      - [4] https://javarush.com/fr/groups/posts/fr.701.erreurs-courantes-dans-la-gestion-des-exceptions
      - [5] https://www.jmdoudoux.fr/java/dej/chap-validation_donnees.htm




-------

??? info "Utilisation de l'IA"
    Page rédigée en partie avec l'aide d'un assistant IA. L'IA a été utilisée pour générer des 
    explications, des exemples et/ou des suggestions de structure. Toutes les informations ont 
    été vérifiées, éditées et complétées par l'auteur.