<h1 id="relations-prisma">Relations en Prisma – Cours exhaustif</h1>

Dans Prisma, les **relations entre modèles** correspondent aux relations classiques des bases SQL : 1:1, 1\:N, N\:N. Elles se déclarent avec l’annotation `@relation`.

Chaque relation est définie par :

* Un champ de type **modèle**
* Une **clé étrangère** (`fields` / `references`)
* Des **modificateurs** pour le comportement (`onDelete`, `onUpdate`)

---

<h2 id="one-to-one">1. Relation One-to-One</h2>

**Définition** : Un enregistrement du modèle A est lié à **un seul** enregistrement du modèle B, et réciproquement.

### Exemple : `User` et `Profile`

#### Schéma Prisma

```prisma
model User {
  id      String   @id @default(cuid())
  email   String   @unique
  profile Profile?
}

model Profile {
  id     String  @id @default(cuid())
  bio    String
  user   User    @relation(fields: [userId], references: [id])
  userId String  @unique
}
```

#### Explication :

* `User` possède un champ `profile` (optionnel ici).
* `Profile` a une clé étrangère `userId` qui référence `User.id`.
* Le champ `userId` est `@unique` : un seul `Profile` par `User`.

#### Insertion (JS) :

```js
await prisma.user.create({
  data: {
    email: 'alice@test.com',
    profile: {
      create: {
        bio: 'Développeuse passionnée',
      },
    },
  },
})
```

#### Lecture avec jointure :

```js
const user = await prisma.user.findUnique({
  where: { email: 'alice@test.com' },
  include: { profile: true },
})
```

---

<h2 id="one-to-many">2. Relation One-to-Many</h2>

**Définition** : Un enregistrement du modèle A peut être lié à **plusieurs** enregistrements du modèle B.

### Exemple : `User` et `Post`

#### Schéma Prisma

```prisma
model User {
  id    String @id @default(cuid())
  email String @unique
  posts Post[]       // <- plusieurs posts
}

model Post {
  id       String @id @default(cuid())
  title    String
  author   User   @relation(fields: [authorId], references: [id])
  authorId String
}
```

#### Explication :

* Un `User` peut avoir plusieurs `Post[]`.
* Chaque `Post` a un champ `authorId` qui pointe vers `User.id`.

#### Insertion (JS) :

```js
await prisma.user.create({
  data: {
    email: 'bob@example.com',
    posts: {
      create: [
        { title: 'Article 1' },
        { title: 'Article 2' },
      ],
    },
  },
})
```

#### Lecture avec jointure :

```js
const userWithPosts = await prisma.user.findUnique({
  where: { email: 'bob@example.com' },
  include: { posts: true },
})
```

---

<h2 id="many-to-many">3. Relation Many-to-Many</h2>

**Définition** : Plusieurs enregistrements du modèle A peuvent être liés à plusieurs enregistrements du modèle B.

### Exemple : `Student` et `Course`

#### Schéma Prisma

```prisma
model Student {
  id      String   @id @default(cuid())
  name    String
  courses Course[] @relation("Enrollment")
}

model Course {
  id       String    @id @default(cuid())
  title    String
  students Student[] @relation("Enrollment")
}
```

#### Explication :

* Prisma gère **automatiquement la table de liaison**.
* La relation est symétrique : chaque `Student` peut suivre plusieurs `Course` et inversement.

#### Insertion (JS) :

```js
await prisma.student.create({
  data: {
    name: 'Jean',
    courses: {
      create: [
        { title: 'Mathématiques' },
        { title: 'Physique' },
      ],
    },
  },
})
```

Autre variante : lier à un cours déjà existant

```js
await prisma.student.update({
  where: { id: 'student123' },
  data: {
    courses: {
      connect: { id: 'course456' },
    },
  },
})
```

#### Lecture avec jointure :

```js
const student = await prisma.student.findUnique({
  where: { id: 'student123' },
  include: { courses: true },
})
```

---

<h2 id="complements">4. Comportements relationnels (`onDelete`, `onUpdate`)</h2>

Vous pouvez ajouter :

```prisma
@relation(fields: [userId], references: [id], onDelete: Cascade)
```

* `Cascade` : suppression en cascade
* `Restrict` : empêche la suppression s’il y a des dépendances
* `SetNull` : met le champ à `NULL`

Exemple :

```prisma
user   User @relation(fields: [userId], references: [id], onDelete: Cascade)
```

---

<h2 id="nullability">5. Optionnalité et cardinalité</h2>

| Déclaration        | Signification                          |
| ------------------ | -------------------------------------- |
| `profile Profile?` | Relation optionnelle (`null` possible) |
| `posts Post[]`     | Liste (possiblement vide)              |
| `user User`        | Relation obligatoire                   |

---

<h1 id="conclusion">Conclusion</h1>

* **One-to-One** : clé étrangère unique dans le modèle lié
* **One-to-Many** : champ tableau côté "un", clé étrangère côté "many"
* **Many-to-Many** : tableau des deux côtés, Prisma crée une table de liaison
* Les requêtes Prisma sont explicites et typées, facilitant l’usage des relations
* Prisma simplifie la navigation entre entités liées avec `include`, `select`, `connect`, `create`, etc.



<br/>

# Annexe 1 - ?


### <h2 id="definition">Définition de `Profile?`</h2>

```prisma
model User {
  id      String   @id @default(cuid())
  email   String   @unique
  profile Profile?
}
```

* `Profile?` signifie que **le champ `profile` peut être nul (null)**.
* Autrement dit, **un utilisateur peut ne pas avoir de profil associé**.
* Prisma interprète cela comme une **relation optionnelle** en base de données (clé étrangère facultative ou inverse non obligatoire).

---

### <h2 id="comparaison">Comparaison avec `Profile` (sans `?`)</h2>

| Syntaxe dans Prisma | Interprétation                                                                 |
| ------------------- | ------------------------------------------------------------------------------ |
| `profile Profile?`  | **Relation optionnelle** : un utilisateur peut avoir ou non un profil          |
| `profile Profile`   | **Relation obligatoire** : un utilisateur doit obligatoirement avoir un profil |

Dans les deux cas, cela affecte :

* Les **contraintes de base de données** (NOT NULL ou non)
* Le comportement des requêtes Prisma (champ nullable ou non dans le type TypeScript)

---

### <h2 id="exemple-optionnel">Exemple : relation One-to-One optionnelle</h2>

```prisma
model User {
  id      String   @id @default(cuid())
  email   String   @unique
  profile Profile?          // un utilisateur peut ne pas avoir de profil
}

model Profile {
  id     String @id @default(cuid())
  bio    String
  user   User   @relation(fields: [userId], references: [id])
  userId String @unique
}
```

### Cas concrets :

* Utilisateur sans profil :

```js
await prisma.user.create({
  data: { email: 'no-profile@test.com' }
})
```

* Utilisateur avec profil :

```js
await prisma.user.create({
  data: {
    email: 'with-profile@test.com',
    profile: {
      create: {
        bio: 'Développeuse passionnée'
      }
    }
  }
})
```

---

### <h2 id="remarques">Remarques importantes</h2>

* L’optionnalité est toujours côté **champ relationnel**, pas nécessairement côté clé étrangère.
* `Profile?` signifie que le champ `profile` **peut être omis** ou `null` dans les requêtes `findUnique()`, `include`, etc.


