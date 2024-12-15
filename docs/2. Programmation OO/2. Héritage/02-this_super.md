# Les mots-clé `this` et `super`

Dans le contexte de la programmation orientée objet en Java, voici les différences clés entre `this` et `super` :

## Définition et Portée

**this** fait référence à l'instance courante de la classe actuelle, tandis que **super** fait référence à la classe
parente immédiate[1].

## Utilisations Principales

### Accès aux attributs

- `this.attribut` accède aux attributs de la classe courante
- `super.attribut` accède aux attributs de la classe parente[1]

### Appel des constructeurs

- `this()` appelle un autre constructeur de la même classe
- `super()` appelle le constructeur de la classe parente[2]

### Résolution des conflits de noms

```java
public class Etudiant extends Personne {
    private String nom; // Attribut local

    public void setNom(String nom) {
        this.nom = nom;        // Attribut local
        super.nom = nom;       // Attribut de la classe parente
    }
}
```

## Règles importantes

- `super()` doit être la première instruction dans un constructeur[3]
- On ne peut pas utiliser `this()` et `super()` dans le même constructeur[5]
- L'utilisation de `super` est essentielle dans l'héritage pour accéder aux membres de la classe parente qui sont
  masqués par la classe enfant[3]

## Tableau comparatif

| Caractéristique | this                                              | super                                             |
|-----------------|---------------------------------------------------|---------------------------------------------------|
| Référence       | Instance courante                                 | Classe parente                                    |
| Portée          | Classe actuelle                                   | Classe parente immédiate                          |
| Constructeur    | Appelle autre constructeur de la même classe      | Appelle constructeur de la classe parente         |
| Position        | Première instruction si utilisé dans constructeur | Première instruction si utilisé dans constructeur |

Citations:
[1] https://www.studysmarter.fr/resumes/informatique/programmation-informatique/mot-cle-this-de-java/
[2] https://www.justacademy.co/blog-detail/difference-between-this-and-super-in-java
[3] https://www.scientecheasy.com/2019/11/difference-between-super-and-this-keyword-in-java.html/
[4] https://www.javatpoint.com/this-vs-super-in-java
[5] https://www.scaler.com/topics/java/this-and-super-keyword-in-java/