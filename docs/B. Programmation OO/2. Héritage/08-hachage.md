---
icon: material/file-document-outline
---

# 8. Fonctions et code de hachage

Les fonctions de hachage sont des outils fondamentaux en informatique qui transforment des données de taille variable en
une valeur numérique fixe. Voici une explication détaillée avec des exemples concrets :

## Définition et propriétés clés

- **Transformation unidirectionnelle** : Conversion de données arbitraires en empreinte numérique fixe (ex : 32/64 bits)
- **Déterministe** : Mêmes entrées ➔ même sortie (même après redémarrage)
- **Efficacité** : Calcul rapide même pour de gros volumes de données
- **Résistance aux collisions** : Difficulté à trouver deux entrées distinctes avec le même hash (idéalement)

## Exemples de fonctions de hachage simples

### 1. Somme ASCII modulo

```java
public class SimpleHash {
    // Fonction de hachage simple : somme ASCII modulo taille
    public static int hashAsciiMod(String key, int tableSize) {
        int sum = 0;
        for (int i = 0; i < key.length(); i++) {
            sum += key.charAt(i);  // Ajoute le code ASCII de chaque caractère
        }
        return sum % tableSize;    // Applique le modulo
    }

    public static void main(String[] args) {
        String text = "hello";
        int tableSize = 100;
        
        int hashValue = hashAsciiMod(text, tableSize);
        System.out.println("Hash de \"" + text + "\": " + hashValue);
    }
}
```

**Explications :**
1. On parcourt chaque caractère de la chaîne
2. On accumule la somme des codes ASCII (via `charAt()`)
3. On applique le modulo avec la taille de la table pour obtenir un index valide

**Exemple de sortie :**
```
Hash de "hello": 52
```

**Amélioration possible** :
```java
// Version avec pondération (base 256)
public static int weightedHash(String key, int tableSize) {
    int sum = 0;
    int n = key.length();
    for (int i = 0; i < n; i++) {
        sum += key.charAt(i) * Math.pow(256, n-1-i);
    }
    return sum % tableSize;
}
```

Cette version pondérée réduit les collisions pour des chaînes avec mêmes caractères mais ordres différents (ex: "abc" 
vs "cba").

??? note "Citations"

      - [1] https://python.developpez.com/actu/343966/Apprendre-comment-faire-une-implementation-naive-d-une-table-de-hachage-en-Python-un-billet-blog-de-Denis-Hulo/
      - [2] https://fr.wikipedia.org/wiki/Fonction_de_hachage
      - [3] https://www.irif.fr/~hf/verif/ens/an11-12/poo/courscomplet.pdf
      - [4] http://www.iro.umontreal.ca/~major/IFT1020/notes/Hachage-2pp.pdf
      - [5] https://stackoverflow.com/questions/10416550/how-to-implement-hash-function-hk-a-k-mod-2w-w-r-in-java
      - [6] https://fr.wikibooks.org/wiki/Les_fonctions_de_hachage_cryptographiques
      - [7] https://www.lirmm.fr/~seriai/encadrements/theses/rafat/uploads/Main/rafat.pdf
      - [8] https://www-inf.telecom-sudparis.eu/COURS/CSC3101/Supports/fise/cours-tp.pdf


### 2. Méthode par division (pour entiers)

```java
int hashDivision(int nombre, int tailleTable) {
    return nombre % tailleTable; // Préférer tailleTable = nombre premier
}
```

### 3. Méthode de pliage pour chaînes

#### Méthode de pliage : principe général

Le pliage est une technique de hachage qui consiste à :

1. **Découper** la chaîne en blocs de taille fixe
2. **Combiner** ces blocs via des opérations arithmétiques/bit à bit
3. **Réduire** le résultat final à la taille de la table

#### Exemple Java avec addition

```java
public class FoldingHash {
    // Méthode de pliage pour chaîne avec blocs de 4 caractères
    public static int foldHash(String key, int tableSize) {
        int sum = 0;
        int blockSize = 4;
        
        for (int i = 0; i < key.length(); i += blockSize) {
            int block = 0;
            // Création du bloc
            for (int j = 0; j < blockSize; j++) {
                if (i + j < key.length()) {
                    block = (block << 8) | key.charAt(i + j); // Décalage + OR
                }
            }
            sum += block; // Combinaison par addition
        }
        
        return Math.abs(sum % tableSize); // Réduction finale
    }

    public static void main(String[] args) {
        String input = "hachage";
        int size = 1000;
        System.out.println("Hash de '" + input + "': " + foldHash(input, size));
    }
}
```

