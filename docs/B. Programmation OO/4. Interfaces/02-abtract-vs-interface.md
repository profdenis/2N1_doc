---
icon: material/file-document-outline
---

# 2. Classes Abstraites vs. les Interfaces

## Classes Abstraites : La Relation "Est-un"

Les classes abstraites sont utilisées pour définir la **nature fondamentale** des objets dans une hiérarchie.

**Quand utiliser une classe abstraite:**
- Lorsque vous voulez créer une catégorie générale d'objets
- Quand plusieurs classes partagent des caractéristiques et des comportements communs
- Pour établir une hiérarchie basée sur l'identité des objets

**Exemple:**
```java
public abstract class Vehicule {
    protected String marque;
    protected int annee;

    public abstract void demarrer();

    public void klaxonner() {
        System.out.println("Beep beep!");
    }
}

public class Voiture extends Vehicule {
    @Override
    public void demarrer() {
        System.out.println("La voiture démarre");
    }
}
```

## Interfaces : La Relation "Peut-faire"

Les interfaces définissent des **capacités** ou des **comportements** que les classes peuvent adopter.

**Quand utiliser une interface:**
- Pour définir un ensemble de méthodes que plusieurs classes non liées peuvent implémenter
- Quand vous voulez spécifier un comportement sans vous soucier de qui l'implémente
- Pour permettre à une classe d'avoir plusieurs comportements

**Exemple:**
```java
public interface Rechargeable {
    void recharger();
}

public class Smartphone extends Appareil implements Rechargeable {
    @Override
    public void recharger() {
        System.out.println("Le smartphone se recharge");
    }
}

public class VoitureElectrique extends Voiture implements Rechargeable {
    @Override
    public void recharger() {
        System.out.println("La voiture électrique se recharge");
    }
}
```

## Points Clés à Retenir

1. **Classes Abstraites:**
   - Définissent "ce qu'est" un objet
   - Créent une taxonomie ou une hiérarchie
   - Peuvent contenir des attributs et des méthodes concrètes

2. **Interfaces:**
   - Définissent "ce que peut faire" un objet
   - Permettent de partager des comportements entre classes non liées
   - Ne contiennent que des signatures de méthodes (sauf méthodes default en Java 8+)

3. **Choix de Conception:**
   - Utilisez une classe abstraite quand vous voulez définir une catégorie d'objets
   - Utilisez une interface quand vous voulez définir une capacité que plusieurs types d'objets peuvent avoir

En comprenant cette distinction, vous serez mieux équipés pour concevoir des systèmes orientés objet flexibles et bien
structurés.




-------

??? info "Utilisation de l'IA"
    Page rédigée en partie avec l'aide d'un assistant IA. L'IA a été utilisée pour générer des 
    explications, des exemples et/ou des suggestions de structure. Toutes les informations ont 
    été vérifiées, éditées et complétées par l'auteur.