# 🔸3🔸Exemples pour une banque

!!! warning "Avertissement"

    Les exemples ci-dessous sont des illustrations simplifiées de concepts de programmation orientée objet. Ils ne
    représentent pas des implémentations complètes de transactions bancaires et nécessitent des adaptations pour être 
    utilisés dans un contexte réel. Par exemple, les méthodes ne contiendraient pas seulement des `println` mais des 
    logiques plus complexes.

## Classe Abstraite Transaction

```java
public abstract class Transaction {
    protected String numeroCompte;
    protected double montant;
    protected LocalDateTime dateTransaction;
    protected String description;

    public Transaction(String numeroCompte, double montant) {
        this.numeroCompte = numeroCompte;
        this.montant = montant;
        this.dateTransaction = LocalDateTime.now();
    }

    public abstract void executer();

    public abstract void annuler();

    public abstract String genererRecu();
}
```

## Types de Transactions

**Retrait**

```java
public class Retrait extends Transaction {
    private String guichet;

    public Retrait(String numeroCompte, double montant, String guichet) {
        super(numeroCompte, montant);
        this.guichet = guichet;
    }

    @Override
    public void executer() {
        System.out.println("Vérification du solde disponible");
        System.out.println("Retrait de " + montant + "$ du compte " + numeroCompte);
        // Logique de retrait
    }

    @Override
    public void annuler() {
        System.out.println("Annulation du retrait : remise du montant sur le compte");
        // Logique d'annulation
    }

    @Override
    public String genererRecu() {
        return "Reçu de retrait - Compte: " + numeroCompte +
                " - Montant: " + montant + "$ - Guichet: " + guichet;
    }
}
```

**Dépôt**

```java
public class Depot extends Transaction {
    private String typeDepot; // "espèces", "chèque"

    public Depot(String numeroCompte, double montant, String typeDepot) {
        super(numeroCompte, montant);
        this.typeDepot = typeDepot;
    }

    @Override
    public void executer() {
        System.out.println("Vérification de la validité du dépôt");
        System.out.println("Dépôt de " + montant + "$ sur le compte " + numeroCompte);
        // Logique de dépôt
    }

    @Override
    public void annuler() {
        System.out.println("Annulation du dépôt");
        // Logique d'annulation
    }

    @Override
    public String genererRecu() {
        return "Reçu de dépôt - Compte: " + numeroCompte +
                " - Montant: " + montant + "$ - Type: " + typeDepot;
    }
}
```

**Virement**

```java
public class Virement extends Transaction {
    private String compteDestinataire;
    private String motif;

    public Virement(String numeroCompte, String compteDestinataire,
                    double montant, String motif) {
        super(numeroCompte, montant);
        this.compteDestinataire = compteDestinataire;
        this.motif = motif;
    }

    @Override
    public void executer() {
        System.out.println("Vérification des comptes source et destination");
        System.out.println("Virement de " + montant + "$ vers " + compteDestinataire);
        // Logique de virement
    }

    @Override
    public void annuler() {
        System.out.println("Annulation du virement : opération inverse");
        // Logique d'annulation
    }

    @Override
    public String genererRecu() {
        return "Reçu de virement - De: " + numeroCompte +
                " - Vers: " + compteDestinataire +
                " - Montant: " + montant + "$ - Motif: " + motif;
    }
}
```

**Paiement**

```java
public class Paiement extends Transaction {
    private String beneficiaire;
    private String reference;

    public Paiement(String numeroCompte, double montant,
                    String beneficiaire, String reference) {
        super(numeroCompte, montant);
        this.beneficiaire = beneficiaire;
        this.reference = reference;
    }

    @Override
    public void executer() {
        System.out.println("Vérification du compte et du bénéficiaire");
        System.out.println("Paiement de " + montant + "$ à " + beneficiaire);
        // Logique de paiement
    }

    @Override
    public void annuler() {
        System.out.println("Annulation du paiement : remboursement");
        // Logique d'annulation
    }

    @Override
    public String genererRecu() {
        return "Reçu de paiement - Compte: " + numeroCompte +
                " - Bénéficiaire: " + beneficiaire +
                " - Montant: " + montant + "$ - Réf: " + reference;
    }
}
```

