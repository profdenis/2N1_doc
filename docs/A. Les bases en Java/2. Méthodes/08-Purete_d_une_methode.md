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

??? info "Classe `Etudiant`"
```java
public class Etudiant {
    private String nom;
    private double note;

    public Etudiant(String nom, double note) {
        this.nom = nom;
        this.note = note;
    }

    // Utilisé par calculerMoyenne et identifierEchecs
    public double getNote() {
        return note;
    }

    // Utilisé pour afficher les informations ou envoyer des courriels
    public String getNom() {
        return nom;
    }

    @Override
    public String toString() {
        return nom + " (Note: " + note + ")";
    }
}
```



```java
// Mauvais exemple : trop de responsabilités
import java.util.ArrayList;
import java.util.List;

public class GestionEtudiants {
    public static void traiterResultatsExamen(List<Etudiant> etudiants) {
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

    public static void envoyerCourriel(Etudiant etudiant) {
        System.out.println("Envoi d'un courriel à " + etudiant.getNom() + " : Votre note est de " + etudiant.getNote());
    }
}

// Version améliorée : responsabilités séparées
public class GestionEtudiants {
    public static double calculerMoyenne(List<Etudiant> etudiants) {
        double somme = 0;
        for (Etudiant etudiant : etudiants) {
            somme += etudiant.getNote();
        }
        return somme / etudiants.size();
    }

    public static List<Etudiant> identifierEchecs(List<Etudiant> etudiants) {
        List<Etudiant> echecs = new ArrayList<>();
        for (Etudiant e : etudiants) {
            if (e.getNote() < 60) {
                echecs.add(e);
            }
        }
        return echecs;
    }

    public static void notifierEchecs(List<Etudiant> etudiantsEnEchec) {
        for (Etudiant etudiant : etudiantsEnEchec) {
            envoyerCourriel(etudiant);
        }
    }

    public static void genererRapport(double moyenne, List<Etudiant> echecs) {
        System.out.println("Moyenne: " + moyenne);
        System.out.println("Nombre d'échecs: " + echecs.size());
    }

    // Méthode principale qui orchestre les autres
    public static void traiterResultatsExamen(List<Etudiant> etudiants) {
        double moyenne = calculerMoyenne(etudiants);
        List<Etudiant> echecs = identifierEchecs(etudiants);
        notifierEchecs(echecs);
        genererRapport(moyenne, echecs);
    }
    
    public static void envoyerCourriel(Etudiant etudiant) {
        System.out.println("Envoi d'un courriel à " + etudiant.getNom() + " : Votre note est de " + etudiant.getNote());
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
    public static void analyserTexte(String texte) {
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
    public static int compterMots(String texte) {
        return texte.split("\\s+").length;
    }

    public static int compterCaracteres(String texte) {
        return texte.length();
    }

    public static String trouverMotLePlusLong(String texte) {
        String[] mots = texte.split("\\s+");
        String motLePlusLong = "";
        for (String mot : mots) {
            if (mot.length() > motLePlusLong.length()) {
                motLePlusLong = mot;
            }
        }
        return motLePlusLong;
    }

    public static void afficherResultats(int nombreMots, int nombreCaracteres, String motLePlusLong) {
        System.out.println("Nombre de mots: " + nombreMots);
        System.out.println("Nombre de caractères: " + nombreCaracteres);
        System.out.println("Mot le plus long: " + motLePlusLong);
    }

    // Méthode principale qui orchestre l'analyse
    public static void analyserTexte(String texte) {
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