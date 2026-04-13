---
icon: material/file-document-outline
---

# 6. **Exercice : Comprendre les contrats d’interface et les méthodes par défaut**

## **Objectifs**

- Comprendre le rôle d’une interface comme **contrat** en Java.
- Savoir utiliser les **méthodes par défaut** pour factoriser du code dans une interface.
- Implémenter plusieurs classes respectant le même contrat.

---

## **Consignes**

1. **Définir une interface `Logger`** :
    Créez une interface `Logger` qui déclare les méthodes suivantes :

    - `void log(String message)` : Méthode abstraite pour enregistrer un message.
    - **Méthode par défaut** : `void logWithTimestamp(String message)`  
      Cette méthode doit ajouter un *timestamp* (heure actuelle) au message avant de l’enregistrer, puis appeler
      `log(String message)`.  
      *Indice* : Utilisez `java.time.LocalDateTime.now()` pour obtenir l’heure actuelle.

2. **Implémenter deux classes concrètes** :
    Créez deux classes qui implémentent `Logger` :

    - `ConsoleLogger` : Affiche les messages dans la console (utilisez `System.out.println`).
    - `FileLogger` : Enregistre les messages dans un fichier nommé `log.txt`.  
      *Indice* : Utilisez `java.io.FileWriter` pour écrire dans un fichier.

3. **Tester les implémentations** :
    Dans une classe `Main`, créez des instances de `ConsoleLogger` et `FileLogger`, puis appelez :

    - `log("Test sans timestamp")`
    - `logWithTimestamp("Test avec timestamp")`
     
    Vérifiez que les messages s’affichent correctement dans la console et dans le fichier.

---

## **Questions de réflexion**

1. Pourquoi dit-on qu’une interface définit un **contrat** ? En quoi cela diffère-t-il d’une classe abstraite ?
2. Quel est l’avantage d’utiliser une méthode par défaut dans `Logger` plutôt que de redéfinir `logWithTimestamp` dans
   chaque classe ?
3. Si vous ajoutiez une nouvelle méthode abstraite à `Logger`, que devriez-vous faire pour que le code continue de
   compiler ?