## Utilisation

```java
public class GestionnaireTransactions {
    public static void executerTransaction(Transaction transaction) {
        try {
            transaction.executer();
            System.out.println(transaction.genererRecu());
        } catch (Exception e) {
            System.out.println("Erreur lors de la transaction");
            transaction.annuler();
        }
    }

    public static void main(String[] args) {
        Transaction retrait = new Retrait("123456", 100.0, "ATM001");
        Transaction depot = new Depot("123456", 500.0, "chèque");
        Transaction virement = new Virement("123456", "789012",
                250.0, "Remboursement");

        executerTransaction(retrait);
        executerTransaction(depot);
        executerTransaction(virement);
    }
}
```

Cette structure permet de :

- Gérer différents types de transactions de manière uniforme
- Assurer que chaque type de transaction implémente les opérations nécessaires
- Faciliter l'ajout de nouveaux types de transactions
- Maintenir une trace cohérente des opérations bancaires
- Gérer les annulations de manière appropriée pour chaque type de transaction

## Démonstration du Polymorphisme avec les Transactions

```java
public class GestionnaireTransactions {
    public static void executerTransaction(Transaction transaction) {
        try {
            transaction.executer();
            System.out.println(transaction.genererRecu());
        } catch (Exception e) {
            System.out.println("Erreur lors de la transaction");
            transaction.annuler();
        }
    }

    public static void main(String[] args) {
        // Création d'une liste de transactions de différents types
        ArrayList<Transaction> transactions = new ArrayList<>();

        // Ajout de différentes transactions dans la liste
        transactions.add(new Retrait("123456", 100.0, "ATM001"));
        transactions.add(new Depot("123456", 500.0, "chèque"));
        transactions.add(new Virement("123456", "789012", 250.0, "Remboursement"));
        transactions.add(new Paiement("123456", 75.0, "Hydro-Québec", "FACT-2024-01"));

        // Traitement polymorphique des transactions
        for (Transaction transaction : transactions) {
            executerTransaction(transaction);
            System.out.println("-------------------");
        }
    }
}
```

## Explication du Polymorphisme

Le polymorphisme se manifeste ici de plusieurs façons :

1. **Collection polymorphique** :
    - L'`ArrayList<Transaction>` peut contenir n'importe quel objet qui hérite de `Transaction`
    - Chaque élément peut être une instance différente (Retrait, Depot, Virement, Paiement)

2. **Traitement uniforme** :
    - La méthode `executerTransaction()` accepte un paramètre de type `Transaction`
    - Elle peut traiter n'importe quelle sous-classe de `Transaction` sans connaître son type exact

3. **Appels polymorphiques** :
    - Lors de l'appel de `transaction.executer()` et `transaction.genererRecu()`
    - La version appropriée de la méthode est appelée selon le type réel de l'objet
    - Par exemple, pour un Retrait, c'est la méthode `executer()` de la classe `Retrait` qui est appelée

## Avantages de cette Approche

- **Extensibilité** : Pour ajouter un nouveau type de transaction, il suffit de créer une nouvelle sous-classe
- **Maintenance** : Le code de traitement reste le même, quelle que soit la transaction
- **Simplicité** : Une seule boucle peut traiter tous les types de transactions
- **Flexibilité** : Les transactions peuvent être réorganisées ou filtrées facilement dans la liste

Cette approche polymorphique est particulièrement utile dans un système bancaire réel où de nouveaux types de
transactions peuvent être ajoutés sans modifier le code existant.


-------

!!! note "Note"
   Page rédigée en partie avec l'aide d'un assistant IA, principalement à l'aide de Perplexity AI, avec le *LLM*
   **Claude 3.5 Sonnet**. L'IA a été utilisée pour générer des explications, des exemples et/ou des suggestions de
   structure. Toutes les informations ont été vérifiées, éditées et complétées par l'auteur.