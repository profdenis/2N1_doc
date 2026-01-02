# 🔸3🔸Méthode `toString` et introduction au polymorphisme

La redéfinition de méthodes est un excellent exemple pour introduire le polymorphisme.

## Analyse de toString()

### Dans la classe Personne

```java
public class Personne {
    // ... autres attributs et méthodes ...

    @Override
    public String toString() {
        return prenom + " " + nom + " (" + age + " ans)";
    }
}
```

Cette première version crée une représentation textuelle de base d'une personne. L'annotation `@Override` indique que
nous redéfinissons la méthode `toString()` héritée de la classe `Object`.

### Dans la classe Etudiant

```java
public class Etudiant extends Personne {
    // ... autres attributs et méthodes ...

    @Override
    public String toString() {
        return super.toString() + " - " + programme +
                " (Dossier: " + numeroDossier + ")";
    }
}
```

Cette version :

- Utilise `super.toString()` pour réutiliser le format de base de la classe parente
- Ajoute les informations spécifiques à un étudiant

### Dans la classe Professeur

```java
public class Professeur extends Personne {
    // ... autres attributs et méthodes ...

    @Override
    public String toString() {
        return super.toString() + " - " + departement +
                " (Spécialité: " + specialite + ")";
    }
}
```

## Introduction au Polymorphisme

Le polymorphisme permet à une référence de type parent de manipuler un objet de type enfant. Voici un exemple concret :

```java
public class ExemplePolymorphisme {
    public static void main(String[] args) {
        // Création d'un tableau de Personnes
        Personne[] personnes = new Personne[3];

        // Remplissage avec différents types
        personnes[0] = new Personne("Dupont", "Jean", 30);
        personnes[1] = new Etudiant("Tremblay", "Marie", 20, "12345", "Informatique");
        personnes[2] = new Professeur("Dubois", "Pierre", 45, "Informatique", "Java");

        // Affichage polymorphique
        for (Personne p : personnes) {
            System.out.println(p.toString());
            // ou simplement
            //System.out.println(p);
        }
    }
}
```

### Résultat d'exécution

```
Jean Dupont (30 ans)
Marie Tremblay (20 ans) - Informatique (Dossier: 12345)
Pierre Dubois (45 ans) - Informatique (Spécialité: Java)
```

## Points clés du polymorphisme

- Une référence de type parent peut contenir un objet de type enfant
- La méthode appelée est déterminée à l'exécution (liaison dynamique)
- Le comportement dépend du type réel de l'objet, pas du type de la référence
- Permet d'écrire du code plus générique et réutilisable

### Exemple supplémentaire avec une méthode polymorphique

```java
public class GestionnairePersonnes {
    public static void afficherDetails(Personne p) {
        System.out.println("Détails de la personne:");
        System.out.println(p);  // Appel polymorphique de toString()
    }

    public static void main(String[] args) {
        Personne pers = new Personne("Dupont", "Jean", 30);
        Etudiant etud = new Etudiant("Tremblay", "Marie", 20, "12345", "Informatique");

        afficherDetails(pers);  // Appelle toString de Personne
        afficherDetails(etud);  // Appelle toString d'Etudiant
    }
}
```

Cette capacité à traiter différents types d'objets de manière uniforme tout en conservant leur comportement spécifique
est l'essence même du polymorphisme.



-------

??? info "Utilisation de l'IA"
    Page rédigée en partie avec l'aide d'un assistant IA. L'IA a été utilisée pour générer des 
    explications, des exemples et/ou des suggestions de structure. Toutes les informations ont 
    été vérifiées, éditées et complétées par l'auteur.