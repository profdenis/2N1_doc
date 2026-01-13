---
icon: material/file-document-outline
---

# 8. Pureté d'une méthode

## Méthodes pures vs impures

Une **méthode pure** :

- Retourne toujours la même sortie pour les mêmes entrées
- Ne modifie pas l'état du programme
- N'a pas d'effets secondaires

```java
public class ExemplePur {
    // Méthode pure
    int additionner(int a, int b) {
        return a + b;
    }

    // Méthode pure
    double calculerAire(double rayon) {
        return Math.PI * rayon * rayon;
    }
}
```

Une **méthode impure** modifie l'état du programme ou dépend d'états externes :

```java
public class ExempleImpur {
    private int total = 0;

    // Méthode impure : modifie l'état
    void ajouterAuTotal(int valeur) {
        total += valeur;
    }

    // Méthode impure : dépend d'un état externe
    double calculerTaxe(double montant) {
        return montant * getTauxTaxe(); // dépend d'une valeur externe
    }

    // Méthode impure : effet secondaire (I/O)
    void sauvegarderDonnees(String donnees) {
        System.out.println(donnees); // effet secondaire
    }
}
```

## Avantages des méthodes pures

1. **Testabilité** : Faciles à tester, car le résultat dépend uniquement des paramètres
2. **Prévisibilité** : Comportement constant et prévisible
3. **Réutilisabilité** : Peuvent être utilisées n'importe où sans effets indésirables
4. **Parallélisation** : Peuvent s'exécuter en parallèle sans risque

## Principe de responsabilité unique

Une méthode devrait avoir une seule responsabilité. Voici un exemple de refactorisation :

```java
// Mauvais exemple : trop de responsabilités
public class GestionEtudiants {
    void traiterResultatsExamen(List<Etudiant> etudiants) {
        double somme = 0;
        int nombreEchecs = 0;

        for (Etudiant etudiant : etudiants) {
            somme += etudiant.getNote();
            if (etudiant.getNote() < 60) {
                nombreEchecs++;
                System.out.println(etudiant.getNom() + " a échoué");
                envoyerCourriel(etudiant);
            }
        }

        double moyenne = somme / etudiants.size();
        System.out.println("Moyenne: " + moyenne);
        System.out.println("Nombre d'échecs: " + nombreEchecs);
    }
}

// Version améliorée : responsabilités séparées
public class GestionEtudiants {
    double calculerMoyenne(List<Etudiant> etudiants) {
        double somme = 0;
        for (Etudiant etudiant : etudiants) {
            somme += etudiant.getNote();
        }
        return somme / etudiants.size();
    }

    List<Etudiant> identifierEchecs(List<Etudiant> etudiants) {
        return etudiants.stream()
                .filter(e -> e.getNote() < 60)
                .collect(Collectors.toList());
    }

    void notifierEchecs(List<Etudiant> etudiantsEnEchec) {
        for (Etudiant etudiant : etudiantsEnEchec) {
            envoyerCourriel(etudiant);
        }
    }

    void genererRapport(double moyenne, List<Etudiant> echecs) {
        System.out.println("Moyenne: " + moyenne);
        System.out.println("Nombre d'échecs: " + echecs.size());
    }

    // Méthode principale qui orchestre les autres
    void traiterResultatsExamen(List<Etudiant> etudiants) {
        double moyenne = calculerMoyenne(etudiants);
        List<Etudiant> echecs = identifierEchecs(etudiants);
        notifierEchecs(echecs);
        genererRapport(moyenne, echecs);
    }
}
```

## Avantages de la décomposition

1. **Lisibilité** : Chaque méthode est plus simple à comprendre
2. **Maintenabilité** : Plus facile à modifier ou corriger
3. **Réutilisabilité** : Les petites méthodes peuvent être réutilisées ailleurs
4. **Testabilité** : Plus facile de tester des fonctionnalités isolées
5. **Débogage** : Plus facile d'identifier la source d'un problème

## Autre exemple

```java
public class AnalyseurTexte {
    // Version initiale : trop de responsabilités
    void analyserTexte(String texte) {
        // Compte les mots
        String[] mots = texte.split("\\s+");
        System.out.println("Nombre de mots: " + mots.length);

        // Compte les caractères
        int nombreCaracteres = texte.length();
        System.out.println("Nombre de caractères: " + nombreCaracteres);

        // Trouve le mot le plus long
        String motLePlusLong = "";
        for (String mot : mots) {
            if (mot.length() > motLePlusLong.length()) {
                motLePlusLong = mot;
            }
        }
        System.out.println("Mot le plus long: " + motLePlusLong);
    }
}

// Version refactorisée
public class AnalyseurTexte {
    int compterMots(String texte) {
        return texte.split("\\s+").length;
    }

    int compterCaracteres(String texte) {
        return texte.length();
    }

    String trouverMotLePlusLong(String texte) {
        return Arrays.stream(texte.split("\\s+"))
                .max(Comparator.comparingInt(String::length))
                .orElse("");
    }

    void afficherResultats(int nombreMots, int nombreCaracteres, String motLePlusLong) {
        System.out.println("Nombre de mots: " + nombreMots);
        System.out.println("Nombre de caractères: " + nombreCaracteres);
        System.out.println("Mot le plus long: " + motLePlusLong);
    }

    // Méthode principale qui orchestre l'analyse
    void analyserTexte(String texte) {
        int nombreMots = compterMots(texte);
        int nombreCaracteres = compterCaracteres(texte);
        String motLePlusLong = trouverMotLePlusLong(texte);
        afficherResultats(nombreMots, nombreCaracteres, motLePlusLong);
    }
}
```



-------

??? info "Utilisation de l'IA"
    Page rédigée en partie avec l'aide d'un assistant IA. L'IA a été utilisée pour générer des 
    explications, des exemples et/ou des suggestions de structure. Toutes les informations ont 
    été vérifiées, éditées et complétées par l'auteur.