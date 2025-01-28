# La classe `Menu`, version 1

- Github: [v1/Menu.java](https://github.com/profdenis/menu/tree/master/src/v1/Menu.java)

```java
package v1;

import java.util.Scanner;

public class Menu {

    public static void main(String[] args) {
        boolean done = false;
        Scanner scanner = new Scanner(System.in);

        while (!done) {
            showMenu();
            String option = scanner.nextLine();
            done = handleOption(option);
        }

        scanner.close();
    }

    public static void showMenu() {
        System.out.println("Choisissez une option :");
        System.out.println("1. Option 1");
        System.out.println("2. Option 2");
        System.out.println("3. Option 3");
        System.out.println("4. Quitter");
    }

    public static boolean handleOption(String option) {
        switch (option) {
            case "1":
                System.out.println("Vous avez choisi l'option 1 !");
                break;
            case "2":
                System.out.println("Vous avez choisi l'option 2 !");
                break;
            case "3":
                System.out.println("Vous avez choisi l'option 3 !");
                break;
            case "4":
                System.out.println("Vous voulez quitter !");
                return true;
            default:
                System.out.println("Option invalide. SVP choisir une option valide.");
        }
        return false;
    }
}
```

!!! warning "Avertissement"

    Cet exemple n'est pas un programme complet, mais une première version d'un exemple de structure de menu pouvant 
    être utilisé dans un programme plus complet.

Voici une explication du code de la classe `Menu` :

La classe `Menu` présente un menu interactif à l’utilisateur dans la console. Elle utilise une boucle `while` pour
afficher le menu de façon répétée jusqu’à ce que l’utilisateur choisisse de quitter. Examinons les méthodes :

* **`main(String[] args)` :**
    * C’est le point d’entrée du programme.
    * Elle initialise une variable booléenne `done` à `false`.
    * Elle crée un `Scanner` pour lire l’entrée de l’utilisateur.
    * Elle entre dans une boucle `while` qui continue tant que `done` est `false`.
    * À l’intérieur de la boucle :
        * Elle appelle `showMenu()` pour afficher les options du menu.
        * Elle lit l’entrée de l’utilisateur et la stocke dans la variable `option`.
        * Elle appelle `handleOption(option)` pour traiter l’option choisie par l’utilisateur. Le résultat (une valeur
          booléenne indiquant si l’utilisateur veut quitter) est stocké dans la variable `done`.
    * Elle ferme le `scanner`.

* **`showMenu()` :**
    * Cette méthode affiche simplement les options du menu à la console en utilisant `System.out.println()`.

* **`handleOption(String option)` :**
    * Cette méthode prend l’`option` de l’utilisateur (une `String`) comme entrée.
    * Elle utilise une instruction `switch` pour déterminer l’action à effectuer en fonction de l’option choisie.
    * Si l’option est « 1 », « 2 » ou « 3 », elle affiche un message indiquant l’option choisie.
    * Si l’option est « 4 », elle affiche un message de sortie et renvoie `true` (pour indiquer que l’utilisateur veut
      quitter).
    * Si l’option n’est pas valide, elle affiche un message d’erreur et renvoie `false` (pour que la boucle `while`
      continue).

En résumé, le programme affiche un menu, lit le choix de l’utilisateur, traite le choix et répète ce processus jusqu’à
ce que l’utilisateur choisisse l’option « 4 » (Quitter).



-------

??? info "Utilisation de l'IA"
      Page rédigée en partie avec l'aide d'un assistant IA, principalement à l'aide de Perplexity AI, avec le *LLM*
      **Claude 3.5 Sonnet**. L'IA a été utilisée pour générer des explications, des exemples et/ou des suggestions de
      structure. Toutes les informations ont été vérifiées, éditées et complétées par l'auteur.
     
