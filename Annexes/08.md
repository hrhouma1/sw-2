### **Quiz Prisma – Relations entre Modèles (Avec Code)**

---

#### **1. Quelle annotation est utilisée pour déclarer une relation dans Prisma ?**

* A. `@connect`
* B. `@relation`
* C. `@foreignKey`
* D. `@join`

**Réponse : B. `@relation`**
→ C’est l’annotation utilisée pour établir des relations entre deux modèles.

```prisma
model Post {
  id       String @id @default(cuid())
  author   User   @relation(fields: [authorId], references: [id])
  authorId String
}
```

---

#### **2. Quel mot-clé rend une relation optionnelle ?**

* A. `nullable`
* B. `optional`
* C. `?`
* D. `@optional`

**Réponse : C. `?`**
→ Le point d’interrogation rend un champ relationnel facultatif.

```prisma
model User {
  profile Profile?
}
```

---

#### **3. Dans une relation One-to-One, que faut-il ajouter sur la clé étrangère pour assurer l’unicité ?**

* A. `@id`
* B. `@default`
* C. `@unique`
* D. `@nullable`

**Réponse : C. `@unique`**
→ Cela garantit qu’un seul profil correspond à un utilisateur.

```prisma
model Profile {
  userId String @unique
  user   User   @relation(fields: [userId], references: [id])
}
```

---

#### **4. Quel type de relation correspond à `Post[]` dans un modèle `User` ?**

* A. One-to-One
* B. One-to-Many
* C. Many-to-One
* D. Many-to-Many

**Réponse : B. One-to-Many**

```prisma
model User {
  posts Post[]  // un utilisateur peut avoir plusieurs posts
}
```

---

#### **5. Quelle annotation Prisma permet de renommer une table de liaison automatique ?**

* A. `@@map`
* B. `@@link`
* C. `@@relation`
* D. `@pivot`

**Réponse : A. `@@map`**

```prisma
model UserCourse {
  @@map("user_course_link")
}
```

---

#### **6. Dans une relation Many-to-Many, combien de champs sont nécessaires dans `schema.prisma` ?**

* A. Un seul
* B. Deux champs tableau
* C. Un champ avec `@relation`
* D. Aucun champ

**Réponse : B. Deux champs tableau**

```prisma
model Student {
  courses Course[]
}

model Course {
  students Student[]
}
```

---

#### **7. Quel comportement empêche la suppression d’un parent s’il est référencé ?**

* A. `onDelete: Cascade`
* B. `onDelete: Restrict`
* C. `onDelete: SetNull`
* D. `onDelete: Deny`

**Réponse : B. `onDelete: Restrict`**

```prisma
user User @relation(fields: [userId], references: [id], onDelete: Restrict)
```

---

#### **8. Que signifie `@relation(fields: [authorId], references: [id])` ?**

* C. `authorId` est une clé étrangère vers `id` du modèle `User`.

```prisma
author   User   @relation(fields: [authorId], references: [id])
authorId String
```

---

#### **9. Quelle structure permet d’avoir plusieurs commentaires associés à un article ?**

* C. `comments: Comment[]`

```prisma
model Article {
  comments Comment[]
}
```

---

#### **10. Dans une relation `User` – `Profile`, où place-t-on la clé étrangère ?**

* B. Dans `Profile`

```prisma
model Profile {
  userId String @unique
  user   User   @relation(fields: [userId], references: [id])
}
```

---

#### **11. Quel modificateur permet d’automatiser la suppression liée ?**

* C. `onDelete: Cascade`

```prisma
@relation(fields: [userId], references: [id], onDelete: Cascade)
```

---

#### **12. Quelle déclaration décrit une relation One-to-One optionnelle ?**

* C. `profile Profile?`

```prisma
model User {
  profile Profile?
}
```

---

#### **13. Dans une relation One-to-Many, quel champ est généralement `@relation` ?**

* B. La clé étrangère

```prisma
model Post {
  authorId String
  author   User @relation(fields: [authorId], references: [id])
}
```

---

#### **14. Quelle relation implique une table intermédiaire générée automatiquement ?**

* C. Many-to-Many

```prisma
model Student {
  courses Course[]
}

model Course {
  students Student[]
}
```

---

#### **15. Peut-on avoir plusieurs relations entre deux mêmes modèles ?**

* B. Oui, avec des noms différents

```prisma
model Post {
  author User @relation("Author")
  editor User @relation("Editor")
}
```

---

#### **16. Quelle commande permet d’inclure une relation dans une requête Prisma ?**

* B. `include`

```js
await prisma.user.findUnique({
  where: { id },
  include: { profile: true },
})
```

---

#### **17. Que signifie `students Course[]` dans un modèle `Course` ?**

* C. Un cours peut avoir plusieurs étudiants

```prisma
model Course {
  students Student[]
}
```

---

#### **18. Quel type de relation est défini par une clé étrangère avec `@unique` ?**

* C. One-to-One

---

#### **19. Quelle est la différence entre `Profile` et `Profile?` dans un modèle ?**

* B. `Profile?` rend la relation facultative

---

#### **20. Où écrit-on `@relation("Nom")` lorsqu’on a plusieurs relations entre deux modèles ?**

* C. Dans les deux modèles concernés

```prisma
author User @relation("Author")
editor User @relation("Editor")
```

---

#### **21. Quelle relation nécessite d’ajouter une contrainte `@unique` sur la clé étrangère ?**

* C. One-to-One

---

#### **22. Quelle annotation peut être combinée avec `@relation` ?**

* D. `@unique`

---

#### **23. Quelle commande permet de visualiser les relations dans Prisma ?**

* A. `npx prisma studio`

---

#### **24. Une relation Many-to-Many peut être modélisée manuellement avec…**

* C. Un modèle pivot avec deux clés étrangères

```prisma
model Enrollment {
  studentId String
  courseId  String

  student Student @relation(fields: [studentId], references: [id])
  course  Course  @relation(fields: [courseId], references: [id])

  @@id([studentId, courseId])
}
```

---

#### **25. Dans Prisma, une relation est toujours…**

* A. Réversible

---

#### **26. Quel champ faut-il ajouter dans un modèle pour représenter une relation inverse ?**

* A. Un tableau ou un champ du modèle lié

---

#### **27. Que faut-il faire pour que Prisma crée une table de liaison automatiquement ?**

* B. Ne rien faire, juste deux tableaux

---

#### **28. Peut-on combiner `onDelete` avec `@relation` ?**

* B. Oui

---

#### **29. Quelle syntaxe connecte un modèle existant à une relation ?**

* C. `connect`

```js
await prisma.post.create({
  data: {
    title: 'Nouvel article',
    author: {
      connect: { id: 'user123' },
    },
  },
})
```

---

#### **30. Comment écrire une relation One-to-One obligatoire ?**

* B. `profile Profile`

