# Solutions : exercices partie 1

## Question 1 : Valeur absolue

Pour calculer la valeur absolue d'un nombre, nous devons :

1. Lire un nombre de l'utilisateur
2. Déterminer si le nombre est négatif
3. Si le nombre est négatif, le multiplier par -1.
4. Afficher le résultat

Voici le code solution :

```java
import java.util.Scanner;

public class ExercicesPartie1 {
    public static void valeurAbsolue() {
        Scanner clavier = new Scanner(System.in);

        System.out.print("Entrez un nombre: ");
        int nombre = clavier.nextInt();

        int valeurAbsolue = nombre;
        if (nombre < 0) {
            valeurAbsolue = -nombre;
        }

        System.out.println("La valeur absolue de " + nombre + " est " + valeurAbsolue);
    }

    public static void main(String[] args) {
        valeurAbsolue();
    }
}
```

**Points importants à expliquer aux étudiants :**

- La méthode est déclarée `static` car elle sera appelée directement dans le `main`
- Nous utilisons un `Scanner` pour lire l'entrée de l'utilisateur
- La condition `if` vérifie si le nombre est négatif
- Il n'est pas nécessaire d'utiliser un `else` car si le nombre est positif, nous voulons garder sa valeur initiale
- La méthode `Math.abs()` existe en Java pour calculer la valeur absolue, mais l'exercice demande d'implémenter la
  logique nous-mêmes

**Exemples de tests à effectuer :**

- Entrée : 5 → Sortie attendue : 5
- Entrée : -3 → Sortie attendue : 3
- Entrée : 0 → Sortie attendue : 0
- Entrée : -10 → Sortie attendue : 10

## Question 2 : Nombre pair ou impair

Pour déterminer si un nombre est pair ou impair, nous utilisons l'opérateur modulo (%). Un nombre est pair si le reste
de sa division par 2 est égal à 0.

Voici le code solution :

```java
import java.util.Scanner;

public class ExercicesPartie1 {
    public static void verifierPairImpair() {
        Scanner clavier = new Scanner(System.in);

        System.out.print("Entrez un nombre entier: ");
        int nombre = clavier.nextInt();

        if (nombre % 2 == 0) {
            System.out.println(nombre + " est pair");
        } else {
            System.out.println(nombre + " est impair");
        }
    }

    public static void main(String[] args) {
        verifierPairImpair();
    }
}
```

**Points importants à expliquer aux étudiants :**

- L'opérateur modulo `%` retourne le reste de la division
- Pour un nombre pair, `nombre % 2` donne toujours 0
- Pour un nombre impair, `nombre % 2` donne toujours 1
- La structure if/else est appropriée ici, car nous avons exactement deux cas possibles
- La méthode traite aussi correctement les nombres négatifs

**Exemples de tests à effectuer :**

- Entrée : 4 → Sortie : "4 est pair"
- Entrée : 7 → Sortie : "7 est impair"
- Entrée : 0 → Sortie : "0 est pair"
- Entrée : -3 → Sortie : "-3 est impair"
- Entrée : -2 → Sortie : "-2 est pair"

## Question 3 : Le plus petit de trois nombres

Pour trouver le plus petit de trois nombres, nous devons comparer les nombres de manière systématique.

Voici le code solution :

```java
import java.util.Scanner;

public class ExercicesPartie1 {
    public static void trouverPlusPetit() {
        Scanner clavier = new Scanner(System.in);

        System.out.print("Entrez le premier nombre: ");
        int nombre1 = clavier.nextInt();

        System.out.print("Entrez le deuxième nombre: ");
        int nombre2 = clavier.nextInt();

        System.out.print("Entrez le troisième nombre: ");
        int nombre3 = clavier.nextInt();

        int plusPetit = nombre1;

        if (nombre2 < plusPetit) {
            plusPetit = nombre2;
        }

        if (nombre3 < plusPetit) {
            plusPetit = nombre3;
        }

        System.out.println("Le plus petit nombre est: " + plusPetit);
    }

    public static void main(String[] args) {
        trouverPlusPetit();
    }
}
```

**Points importants à expliquer aux étudiants :**

