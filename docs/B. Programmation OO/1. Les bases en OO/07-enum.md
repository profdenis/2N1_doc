# 🔸7🔸Les énumérations (enum) en Java

Une énumération est un type spécial qui définit un ensemble fixe de constantes. Voici un exemple basique
d'énumération des saisons :

```java
public enum Saison {
    PRINTEMPS,
    ETE,
    AUTOMNE,
    HIVER
}
```

Pour utiliser cette énumération :

```java
Saison saison = Saison.PRINTEMPS;
if(saison == Saison.PRINTEMPS) {
    System.out.println("C'est le printemps!");
}
```

## Énumérations avancées

Les énumérations en Java peuvent être plus sophistiquées en incluant des attributs, des constructeurs et des méthodes.

### Attributs et constructeurs

Dans l'exemple de `Couleur`, qui représente les 4 couleurs possibles dans un jeu de cartes standard, chaque constante 
est associée à un symbole :

```java
public enum Couleur {
    COEUR("♥"),    // Appelle le constructeur avec "♥"
    CARREAU("♦"),  // Appelle le constructeur avec "♦"
    PIQUE("♠"),    // Appelle le constructeur avec "♠"
    TREFLE("♣");   // Appelle le constructeur avec "♣"

    private final String symbole;  // Attribut privé

    Couleur(String symbole) {      // Constructeur
        this.symbole = symbole;
    }

    public String getSymbole() {   // Méthode d'accès
        return symbole;
    }
}
```

Dans l'exemple de `NomCarte`, qui représente les 13 noms de carte possibles dans un jeu de cartes standard, chaque 
constante à une valeur :

```java
public enum NomCarte {
    AS(1),
    DEUX(2),
    TROIS(3),
    QUATRE(4),
    CINQ(5),
    SIX(6),
    SEPT(7),
    HUIT(8),
    NEUF(9),
    DIX(10),
    VALET(10),
    DAME(10),
    ROI(10);

    private final int valeur;

    NomCarte(int valeur) {
        this.valeur = valeur;
    }

    public int getValeur() {
        return valeur;
    }
}
```

### Utilisation avancée

Voici comment utiliser les énumérations `Couleur` et `NomCarte` :

```java
Couleur couleur = Couleur.COEUR;
System.out.println(couleur.getSymbole());  // Affiche: ♥

NomCarte carte = NomCarte.AS;
System.out.println(carte.getValeur());     // Affiche: 1
```

## Points importants

- Les constructeurs d'un `enum` sont toujours privés (même si on ne met pas le mot-clé `private`)
- Les constantes d'un `enum` doivent être déclarées en premier dans la classe
- Chaque constante est une instance unique de l'énumération
- Les énumérations héritent implicitement de `java.lang.Enum`

### Méthodes utiles héritées

- `name()`: retourne le nom de la constante
- `ordinal()`: retourne la position (commence à 0)
- `values()`: retourne un tableau de toutes les constantes
- `valueOf(String)`: convertit une chaîne en constante

```java
// Exemple d'utilisation des méthodes héritées
for(NomCarte carte : NomCarte.values()){
    System.out.printf("%s a la valeur %d%n", carte.name(),carte.getValeur());
}
```



-------

??? info "Utilisation de l'IA"
      Page rédigée en partie avec l'aide d'un assistant IA, principalement à l'aide de Perplexity AI, avec le *LLM*
      **Claude 3.5 Sonnet**. L'IA a été utilisée pour générer des explications, des exemples et/ou des suggestions de
      structure. Toutes les informations ont été vérifiées, éditées et complétées par l'auteur.
     