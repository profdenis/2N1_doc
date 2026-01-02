# 🔸1🔸L'héritage

L'héritage est un concept fondamental en programmation orientée objet qui permet de créer une nouvelle classe à partir
d'une classe existante. La nouvelle classe hérite des attributs et méthodes de la classe parente.

## Exemple avec la classe Personne

Commençons par une classe de base `Personne` :

```java
public class Personne {
    private String nom;
    private String prenom;
    private int age;

    public Personne(String nom, String prenom, int age) {
        this.nom = nom;
        this.prenom = prenom;
        this.age = age;
    }

    // Accesseurs
    public String getNom() {
        return nom;
    }

    public String getPrenom() {
        return prenom;
    }

    public int getAge() {
        return age;
    }

    // Mutateurs
    public void setNom(String nom) {
        this.nom = nom;
    }

    public void setPrenom(String prenom) {
        this.prenom = prenom;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public String toString() {
        return prenom + " " + nom + " (" + age + " ans)";
    }
}
```

## Première sous-classe : Etudiant

La classe `Etudiant` hérite de `Personne` en utilisant le mot-clé `extends`. Elle ajoute des attributs spécifiques aux
étudiants :

```java
public class Etudiant extends Personne {
    private String numeroDossier;
    private String programme;

    public Etudiant(String nom, String prenom, int age,
                    String numeroDossier, String programme) {
        super(nom, prenom, age);  // Appel du constructeur de la classe parente
        this.numeroDossier = numeroDossier;
        this.programme = programme;
    }

    // Accesseurs spécifiques à Etudiant
    public String getNumeroDossier() {
        return numeroDossier;
    }

    public String getProgramme() {
        return programme;
    }

    // Mutateurs spécifiques à Etudiant
    public void setNumeroDossier(String numeroDossier) {
        this.numeroDossier = numeroDossier;
    }

    public void setProgramme(String programme) {
        this.programme = programme;
    }

    @Override
    public String toString() {
        return super.toString() + " - " + programme +
                " (Dossier: " + numeroDossier + ")";
    }
}
```

## Deuxième sous-classe : Professeur

Ajoutons maintenant une classe `Professeur` qui hérite aussi de `Personne` :

```java
public class Professeur extends Personne {
    private String departement;
    private String specialite;

    public Professeur(String nom, String prenom, int age,
                      String departement, String specialite) {
        super(nom, prenom, age);
        this.departement = departement;
        this.specialite = specialite;
    }

    // Accesseurs spécifiques à Professeur
    public String getDepartement() {
        return departement;
    }

    public String getSpecialite() {
        return specialite;
    }

    // Mutateurs spécifiques à Professeur
    public void setDepartement(String departement) {
        this.departement = departement;
    }

    public void setSpecialite(String specialite) {
        this.specialite = specialite;
    }

    @Override
    public String toString() {
        return super.toString() + " - " + departement +
                " (Spécialité: " + specialite + ")";
    }
}
```

## Points importants à noter

- Le mot-clé `extends` indique l'héritage
- `super()` appelle le constructeur de la classe parente
- Les sous-classes héritent de toutes les méthodes publiques et protégées
- `@Override` indique qu'on redéfinit une méthode de la classe parente
- Les sous-classes peuvent ajouter leurs propres attributs et méthodes
- Une sous-classe peut accéder aux méthodes de la classe parente avec `super`

Pour tester ces classes, voici un exemple d'utilisation :

```java
public class TestHeritage {
    public static void main(String[] args) {
        Etudiant etudiant = new Etudiant("Tremblay", "Marie", 20,
                "12345", "Informatique");
        Professeur prof = new Professeur("Dubois", "Pierre", 45,
                "Informatique", "Java");

        System.out.println(etudiant);
        System.out.println(prof);
    }
}
```



-------

??? info "Utilisation de l'IA"
    Page rédigée en partie avec l'aide d'un assistant IA. L'IA a été utilisée pour générer des 
    explications, des exemples et/ou des suggestions de structure. Toutes les informations ont 
    été vérifiées, éditées et complétées par l'auteur.