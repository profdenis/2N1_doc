## Pourquoi Éviter les Attributs Publics

Les attributs publics posent plusieurs problèmes importants :
- Ils permettent la modification directe des données sans aucun contrôle
- Ils ne garantissent pas la cohérence des données de l'objet
- Ils violent le principe d'encapsulation où un objet doit être responsable de sa propre cohérence[1]

Par exemple, avec des attributs publics, on pourrait faire :
```java
Personne personne = new Personne();
personne.age = -8; // Valeur invalide mais acceptée
```

## Solution : Encapsulation avec Accesseurs et Mutateurs

Pour protéger les données tout en permettant leur accès contrôlé, on utilise :

**Accesseurs (getters)** :
```java
public class Personne {
    private int age;
    
    public int getAge() {
        return age;
    }
}
```

**Mutateurs (setters)** :
```java
public class Personne {
    private int age;
    
    public void setAge(int age) {
        if (age > 0 && age < 125) {  // Validation des données
            this.age = age;
        }
    }
}
```

Cette approche offre plusieurs avantages :
- Contrôle de la validité des données avant modification[1]
- Protection de l'intégrité des données de l'objet[3]
- Possibilité de modifier l'implémentation interne sans affecter le code client
- Capacité d'ajouter des traitements supplémentaires lors de l'accès ou de la modification

En utilisant cette approche, l'objet maintient le contrôle sur ses données tout en fournissant une interface claire pour y accéder et les modifier de manière sécurisée.

Citations:
[1] https://prog101.com/exemples/csharp/poo/attribut-prive-public.php
[2] https://www.louismarchand.me/index.php/2021/06/25/pourquoi-je-naime-pas-la-portee-privee/
[3] https://datascientest.com/programmation-orientee-objet-guide-ultime
[4] https://jmdoudoux.developpez.com/cours/developpons/java/chap-poo.php
[5] https://www.jmdoudoux.fr/java/dej/chap-poo.htm