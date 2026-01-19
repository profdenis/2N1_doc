---
icon: material/file-document-outline
---

# 1. Mot-clé `abstract`

## Classes Concrètes vs Classes Abstraites

Une **classe concrète** est une classe standard qui peut être instanciée directement pour créer des objets. Elle doit
implémenter toutes ses méthodes. Par exemple, `Voiture` et `Moto` sont des classes concrètes car on peut créer des
objets de ces types.

Une **classe abstraite** est une classe qui ne peut pas être instanciée directement. Voici la classe abstraite
`Vehicule` :

```java
public abstract class Vehicule {
    private String marque;
    private String modele;

    public Vehicule(String marque, String modele) {
        this.marque = marque;
        this.modele = modele;
    }

    // Méthode abstraite que les sous-classes devront implémenter
    public abstract void demarrer();

    // Méthode concrète commune à tous les véhicules
    public String getDescription() {
        return marque + " " + modele;
    }
}
```

## Méthodes Abstraites

Une **méthode abstraite** est une méthode déclarée sans implémentation. Les classes qui héritent de `Vehicule` doivent
implémenter la méthode `demarrer()` :

```java
public class Voiture extends Vehicule {
    private int nombrePortes;

    public Voiture(String marque, String modele, int nombrePortes) {
        super(marque, modele);
        this.nombrePortes = nombrePortes;
    }

    @Override
    public void demarrer() {
        System.out.println("La voiture démarre en tournant la clé");
    }

    @Override
    public String getDescription() {
        return super.getDescription() + " (" + nombrePortes + " portes)";
    }
}

public class Moto extends Vehicule {
    private int cylindree;

    public Moto(String marque, String modele, int cylindree) {
        super(marque, modele);
        this.cylindree = cylindree;
    }

    @Override
    public void demarrer() {
        System.out.println("La moto démarre avec le kick");
    }

    @Override
    public String getDescription() {
        return super.getDescription() + " (" + cylindree + "cc)";
    }
}
```

## Utilisation Pratique avec le Polymorphisme

Voici comment utiliser ces classes de manière polymorphique :

```java
public class DemoPolymorphisme {
    public static void main(String[] args) {
        // Tableau polymorphique
        Vehicule[] vehicules = new Vehicule[2];
        vehicules[0] = new Voiture("Toyota", "Corolla", 4);
        vehicules[1] = new Moto("Honda", "CBR", 600);

        // Utilisation polymorphique
        for (Vehicule v : vehicules) {
            System.out.println("Description: " + v.getDescription());
            v.demarrer();
            System.out.println("---");
        }
    }
}
```

On peut également créer des méthodes utilitaires qui travaillent avec n'importe quel véhicule :

```java
public class GarageAuto {
    public static void demarrerTousLesVehicules(Vehicule[] vehicules) {
        for (Vehicule v : vehicules) {
            System.out.println("Démarrage de: " + v.getDescription());
            v.demarrer();
        }
    }
}
```

## Caractéristiques Importantes

**Points clés sur les classes abstraites** :

- Une classe abstraite peut avoir des méthodes abstraites et des méthodes concrètes (comme `getDescription()`)
- Elle peut avoir des constructeurs (comme `Vehicule(String marque, String modele)`)
- Elle peut avoir des attributs (comme `marque` et `modele`)

**Points clés sur les méthodes abstraites** :

- Elles définissent un comportement obligatoire que les sous-classes doivent implémenter
- Dans notre exemple, chaque type de véhicule doit définir sa propre façon de démarrer
- Elles sont particulièrement utiles quand un comportement varie selon le type spécifique de l'objet

Cette approche permet une grande flexibilité : pour ajouter un nouveau type de véhicule (comme un Scooter), il suffit de
créer une nouvelle classe qui hérite de `Vehicule` et implémente `demarrer()`.une nouvelle classe qui hérite de `Forme`
et implémente `calculerAire()`.




-------

??? info "Utilisation de l'IA"
    Page rédigée en partie avec l'aide d'un assistant IA. L'IA a été utilisée pour générer des 
    explications, des exemples et/ou des suggestions de structure. Toutes les informations ont 
    été vérifiées, éditées et complétées par l'auteur.
