# BookManager

Application de gestion de livres construite avec Spring Boot et Kotlin.

## Architecture

Le projet suit une architecture hexagonale (ports et adaptateurs) avec les couches suivantes :
- **Domain** : logique métier et modèles
- **Application** : use cases
- **Infrastructure** : adaptateurs (base de données, API REST)

## Prérequis

- Java 21 (OpenJDK Temurin)
- Docker (pour les tests d'intégration)

## Lancer l'application

```bash
./gradlew bootRun
```

L'application démarre sur `http://localhost:8080`.

## Tests

### Tests unitaires
```bash
./gradlew test
```

### Tests d'intégration (PostgreSQL)
```bash
./gradlew testIntegration
```

### Tests de composants (Cucumber/BDD)
```bash
./gradlew testComponent
```

### Tous les tests
```bash
./gradlew check
```

## API REST

### Créer un livre
```bash
POST /books
Content-Type: application/json

{
  "name": "Hamlet",
  "author": "William Shakespeare"
}
```
**Réponse** : 201 Created

### Récupérer tous les livres
```bash
GET /books
```
**Réponse** : 200 OK
```json
[
  {
    "name": "Hamlet",
    "author": "William Shakespeare",
    "reserved": false
  }
]
```

### Réserver un livre
```bash
POST /books/{name}/reserve
```
**Réponse** : 200 OK (succès) ou 409 Conflict (déjà réservé)

## Validation

- Le nom du livre ne peut pas être vide
- L'auteur ne peut pas être vide
- Un livre ne peut être réservé que s'il n'est pas déjà réservé

## Stack technique

- **Framework** : Spring Boot 3.1.3
- **Langage** : Kotlin 2.0.21
- **Test** : Kotest, Mockk, Cucumber, TestContainers
- **Base de données** : PostgreSQL (Liquibase pour les migrations)
- **Build** : Gradle 8.13

## Couverture de code

Utilise JaCoCo pour mesurer la couverture des tests.

```bash
./gradlew jacocoTestReport
```

Rapport généré : `build/reports/jacoco/test/html/index.html`
