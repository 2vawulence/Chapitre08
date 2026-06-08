# BookShelf

## Description

BookShelf est un projet Java qui implémente une bibliothèque de livres en utilisant les principes de la programmation orientée objet (POO) et les fonctionnalités modernes de Java telles que les Streams, les Collections et les Expressions Lambda.

Le projet permet :

* d'ajouter des livres dans une bibliothèque ;
* de consulter la liste des livres ;
* de trier les livres selon différents critères ;
* de regrouper les livres selon leur année de publication ;
* de regrouper les livres selon un critère fourni par l'utilisateur.

Les tests unitaires sont réalisés avec **JUnit 5** et **AssertJ**.

---

## Structure du projet

### Classe Book

Représente un livre avec les informations suivantes :

* Titre
* Auteur
* Date de publication

Exemple :

```java
Book effectiveJava = new Book(
    "Effective Java",
    "Joshua Bloch",
    LocalDate.of(2008, Month.MAY, 8)
);
```

---

### Classe BookShelf

Représente une bibliothèque contenant plusieurs livres.

#### Ajouter des livres

```java
shelf.add(book1, book2, book3);
```

#### Consulter les livres

```java
List<Book> books = shelf.books();
```

La liste retournée est immuable afin d'empêcher les modifications externes.

---

## Fonctionnalités

### 1. Bibliothèque vide

Une nouvelle bibliothèque ne contient aucun livre.

```java
BookShelf shelf = new BookShelf();
assertTrue(shelf.books().isEmpty());
```

---

### 2. Ajout de livres

```java
shelf.add(effectiveJava, codeComplete);
```

Permet d'ajouter un ou plusieurs livres.

---

### 3. Tri des livres

#### Tri par défaut (titre)

```java
List<Book> books = shelf.arrange();
```

Les livres sont triés par ordre alphabétique du titre.

Exemple :

```
Code Complete
Effective Java
The Mythical Man-Month
```

---

#### Tri personnalisé

```java
List<Book> books =
    shelf.arrange(Comparator.<Book>naturalOrder().reversed());
```

Permet de fournir n'importe quel Comparator.

---

### 4. Regroupement par année de publication

```java
Map<Year, List<Book>> booksByYear =
    shelf.groupByPublicationYear();
```

Exemple :

```text
2008 -> [Effective Java, Clean Code]
2004 -> [Code Complete]
1975 -> [The Mythical Man-Month]
```

---

### 5. Regroupement selon un critère utilisateur

La méthode générique :

```java
public <K> Map<K, List<Book>> groupBy(Function<Book, K> fx)
```

permet de regrouper les livres selon n'importe quelle propriété.

#### Regroupement par auteur

```java
Map<String, List<Book>> booksByAuthor =
    shelf.groupBy(Book::getAuthor);
```

Résultat :

```text
Joshua Bloch -> [Effective Java]
Steve McConnel -> [Code Complete]
Robert C. Martin -> [Clean Code]
Frederick Phillips Brooks -> [The Mythical Man-Month]
```

---

## Technologies utilisées

* Java 8+
* JUnit 5
* AssertJ
* Java Streams API
* Collections Framework

---

## Tests

Les tests vérifient :

* qu'une bibliothèque vide ne contient aucun livre ;
* que l'ajout de livres fonctionne correctement ;
* que la collection retournée est immuable ;
* que les livres peuvent être triés ;
* que les livres peuvent être regroupés par année ;
* que les livres peuvent être regroupés selon un critère fourni par l'utilisateur.

Exécution des tests :

```bash
mvn test
```

ou

```bash
gradle test
```

selon votre système de build.

---

## Exemple complet

```java
BookShelf shelf = new BookShelf();

shelf.add(
    new Book("Effective Java", "Joshua Bloch",
             LocalDate.of(2008, 5, 8)),
    new Book("Clean Code", "Robert C. Martin",
             LocalDate.of(2008, 8, 1))
);

Map<Year, List<Book>> books =
        shelf.groupByPublicationYear();

System.out.println(books);
```

---

## Auteur

Projet pédagogique destiné à l'apprentissage de :

* la programmation orientée objet en Java ;
* les Collections Java ;
* les Streams ;
* les Génériques ;
* les Expressions Lambda ;
* les Tests Unitaires avec JUnit 5.
se code a ete fait dans le but de pouvoir comprendre les test avec junits



