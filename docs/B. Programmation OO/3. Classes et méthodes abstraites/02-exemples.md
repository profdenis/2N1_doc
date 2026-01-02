# 🔸2🔸Exemples pour les jeux vidéos

!!! warning "Avertissement"

    Les exemples ci-dessous sont des illustrations simplifiées de concepts de programmation orientée objet. Ils ne
    représentent pas des implémentations complètes de jeux vidéo et nécessitent des adaptations pour être utilisés
    dans un contexte réel. Par exemple, les méthodes ne contiendraient pas seulement des `println` mais des logiques
    plus complexes.
  


## Exemples dans les Jeux Vidéo

**Gestion des Personnages**

- Une classe abstraite `Personnage` avec des méthodes abstraites comme `attaquer()` ou `seDeplacer()` que chaque type de
  personnage (guerrier, mage, archer) doit implémenter différemment[1].
- Des PNJs (Personnages Non Joueurs) qui doivent définir leurs propres comportements via des méthodes abstraites[1].

```java
public abstract class Personnage {
    protected String nom;
    protected int pointsDeVie;
    protected int niveau;

    public abstract void attaquer(Personnage cible);
    public abstract void seDeplacer(Position position);
    public abstract void utiliserCapaciteSpeciale();
}

public class Guerrier extends Personnage {
    private int force;
    private String arme;

    @Override
    public void attaquer(Personnage cible) {
        System.out.println(nom + " frappe avec son " + arme);
        // Logique de dégâts basée sur la force
    }

    @Override
    public void seDeplacer(Position position) {
        System.out.println(nom + " court lourdement vers la position");
        // Déplacement plus lent mais résistant
    }

    @Override
    public void utiliserCapaciteSpeciale() {
        System.out.println(nom + " entre dans une rage berserk!");
        // Augmente temporairement la force
    }
}

public class Mage extends Personnage {
    private int mana;
    private List<Sort> sorts;

    @Override
    public void attaquer(Personnage cible) {
        System.out.println(nom + " lance un projectile magique");
        // Logique de dégâts magiques
    }

    @Override
    public void seDeplacer(Position position) {
        System.out.println(nom + " se téléporte");
        // Téléportation sur courte distance
    }

    @Override
    public void utiliserCapaciteSpeciale() {
        System.out.println(nom + " crée un bouclier magique!");
        // Activation d'une protection magique
    }
}
```

## Intelligence Artificielle

**Comportements des Ennemis**

```java
public abstract class EnnemiIA {
    protected Position position;
    protected int niveau;
    protected int pointsDeVie;

    public abstract void deplacer();
    public abstract void attaquer();
    public abstract void reagirAuJoueur();
}

public class ZombieIA extends EnnemiIA {
    private double vitesseDeplacement;

    @Override
    public void deplacer() {
        System.out.println("Le zombie se déplace lentement vers le joueur");
        // Logique de déplacement direct vers le joueur
    }

    @Override
    public void attaquer() {
        System.out.println("Le zombie tente de mordre");
        // Attaque corps à corps avec dégâts d'infection
    }

    @Override
    public void reagirAuJoueur() {
        System.out.println("Le zombie a repéré le joueur et le poursuit");
        // Poursuite directe du joueur
    }
}

public class SentinelleIA extends EnnemiIA {
    private double porteeDetection;
    private boolean modeAlerte;

    @Override
    public void deplacer() {
        System.out.println("La sentinelle patrouille dans sa zone");
        // Logique de patrouille sur un chemin prédéfini
    }

    @Override
    public void attaquer() {
        System.out.println("La sentinelle tire avec son arme");
        // Attaque à distance
    }

    @Override
    public void reagirAuJoueur() {
        System.out.println("La sentinelle déclenche l'alarme et engage le combat");
        // Alerte les autres ennemis et engage le combat
    }
}
```

## Système de Combat

**Capacités et Compétences**

