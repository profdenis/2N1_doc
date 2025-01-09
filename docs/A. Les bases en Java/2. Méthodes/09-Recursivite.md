# 🔸9🔸Récursivité 

## Comprendre la récursivité

La récursivité est basée sur deux principes fondamentaux :

1. Un ou plusieurs **cas de base** qui arrêtent la récursion
2. Un ou plusieurs **cas récursifs** qui décomposent le problème

Prenons l'exemple de la suite de Fibonacci où :

- $F(0) = 0$ (cas de base)
- $F(1) = 1$ (cas de base)
- $F(n) = F(n-1) + F(n-2)$ pour $n > 1$ (cas récursif)

```java
public class ExempleFibonacci {
    public static long fibonacci(int n) {
        // Cas de base
        if (n == 0) return 0;
        if (n == 1) return 1;

        // Cas récursif
        return fibonacci(n - 1) + fibonacci(n - 2);
    }

    public static void main(String[] args) {
        System.out.println("F(5) = " + fibonacci(5));
    }
}
```

## Visualisation avec le débogueur

Pour visualiser les appels récursifs dans IntelliJ :

1. Placez un point d'arrêt sur la ligne du cas récursif
2. Démarrez le débogage (`Maj+F9`)
3. Utilisez les commandes suivantes :
    - `F7` (Step Into) pour suivre les appels récursifs
    - `F8` (Step Over) pour exécuter une ligne
    - `Alt+F7` pour sortir de la méthode courante

```java
public class FibonacciDebug {
    public static long fibonacci(int n) {
        // Ajoutez cette ligne pour faciliter le débogage
        System.out.printf("Calcul de F(%d)%n", n);

        if (n == 0) {
            System.out.println("Cas de base F(0) = 0");
            return 0;
        }
        if (n == 1) {
            System.out.println("Cas de base F(1) = 1");
            return 1;
        }

        // Point d'arrêt ici
        long resultat = fibonacci(n - 1) + fibonacci(n - 2);
        System.out.printf("F(%d) = %d%n", n, resultat);
        return resultat;
    }

    public static void main(String[] args) {
        System.out.println("Début du calcul de F(4)");
        long resultat = fibonacci(4);
        System.out.println("Résultat final: " + resultat);
    }
}
```

## Exemple plus complexe : Tours de Hanoï

```java
public class ToursHanoi {
    private static int compteurEtapes = 0;

    public static void deplacerDisques(int n, char source, char destination, char auxiliaire) {
        compteurEtapes++;

        // Cas de base
        if (n == 1) {
            System.out.printf("Étape %d: Déplacer disque 1 de %c vers %c%n",
                    compteurEtapes, source, destination);
            return;
        }

        // Cas récursifs
        // 1. Déplacer n-1 disques de source vers auxiliaire
        deplacerDisques(n - 1, source, auxiliaire, destination);

        // 2. Déplacer le dernier disque de source vers destination
        System.out.printf("Étape %d: Déplacer disque %d de %c vers %c%n",
                compteurEtapes, n, source, destination);

        // 3. Déplacer n-1 disques de auxiliaire vers destination
        deplacerDisques(n - 1, auxiliaire, destination, source);
    }

    public static void main(String[] args) {
        int nombreDisques = 3;
        System.out.printf("Résolution des Tours de Hanoï avec %d disques:%n", nombreDisques);
        deplacerDisques(nombreDisques, 'A', 'C', 'B');
        System.out.printf("Résolu en %d étapes%n", compteurEtapes);
    }
}
```

## Visualisation de la pile d'appels

Dans IntelliJ, vous pouvez voir la pile d'appels de plusieurs façons :

1. **Vue *Frames*** (Cadres)
   ```java
   // Placez un point d'arrêt ici
   if(n ==1){
       System.out.printf("Déplacer disque 1 de %c vers %c%n",source, destination);
       return;
   }
   ```

2. **Vue *Variables***
    - Montre les valeurs des paramètres à chaque niveau
    - Permet de voir comment les variables changent

3. **Vue *Debugger***
    - Affiche la pile complète des appels
    - Montre la progression de la récursion

## Conseils pour le débogage récursif

1. **Points d'arrêt conditionnels**
   ```java
   // Dans IntelliJ, clic droit sur le point d'arrêt
   // Condition: n == 2 (par exemple)
   if(n ==1){
       return;
   }
   ```

2. **Logging des appels**
   ```java
   public static long fibonacci(int n, int niveau) {
       String indentation = "  ".repeat(niveau);
       System.out.println(indentation + "Entrée: F(" + n + ")");
   
       if (n <= 1) {
           System.out.println(indentation + "Retour cas de base: " + n);
           return n;
       }
   
       long resultat = fibonacci(n - 1, niveau + 1) +
               fibonacci(n - 2, niveau + 1);
   
       System.out.println(indentation + "Retour F(" + n + ") = " + resultat);
       return resultat;
   }
   ```

3. **Utilisation de la vue "Evaluate Expression"**
   - Permet d'évaluer des expressions pendant le débogage
   - Utile pour vérifier des valeurs intermédiaires

La récursivité peut être difficile à visualiser mentalement, mais le débogueur d'IntelliJ offre des outils puissants
pour comprendre comment les appels s'empilent et se résolvent.



-------

!!! note "Note"
    Page rédigée en partie avec l'aide d'un assistant IA, principalement à l'aide de Perplexity AI, avec le *LLM* 
    **Claude 3.5 Sonnet**. L'IA a été utilisée pour générer des explications, des exemples et/ou des suggestions de 
    structure. Toutes les informations ont été vérifiées, éditées et complétées par l'auteur.