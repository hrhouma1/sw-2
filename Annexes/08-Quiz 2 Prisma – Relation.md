### **Quiz Prisma – Relations entre Modèles**

---

#### **1. Quelle annotation est utilisée pour déclarer une relation dans Prisma ?**

* A. `@connect`
* B. `@relation`
* C. `@foreignKey`
* D. `@join`

**1. B. `@relation`**
→ Prisma utilise l’annotation `@relation` pour établir des relations entre deux modèles, souvent accompagnée de `fields` et `references`.

---

#### **2. Quel mot-clé rend une relation optionnelle ?**

* A. `nullable`
* B. `optional`
* C. `?`
* D. `@optional`

**2. C. `?`**
→ Un `?` après un type de modèle (`Profile?`) indique que la relation est optionnelle.

---

#### **3. Dans une relation One-to-One, que faut-il ajouter sur la clé étrangère pour assurer l’unicité ?**

* A. `@id`
* B. `@default`
* C. `@unique`
* D. `@nullable`

**3. C. `@unique`**
→ Pour garantir une relation 1:1, il faut rendre la clé étrangère unique.

---

#### **4. Quel type de relation correspond à `Post[]` dans un modèle `User` ?**

* A. One-to-One
* B. One-to-Many
* C. Many-to-One
* D. Many-to-Many

**4. B. One-to-Many**
→ Un tableau signifie que l’utilisateur a plusieurs posts (1 utilisateur ↔ N posts).

---

#### **5. Quelle annotation Prisma permet de renommer une table de liaison automatique ?**

* A. `@@map`
* B. `@@link`
* C. `@@relation`
* D. `@pivot`

**5. A. `@@map`**
→ `@@map("nom_table")` permet de renommer une table ou une table de liaison.

---

#### **6. Dans une relation Many-to-Many, combien de champs sont nécessaires dans `schema.prisma` ?**

* A. Un seul
* B. Deux champs tableau
* C. Un champ avec `@relation`
* D. Aucun champ

**6. B. Deux champs tableau**
→ Prisma crée la table intermédiaire automatiquement quand deux modèles se réfèrent mutuellement avec des tableaux.

---

#### **7. Quel comportement empêche la suppression d’un parent s’il est référencé ?**

* A. `onDelete: Cascade`
* B. `onDelete: Restrict`
* C. `onDelete: SetNull`
* D. `onDelete: Deny`

**7. B. `onDelete: Restrict`**
→ La suppression est bloquée tant que des enregistrements liés existent.

---

#### **8. Que signifie `@relation(fields: [authorId], references: [id])` ?**

* A. Aucune relation
* B. Le champ `authorId` est une clé primaire
* C. `authorId` est une clé étrangère vers `id`
* D. `authorId` est ignoré par Prisma

**8. C. `authorId` est une clé étrangère vers `id`**
→ Prisma relie les champs spécifiés via cette annotation.

---

#### **9. Quelle structure permet d’avoir plusieurs commentaires associés à un article ?**

* A. `comment: Comment`
* B. `comment: Comment?`
* C. `comments: Comment[]`
* D. `comments: Comment`

**9. C. `comments: Comment[]`**
→ Le tableau représente plusieurs commentaires (relation 1\:N).

---

#### **10. Dans une relation `User` – `Profile`, où place-t-on la clé étrangère ?**

* A. Dans `User`
* B. Dans `Profile`
* C. Dans les deux
* D. Dans un fichier séparé

**10. B. Dans `Profile`**
→ `Profile` contient un champ `userId` qui référence `User.id`.

---

#### **11. Quel modificateur permet d’automatiser la suppression liée ?**

* A. `@cascade`
* B. `@delete`
* C. `onDelete: Cascade`
* D. `onDelete: Remove`

**11. C. `onDelete: Cascade`**
→ Les enregistrements dépendants sont supprimés automatiquement.

---

#### **12. Quelle déclaration décrit une relation One-to-One optionnelle ?**

* A. `profile Profile`
* B. `profile Profile[]`
* C. `profile Profile?`
* D. `profile: string`

**12. C. `profile Profile?`**
→ Le `?` rend la relation optionnelle.

---

#### **13. Dans une relation One-to-Many, quel champ est généralement `@relation` ?**

* A. Le tableau
* B. La clé étrangère
* C. Les deux
* D. Aucun

**13. B. La clé étrangère**
→ Le champ contenant `@relation(...)` est du côté "many".

---

#### **14. Quelle relation implique une table intermédiaire générée automatiquement ?**

* A. One-to-One
* B. One-to-Many
* C. Many-to-Many
* D. Aucun

**14. C. Many-to-Many**
→ Prisma gère une table de liaison automatiquement.

---

#### **15. Peut-on avoir plusieurs relations entre deux mêmes modèles ?**

* A. Non
* B. Oui, avec des noms différents
* C. Oui, sans contrainte
* D. Seulement avec PostgreSQL

