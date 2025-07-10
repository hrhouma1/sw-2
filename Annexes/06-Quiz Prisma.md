### **Quiz Prisma – 30 Questions**

---

#### **1. Quelle commande initialise Prisma dans un projet Node.js ?**

* A. `npm install prisma`
* B. `npx prisma init`
* C. `npx prisma start`
* D. `npx init prisma`

**1. B. `npx prisma init`**
→ Initialise Prisma, crée `schema.prisma` et `.env`.

---

#### **2. Où définit-on la chaîne de connexion à la base de données ?**

* A. `schema.prisma`
* B. `.prisma`
* C. `.env`
* D. `package.json`

**2. C. `.env`**
→ Le fichier `.env` contient `DATABASE_URL`, lu par `schema.prisma`.

---

#### **3. Quel fichier contient les modèles de données Prisma ?**

* A. `models.ts`
* B. `database.prisma`
* C. `schema.prisma`
* D. `config.js`

**3. C. `schema.prisma`**
→ Tous les modèles sont déclarés dans ce fichier.

---

#### **4. Que fait la commande `npx prisma generate` ?**

* A. Démarre un serveur Prisma
* B. Formate les fichiers
* C. Lance Prisma Studio
* D. Génère le client Prisma

**4. D. Génère le client Prisma**
→ Le client est utilisé dans le code (`prisma.user.findMany()`).

---

#### **5. Quel est le rôle du champ `@id` dans un modèle ?**

* A. Index
* B. Valeur par défaut
* C. Clé primaire
* D. Clé étrangère

**5. C. Clé primaire**
→ `@id` indique que ce champ est l’identifiant principal de la table.

---

#### **6. Quelle annotation permet de définir une relation entre deux modèles ?**

* A. `@foreign`
* B. `@connect`
* C. `@relation`
* D. `@link`

**6. C. `@relation`**
→ Permet de relier deux modèles (clé étrangère).

---

#### **7. Quelle commande applique une migration avec nom et mise à jour du client ?**

* A. `npx prisma db update`
* B. `npx prisma migrate dev --name <nom>`
* C. `npx prisma apply migration`
* D. `npx prisma migrate run`

**7. B. `npx prisma migrate dev --name <nom>`**
→ Crée, applique la migration et met à jour le client.

---

#### **8. Comment se nomme l’interface graphique fournie par Prisma ?**

* A. Prisma Viewer
* B. Prisma Admin
* C. Prisma Studio
* D. Prisma Panel

**8. C. Prisma Studio**
→ Interface web pour voir/modifier les données.

---

#### **9. Quelle annotation renomme une table dans la base de données ?**

* A. `@@name`
* B. `@@rename`
* C. `@@map`
* D. `@alias`

**9. C. `@@map`**
→ Change le nom de la **table** dans la base SQL.

---

#### **10. Quel type de relation est représenté par un champ tableau dans un modèle ?**

* A. One-to-One
* B. One-to-Many
* C. Many-to-One
* D. Many-to-Many

**10. B. One-to-Many**
→ Un tableau (`Post[]`) signifie plusieurs objets liés.

---

#### **11. Que fait `@default(now())` ?**

* A. Met à jour la valeur à chaque update
* B. Donne la date d’aujourd’hui par défaut
* C. Empêche les modifications
* D. Génère une chaîne UUID

**11. B. Donne la date d’aujourd’hui par défaut**
→ `now()` est utilisé pour `createdAt`.

---

#### **12. Quelle commande synchronise le schéma avec la base sans créer de migration ?**

* A. `npx prisma db pull`
* B. `npx prisma db push`
* C. `npx prisma sync`
* D. `npx prisma generate`

**12. B. `npx prisma db push`**
→ Pousse le schéma dans la base (sans migration).

---

#### **13. Quelle commande inverse l’ordre classique et génère un modèle à partir d’une base ?**

* A. `npx prisma sync`
* B. `npx prisma reverse`
* C. `npx prisma db introspect`
* D. `npx prisma db import`

**13. C. `npx prisma db introspect`**
→ Lit une base existante et génère un schéma.

---

#### **14. Que signifie `@unique` ?**

* A. Le champ est optionnel
* B. Le champ est une clé étrangère
* C. Le champ est indexé
* D. Le champ doit être unique

**14. D. Le champ doit être unique**
→ Prisma imposera une contrainte d’unicité dans la base.

---

#### **15. Quelle commande efface toute la base et relance les migrations + seed ?**

* A. `npx prisma db drop`
* B. `npx prisma reset`
* C. `npx prisma migrate reset`
* D. `npx prisma migrate wipe`

**15. C. `npx prisma migrate reset`**
→ Supprime la base, relance toutes les migrations, puis `seed`.

---

#### **16. Quelle commande affiche les différences entre deux schémas ?**

