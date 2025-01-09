# La classe `Menu`, version 3

- Github: [v3/Menu.java](https://github.com/profdenis/menu/tree/master/src/v3/Menu.java)

??? note "Code"

    ```java
    package v3;
    
    import java.io.IOException;
    import java.nio.file.Files;
    import java.nio.file.Paths;
    import java.util.HashMap;
    import java.util.Map;
    import java.util.Scanner;
    
    public class Menu {
    
        private static final Scanner scanner = new Scanner(System.in);
    
        public static void main(String[] args) {
            boolean done = false;
    
            while (!done) {
                if (showMenu("main")) {
                    String option = scanner.nextLine();
                    done = handleMainMenuOption(option);
                } else {
                    done = true;
                }
            }
        }
    
        private static Map<String, String> menuStrings = new HashMap<>();
    
        public static boolean showMenu(String name) {
            if (!menuStrings.containsKey(name)) {
                try {
                    String menuPath = "menu/" + name + ".txt";
                    byte[] menuBytes = Files.readAllBytes(Paths.get(menuPath));
                    menuStrings.put(name, new String(menuBytes));
                } catch (IOException e) {
                    System.err.println("Error reading menu content: " + e.getMessage());
                    return false;
                }
            }
            System.out.println(menuStrings.get(name));
            return true;
        }
    
        public static boolean handleMainMenuOption(String option) {
            switch (option) {
                case "1":
                    handleMainMenuCase1();
                    break;
                case "2":
                    handleMainMenuCase2();
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
    
        private static void handleMainMenuCase1() {
            System.out.println("Vous avez choisi l'option 1 !");
            if (showMenu("sub")) {
                String option = scanner.nextLine();
                // ignore la valeur de retour parce que le sous-menu est exécuté une seule fois, pas de boucle ici ;
                // on pourrait utiliser la valeur de retour pour déterminer si une option valide a été sélectionnée
                // ou non
                handleSubMenuOption(option);
            }
        }
    
        private static void handleMainMenuCase2() {
            System.out.println("Vous avez choisi l'option 2 !");
            boolean done = false;
            while (!done) {
                if (showMenu("sub")) {
                    String option = scanner.nextLine();
                    done = handleSubMenuOption(option);
                } else {
                    done = true;
                }
            }
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

    Cet exemple n'est pas un programme complet, mais la troisième version d'un exemple de structure de menu pouvant 
    être utilisé dans un programme plus complet.

La principale différence entre la v2 et la v3 de la classe `Menu` réside dans la façon dont le contenu du menu est géré.
Au lieu d'être codé en dur dans le programme, le contenu du menu de la v3 est chargé depuis des fichiers externes. Voici
les changements :

* **Chargement du menu depuis des fichiers :** La v3 utilise la méthode `showMenu(String name)` pour charger le contenu
  du menu depuis des fichiers texte situés dans un répertoire "menu". Le nom du fichier correspond au nom du menu passé
  en argument (par exemple, "main" pour le menu principal, "sub" pour le sous-menu). Le contenu du fichier est lu et
  stocké dans une `HashMap` appelée `menuStrings`.
* **Gestion des erreurs :** La méthode `showMenu()` gère maintenant les erreurs potentielles lors de la lecture des
  fichiers menu. Si une erreur se produit (par exemple, si le fichier n'existe pas), elle affiche un message d'erreur et
  renvoie `false`. Ceci est important pour la robustesse du programme.
* **`HashMap` pour stocker le contenu du menu :**  Une `HashMap` appelée `menuStrings` est utilisée pour stocker le
  contenu des menus. La clé est le nom du menu ("main" ou "sub") et la valeur est le texte du menu lu depuis le fichier
  correspondant. Cela permet de ne lire le contenu du fichier qu'une seule fois, améliorant ainsi les performances.
* **`Scanner` statique :**  L'objet `Scanner` est maintenant un attribut statique de la classe, ce qui évite de le créer
  à chaque fois dans `main` et  `handleMainMenuOption`.
* **Refactorisation du code pour `case "1"` et `case "2"` :** Le code des blocs `case "1"` et `case "2"` de la méthode
  `handleMainMenuOption` a été extrait dans les méthodes  `handleMainMenuCase1()` et `handleMainMenuCase2()`
  respectivement, améliorant la lisibilité et l’organisation du code.

En résumé, la v3 externalise le contenu des menus dans des fichiers, ce qui rend le code plus flexible et maintenable.
La gestion des erreurs et l’utilisation d’une `HashMap` améliorent également la robustesse et les performances du
programme. L’utilisation d’un `Scanner` statique et le déplacement de la logique des blocs `case` vers des méthodes
dédiées améliore la qualité et la lisibilité du code.



-------

!!! note "Note"
Page rédigée en partie avec l'aide d'un assistant IA, principalement à l'aide de Perplexity AI, avec le *LLM*
**Claude 3.5 Sonnet**. L'IA a été utilisée pour générer des explications, des exemples et/ou des suggestions de
structure. Toutes les informations ont été vérifiées, éditées et complétées par l'auteur.