- Nous commençons par supposer que le premier nombre est le plus petit
- Nous comparons ensuite cette valeur avec les autres nombres
- Si nous trouvons un nombre plus petit, nous mettons à jour notre variable `plusPetit`
- Cette approche est plus simple et plus claire que d'utiliser des conditions imbriquées
- Il existe aussi la méthode `Math.min()`, mais l'exercice demande d'implémenter la logique nous-mêmes

**Exemples de tests à effectuer :**

- Entrée : 5, 3, 7 → Sortie : 3
- Entrée : 2, 2, 2 → Sortie : 2
- Entrée : -1, 0, 1 → Sortie : -1
- Entrée : 10, -5, 3 → Sortie : -5
- Entrée : 0, 0, 1 → Sortie : 0

## Question 4 : Calcul du salaire avec heures supplémentaires

Pour calculer le salaire total, nous devons :

1. Lire le salaire horaire et les heures travaillées
2. Calculer le salaire de base pour les 40 premières heures
3. Si applicable, calculer le salaire pour les heures supplémentaires (1.5x le taux horaire)
4. Additionner les deux montants

Voici le code solution :

```java
import java.util.Scanner;

public class ExercicesPartie1 {
    public static void calculerSalaire() {
        Scanner clavier = new Scanner(System.in);

        System.out.print("Entrez le salaire horaire: ");
        double salaireHoraire = clavier.nextDouble();

        System.out.print("Entrez le nombre d'heures travaillées: ");
        double heuresTravaillees = clavier.nextDouble();

        double salaireFinal;

        if (heuresTravaillees <= 40) {
            salaireFinal = salaireHoraire * heuresTravaillees;
        } else {
            double heuresNormales = 40;
            double heuresSupp = heuresTravaillees - 40;
            salaireFinal = (salaireHoraire * heuresNormales) +
                    (salaireHoraire * 1.5 * heuresSupp);
        }

        System.out.printf("Le salaire total est: %.2f$\n", salaireFinal);
    }

    public static void main(String[] args) {
        calculerSalaire();
    }
}
```

**Points importants à expliquer aux étudiants :**

- Nous utilisons le type `double` pour gérer les décimales dans les calculs monétaires
- La structure if/else sépare clairement les deux cas possibles :
    - Heures régulières seulement (≤ 40 heures)
    - Heures régulières + heures supplémentaires (> 40 heures)
- `printf` est utilisé pour formater l'affichage à deux décimales
- Les calculs sont séparés en parties distinctes pour plus de clarté

**Exemples de tests à effectuer :**

- Entrée : 20\$/h, 35h → Sortie : 700.00\$
- Entrée : 15\$/h, 45h → Sortie : 712.50\$ (600\$ + 112.50\$)
- Entrée : 25\$/h, 40h → Sortie : 1000.00\$
- Entrée : 18\$/h, 50h → Sortie : 990.00\$ (720\$ + 270\$)

## Question 5 : Type de triangle

Pour déterminer le type de triangle, nous devons :

1. Lire les trois côtés
2. Vérifier les égalités entre les côtés
3. Classifier le triangle selon ces égalités

Voici le code solution :

```java
import java.util.Scanner;

public class ExercicesPartie1 {
    public static void determinerTypeTriangle() {
        Scanner clavier = new Scanner(System.in);

        System.out.print("Entrez la longueur du premier côté: ");
        double cote1 = clavier.nextDouble();

        System.out.print("Entrez la longueur du deuxième côté: ");
        double cote2 = clavier.nextDouble();

        System.out.print("Entrez la longueur du troisième côté: ");
        double cote3 = clavier.nextDouble();

        // Vérifier si les côtés sont positifs
        if (cote1 <= 0 || cote2 <= 0 || cote3 <= 0) {
            System.out.println("Les côtés doivent être positifs");
            return;
        }

        // Déterminer le type de triangle
        if (cote1 == cote2 && cote2 == cote3) {
            System.out.println("Équilatéral");
        } else if (cote1 == cote2 || cote2 == cote3 || cote1 == cote3) {
            System.out.println("Isocèle");
        } else {
            System.out.println("Scalène");
        }
    }

    public static void main(String[] args) {
        determinerTypeTriangle();
    }
}
```

**Points importants à expliquer aux étudiants :**

