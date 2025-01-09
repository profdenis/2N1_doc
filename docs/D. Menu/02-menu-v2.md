# La classe `Menu`, version 2

- Github: [v2/Menu.java](https://github.com/profdenis/menu/tree/master/src/v2/Menu.java)

??? note "Code"

    ```java
    package v2;
    
    import java.util.Scanner;
    
    public class Menu {
    
        public static void main(String[] args) {
            boolean done = false;
            while (!done) {
                showMainMenu();
                Scanner scanner = new Scanner(System.in);
                String option = scanner.nextLine();
                done = handleMainMenuOption(option);
            }
        }
    
        public static void showMainMenu() {
            System.out.println("Choisissez une option :");
            System.out.println("1. Sous-menu (1 fois)");
            System.out.println("2. Sous-menu (boucle)");
            System.out.println("3. Option 3");
            System.out.println("4. Quitter");
        }
    
        public static void showSubMenu() {
            System.out.println("Choisissez une option :");
            System.out.println("a. Option a");
            System.out.println("b. Option b");
            System.out.println("c. Option c");
            System.out.println("d. Quitter");
        }
    
        public static boolean handleMainMenuOption(String option) {
            Scanner scanner = new Scanner(System.in);
            String subOption;
    
            switch (option) {
                case "1":
                    System.out.println("Vous avez choisi l'option 1 !");
                    showSubMenu();
                    subOption = scanner.nextLine();
                    // ignore la valeur de retour parce que le sous-menu est exécuté une seule fois, pas de boucle ici ; on
                    // pourrait utiliser la valeur de retour pour déterminer si une option valide a été sélectionnée ou non
                    handleSubMenuOption(subOption);
                    break;
                case "2":
                    // plusieurs lignes de code dans un seul bloc case, probablement mieux de les extraire dans une méthode
                    System.out.println("Vous avez choisi l'option 2 !");
                    boolean done = false;
                    while (!done) {
                        showSubMenu();
                        subOption = scanner.nextLine();
                        done = handleSubMenuOption(subOption);
                    }
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
    
        public static boolean handleSubMenuOption(String option) {
            switch (option) {
                case "a":
                    System.out.println("Vous avez choisi l'option a !");
                    break;
                case "b":
                    System.out.println("Vous avez choisi l'option b !");
                    break;
                case "c":
                    System.out.println("Vous avez choisi l'option c !");
                    break;
                case "d":
                    System.out.println("Vous voulez quitter le sous-menu!");
                    return true;
                default:
                    System.out.println("Option invalide. SVP choisir une option valide.");
            }
            return false;
        }
    }
    ```

!!! warning "Avertissement"

    Cet exemple n'est pas un programme complet, mais la deuxième version d'un exemple de structure de menu pouvant 
    être utilisé dans un programme plus complet.

La v2 de la classe `Menu` introduit la notion de sous-menu, ce qui représente la principale différence avec la v1. Voici
les changements importants :

* **Ajout d'un sous-menu :** La v2 inclut un nouveau sous-menu, accessible via les options 1 et 2 du menu principal. Ce
  sous-menu possède ses propres options (a, b, c et d). La méthode `showSubMenu()` affiche les options de ce sous-menu.
* **`showMainMenu()` et `handleMainMenuOption()` :** L'ancienne méthode `showMenu()` a été renommée en `showMainMenu()`
  et `handleOption()` en `handleMainMenuOption()` pour plus de clarté, et pour refléter l’ajout d’un menu principal
  distinct du sous-menu.
* **Comportement différent des options 1 et 2 :**
    * **Option 1:**  Affiche le sous-menu une seule fois. L'utilisateur choisit une option du sous-menu, puis revient au
      menu principal. Il est à noter que la valeur de retour de `handleSubMenuOption` est ignorée dans ce cas.
    * **Option 2:** Affiche le sous-menu en boucle, jusqu'à ce que l'utilisateur choisisse de quitter le sous-menu
      (option d). Cela est implémenté avec une boucle `while` similaire à celle du menu principal.
* **`handleSubMenuOption()` :** Cette nouvelle méthode gère les options du sous-menu. Elle renvoie `true` si
  l'utilisateur choisit de quitter le sous-menu (option d), et `false` sinon. Ce comportement permet la boucle dans
  l'option 2 du menu principal.

En résumé, la v2 offre une structure de menu plus complexe avec un sous-menu, permettant une navigation hiérarchique.
L'option 1 du menu principal affiche le sous-menu une seule fois, tandis que l'option 2 l'affiche en boucle. Le code est
également plus organisé avec des noms de méthodes plus descriptifs.




-------

!!! note "Note"
    Page rédigée en partie avec l'aide d'un assistant IA, principalement à l'aide de Perplexity AI, avec le *LLM*
    **Claude 3.5 Sonnet**. L'IA a été utilisée pour générer des explications, des exemples et/ou des suggestions de
    structure. Toutes les informations ont été vérifiées, éditées et complétées par l'auteur.