* A. `npx prisma compare`
* B. `npx prisma migrate diff`
* C. `npx prisma db diff`
* D. `npx prisma model diff`

**16. B. `npx prisma migrate diff`**
→ Compare deux schémas ou bases et génère un fichier SQL diff.

---

#### **17. Dans quelle propriété du `package.json` place-t-on la commande seed ?**

* A. `"scripts"`
* B. `"prisma.seed"`
* C. `"prisma"`
* D. `"db"`

**17. C. `"prisma"`**
→ Exemple : `"prisma": { "seed": "node prisma/seed.js" }`

---

#### **18. Quel type correspond à une date dans Prisma ?**

* A. `Date`
* B. `Datetime`
* C. `DateTime`
* D. `Timestamp`

**18. C. `DateTime`**
→ Type utilisé pour les dates/heures.

---

#### **19. Quelle annotation permet de créer un index simple ou composé ?**

* A. `@index`
* B. `@@index`
* C. `@map`
* D. `@@ref`

**19. B. `@@index`**
→ Définit un index (accélère les requêtes).

---

#### **20. Comment Prisma gère-t-il les relations Many-to-Many sans table pivot ?**

* A. Il crée une vue
* B. Il génère une table intermédiaire automatiquement
* C. Il refuse cette relation
* D. Il utilise un champ JSON

**20. B. Il génère une table intermédiaire automatiquement**
→ Prisma gère les many-to-many via une table pivot automatique.

---

#### **21. Quel champ permet à Prisma de mettre à jour une date à chaque update ?**

* A. `@timestamp`
* B. `@default(now())`
* C. `@updatedAt`
* D. `@now`

**21. C. `@updatedAt`**
→ Le champ est mis à jour à chaque modification.

---

#### **22. Que contient le dossier `prisma/migrations/` ?**

* A. Les fichiers de seed
* B. Les clients générés
* C. Les fichiers SQL de migration
* D. Les sauvegardes JSON

**22. C. Les fichiers SQL de migration**
→ Chaque migration contient le script SQL appliqué.

---

#### **23. Quelle commande permet d'exécuter un script SQL sur la base ?**

* A. `npx prisma sql`
* B. `npx prisma db execute`
* C. `npx prisma migrate run`
* D. `npx prisma run sql`

**23. B. `npx prisma db execute`**
→ Permet d’exécuter un fichier SQL directement.

---

#### **24. Que se passe-t-il si `prisma generate` n’est pas exécuté après modification ?**

* A. Erreur au lancement de Prisma Studio
* B. La base est écrasée
* C. Le client ne reflète pas les changements du schéma
* D. Rien, Prisma le fait automatiquement

**24. C. Le client ne reflète pas les changements du schéma**
→ Il faut régénérer le client à chaque changement.

---

#### **25. Quelle commande permet de formater `schema.prisma` ?**

* A. `npx prisma lint`
* B. `npx prisma schema:format`
* C. `npx prisma format`
* D. `npx prisma clean`

**25. C. `npx prisma format`**
→ Formate proprement le fichier `schema.prisma`.

---

#### **26. Peut-on utiliser Prisma avec MongoDB ?**

* A. Non, Prisma est uniquement relationnel
* B. Oui, avec `@provider = "mongodb"`
* C. Oui, mais uniquement en CLI
* D. Oui, mais sans support des relations

**26. B. Oui, avec `@provider = "mongodb"`**
→ Prisma supporte MongoDB, en preview.

---

#### **27. Quelle fonction TypeScript est utilisée pour interroger un modèle ?**

* A. `find()`
* B. `findOne()`
* C. `findMany()`
* D. `search()`

**27. C. `findMany()`**
→ Méthode utilisée pour lire plusieurs enregistrements.

---

#### **28. Quelle commande donne l’état des migrations ?**

* A. `npx prisma migrate show`
* B. `npx prisma migrate state`
* C. `npx prisma migrate status`
* D. `npx prisma status`

**28. C. `npx prisma migrate status`**
→ Donne l’état des migrations dans le projet.

---

#### **29. Quelle annotation permet de mapper un champ vers un nom différent en SQL ?**

* A. `@field("nom_sql")`
* B. `@map("nom_sql")`
* C. `@@map("nom_sql")`
* D. `@alias("nom_sql")`

**29. B. `@map("nom_sql")`**
→ Renomme un champ dans la base SQL.

---

#### **30. Quelle est la meilleure pratique après une modification du schéma ?**

* A. Refaire tout le projet
* B. Exécuter uniquement `generate`
* C. Exécuter `migrate dev` ou `db push` puis `generate`
* D. Supprimer le schéma et recommencer

**30. C. Exécuter `migrate dev` ou `db push` puis `generate`**
→ Il faut synchroniser la base et régénérer le client.


