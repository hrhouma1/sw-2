# Rappel rapide

Dans un fichier `schema.prisma`, **les annotations** sont utilisées pour définir des métadonnées sur les modèles et les champs. Prisma distingue deux types :

| Type       | Syntaxe       | S'applique à     |
| ---------- | ------------- | ---------------- |
| **Champ**  | `@` (simple)  | Un champ         |
| **Modèle** | `@@` (double) | Le modèle entier |



# Un seul `@` = annotation sur **un champ**

Exemples :

```ts
id        String   @id @default(cuid())
createdAt DateTime @default(now())
updatedAt DateTime @updatedAt
```

Ici, chaque `@truc` **s'applique au champ** sur la même ligne :

* `@id` → ce champ est la clé primaire.
* `@default(...)` → valeur par défaut.
* `@updatedAt` → met à jour la valeur à chaque `update`.



# Deux `@@` = annotation sur **tout le modèle**

Exemple :

```ts
@@map("articles")
```

Ici :

* `@@map(...)` signifie : **le modèle `Article` correspond à la table `articles` dans la base de données**.

Autres exemples d’annotations globales :

```ts
@@index([email])
@@unique([email, username])
@@id([userId, postId]) // clé primaire composée
```

> Toutes ces annotations ne concernent **pas un champ individuel**, mais **l’ensemble de la table ou du modèle**.



# En résumé

| Syntaxe | Signifie…                            | Exemple                                |
| ------- | ------------------------------------ | -------------------------------------- |
| `@...`  | Annotation de champ                  | `@default(now())`, `@id`, `@updatedAt` |
| `@@...` | Annotation de modèle (table entière) | `@@map("articles")`, `@@index([...])`  |


