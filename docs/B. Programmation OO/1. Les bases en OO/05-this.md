---
icon: material/file-document-outline
---

# 5. Le mot-clé `this`

## Objectif

En Java, `this` est une référence vers **l’objet courant** (l’instance qui exécute la méthode).  
On l’utilise principalement pour :

1. **Distinguer** un attribut d’un paramètre de même nom
2. **Appeler un autre constructeur** de la même classe avec `this(...)`
3. Mieux comprendre le fonctionnement des **références** (plusieurs variables peuvent pointer sur le même objet)

---

## Exemple : classe `Personne` (avec `LocalDate`)

Voici une version améliorée de la classe `Personne` utilisant `LocalDate` pour gérer les dates.

```java
import java.time.LocalDate;

public class Personne {
    private String nom;
    private String prenom;
    private LocalDate dateNaissance;

    // Constructeur complet
    public Personne(String nom, String prenom, LocalDate dateNaissance) {
        this.nom = nom;
        this.prenom = prenom;
        this.dateNaissance = dateNaissance;
    }

    // Constructeur qui appelle l'autre constructeur avec la date d'aujourd'hui
    public Personne(String nom, String prenom) {
        this(nom, prenom, LocalDate.now());
    }

    // Accesseurs et mutateurs
    public String getNom() {
        return nom;
    }

    public void setNom(String nom) {
        this.nom = nom;
    }

    public String getPrenom() {
        return prenom;
    }

    public void setPrenom(String prenom) {
        this.prenom = prenom;
    }

    public LocalDate getDateNaissance() {
        return dateNaissance;
    }

    public void setDateNaissance(LocalDate dateNaissance) {
        this.dateNaissance = dateNaissance;
    }

    // Méthode utilitaire pour calculer l'âge
    public int getAge() {
        return LocalDate.now().getYear() - dateNaissance.getYear();
    }
}
```

### Utilisation

```java
// Création avec date spécifique
LocalDate dateNaissance = LocalDate.of(2000, 1, 15);
Personne personne1 = new Personne("Dupont", "Jean", dateNaissance);

// Création sans date (utilisera la date d'aujourd'hui)
Personne personne2 = new Personne("Martin", "Marie");
```

### À retenir dans cet exemple

- `this.nom = nom` : **désambiguïsation** entre attribut et paramètre
- `this(nom, prenom, LocalDate.now())` : **appel d’un autre constructeur**
- `LocalDate` : manipulation de dates plus fiable que des `String` ou des entiers

!!! note "Note"
    Le calcul de l'âge dans cet exemple est simplifié. Pour un calcul plus précis, il faudrait tenir compte des mois
    et des jours.

---

## 1) `this` pour distinguer attributs et paramètres

Quand un paramètre a le même nom qu’un attribut, `this` permet de dire clairement qu’on parle de l’attribut.

```java
public class Personne {
    private String nom;

    public Personne(String nom) {
        this.nom = nom;  // Sans this, nom référerait au paramètre
    }
}
```

---

## 2) `this(...)` pour appeler un autre constructeur

`this(...)` appelle **un autre constructeur de la même classe**. Il doit être la **première instruction** du constructeur.

```java
import java.time.LocalDate;

public class Personne {
    private String nom;
    private LocalDate dateNaissance;

    public Personne(String nom) {
        this(nom, LocalDate.now());  // Date d'aujourd'hui par défaut
    }

    public Personne(String nom, LocalDate dateNaissance) {
        this.nom = nom;
        this.dateNaissance = dateNaissance;
    }
}
```

---

## 3) Références : plusieurs variables, un seul objet

En Java, une variable objet contient une **référence** vers un objet, pas l’objet lui-même.

```java
public class Personne {
    private String nom;

    public void setNom(String nom) {
        this.nom = nom;  // this.nom réfère à l'attribut de l'instance
    }
}

// Utilisation avec plusieurs références
Personne p1 = new Personne();
Personne p2 = p1;  // p2 réfère au même objet que p1
```

### Conséquence : modifier via une référence modifie l’objet partagé

```java
Personne p1 = new Personne("Alice");
Personne p2 = p1;  // Nouvelle référence au même objet
p2.

setNom("Bob");  // Modifie l'objet via p2
System.out.

println(p1.getNom());  // Affiche "Bob" car p1 et p2 réfèrent au même objet
```

---

## 4) Passage de paramètres : modification vs réaffectation

Un paramètre de méthode reçoit une **copie de la référence**.

- Modifier l’objet via cette référence : impacte l’objet original
- Réaffecter la variable paramètre : ne change pas la référence à l’extérieur

```java
public class ExempleReferences {
    public static void modifierPersonne(Personne p) {
        p.setNom("Charlie");  // Modifie l'objet original
        p = new Personne("David");  // Crée un nouvel objet, ne modifie pas la référence originale
    }

    public static void main(String[] args) {
        Personne p1 = new Personne("Alice");
        modifierPersonne(p1);
        System.out.println(p1.getNom());  // Affiche "Charlie"
    }
}
```

---

## Synthèse

- `this` = **l’objet courant**
- `this.attribut` sert souvent à éviter les ambiguïtés avec les paramètres
- `this(...)` sert à **factoriser** des constructeurs
- Plusieurs références peuvent pointer sur le même objet : une modification est visible via toutes ces références

-------

??? info "Utilisation de l'IA"
    Page rédigée en partie avec l'aide d'un assistant IA. L'IA a été utilisée pour générer des
    explications, des exemples et/ou des suggestions de structure. Toutes les informations ont
    été vérifiées, éditées et complétées par l'auteur.
