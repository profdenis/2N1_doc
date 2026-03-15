# Exercice - Jeu de Devinettes de Mots

## Description Générale

Développez un jeu de devinettes de mots où le joueur doit découvrir un mot caché en devinant une lettre à la fois. Le
jeu propose deux niveaux de difficulté et utilise un fichier externe pour la banque de mots.

## Structure du Projet

```
projet/
├── src/
│   ├── jeu/
│   │   ├── MotCache.java
│   │   └── GestionnaireMots.java
│   └── Main.java
└── mots.txt
```

## Spécifications Fonctionnelles

### Déroulement d'une Partie

- Le mot à deviner est affiché avec des `_` pour chaque lettre non découverte
- Le joueur propose une lettre à la fois
- Maximum 7 tentatives incorrectes permises
- Une même lettre ne peut être proposée qu'une seule fois
- La partie est gagnée si le mot est découvert avant d'épuiser les tentatives
- La partie est perdue si les 7 tentatives sont épuisées

### Exemple de Déroulement (PIANO)

```
Mot à deviner: _ _ _ _ _
Tentatives restantes: 7
Lettres essayées: 

Proposez une lettre: A
Mot à deviner: _ _ A _ _ 
Tentatives restantes: 7
Lettres essayées: A

Proposez une lettre: E
Mot à deviner: _ _ A _ _ 
Tentatives restantes: 6
Lettres essayées: A, E
```

## Classes à Implémenter

### Classe MotCache

```java
public class MotCache {
    private String motComplet;
    private boolean[] lettresDecouvertes;
    private ArrayList<Character> lettresEssayees;
    private int tentativesRestantes;

    // Constructeur et méthodes à implémenter
    public boolean proposerLettre(char lettre) {
    }

    public String getMotAffichage() {
    }

    public boolean estGagne() {
    }

    public boolean estPerdu() {
    }
    // ... autres méthodes nécessaires
}
```

### Classe GestionnaireMots

```java
public class GestionnaireMots {
    private ArrayList<String> motsFaciles;    // 6 lettres ou moins
    private ArrayList<String> motsDifficiles; // 7 lettres ou plus

    // Constructeur et méthodes à implémenter
    public void chargerMots(String nomFichier) {
    }

    public String choisirMotAleatoire(boolean modeFacile) {
    }
    // ... autres méthodes nécessaires
}
```

## Menu Principal

1. Jeu Facile (mots de 6 lettres ou moins)
2. Jeu Difficile (mots de 7 lettres ou plus)
3. Quitter

## Exigences Techniques

- Le fichier `mots.txt` doit être chargé au démarrage
- Validation des entrées utilisateur
- Gestion des erreurs (fichier manquant, format incorrect)
- Les lettres proposées doivent être insensibles à la casse
- Affichage clair de l'état du jeu à chaque tour

## Format du Fichier `mots.txt`

- Un mot par ligne
- Uniquement des lettres (pas d'accents, pas d'espaces)
- Mots en majuscules

```
CHAT
CHIEN
MAISON
ORDINATEUR
```