- Nous utilisons le type `double` pour permettre des mesures décimales
- La validation des côtés positifs est importante pour la cohérence mathématique
- L'ordre des conditions est crucial :
    1. D'abord vérifier si tous les côtés sont égaux (équilatéral).
    2. Ensuite vérifier si deux côtés sont égaux (isocèle).
    3. Sinon, c'est un triangle scalène
- L'utilisation de `return` permet de terminer la méthode si les données sont invalides

**Exemples de tests à effectuer :**

- Entrée : 5, 5, 5 → Sortie : "Équilatéral"
- Entrée : 5, 5, 3 → Sortie : "Isocèle"
- Entrée : 3, 4, 5 → Sortie : "Scalène"
- Entrée : -1, 2, 3 → Sortie : "Les côtés doivent être positifs"
- Entrée : 4, 4, 6 → Sortie : "Isocèle"

## Question 6 : Calcul de moyenne et validation

Pour calculer la moyenne de trois notes et déterminer la réussite, nous devons :

1. Lire les trois notes
2. Calculer la moyenne
3. Déterminer si c'est un échec ou une réussite

Voici le code solution :

```java
import java.util.Scanner;

public class ExercicesPartie1 {
    public static void calculerMoyenne() {
        Scanner clavier = new Scanner(System.in);

        System.out.print("Entrez la première note (sur 100): ");
        double note1 = clavier.nextDouble();

        System.out.print("Entrez la deuxième note (sur 100): ");
        double note2 = clavier.nextDouble();

        System.out.print("Entrez la troisième note (sur 100): ");
        double note3 = clavier.nextDouble();

        // Validation des notes
        if (note1 < 0 || note1 > 100 || note2 < 0 || note2 > 100 || note3 < 0 || note3 > 100) {
            System.out.println("Les notes doivent être entre 0 et 100");
            return;
        }

        // Calcul de la moyenne
        double moyenne = (note1 + note2 + note3) / 3;

        // Affichage du résultat
        if (moyenne < 60) {
            System.out.println("Échec");
        } else {
            System.out.printf("Note finale: %.1f/100\n", moyenne);
        }
    }

    public static void main(String[] args) {
        calculerMoyenne();
    }
}
```

**Points importants à expliquer aux étudiants :**

- La validation des notes est importante pour assurer la cohérence des résultats
- Nous utilisons le type `double` pour gérer les décimales dans les calculs
- La moyenne est calculée en additionnant les notes et en divisant par le nombre de notes
- `printf` permet de formater l'affichage à une décimale
- La condition de réussite (≥ 60) détermine le message à afficher

**Exemples de tests à effectuer :**

- Entrée : 70, 80, 90 → Sortie : "Note finale : 80.0/100"
- Entrée : 50, 55, 45 → Sortie : "Échec"
- Entrée : 60, 60, 60 → Sortie : "Note finale : 60.0/100"
- Entrée : -10, 80, 90 → Sortie : "Les notes doivent être entre 0 et 100"
- Entrée : 59, 59, 59 → Sortie : "Échec"

## Question 7 : Conversion de note numérique en lettre

Pour convertir une note numérique en lettre, nous devons :

1. Lire la note
2. Valider qu'elle est entre 0 et 100
3. Déterminer la lettre correspondante selon les intervalles donnés

Voici le code solution :

```java
import java.util.Scanner;

public class ExercicesPartie1 {
    public static void convertirNoteEnLettre() {
        Scanner clavier = new Scanner(System.in);

        System.out.print("Entrez la note finale (0-100): ");
        double note = clavier.nextDouble();

        // Validation de la note
        if (note < 0 || note > 100) {
            System.out.println("Cette note est invalide");
            return;
        }

        // Conversion en lettre
        char lettre;
        if (note >= 90) {
            lettre = 'A';
        } else if (note >= 80) {
            lettre = 'B';
        } else if (note >= 70) {
            lettre = 'C';
        } else if (note >= 60) {
            lettre = 'D';
        } else {
            lettre = 'E';
        }

        System.out.println("Note: " + lettre);
    }

    public static void main(String[] args) {
        convertirNoteEnLettre();
    }
}
```

**Points importants à expliquer aux étudiants :**