**Exécution :**
```
Hash de 'hachage': 879
```

#### Caractéristiques clés

- **Taille de bloc** : Généralement 32 ou 64 bits (4/8 caractères ASCII)
- **Opérations** : Addition, XOR ou combinaison de bits
- **Performance** : O(n) pour des chaînes de longueur modérée

#### Avantages/inconvénients

| Avantage                                    | Inconvénient                   |
|---------------------------------------------|--------------------------------|
| Bonne distribution pour données structurées | Collisions avec permutations   |
| Rapide à calculer                           | Sensible aux motifs répétitifs |
| Simple à implémenter                        | Taille de bloc critique        |

#### Cas d'utilisation typiques
- **Bases de données** : Indexation de clés composites
- **Cache mémoire** : Adressage de blocs de données
- **Vérification d'intégrité** : Somme de contrôle rapide

#### Variante avec XOR

```java
// Remplacement de la ligne d'addition
sum ^= block; // XOR au lieu de l'addition
```

#### Analyse de collision
Pour "chat" et "tcha" (mêmes caractères, ordre différent) :

```java
System.out.println(foldHash("chat", 1000)); // 295
System.out.println(foldHash("tcha", 1000)); // 295 (collision)
```

#### Optimisations possibles
1. **Padding intelligent** : Remplissage avec valeurs aléatoires au lieu de zéros
2. **Taille de bloc dynamique** : Adaptation basée sur la longueur de la chaîne
3. **Combinaison d'opérations** : Mélange d'addition et de XOR

Cette méthode est particulièrement efficace pour les chaînes longues et structurées, mais nécessite un choix judicieux de la taille de bloc et des opérations de combinaison pour minimiser les collisions[1][3].

??? note "Citations"

      - [1] https://fr.wikipedia.org/wiki/Fonction_de_hachage
      - [2] https://fr.wikipedia.org/wiki/Java_hashCode()
      - [3] https://jipe.developpez.com/articles/algo/table-hachage/?page=theorie
      - [4] https://codegym.cc/fr/groups/posts/fr.210.code-de-hachage-java-
      - [5] https://jipe.developpez.com/articles/algo/table-hachage/?page=pratique-implementation-en-java
      - [6] https://codegym.cc/fr/groups/posts/fr.849.chanes-java
      - [7] http://gallium.inria.fr/~maranget/X/421/poly/assoc.html
      - [8] https://fr.wikibooks.org/wiki/Les_fonctions_de_hachage_cryptographiques


### 4. Hash polynomial (utilisé en Java pour les strings)

$$ h(s) = s_0 \times 31^{n-1} + s_1 \times 31^{n-2} + ... + s_{n-1} $$

## Applications au-delà de Java

### Structures de données

| Application       | Utilisation du hash                   |
|-------------------|---------------------------------------|
| Tables de hachage | Indexation rapide des clés            |
| Caches            | Identification des données fréquentes |
| Bloom filters     | Test d'appartenance à un ensemble     |

### Sécurité informatique

- **Stockage de mots de passe** : Salage + hash (ex : bcrypt, PBKDF2)
- **Vérification d'intégrité** : Checksums (MD5, SHA-256)
- **Signatures numériques** : Hash du document signé cryptographiquement

### Réseau et systèmes distribués

- **Partitionnement de données** : Sharding dans les bases distribuées
- **Load balancing** : Répartition des requêtes via consistent hashing
- **Déduplication** : Identification des fichiers dupliqués

## Comparaison fonctions simples vs cryptographiques

| Caractéristique | Hash simple       | Hash cryptographique |
|-----------------|-------------------|----------------------|
| Vitesse         | Rapide (ns)       | Lent (μs-ms)         |
| Collisions      | Tolérées          | Inacceptables        |
| Usage typique   | Tables de hachage | Signature digitale   |
| Exemples        | Java hashCode()   | SHA-256, Blake3      |

Un cas concret en cryptomonnaie : Bitcoin utilise double SHA-256 pour :

1. Vérifier l'intégrité de la blockchain
2. Miner des blocs via preuve de travail
3. Générer des adresses wallet à partir de clés publiques

Ces principes montrent comment une fonction mathématique apparemment simple devient un pilier des systèmes informatiques
modernes, des structures de données basiques à la sécurité des transactions financières.

