---
icon: material/file-document-outline
---

# 1. Interfaces

Une interface en Java est un contrat qui définit un ensemble de méthodes qu'une classe doit implémenter. Elle permet de
définir un comportement commun que plusieurs classes non liées peuvent partager.

## Exemple

```java
// Définition de l'interface
public interface Animal {
    void faireBruit();

    void seDeplacer();
}

// Implémentation de l'interface
public class Chat implements Animal {
    @Override
    public void faireBruit() {
        System.out.println("Miaou!");
    }

    @Override
    public void seDeplacer() {
        System.out.println("Le chat marche silencieusement");
    }
}

// Une autre implémentation
public class Chien implements Animal {
    @Override
    public void faireBruit() {
        System.out.println("Wouf!");
    }

    @Override
    public void seDeplacer() {
        System.out.println("Le chien court joyeusement");
    }
}
```

## Comparaison entre Interfaces et Classes Abstraites

| Caractéristique   | Interface                                                     | Classe Abstraite                                            |
|-------------------|---------------------------------------------------------------|-------------------------------------------------------------|
| Méthodes          | Uniquement abstraites (par défaut) et statiques               | Peut avoir des méthodes abstraites et concrètes             |
| Attributs         | Constants uniquement (public static final)                    | Peut avoir des variables d'instance                         |
| Héritage multiple | Une classe peut implémenter plusieurs interfaces              | Une classe ne peut hériter que d'une seule classe abstraite |
| Constructeur      | Ne peut pas avoir de constructeur                             | Peut avoir des constructeurs                                |
| Implémentation    | Ne peut pas contenir d'implémentation (sauf méthodes default) | Peut contenir des implémentations partielles                |

## Points Clés à Retenir

Les interfaces sont particulièrement utiles pour:

- Définir un contrat que plusieurs classes doivent respecter
- Permettre le polymorphisme sans créer une hiérarchie d'héritage
- Créer des systèmes faiblement couplés

Les classes abstraites sont préférables quand:

- On veut partager du code entre plusieurs classes étroitement liées
- On a besoin de déclarer des attributs non constants
- On souhaite fournir une implémentation partielle d'une classe