- L'ordre des conditions est important : on commence par la plus haute note
- Les conditions utilisent >= pour inclure la borne inférieure de chaque intervalle
- La structure `if-else if` permet de n'exécuter qu'une seule condition
- Le type `char` est utilisé pour stocker la lettre
- La validation est faite avant la conversion.

**Exemples de tests à effectuer :**

- Entrée : 95 → Sortie : "Note : A"
- Entrée : 85 → Sortie : "Note : B"
- Entrée : 75 → Sortie : "Note : C"
- Entrée : 65 → Sortie : "Note : D"
- Entrée : 55 → Sortie : "Note : E"
- Entrée : -5 → Sortie : "Cette note est invalide"
- Entrée : 101 → Sortie : "Cette note est invalide"

### Avec une expression `switch` moderne

Voici la même conversion de notes en utilisant le switch moderne (*switch expressions*) disponible depuis Java 14 :

```java
import java.util.Scanner;

public class ExercicesPartie1 {
    public static void convertirNoteEnLettre() {
        Scanner clavier = new Scanner(System.in);

        System.out.print("Entrez la note finale (0-100): ");
        double note = clavier.nextDouble();

        // Validation de la note
        if (note < 0 || note > 100) {
            System.out.println("Cette note est invalide");
            return;
        }

        // Conversion en lettre avec switch moderne
        char lettre = switch ((int) (note / 10)) {
            case 9, 10 -> 'A';
            case 8 -> 'B';
            case 7 -> 'C';
            case 6 -> 'D';
            default -> 'E';
        };

        System.out.println("Note: " + lettre);
    }

    public static void main(String[] args) {
        convertirNoteEnLettre();
    }
}
```

Les avantages de cette version moderne sont :
- La syntaxe est plus concise avec l'opérateur fléché (`->`)
- Pas besoin d'utiliser `break`
- L'assignation peut se faire directement dans une expression
- Les cas multiples peuvent être listés avec des virgules (`case 9, 10`)

## Question 8 : Validation simple d'un intervalle

Pour valider qu'un nombre est entre 1 et 10 inclusivement, nous devons :

1. Lire le nombre
2. Vérifier s'il est dans l'intervalle [1,10]
3. Afficher le message approprié

Voici le code solution :

```java
import java.util.Scanner;

public class ExercicesPartie1 {
    public static void validerIntervalle() {
        Scanner clavier = new Scanner(System.in);

        System.out.print("Entrez un nombre entre 1 et 10: ");
        int nombre = clavier.nextInt();

        if (nombre >= 1 && nombre <= 10) {
            System.out.println("valide");
        } else {
            System.out.println("invalide");
        }
    }

    public static void main(String[] args) {
        validerIntervalle();
    }
}
```

**Points importants à expliquer aux étudiants :**

- L'opérateur `&&` permet de combiner deux conditions
- Les bornes (1 et 10) sont incluses dans l'intervalle grâce à `>=` et `<=`
- La structure if/else est appropriée, car nous avons exactement deux cas possibles
- Le message affiché doit être exactement "valide" ou "invalide" selon l'énoncé

**Exemples de tests à effectuer :**

- Entrée : 5 → Sortie : "valide"
- Entrée : 1 → Sortie : "valide"
- Entrée : 10 → Sortie : "valide"
- Entrée : 0 → Sortie : "invalide"
- Entrée : 11 → Sortie : "invalide"
- Entrée : -5 → Sortie : "invalide"

## Question 9 : Validation avec répétition

Cette question est similaire à la précédente, mais nous devons continuer à demander un nombre jusqu'à ce qu'il soit
valide.

Voici le code solution :

```java
import java.util.Scanner;

public class ExercicesPartie1 {
    public static void validerIntervalleAvecRepetition() {
        Scanner clavier = new Scanner(System.in);
        int nombre;

        do {
            System.out.print("Entrez un nombre entre 1 et 10: ");
            nombre = clavier.nextInt();

            if (nombre < 1 || nombre > 10) {
                System.out.println("invalide");
            }
        } while (nombre < 1 || nombre > 10);

        System.out.println("valide");
    }

    public static void main(String[] args) {
        validerIntervalleAvecRepetition();
    }
}
```

**Points importants à expliquer aux étudiants :**

