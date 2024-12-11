# 5- stdin

## Lecture depuis le stdin

**Utilisation de Scanner**

```java
import java.util.Scanner;

public class LectureConsole {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Lecture simple
        System.out.print("Entrez votre nom: ");
        String nom = scanner.nextLine();

        // Lecture avec validation
        int age = 0;
        boolean saisieValide = false;
        while (!saisieValide) {
            try {
                System.out.print("Entrez votre âge: ");
                age = Integer.parseInt(scanner.nextLine());
                saisieValide = true;
            } catch (NumberFormatException e) {
                System.out.println("Erreur: Veuillez entrer un nombre valide");
            }
        }

        System.out.printf("Bonjour %s, vous avez %d ans%n", nom, age);
    }
}
```

## Gestion des exceptions courantes

```java
import java.util.Scanner;
import java.util.InputMismatchException;

public class GestionExceptions {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Lecture d'un nombre avec gestion complète des erreurs
        double nombre = 0;
        boolean lectureOK = false;

        while (!lectureOK) {
            try {
                System.out.print("Entrez un nombre décimal: ");
                nombre = scanner.nextDouble();
                lectureOK = true;
            } catch (InputMismatchException e) {
                System.out.println("Erreur: Format invalide");
                scanner.nextLine(); // Vider le buffer
            }
        }

        System.out.printf("Nombre saisi: %.2f%n", nombre);
    }
}
```

## Exemple pratique complet

```java
import java.util.Scanner;

public class CalculatriceInteractive {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        while (true) {
            try {
                // Lecture du premier nombre
                System.out.print("Premier nombre (ou 'q' pour quitter): ");
                String input = scanner.nextLine();

                if (input.equalsIgnoreCase("q")) {
                    break;
                }

                double nombre1 = Double.parseDouble(input);

                // Lecture de l'opération
                System.out.print("Opération (+, -, *, /): ");
                String operation = scanner.nextLine();

                // Lecture du deuxième nombre
                System.out.print("Deuxième nombre: ");
                double nombre2 = Double.parseDouble(scanner.nextLine());

                // Calcul et affichage du résultat
                double resultat = switch (operation) {
                    case "+" -> nombre1 + nombre2;
                    case "-" -> nombre1 - nombre2;
                    case "*" -> nombre1 * nombre2;
                    case "/" -> {
                        if (nombre2 == 0) {
                            throw new ArithmeticException("Division par zéro");
                        }
                        yield nombre1 / nombre2;
                    }
                    default -> throw new IllegalArgumentException("Opération non valide");
                };

                System.out.printf("Résultat: %.2f%n", resultat);

            } catch (NumberFormatException e) {
                System.out.println("Erreur: Veuillez entrer un nombre valide");
            } catch (ArithmeticException e) {
                System.out.println("Erreur: Division par zéro impossible");
            } catch (IllegalArgumentException e) {
                System.out.println("Erreur: " + e.getMessage());
            }

            System.out.println(); // Ligne vide pour la lisibilité
        }

        System.out.println("Au revoir!");
        scanner.close();
    }
}
```

## Points importants à retenir

**Types d'exceptions courantes** :

- `NumberFormatException` : Conversion de chaîne en nombre échouée
- `InputMismatchException` : Type de donnée incorrect lors de la lecture
- `NoSuchElementException` : Plus de données à lire
- `IllegalArgumentException` : Argument invalide

**Bonnes pratiques** :

- Toujours vider le buffer après une erreur de lecture
- Fermer le Scanner à la fin du programme
- Utiliser des boucles pour permettre plusieurs tentatives de saisie
- Préférer `scanner.nextLine()` suivi de conversion plutôt que les méthodes spécifiques comme `nextInt()`

**Structure try-catch recommandée** :

```java
try{
// Code pouvant générer une exception
} catch(Exception1 e) {
// Gestion de l'exception 1
} catch(Exception2 e) {
// Gestion de l'exception 2
} finally {
// Code exécuté dans tous les cas
}
```