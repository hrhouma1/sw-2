<h1 id="introduction">1. Introduction à Prisma</h1>

**Prisma** est un ORM (Object Relational Mapper) moderne pour Node.js qui facilite la manipulation de bases de données relationnelles à travers du code JavaScript ou TypeScript. Il offre :

* Une syntaxe déclarative via un fichier `schema.prisma`
* Un générateur de client automatique (`prisma generate`)
* Une gestion des migrations (`prisma migrate`)
* Une documentation claire et un typage fort (TS)

Prisma prend en charge plusieurs SGBD :

* PostgreSQL
* MySQL
* SQLite
* SQL Server
* MongoDB (support limité, en preview)



<h1 id="installation">2. Installation et configuration</h1>

<h2 id="2.1-creer-un-projet-nodejs">2.1 Créer un projet Node.js</h2>

```bash
mkdir mon-projet-prisma
cd mon-projet-prisma
npm init -y
```

<h2 id="2.2-installer-prisma-et-initialiser">2.2 Installer Prisma et initialiser le schéma</h2>

```bash
npm install prisma --save-dev
npx prisma init
```

Cela crée :

* un dossier `prisma/` contenant `schema.prisma`
* un fichier `.env` pour la variable `DATABASE_URL`

<h2 id="2.3-installer-le-client">2.3 Installer le client Prisma</h2>

```bash
npm install @prisma/client
```

---

<h1 id="configuration">3. Configuration du fichier `schema.prisma`</h1>

Exemple de configuration PostgreSQL :

```prisma
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}
```

Dans `.env` :

```env
DATABASE_URL="postgresql://user:password@host:port/database?sslmode=require"
```

---

<h1 id="modelisation">4. Définir les modèles</h1>

Exemple de deux modèles liés `User` et `Post` :

```prisma
model User {
  id    String  @id @default(cuid())
  email String  @unique
  name  String?

  posts Post[]
}

model Post {
  id        String   @id @default(cuid())
  title     String
  content   String
  published Boolean  @default(false)

  authorId  String
  author    User     @relation(fields: [authorId], references: [id])
}
```

---

<h1 id="migrations">5. Gérer les migrations</h1>

Prisma permet de synchroniser les modèles Prisma avec la base via un système de migrations.

```bash
npx prisma migrate dev --name init
```

* Applique la migration
* Crée un fichier SQL dans `prisma/migrations/`
* Met à jour la base
* Génère le client



<h1 id="generate-client">6. Générer le client Prisma</h1>

Le client est généré automatiquement lors des migrations, mais peut être régénéré à tout moment :

```bash
npx prisma generate
```



<h1 id="utilisation-client">7. Utilisation du client Prisma dans le code</h1>

```js
const { PrismaClient } = require('@prisma/client')
const prisma = new PrismaClient()

async function main() {
  const user = await prisma.user.create({
    data: {
      email: 'alice@exemple.com',
      name: 'Alice',
      posts: {
        create: {
          title: 'Premier post',
          content: 'Contenu ici...',
        },
      },
    },
  })

  const posts = await prisma.post.findMany({
    where: { published: false },
  })

  console.log(posts)
}

main().catch(console.error).finally(() => prisma.$disconnect())
```



<h1 id="requêtes-crud">8. Requêtes CRUD avec Prisma Client</h1>

| Opération     | Exemple                                     |
| ------------- | ------------------------------------------- |
| Créer         | `prisma.user.create({ data: { ... } })`     |
| Lire          | `prisma.user.findMany()`                    |
| Lire unique   | `prisma.user.findUnique({ where: { id } })` |
| Mettre à jour | `prisma.user.update({ where, data })`       |
| Supprimer     | `prisma.user.delete({ where: { id } })`     |



<h1 id="relations">9. Relations entre modèles</h1>

<h2 id="9.1-one-to-many">9.1 Relation One-to-Many</h2>

Un utilisateur possède plusieurs articles :

```prisma
model User {
  id    String  @id @default(cuid())
  posts Post[]
}

model Post {
  id       String @id @default(cuid())
  author   User   @relation(fields: [authorId], references: [id])
  authorId String
}
```


<h2 id="9.2-many-to-many">9.2 Relation Many-to-Many</h2>

```prisma
model Student {
  id      String    @id @default(cuid())
  courses Course[]  @relation("Enrollment")
}

model Course {
  id       String     @id @default(cuid())
  students Student[]  @relation("Enrollment")
}
```

Prisma gère la table intermédiaire automatiquement.



<h1 id="relation-avancees">10. Requêtes relationnelles avancées</h1>

```js
const posts = await prisma.user.findUnique({
  where: { email: 'alice@exemple.com' },
  include: { posts: true }
})
```

Inclure les relations inverses :

```js
const post = await prisma.post.findMany({
  include: { author: true }
})
```


<h1 id="seed-et-reset">11. Rechargement et seed</h1>

Créer un fichier `prisma/seed.js` :

```js
const { PrismaClient } = require('@prisma/client')
const prisma = new PrismaClient()

async function main() {
  await prisma.user.create({
    data: {
      email: 'test@test.com',
      name: 'Testeur',
    },
  })
}

main().catch(console.error).finally(() => prisma.$disconnect())
```

Dans `package.json` :

```json
"prisma": {
  "seed": "node prisma/seed.js"
}
```

Lancer :

```bash
npx prisma db seed
```



<h1 id="visualisation">12. Prisma Studio (GUI)</h1>

```bash
npx prisma studio
```

Lance une interface graphique web pour visualiser les données.


<h1 id="bonnes-pratiques">13. Bonnes pratiques</h1>

* Toujours versionner les fichiers de migration
* Utiliser les types générés pour éviter les erreurs de typage
* Valider les entrées côté application (Prisma ne valide pas les emails, etc.)
* Ne jamais exposer Prisma Client directement à l'extérieur (via des API publiques)
* Regénérer le client après chaque modification du schéma