- La boucle `do-while` est idéale ici car :
    - Nous devons exécuter le code au moins une fois
    - Nous ne connaissons pas à l'avance le nombre d'itérations nécessaires
- La condition de la boucle est l'inverse de la validation
- Le message "invalide" est affiché à chaque tentative incorrecte
- Le message "valide" n'est affiché qu'une seule fois, après avoir obtenu un nombre valide

**Exemples de tests à effectuer :**

```
Test 1 :
Entrée : 15
Sortie : "invalide"
Entrée : 0
Sortie : "invalide"
Entrée : 7
Sortie : "valide"

Test 2 :
Entrée : 5
Sortie : "valide"

Test 3 :
Entrée : -3
Sortie : "invalide"
Entrée : 11
Sortie : "invalide"
Entrée : 1
Sortie : "valide"
```

## Question 10 : Validation avec nombre limité d'essais

Cette question ajoute une limite de 3 essais incorrects à la validation précédente.

Voici le code solution :

```java
import java.util.Scanner;

public class ExercicesPartie1 {
    public static void validerIntervalleAvecLimite() {
        Scanner clavier = new Scanner(System.in);
        int nombre;
        int essaisIncorrects = 0;
        final int MAX_ESSAIS = 3;

        do {
            System.out.print("Entrez un nombre entre 1 et 10: ");
            nombre = clavier.nextInt();

            if (nombre < 1 || nombre > 10) {
                essaisIncorrects++;
                System.out.println("invalide");

                if (essaisIncorrects >= MAX_ESSAIS) {
                    System.out.println("Nombre maximal d'essais atteint.");
                    return;
                }
            }
        } while (nombre < 1 || nombre > 10);

        System.out.println("valide");
    }

    public static void main(String[] args) {
        validerIntervalleAvecLimite();
    }
}
```

**Points importants à expliquer aux étudiants :**

- Une constante `MAX_ESSAIS` est utilisée pour définir la limite
- Le compteur `essaisIncorrects` est incrémenté à chaque essai invalide
- L'instruction `return` permet de sortir immédiatement de la méthode quand la limite est atteinte
- La structure reste similaire à la question précédente, avec l'ajout du compteur
- Le message de limite atteinte doit être exact selon l'énoncé

**Exemples de tests à effectuer :**

```
Test 1 (succès rapide) :
Entrée : 5
Sortie : "valide"

Test 2 (succès après erreurs) :
Entrée : 11
Sortie : "invalide"
Entrée : 0
Sortie : "invalide"
Entrée : 7
Sortie : "valide"

Test 3 (échec après 3 essais) :
Entrée : 15
Sortie : "invalide"
Entrée : -1
Sortie : "invalide"
Entrée : 11
Sortie : "invalide"
Sortie : "Nombre maximal d'essais atteint."
```

## Question 11 : Inverser un nombre entier

Pour inverser un nombre entier sans utiliser de chaîne de caractères, nous devons :

1. Extraire chaque chiffre avec l'opérateur modulo (%)
2. Construire le nouveau nombre en multipliant par 10 et en ajoutant chaque chiffre
3. Utiliser la division entière pour passer au chiffre suivant

Voici le code solution :

```java
import java.util.Scanner;

public class ExercicesPartie1 {
    public static void inverserNombre() {
        Scanner clavier = new Scanner(System.in);

        System.out.print("Entrez un nombre entier: ");
        int nombre = clavier.nextInt();

        int nombreInverse = 0;
        int nombreTemp = Math.abs(nombre); // Traiter le signe à part

        while (nombreTemp > 0) {
            int chiffre = nombreTemp % 10;        // Extraire le dernier chiffre
            nombreInverse = nombreInverse * 10 + chiffre;  // Construire le nombre inverse
            nombreTemp = nombreTemp / 10;         // Enlever le dernier chiffre
        }

        // Gérer le signe du nombre original
        if (nombre < 0) {
            nombreInverse = -nombreInverse;
        }

        System.out.println("Nombre inversé: " + nombreInverse);
    }

    public static void main(String[] args) {
        inverserNombre();
    }
}
```

**Points importants à expliquer aux étudiants :**

