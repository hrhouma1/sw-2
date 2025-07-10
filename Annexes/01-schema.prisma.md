#  Partie 1 : Expliquez le code suivant

```ts
// This is your Prisma schema file,
// learn more about it in the docs: https://pris.ly/d/prisma-schema

// Looking for ways to speed up your queries, or scale easily with your serverless or edge functions?
// Try Prisma Accelerate: https://pris.ly/cli/accelerate-init
// C'est un commentaire indiquant que ce fichier est le **fichier de schéma Prisma**, utilisé pour définir les modèles de données. Il donne aussi un lien vers la documentation officielle pour apprendre davantage.


generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model Article {
  id        String   @id @default(cuid())
  title     String
  content   String
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt

  @@map("articles")
}
```




## Partie 2 : Générateur de client Prisma

```ts
generator client {
  provider = "prisma-client-js"
}
```

* `generator` indique à Prisma quel **type de client** générer après la commande `npx prisma generate`.
* `provider = "prisma-client-js"` signifie que Prisma va générer un **client JavaScript/TypeScript** pour interagir avec la base de données.
* Le client généré sera utilisé dans votre code avec des appels comme `prisma.article.findMany()`.



## 🔌 Partie 3 : Connexion à la base de données (datasource)

```ts
datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}
```

* `datasource` définit la **source de données** (la base de données).
* `provider = "postgresql"` indique que la base utilisée est **PostgreSQL**.
* `url = env("DATABASE_URL")` : Prisma lira l’URL de connexion dans un fichier `.env`, par exemple :

```env
DATABASE_URL="postgresql://user:password@host:port/dbname?sslmode=require"
```

> **Important** : si la variable `DATABASE_URL` est absente, une erreur comme `P1012` s’affiche lors de la compilation du schéma.



# Partie 4 : Définition du modèle `Article`

```ts
model Article {
  id        String   @id @default(cuid())
  title     String
  content   String
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt

  @@map("articles")
}
```

Ce bloc décrit un modèle de données `Article`. Prisma générera une table SQL correspondante dans PostgreSQL. Voici les champs :

| Champ       | Type       | Description                                                                                             |
| ----------- | ---------- | ------------------------------------------------------------------------------------------------------- |
| `id`        | `String`   | Identifiant unique (clé primaire). Généré automatiquement par `cuid()` — un identifiant unique lisible. |
| `title`     | `String`   | Le titre de l’article.                                                                                  |
| `content`   | `String`   | Le contenu de l’article.                                                                                |
| `createdAt` | `DateTime` | La date de création, automatiquement définie avec `now()` (date/heure actuelle).                        |
| `updatedAt` | `DateTime` | Mise à jour automatique à chaque modification grâce à `@updatedAt`.                                     |

###  Lignes spéciales

* `@id` : indique que `id` est la **clé primaire**.
* `@default(cuid())` : Prisma génère une valeur unique avec l’algorithme **cuid**.
* `@default(now())` : date par défaut à **l’insertion**.
* `@updatedAt` : Prisma met automatiquement ce champ à jour à chaque **modification** du modèle.
* `@@map("articles")` : **renomme** la table SQL en `"articles"` au lieu de `"Article"` (par défaut Prisma utilise des noms en PascalCase).



# Résumé visuel

```ts
┌────────────┐
│ Article    │  ← modèle Prisma
├────────────┤
│ id         │  ← String, cuid() unique, clé primaire
│ title      │  ← String
│ content    │  ← String
│ createdAt  │  ← DateTime, par défaut = maintenant
│ updatedAt  │  ← DateTime, MAJ automatique
└────────────┘
```



# Utilisation typique dans le code

```ts
import { PrismaClient } from '@prisma/client'

const prisma = new PrismaClient()

// Créer un nouvel article
await prisma.article.create({
  data: {
    title: 'Mon premier article',
    content: 'Ceci est le contenu.',
  },
})

// Récupérer tous les articles
const articles = await prisma.article.findMany()
```