```java
public abstract class Competence {
    protected String nom;
    protected int coutMana;
    protected int tempsRecharge;

    public abstract void executer(Personnage cible);
    public abstract boolean estUtilisable();
}

public class BouleDeFeu extends Competence {
    private int degats;
    private int rayonExplosion;

    @Override
    public void executer(Personnage cible) {
        System.out.println("Lance une boule de feu qui explose sur la cible");
        // Logique de dégâts de zone et effets de brûlure
    }

    @Override
    public boolean estUtilisable() {
        return tempsRecharge == 0 && coutMana <= personnage.getMana();
    }
}

public class Soin extends Competence {
    private int puissanceSoin;
    private boolean soigneGroupe;

    @Override
    public void executer(Personnage cible) {
        System.out.println("Lance un sort de soin sur " + cible.getNom());
        // Logique de restauration de points de vie
    }

    @Override
    public boolean estUtilisable() {
        return tempsRecharge == 0 && coutMana <= personnage.getMana();
    }
}
```

## Mécaniques de Jeu

**Système de Points et Scores**

```java
public abstract class SystemeScore {
    protected int scoreActuel;
    protected int multiplicateur;

    public abstract void calculerPoints(Action action);
    public abstract void mettreAJourHighScore();
}

public class ScoreArcade extends SystemeScore {
    private int combo;
    
    @Override
    public void calculerPoints(Action action) {
        System.out.println("Calcul des points style arcade avec combos");
        // Logique de score basée sur les combos et la rapidité
    }

    @Override
    public void mettreAJourHighScore() {
        System.out.println("Mise à jour du tableau des meilleurs scores arcade");
        // Sauvegarde du score dans la table des high scores
    }
}

public class ScoreSurvie extends SystemeScore {
    private int tempsDeJeu;
    
    @Override
    public void calculerPoints(Action action) {
        System.out.println("Calcul des points basé sur le temps de survie");
        // Logique de score basée sur le temps et les ressources
    }

    @Override
    public void mettreAJourHighScore() {
        System.out.println("Mise à jour des records de temps de survie");
        // Sauvegarde du temps de survie et des statistiques
    }
}
```

## Avantages de cette Approche

- Permet une structure commune pour des comportements similaires[9]
- Facilite l'ajout de nouveaux types d'ennemis ou de personnages[9]
- Assure que toutes les sous-classes implémentent les comportements nécessaires[9]
- Permet une meilleure organisation du code et une maintenance plus facile[1]

Cette approche est particulièrement utile dans les jeux vidéo car elle permet de définir des comportements standards
tout en laissant la flexibilité nécessaire pour les variations spécifiques à chaque type d'entité du jeu.

??? note "Citations"
      - [1] https://www.saagie.com/fr/blog/blog-l-intelligence-artificielle-dans-les-jeux-video/
      - [2] https://artificialpaintings.com/fr/blog/2024/07/01/explorer-lart-abstrait-dans-les-jeux-video/
      - [3] https://www.youtube.com/watch?v=MLqplTsgga0
      - [4] https://zestedesavoir.com/tutoriels/646/apprenez-a-programmer-en-java/557_java-oriente-objet/2698_les-classes-abstraites-et-les-interfaces/
      - [5] https://www.firstpersonscholar.com/the-importance-of-abstraction/
      - [6] https://dev.to/carlillo/understanding-design-patterns-abstract-factory-23e7
      - [7] http://www.iro.umontreal.ca/~dift1170/A09/docPDF/chapit09.pdf
      - [8] https://ludobel.be/2022/11/03/limportance-des-jeux-abstraits/
      - [9] https://refactoring.guru/fr/design-patterns/template-method
      - [10] https://blackshellmedia.com/2015/09/15/game-design-101-the-beauty-of-abstraction/




-------

??? info "Utilisation de l'IA"
    Page rédigée en partie avec l'aide d'un assistant IA. L'IA a été utilisée pour générer des 
    explications, des exemples et/ou des suggestions de structure. Toutes les informations ont 
    été vérifiées, éditées et complétées par l'auteur.