- L'algorithme utilise trois opérations mathématiques clés :
    - `% 10` pour obtenir le dernier chiffre
    - `* 10` pour décaler les chiffres vers la gauche
    - `/ 10` pour enlever le dernier chiffre
- Nous traitons le signe séparément pour simplifier les calculs
- La boucle continue tant qu'il reste des chiffres à traiter
- Chaque itération :
    1. Extrait le dernier chiffre
    2. L'ajoute au résultat (décalé).
    3. Réduit le nombre original

**Exemples de tests à effectuer :**

```
Test 1 :
Entrée : 123456
Sortie : 654321

Test 2 :
Entrée : 100
Sortie : 1

Test 3 :
Entrée : -123
Sortie : -321

Test 4 :
Entrée : 1000
Sortie : 1

Test 5 :
Entrée : 5
Sortie : 5
```

## Question 12 : Décompte avec message final

Pour réaliser un décompte et afficher "Terminé !" à la fin, nous devons :

1. Lire le nombre de départ
2. Afficher chaque nombre en décrémentant
3. Remplacer le 0 par "Terminé !"

Voici le code solution :

```java
import java.util.Scanner;

public class ExercicesPartie1 {
    public static void faireDecompte() {
        Scanner clavier = new Scanner(System.in);

        System.out.print("Entrez un nombre entier positif: ");
        int nombre = clavier.nextInt();

        if (nombre <= 0) {
            System.out.println("Le nombre doit être positif");
            return;
        }

        for (int i = nombre; i > 0; i--) {
            System.out.println(i);
        }

        System.out.println("Terminé !");
    }

    public static void main(String[] args) {
        faireDecompte();
    }
}
```

**Points importants à expliquer aux étudiants :**

- La boucle `for` est idéale ici car :
    - Nous connaissons le nombre exact d'itérations
    - Nous avons besoin d'un compteur qui décrémente
- La validation du nombre positif est importante.
- Le message "Terminé !" remplace le 0 et n'est affiché qu'une fois à la fin
- Chaque nombre est affiché sur une nouvelle ligne

**Exemples de tests à effectuer :**

```
Test 1 :
Entrée : 5
Sortie :
5
4
3
2
1
Terminé !

Test 2 :
Entrée : 1
Sortie :
1
Terminé !

Test 3 :
Entrée : 0
Sortie : Le nombre doit être positif

Test 4 :
Entrée : -3
Sortie : Le nombre doit être positif
```

## Question 13 : Opérations sur tableau avec boucle for

Cette question comporte trois sous-parties utilisant un même tableau, mais avec des opérations différentes.

```java
public class ExercicesPartie1 {
    // Tableau de test commun pour toutes les sous-questions
    private static final int[] tableau = {4, -2, 7, 8, -5, 10, 3, 6, -8, 1};

    // Sous-question 1 : Somme et moyenne
    public static void calculerSommeMoyenne() {
        int somme = 0;

        for (int i = 0; i < tableau.length; i++) {
            somme += tableau[i];
        }

        double moyenne = (double) somme / tableau.length;
        System.out.println("Somme: " + somme);
        System.out.printf("Moyenne: %.2f\n", moyenne);
    }

    // Sous-question 2 : Nombres pairs
    public static void afficherNombresPairs() {
        System.out.print("Nombres pairs: ");

        for (int i = 0; i < tableau.length; i++) {
            if (tableau[i] % 2 == 0) {
                System.out.print(tableau[i] + " ");
            }
        }
        System.out.println();
    }

    // Sous-question 3 : Vérifier si tous positifs
    public static void verifierTousPositifs() {
        boolean tousPositifs = true;

        for (int i = 0; i < tableau.length; i++) {
            if (tableau[i] <= 0) {
                tousPositifs = false;
                break;
            }
        }

        System.out.println(tousPositifs);
    }

    public static void main(String[] args) {
        System.out.println("Question 13.1 - Somme et moyenne:");
        calculerSommeMoyenne();

        System.out.println("\nQuestion 13.2 - Nombres pairs:");
        afficherNombresPairs();

        System.out.println("\nQuestion 13.3 - Tous positifs:");
        verifierTousPositifs();
    }
}
```

**Points importants à expliquer aux étudiants :**

