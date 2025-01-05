# 🔸7🔸Peut-on modifier la valeur à l'intérieur d'un Integer ?

Non, il est impossible de modifier la valeur à l'intérieur d'un `Integer` car la classe Integer est immuable 
(*immutable*) en Java[1][5]. Cela signifie que lorsqu'un objet de type `Integer` est créé, sa valeur ne peut plus être 
modifiée.

## Alternatives

Pour gérer des entiers modifiables, il existe deux solutions principales :

**Utiliser AtomicInteger** :

```java
import java.util.concurrent.atomic.AtomicInteger;

public class ExempleAtomicInteger {
    public static void incrementer(AtomicInteger nombre) {
        nombre.incrementAndGet();
    }

    public static void main(String[] args) {
        AtomicInteger nombre = new AtomicInteger(5);
        incrementer(nombre);
        System.out.println(nombre.get()); // Affiche 6
    }
}
```

**Créer une classe wrapper personnalisée** :

```java
public class NombreModifiable {
    private int valeur;

    public NombreModifiable(int valeur) {
        this.valeur = valeur;
    }

    public void setValeur(int nouvelleValeur) {
        this.valeur = nouvelleValeur;
    }

    public int getValeur() {
        return valeur;
    }
}
```

Cette limitation des Integer est intentionnelle et fait partie de la conception de Java[2]. Quand on tente de modifier
un Integer, Java crée en fait un nouvel objet plutôt que de modifier l'existant[4].

## Citations

- [1] https://www.geeksforgeeks.org/how-to-pass-integer-by-reference-in-java/
- [2] https://namekdev.net/2012/07/immutability-of-java-integer/
- [3] https://www.scaler.com/topics/integer-class-in-java/
- [4] https://stackoverflow.com/questions/26185527/how-can-i-change-integer-value-when-it-is-an-argument-like-change-arrays-value/26185597
- [5] https://www.geeksforgeeks.org/primitive-wrapper-classes-are-immutable-in-java/



-------

!!! note "Note"
    Page rédigée en partie avec l'aide d'un assistant IA, principalement à l'aide de Perplexity AI, avec le *LLM* 
    **Claude 3.5 Sonnet**. L'IA a été utilisée pour générer des explications, des exemples et/ou des suggestions de 
    structure. Toutes les informations ont été vérifiées, éditées et complétées par l'auteur.