**15. B. Oui, avec des noms différents**
→ Il faut nommer la relation avec `@relation("Nom")`.

---

#### **16. Quelle commande permet d’inclure une relation dans une requête Prisma ?**

* A. `expand`
* B. `include`
* C. `with`
* D. `load`

**16. B. `include`**
→ Permet de charger les entités liées.

---

#### **17. Que signifie `students Course[]` dans un modèle `Course` ?**

* A. Un cours contient un seul étudiant
* B. Plusieurs cours par étudiant
* C. Un cours peut avoir plusieurs étudiants
* D. Le champ est une clé étrangère

**17. C. Un cours peut avoir plusieurs étudiants**
→ Représente le côté inverse d’une relation N\:N.

---

#### **18. Quel type de relation est défini par une clé étrangère avec `@unique` ?**

* A. One-to-Many
* B. Many-to-One
* C. One-to-One
* D. Many-to-Many

**18. C. One-to-One**
→ Le `@unique` garantit qu’un seul enregistrement correspond à la relation.

---

#### **19. Quelle est la différence entre `Profile` et `Profile?` dans un modèle ?**

* A. Aucun effet
* B. `Profile?` rend la relation facultative
* C. `Profile` est pour les tableaux
* D. `Profile` est privé

**19. B. `Profile?` rend la relation facultative**
→ Cela autorise `null` dans la base.

---

#### **20. Où écrit-on `@relation("Nom")` lorsqu’on a plusieurs relations entre deux modèles ?**

* A. Dans le fichier `.env`
* B. Dans `package.json`
* C. Dans les deux modèles concernés
* D. Dans `prisma.config.js`

**20. C. Dans les deux modèles concernés**
→ Il faut nommer la relation dans chaque modèle pour qu’elle soit identifiable.

---

#### **21. Quelle relation nécessite d’ajouter une contrainte `@unique` sur la clé étrangère ?**

* A. Many-to-One
* B. One-to-Many
* C. One-to-One
* D. One-to-Many-to-One

**21. C. One-to-One**
→ Un enregistrement doit correspondre à un seul autre (clé unique).

---

#### **22. Quelle annotation peut être combinée avec `@relation` ?**

* A. `@map`
* B. `@id`
* C. `@default`
* D. `@unique`

**22. D. `@unique`**
→ Particulièrement utile dans les 1:1.

---

#### **23. Quelle commande permet de visualiser les relations dans Prisma ?**

* A. `npx prisma studio`
* B. `npx prisma db pull`
* C. `npx prisma generate`
* D. `npx prisma init`

**23. A. `npx prisma studio`**
→ Interface visuelle permettant de naviguer dans les relations.

---

#### **24. Une relation Many-to-Many peut être modélisée manuellement avec…**

* A. Des tableaux
* B. Un fichier JSON
* C. Un modèle pivot avec deux clés étrangères
* D. Une vue SQL

**24. C. Un modèle pivot avec deux clés étrangères**
→ Pour un contrôle précis, on peut créer la table de liaison manuellement.

---

#### **25. Dans Prisma, une relation est toujours…**

* A. Réversible
* B. Optionnelle
* C. Nominale
* D. Unidirectionnelle

**25. A. Réversible**
→ On peut interroger dans les deux sens si les champs sont définis.

---

#### **26. Quel champ faut-il ajouter dans un modèle pour représenter une relation inverse ?**

* A. Un tableau ou un champ du modèle lié
* B. Un champ `Int`
* C. `@reverse`
* D. `@child`

**26. A. Un tableau ou un champ du modèle lié**
→ Exemple : `posts: Post[]` dans `User` représente la relation inverse de `Post.author`.

---

#### **27. Que faut-il faire pour que Prisma crée une table de liaison automatiquement ?**

* A. Utiliser `@map`
* B. Ne rien faire, juste deux tableaux
* C. Ajouter une contrainte `foreign`
* D. Utiliser `@@table`

**27. B. Ne rien faire, juste deux tableaux**
→ Prisma crée automatiquement la table de jonction.

---

#### **28. Peut-on combiner `onDelete` avec `@relation` ?**

* A. Non
* B. Oui
* C. Seulement en production
* D. Uniquement avec MySQL

**28. B. Oui**
→ Ex : `@relation(fields: [...], references: [...], onDelete: Cascade)`

---

#### **29. Quelle syntaxe connecte un modèle existant à une relation ?**

* A. `create`
* B. `link`
* C. `connect`
* D. `join`

**29. C. `connect`**
→ Permet de lier un enregistrement existant sans en créer un nouveau.

---

#### **30. Comment écrire une relation One-to-One obligatoire ?**

* A. `profile Profile?`
* B. `profile Profile`
* C. `profile: string`
* D. `profile Profile[]`

**30. B. `profile Profile`**
→ Sans `?`, la relation est obligatoire.