- Le tableau est déclaré comme constante de classe pour être réutilisé
- Chaque sous-question utilise une boucle `for` avec index
- La boucle `for` permet d'accéder aux éléments via leur index : `tableau[i]`

**Pour la somme et moyenne :**

- Le cast vers `double` est nécessaire pour avoir une division décimale
- `printf` permet de formater l'affichage des décimales

**Pour les nombres pairs :**

- L'opérateur modulo `%` permet de tester si un nombre est pair
- `print` (sans ln) permet d'afficher sur une même ligne

**Pour la vérification des positifs :**

- L'approche avec un booléen initialisé à `true` est efficace
- Le `break` permet de sortir de la boucle dès qu'un négatif est trouvé

**Exemple d'exécution :**

```
Question 13.1 - Somme et moyenne :
Somme : 24
Moyenne : 2.40

Question 13.2 - Nombres pairs :
Nombres pairs : 4 -2 8 10 6 -8 

Question 13.3 - Tous positifs :
faux
```

## Question 14 : Mêmes opérations avec boucle `while/do-while`

Cette question reprend les mêmes opérations que la question 13, mais en utilisant des boucles while.

```java
public class ExercicesPartie1 {
    // Même tableau de test que la question 13
    private static final int[] tableau = {4, -2, 7, 8, -5, 10, 3, 6, -8, 1};

    // Sous-question 1 : Somme et moyenne avec while
    public static void calculerSommeMoyenneWhile() {
        int somme = 0;
        int i = 0;

        while (i < tableau.length) {
            somme += tableau[i];
            i++;
        }

        double moyenne = (double) somme / tableau.length;
        System.out.println("Somme: " + somme);
        System.out.printf("Moyenne: %.2f\n", moyenne);
    }

    // Sous-question 2 : Nombres pairs avec while
    public static void afficherNombresPairsWhile() {
        System.out.print("Nombres pairs: ");
        int i = 0;

        while (i < tableau.length) {
            if (tableau[i] % 2 == 0) {
                System.out.print(tableau[i] + " ");
            }
            i++;
        }
        System.out.println();
    }

    // Sous-question 3 : Vérifier si tous positifs avec while
    public static void verifierTousPositifsWhile() {
        boolean tousPositifs = true;
        int i = 0;

        while (i < tableau.length && tousPositifs) {
            if (tableau[i] <= 0) {
                tousPositifs = false;
            }
            i++;
        }

        System.out.println(tousPositifs);
    }

    public static void main(String[] args) {
        System.out.println("Question 14.1 - Somme et moyenne (while):");
        calculerSommeMoyenneWhile();

        System.out.println("\nQuestion 14.2 - Nombres pairs (while):");
        afficherNombresPairsWhile();

        System.out.println("\nQuestion 14.3 - Tous positifs (while):");
        verifierTousPositifsWhile();
    }
}
```

**Points importants à expliquer aux étudiants :**

- La principale différence avec la question 13 est la structure de boucle
- Avec `while`, nous devons :
    - Initialiser le compteur avant la boucle
    - Incrémenter manuellement le compteur dans la boucle
    - Gérer la condition de continuation nous-mêmes

**Différences clés avec la version for :**

- La variable de compteur `i` doit être déclarée avant la boucle
- L'incrémentation doit être explicite dans le corps de la boucle
- La logique reste la même, seule la structure change

**Note sur l'optimisation :**

- Dans la version `verifierTousPositifsWhile`, nous pouvons combiner la condition du `while` avec notre booléen
- Cela permet d'arrêter la boucle dès qu'un nombre négatif est trouvé

**Exemple d'exécution :**

```
Question 14.1 - Somme et moyenne (while) :
Somme : 24
Moyenne : 2.40

Question 14.2 - Nombres pairs (while) :
Nombres pairs : 4 -2 8 10 6 -8 

Question 14.3 - Tous positifs (while) :
faux
```

-------

??? info "Utilisation de l'IA"
      Page rédigée en partie avec l'aide d'un assistant IA, principalement à l'aide de Perplexity AI, avec le *LLM*
      **Claude 3.5 Sonnet**. L'IA a été utilisée pour générer des explications, des exemples et/ou des suggestions de
      structure. Toutes les informations ont été vérifiées, éditées et complétées par l'auteur.