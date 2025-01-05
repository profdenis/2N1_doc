# 🔸4🔸Définition du polymorphisme

Le polymorphisme est un concept fondamental en programmation orientée objet qui permet à des objets de différentes
classes d'être traités comme des objets d'une classe commune.

## Définition formelle

Le polymorphisme se manifeste sous deux formes principales :

**Polymorphisme ad hoc (surcharge)**

- Permet à plusieurs méthodes d'avoir le même nom mais des paramètres différents
- Résolu à la compilation

**Polymorphisme par sous-typage (héritage)**

- Permet à une classe enfant de redéfinir le comportement d'une méthode héritée
- Résolu à l'exécution (liaison dynamique)

## Exemple avec des Véhicules

### Classe de base

```java
public class Vehicule {
    private String marque;
    private String modele;

    public Vehicule(String marque, String modele) {
        this.marque = marque;
        this.modele = modele;
    }

    public void demarrer() {
        System.out.println("Le véhicule démarre");
    }

    public String getDescription() {
        return marque + " " + modele;
    }
}
```

### Première sous-classe

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
```

### Deuxième sous-classe

```java
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

## Avantages du polymorphisme

- **Extensibilité**: Ajout facile de nouvelles sous-classes sans modifier le code existant
- **Réutilisabilité**: Le même code peut traiter différents types d'objets
- **Maintenance**: Modification du comportement spécifique sans affecter le code client

## Démonstration du polymorphisme

```java
public class DemoPolymorphisme {
    public static void main(String[] args) {
        // Tableau polymorphique
        Vehicule[] vehicules = new Vehicule[3];
        vehicules[0] = new Vehicule("Generic", "Transport");
        vehicules[1] = new Voiture("Toyota", "Corolla", 4);
        vehicules[2] = new Moto("Honda", "CBR", 600);

        // Utilisation polymorphique
        for (Vehicule v : vehicules) {
            System.out.println("Description: " + v.getDescription());
            v.demarrer();
            System.out.println("---");
        }
    }
}
```

## Exemple d'utilisation pratique

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

Cette implémentation illustre comment le polymorphisme permet d'écrire du code générique qui fonctionne avec n'importe
quelle sous-classe de `Vehicule`. La méthode `demarrerTousLesVehicules` peut traiter n'importe quel type de véhicule
sans avoir besoin de connaître sa classe spécifique.




-------

!!! note "Note"
    Page rédigée en partie avec l'aide d'un assistant IA, principalement à l'aide de Perplexity AI, avec le *LLM* 
    **Claude 3.5 Sonnet**. L'IA a été utilisée pour générer des explications, des exemples et/ou des suggestions de 
    structure. Toutes les informations ont été vérifiées, éditées et complétées par l'auteur.
