# 1- Premier programme en Java

## Création d'un projet Java

Pour démarrer un nouveau projet Java dans IntelliJ IDEA :

1. Lancez IntelliJ IDEA et cliquez sur "New Project"
2. Sélectionnez "Java" dans la liste de gauche
3. Configurez le projet :
    - Donnez un nom au projet
    - Sélectionnez "IntelliJ" comme système de build
    - Choisissez OpenJDK 23[1]

Pour le JDK, si vous ne l'avez pas déjà :

- Cliquez sur "Download JDK"
- Sélectionnez Eclipse Temurin comme fournisseur
- Téléchargez la version 23[1]

## Structure du projet

Une fois le projet créé, créez une nouvelle classe :

1. Clic droit sur le dossier "src"
2. Sélectionnez New > Java Class
3. Entrez le nom complet : "com.example.calculator.Calculator"[7]

## Programme exemple

Voici un exemple de calculatrice simple qui illustre les concepts de base :

```java
package com.example.calculator;

public class Calculator {
    public static void main(String[] args) {
        int[] numbers = {5, 10, 15, 20, 25};
        int sum = 0;

        System.out.println("Calculatrice simple");

        // Calcul de la somme
        for (int num : numbers) {
            System.out.println("Ajout de : " + num);
            sum += num;
            // Pause pour démonstration du débogage
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }

        System.out.println("Somme totale : " + sum);
        System.out.println("Moyenne : " + (sum / numbers.length));
    }
}
```

## Exécution du programme

**Dans l'IDE** :

- Cliquez sur l'icône verte (▶️) à côté de la méthode main
- Ou utilisez le raccourci Maj+F10[4]

**Dans le terminal de l'IDE** :

1. Ouvrez le terminal intégré
2. Naviguez vers le dossier de sortie
3. Exécutez avec la commande `java com.example.calculator.Calculator`[3]

## Débogage

Pour déboguer le programme :

1. Placez des points d'arrêt en cliquant dans la marge gauche de l'éditeur
2. Lancez le débogage avec l'icône de débogage (🐞) ou Maj+F9[5]

**Commandes de débogage essentielles** :

- F8 : Passer à la ligne suivante
- F7 : Entrer dans une méthode
- F9 : Continuer l'exécution[5]

Le mode débogage permet d'inspecter les variables et de suivre l'exécution du programme pas à pas[5].

Citations:
[1] https://blog.jetbrains.com/fr/idea/2024/10/java-23-et-intellij-idea/
[2] https://devdocs.jabref.org/getting-into-the-code/guidelines-for-setting-up-a-local-workspace/intellij-12-build.html
[3] https://fr.linkedin.com/pulse/cr%C3%A9er-votre-premi%C3%A8re-application-java-avec-intellij-philippe-simo
[4] https://www.jetbrains.com/help/idea/run-java-applications.html
[5] https://codegym.cc/fr/groups/posts/fr.243.debogage-dans-intellij-idea-guide-du-debutant
[6] https://www.jetbrains.com/help/idea/debugging-code.html
[7] https://www.jetbrains.com/help/idea/creating-and-running-your-first-java-application.html
[8] https://www.jetbrains.com/help/idea/tutorial-remote-debug.html