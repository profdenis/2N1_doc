---
icon: material/file-document-outline
---

# 3. Conditionnelles

## Instructions conditionnelles

### Structure de base if-else

```java
public class ExemplesConditionnels {
    public static void main(String[] args) {
        int age = 17;

        // If simple
        if (age >= 18) {
            System.out.println("Vous êtes majeur");
        }

        // If-else
        if (age >= 18) {
            System.out.println("Vous êtes majeur");
        } else {
            System.out.println("Vous êtes mineur");
        }

        // If-else if-else
        int note = 85;
        if (note >= 90) {
            System.out.println("Excellent");
        } else if (note >= 80) {
            System.out.println("Très bien");
        } else if (note >= 70) {
            System.out.println("Bien");
        } else {
            System.out.println("À améliorer");
        }
    }
}
```

## Switch

### Switch classique

```java
public class ExemplesSwitch {
    public static void main(String[] args) {
        int jour = 3;

        // Switch traditionnel
        switch (jour) {
            case 1:
                System.out.println("Lundi");
                break;
            case 2:
                System.out.println("Mardi");
                break;
            case 3:
                System.out.println("Mercredi");
                break;
            default:
                System.out.println("Autre jour");
                break;
        }

        // Switch avec groupement de cas
        String typeDejour;
        switch (jour) {
            case 1:
            case 2:
            case 3:
            case 4:
            case 5:
                typeDejour = "Jour de semaine";
                break;
            case 6:
            case 7:
                typeDejour = "Fin de semaine";
                break;
            default:
                typeDejour = "Jour invalide";
                break;
        }
    }
}
```

### Switch expressions (Java 14+)

```java
public class ExemplesSwitchModerne {
    public static void main(String[] args) {
        String saison = "HIVER";

        // Switch expression avec flèches
        String activite = switch (saison) {
            case "PRINTEMPS" -> "Jardinage";
            case "ÉTÉ" -> "Natation";
            case "AUTOMNE" -> "Randonnée";
            case "HIVER" -> "Ski";
            default -> "Repos";
        };

        // Switch avec yield
        String message = switch (saison) {
            case "PRINTEMPS" -> {
                String temp = "Il fait doux";
                yield temp + ", c'est le temps du " + activite;
            }
            case "HIVER" -> {
                String temp = "Il fait froid";
                yield temp + ", allons faire du " + activite;
            }
            default -> "Saison non reconnue";
        };

        // Switch avec types (Java 21+)
        Object valeur = "42";
        String resultat = switch (valeur) {
            case Integer i -> "Nombre entier: " + i;
            case String s -> "Chaîne: " + s;
            case Double d -> "Nombre décimal: " + d;
            default -> "Type non géré";
        };
    }
}
```

On pourrait réécrire un `switch` traditionnel en utilisant un `switch` avec `when` en Java (version 17 ou
ultérieure), en exploitant le **pattern matching** et les **conditions `when`** pour simuler un comportement similaire à
au `if-else` :

```java
int note = 85;
String evaluation = switch (note) {
    case int n when n >= 90 -> "Excellent";
    case int n when n >= 80 -> "Très bien";
    case int n when n >= 70 -> "Bien";
    default -> "À améliorer";
};
System.out.

println(evaluation);
```

### Explications :

- **`case int n when n >= 90`** : Le motif `int n` capture la valeur de `note` dans la variable `n`, et la condition
  `when n >= 90` permet de tester la plage de valeurs.
- **Retour direct** : Le `switch` retourne une chaîne de caractères (`String`) en fonction de la condition remplie.
- **`default`** : Gère tous les cas non couverts par les conditions précédentes.

### Remarques pour ton cours :

- Cette syntaxe est **plus lisible** que des `if-else` imbriqués, surtout pour des plages de valeurs.
- Elle est idéale pour des **notes de cours** ou des exemples où tu veux montrer une alternative moderne au `if-else`.
- Assure-toi que tes étudiants utilisent **Java 17 ou plus récent** pour que ce code fonctionne.

---

## Exemple pratique combiné

```java
public class CalculatriceNotes {
    public static void main(String[] args) {
        int note = 85;
        String mention;

        // Utilisation de if pour validation
        if (note < 0 || note > 100) {
            System.out.println("Note invalide");
            return;
        }

        // Utilisation de switch pour déterminer la mention
        mention = switch (note / 10) {
            case 10, 9 -> {
                if (note == 100) {
                    yield "Parfait!";
                }
                yield "Excellent";
            }
            case 8 -> "Très bien";
            case 7 -> "Bien";
            case 6 -> "Passable";
            default -> "Échec";
        };

        // Affichage du résultat formaté
        System.out.printf("Note: %d/100%nMention: %s%n", note, mention);
    }
}
```

Ce dernier exemple montre comment combiner les instructions conditionnelles avec le formatage des chaînes et les
nouvelles fonctionnalités de switch. Il illustre également l'importance des validations et la façon dont les différentes
structures de contrôle peuvent travailler ensemble.


-------

??? info "Utilisation de l'IA"
    Page rédigée en partie avec l'aide d'un assistant IA. L'IA a été utilisée pour générer des
    explications, des exemples et/ou des suggestions de structure. Toutes les informations ont
    été vérifiées, éditées et complétées par l'auteur.