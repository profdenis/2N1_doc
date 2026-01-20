---
icon: material/file-document-outline
---

# 5. stdin

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

!!! warning "En général, évitez les `while (true)`"
    - **À utiliser avec parcimonie** : Peut rendre le code moins lisible.
    - **Préférer une condition claire** quand c'est possible.
    - En général, **if faut donc éviter les boucles `while (true)`, et essayer d'utiliser `break` et `continue` le moins 
      possible**, pour écrire du code plus lisible et moins complexe. Le code peut rapidement devenir trop complexe et
      illisible si on utilise des boucles `while True`.


## Points importants à retenir

**Types d'exceptions courantes** :

- `NumberFormatException` : Conversion de chaîne en nombre échouée
- `InputMismatchException` : Type de donnée incorrect lors de la lecture
- `NoSuchElementException` : Plus de données à lire
- `IllegalArgumentException` : Argument invalide

**Bonnes pratiques** :

- Toujours vider le buffer après une erreur de lecture
- Fermer le `Scanner` à la fin du programme
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



-------

??? info "Utilisation de l'IA"
    Page rédigée en partie avec l'aide d'un assistant IA. L'IA a été utilisée pour générer des 
    explications, des exemples et/ou des suggestions de structure. Toutes les informations ont 
    été vérifiées, éditées et complétées par l'auteur.