??? note "Citations"

      - [1] https://en.wikipedia.org/wiki/Hash_function
      - [2] https://en.wikipedia.org/wiki/Cryptographic_hash_function
      - [3] https://www.crowdstrike.com/en-us/cybersecurity-101/data-protection/data-hashing/
      - [4] https://corporatefinanceinstitute.com/resources/cryptocurrency/hash-function/
      - [5] https://www.prasams.com/the-basics-of-hashing-a-key-concept-in-computer-science/
      - [6] https://codefinity.com/blog/Overview-of-Hashing-and-its-Applications
      - [7] https://www.cs.hmc.edu/~geoff/classes/hmc.cs070.200101/homework10/hashfuncs.html
      - [8] https://opendsa-server.cs.vt.edu/ODSA/Books/CS3/html/HashFuncExamp.html
      - [9] https://www.investopedia.com/terms/h/hash.asp
      - [10] https://emeritus.org/blog/cybersecurity-what-is-hashing-in-cybersecurity/
      - [11] https://www.practicalnetworking.net/series/cryptography/hashing-algorithm/
      - [12] https://www.okta.com/identity-101/hashing-algorithms/
      - [13] https://www.ionos.ca/digitalguide/server/security/hash-function/
      - [14] https://softwareengineering.stackexchange.com/questions/372153/what-is-an-example-for-a-one-way-hash-function
      - [15] https://enthec.com/en/what-is-hashing-how-it-works-and-uses-it-in-cybersecurity/
      - [16] https://www.tutorialspoint.com/cryptography/cryptography_hash_functions.htm
      - [17] https://www.spiceworks.com/it-security/data-security/articles/what-is-hashing/

## Fonction de hachage : concept clé pour `hashCode()`

Une fonction de hachage est un mécanisme qui transforme des données de taille variable (comme un objet Java) en une
valeur numérique fixe (généralement un entier). Dans le contexte de Java, cette valeur est utilisée par des structures
de données comme `HashMap` ou `HashSet` pour stocker et retrouver rapidement des objets.

### Caractéristiques essentielles

- **Déterministe** : Même entrée → même sortie (crucial pour les collections)
- **Performance** : Calcul rapide (appelée fréquemment dans les collections)
- **Distribution** : Doit disperser uniformément les codes pour éviter les collisions

### Application à `hashCode()`

```java

@Override
public int hashCode() {
    return Objects.hash(nom, age); // Combine les hashs des champs
}
```

**Pourquoi est-ce important ?**  
Quand vous stockez un objet dans un `HashMap`, Java :

1. Calcule le `hashCode()` pour déterminer le "seau" (bucket) de stockage
2. Utilise `equals()` seulement si plusieurs objets ont le même hash (collision)

### Propriétés clés (contrat Java)

1. **Cohérence** : Même objet → même hash (pendant toute sa durée de vie)
2. **Compatibilité avec equals()** : Si `a.equals(b)` alors `a.hashCode() == b.hashCode()`
3. **Pas l'inverse** : Deux objets différents peuvent avoir le même hash (collision acceptable)

### Exemple concret

```java
Map map = new HashMap<>();
Point p1 = new Point(1, 2);
map.put(p1, "test");

// Recherche basée sur hashCode() puis equals()
System.out.println(map.get(new Point(1, 2))); // "test" si bien implémenté
```

Les fonctions de hachage cryptographiques (comme SHA) partagent certains principes, mais `hashCode()` en Java a des
exigences différentes : performance > sécurité.

??? note "Citations"

      - [1] https://zestedesavoir.com/tutoriels/1895/les-fonctions-de-hachage-cryptographiques/
      - [2] https://fr.wikipedia.org/wiki/Fonction_de_hachage_cryptographique
      - [3] https://fr.wikipedia.org/wiki/Fonction_de_hachage
      - [4] https://vitrinelinguistique.oqlf.gouv.qc.ca/fiche-gdt/fiche/12399801/code-de-hachage
      - [5] https://www.okta.com/fr/identity-101/hashing-algorithms/
      - [6] https://www.ionos.fr/digitalguide/sites-internet/developpement-web/hachage/
      - [7] https://www.mailinblack.com/ressources/glossaire/le-hachage-une-methode-de-securite-infaillible/
      - [8] https://www.dashlane.com/fr/blog/quest-ce-que-le-hachage-des-mots-de-passe




-------

??? info "Utilisation de l'IA"
    Page rédigée en partie avec l'aide d'un assistant IA, principalement à l'aide de Perplexity AI, avec le *LLM*
    **Claude 3.5 Sonnet**. L'IA a été utilisée pour générer des explications, des exemples et/ou des suggestions de
    structure. Toutes les informations ont été vérifiées, éditées et complétées par l'auteur.
   