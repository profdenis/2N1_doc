# Guide : La méthode `main` simplifiée en Java (incluant `String[] args`)

---

## 1. Introduction

Depuis Java 21 (Preview), il est possible d’écrire des programmes Java avec une syntaxe simplifiée pour la méthode `main`,
notamment grâce aux **classes sans nom (Unnamed Classes)** et aux **méthodes `main` d’instance**. Ce guide explique
aussi comment utiliser le paramètre `String[] args`, souvent méconnu des débutants, mais essentiel pour interagir avec
un programme via des arguments externes.

---

## 2. Rappel : La méthode `main` classique

Jusqu’à Java 20, la méthode `main` devait être déclarée de manière statique dans une classe nommée, par exemple :

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

- **Points clés** :
    - La classe doit être déclarée (`public class HelloWorld`).
    - La méthode `main` doit être `public`, `static`, et prendre un tableau de `String` en paramètre.

---

## 3. La nouvelle syntaxe simplifiée

### a. Classe sans nom et méthode `main` d’instance

À partir de Java 21 (Preview) et Java 25, il est possible d’écrire :

```java
void main() {
    System.out.println("Hello, World!");
}
```

- **Points clés** :
    - Plus besoin de déclarer une classe.
    - La méthode `main` peut être une méthode d’instance (sans `static`).
    - Le paramètre `String[] args` est optionnel si non utilisé.

### b. Avec paramètre (si nécessaire)

Si vous avez besoin d’accéder aux arguments de la ligne de commande :

```java
void main(String[] args) {
    System.out.println("Bonjour, " + args[0] + "!");
}
```

---

## 4. À quoi sert `String[] args` ?

Le paramètre `String[] args` permet à un programme Java de recevoir des **arguments** lors de son exécution. Ces
arguments sont passés sous forme de chaînes de caractères (`String`) et peuvent être utilisés pour :

- Personnaliser le comportement du programme.
- Passer des données au programme sans avoir à les coder en dur.
- Automatiser des tâches (scripts, traitements par lots, etc.).

### Exemple concret

Supposons que vous voulez écrire un programme qui salue une personne dont le nom est passé en argument :

```java
void main(String[] args) {
    if (args.length > 0) {
        System.out.println("Bonjour, " + args[0] + " !");
    } else {
        System.out.println("Bonjour, inconnu !");
    }
}
```

- Si vous exécutez ce programme avec l’argument `Alice`, il affichera : `Bonjour, Alice !`
- Sans argument, il affichera : `Bonjour, inconnu !`

---

## 5. Comment passer des arguments en ligne de commande ?

### a. Depuis le terminal (Linux/macOS/Windows)

1. Compilez votre programme :

  ```bash
   javac MonProgramme.java
  ```

2. Exécutez-le en passant des arguments :

  ```bash
   java MonProgramme Alice Bob
  ```

- `Alice` et `Bob` seront accessibles dans `args[0]` et `args[1]` respectivement.

**Exemple complet** :

```java
// Fichier : Bonjour.java
void main(String[] args) {
    for (int i = 0; i < args.length; i++) {
        System.out.println("Argument " + i + " : " + args[i]);
    }
}
```

- Compilation : `javac Bonjour.java`
- Exécution : `java Bonjour Alice Bob`
- Sortie :
  ```
  Argument 0 : Alice
  Argument 1 : Bob
  ```

---

### b. Depuis IntelliJ IDEA

1. Ouvrez votre projet et votre fichier Java.
2. Cliquez sur le menu déroulant à côté du bouton d’exécution (▶️) et sélectionnez **Edit Configurations**.
3. Dans la fenêtre qui s’ouvre :

- Dans le champ **Program arguments**, entrez les arguments séparés par des espaces (ex: `Alice Bob`).
- Cliquez sur **OK**.

4. Lancez le programme avec le bouton d’exécution (▶️).

**Exemple** :

- Si vous entrez `Alice Bob` dans **Program arguments**, `args[0]` vaudra `"Alice"` et `args[1]` vaudra `"Bob"`.

---

## 6. Exercices pratiques

### Exercice 1 : Conversion et utilisation des arguments

Convertissez le programme suivant en utilisant la nouvelle syntaxe et ajoutez un message personnalisé en fonction du
premier argument :

```java
public class Bonjour {
    public static void main(String[] args) {
        System.out.println("Bonjour à tous !");
    }
}
```

**Solution attendue** :

```java
void main(String[] args) {
    if (args.length > 0) {
        System.out.println("Bonjour, " + args[0] + " !");
    } else {
        System.out.println("Bonjour à tous !");
    }
}
```

---

### Exercice 2 : Calcul de la somme

Écrivez un programme qui calcule la somme de deux nombres passés en arguments, en utilisant la nouvelle syntaxe.

**Solution attendue** :

```java
void main(String[] args) {
    if (args.length == 2) {
        int a = Integer.parseInt(args[0]);
        int b = Integer.parseInt(args[1]);
        System.out.println("Somme : " + (a + b));
    } else {
        System.out.println("Veuillez fournir exactement deux nombres.");
    }
}
```

---

### Exercice 3 : Affichage des arguments

Écrivez un programme qui affiche tous les arguments passés, chacun sur une nouvelle ligne.

**Solution attendue** :

```java
void main(String[] args) {
    for (String arg : args) {
        System.out.println(arg);
    }
}
```

---

## 7. Points d’attention

- **Gestion des erreurs** : Toujours vérifier la longueur de `args` avant d’y accéder pour éviter les
  `ArrayIndexOutOfBoundsException`.
- **Conversion des types** : Les arguments sont toujours des `String`. Utilisez `Integer.parseInt()`,
  `Double.parseDouble()`, etc., pour convertir vers d’autres types.
- **Espace dans les arguments** : Si un argument contient des espaces, entourez-le de guillemets dans le terminal (ex:
  `"Jean Dupont"`).

---

## 8. Pour aller plus loin

- Essayez de modifier les exercices pour qu’ils gèrent des cas d’erreur (ex: arguments non numériques).
- Explorez comment utiliser `args` avec des boucles `for` ou des streams pour traiter plusieurs arguments.
- Consultez
  la [documentation officielle sur les arguments en ligne de commande](https://docs.oracle.com/javase/tutorial/essential/environment/cmdLineArgs.html)
  pour plus de détails.

---

## 9. Conclusion

La nouvelle syntaxe pour la méthode `main` simplifie l’écriture de programmes Java, surtout pour les débutants. Le
paramètre `String[] args` est un outil puissant pour rendre vos programmes interactifs et flexibles. En maîtrisant ces
concepts, vous serez capable de créer des programmes plus dynamiques et adaptables.