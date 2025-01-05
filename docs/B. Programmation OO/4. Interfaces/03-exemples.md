# 🔸3🔸Exemples

!!! warning "Avertissement"

    Les exemples ci-dessous sont des illustrations simplifiées de concepts de programmation orientée objet. Ils ne
    représentent pas des implémentations complètes de jeux vidéo et nécessitent des adaptations pour être utilisés
    dans un contexte réel. Par exemple, les méthodes ne contiendraient pas seulement des `println` mais des logiques
    plus complexes.

## Exemple avec une Hiérarchie de Véhicules

### Classe Abstraite - Nature Fondamentale

```java
public abstract class Vehicule {
    protected String marque;
    protected int vitesseMax;
    
    public Vehicule(String marque, int vitesseMax) {
        this.marque = marque;
        this.vitesseMax = vitesseMax;
    }
    
    public abstract void demarrer();
    
    // Méthode concrète commune à tous les véhicules
    public void klaxonner() {
        System.out.println("Beep beep!");
    }
}

public class Voiture extends Vehicule {
    public Voiture(String marque, int vitesseMax) {
        super(marque, vitesseMax);
    }
    
    @Override
    public void demarrer() {
        System.out.println("La voiture démarre avec la clé");
    }
}
```

### Interfaces - Capacités

```java
public interface Rechargeable {
    void recharger();
}

public interface Volant {
    void decoller();
    void atterrir();
}

public class VoitureElectrique extends Voiture implements Rechargeable {
    public VoitureElectrique(String marque, int vitesseMax) {
        super(marque, vitesseMax);
    }
    
    @Override
    public void recharger() {
        System.out.println("La voiture se recharge sur une borne");
    }
}

public class VoitureVolante extends Voiture implements Volant {
    @Override
    public void decoller() {
        System.out.println("La voiture s'élève dans les airs");
    }
    
    @Override
    public void atterrir() {
        System.out.println("La voiture revient au sol");
    }
}
```

## Exemple avec des Animaux

### Classe Abstraite - Structure de Base

```java
public abstract class Animal {
    protected String nom;
    protected int age;
    
    public abstract void respirer();
    
    public void dormir() {
        System.out.println("L'animal dort");
    }
}
```

### Interfaces - Comportements

```java
public interface Nageable {
    void nager();
}

public interface Volant {
    void voler();
}

public class Dauphin extends Animal implements Nageable {
    @Override
    public void respirer() {
        System.out.println("Le dauphin remonte à la surface");
    }
    
    @Override
    public void nager() {
        System.out.println("Le dauphin nage rapidement");
    }
}

public class Chauve_Souris extends Animal implements Volant {
    @Override
    public void respirer() {
        System.out.println("La chauve-souris respire");
    }
    
    @Override
    public void voler() {
        System.out.println("La chauve-souris vole silencieusement");
    }
}
```

Ces exemples illustrent comment :

- Les classes abstraites définissent la structure de base et les comportements communs
- Les interfaces permettent d'ajouter des capacités de manière flexible
- Une classe peut hériter d'une seule classe abstraite mais implémenter plusieurs interfaces
- Les interfaces favorisent la réutilisation de code à travers des hiérarchies non liées

## Citations

- [1] https://www.studysmarter.fr/resumes/informatique/programmation-informatique/interfaces-java/
- [2] https://members.loria.fr/ABelaid/Enseignement/FC/Cours7-Classes-abstraites.pdf
- [3] https://codegym.cc/fr/groups/posts/fr.1008.interface-en-java
- [4] https://www.studysmarter.fr/resumes/informatique/programmation-informatique/abstraction-en-java/
- [5] https://www.studysmarter.fr/resumes/informatique/programmation-informatique/interface-set-java/
- [6] https://dev.to/bassaoudev/poo-comprendre-les-classes-abstraites-et-les-interfaces-en-java-3imn
- [7] https://dev.to/bassaoudev/poo-les-interfaces-en-java-simplement-5fdd
- [8] https://codegym.cc/fr/groups/posts/les-classes-abstraites-en-java
- [9] https://blog.paumard.org/cours/java/chap07-heritage-interface-interface.html
- [10] https://gayerie.dev/epsi-b3-java/langage_java/interface.html



-------

!!! note "Note"
    Page rédigée en partie avec l'aide d'un assistant IA, principalement à l'aide de Perplexity AI, avec le *LLM* 
    **Claude 3.5 Sonnet**. L'IA a été utilisée pour générer des explications, des exemples et/ou des suggestions de 
    structure. Toutes les informations ont été vérifiées, éditées et complétées par l'auteur.