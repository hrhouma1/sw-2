### Tableau récapitulatif des annotations Prisma

| Annotation        | Portée | Description                                                         | Exemple                                                   |
| ----------------- | ------ | ------------------------------------------------------------------- | --------------------------------------------------------- |
| `@id`             | Champ  | Définit ce champ comme la clé primaire                              | `id String @id`                                           |
| `@default(...)`   | Champ  | Valeur par défaut si aucune n’est fournie                           | `createdAt DateTime @default(now())`                      |
| `@updatedAt`      | Champ  | Met automatiquement à jour ce champ à chaque modification du modèle | `updatedAt DateTime @updatedAt`                           |
| `@unique`         | Champ  | Ajoute une contrainte d’unicité sur ce champ                        | `email String @unique`                                    |
| `@map("...")`     | Champ  | Spécifie un nom différent dans la base de données pour ce champ     | `firstName String @map("first_name")`                     |
| `@relation(...)`  | Champ  | Définit une relation avec un autre modèle                           | `user User @relation(fields: [userId], references: [id])` |
| `@ignore`         | Champ  | Ignore ce champ lors de la génération du client Prisma              | `temp String @ignore`                                     |
| `@@id([...])`     | Modèle | Clé primaire composée (plusieurs champs)                            | `@@id([userId, postId])`                                  |
| `@@unique([...])` | Modèle | Contrainte d’unicité sur une combinaison de champs                  | `@@unique([email, username])`                             |
| `@@map("...")`    | Modèle | Spécifie un nom différent pour la table associée                    | `@@map("users")`                                          |
| `@@index([...])`  | Modèle | Crée un index sur un ou plusieurs champs                            | `@@index([createdAt])`                                    |
| `@@ignore`        | Modèle | Ignore entièrement ce modèle                                        | `@@ignore`                                                |

---

### Explication des portées

* **Champ** : l’annotation s’applique uniquement à un champ (`@...`)
* **Modèle** : l’annotation s’applique au modèle complet (`@@...`)

