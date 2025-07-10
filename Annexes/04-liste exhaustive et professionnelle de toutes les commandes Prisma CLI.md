# Introduction:

Je vous propose **liste exhaustive et professionnelle de toutes les commandes Prisma CLI**, classées par usage fonctionnel, avec leur syntaxe exacte et une brève explication. Chaque commande commence généralement par :

```bash
npx prisma <commande> [options]
```



<h1 id="generate">1. Génération du client Prisma</h1>

| Commande              | Description                                                                     |
| --------------------- | ------------------------------------------------------------------------------- |
| `npx prisma generate` | Génère le client Prisma (`@prisma/client`) à partir du fichier `schema.prisma`. |



<h1 id="migrate">2. Migration de la base de données</h1>

| Commande                                     | Description                                                                        |
| -------------------------------------------- | ---------------------------------------------------------------------------------- |
| `npx prisma migrate dev --name <nom>`        | Crée une migration et l’applique (développement). Génère aussi le client.          |
| `npx prisma migrate reset`                   | Supprime la base, la recrée, applique toutes les migrations, puis exécute le seed. |
| `npx prisma migrate deploy`                  | Applique les migrations existantes (production ou CI/CD).                          |
| `npx prisma migrate status`                  | Affiche l’état des migrations (appliquées, en attente).                            |
| `npx prisma migrate diff`                    | Compare deux états du schéma (base ↔ modèle) et génère un diff SQL.                |
| `npx prisma migrate resolve --applied <nom>` | Marque une migration comme "déjà appliquée" (à la main).                           |



<h1 id="db">3. Gestion directe de la base (`db`)</h1>

| Commande                | Description                                                                                            |
| ----------------------- | ------------------------------------------------------------------------------------------------------ |
| `npx prisma db push`    | Applique le schéma au SGBD sans créer de migration (utile pour tests, SQLite, reset rapide).           |
| `npx prisma db pull`    | Synchronise le fichier `schema.prisma` à partir d'une base de données existante (reverse engineering). |
| `npx prisma db seed`    | Exécute le script de seed défini dans `package.json`.                                                  |
| `npx prisma db execute` | Exécute une commande SQL manuelle sur la base (`--file`, `--stdin`, etc.).                             |
| `npx prisma db drop`    | Supprime entièrement la base de données (avec confirmation).                                           |


<h1 id="studio">4. Interface graphique Prisma Studio</h1>

| Commande            | Description                                                                          |
| ------------------- | ------------------------------------------------------------------------------------ |
| `npx prisma studio` | Lance Prisma Studio, une interface web pour naviguer, modifier et créer les données. |


<h1 id="validate">5. Validation</h1>

| Commande              | Description                                                            |
| --------------------- | ---------------------------------------------------------------------- |
| `npx prisma validate` | Vérifie que le fichier `schema.prisma` est bien formé et sans erreurs. |



<h1 id="format">6. Formatage</h1>

| Commande            | Description                                         |
| ------------------- | --------------------------------------------------- |
| `npx prisma format` | Formate automatiquement le fichier `schema.prisma`. |



<h1 id="introspect">7. Introspection (reverse engineering)</h1>

| Commande                | Description                                                                            |
| ----------------------- | -------------------------------------------------------------------------------------- |
| `npx prisma introspect` | Analyse une base de données existante et génère un fichier `schema.prisma` compatible. |



<h1 id="generate-schema">8. Génération de fichiers SQL (avancé)</h1>

| Commande                                                                                                                        | Description                                         |
| ------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------- |
| `npx prisma migrate diff \`<br/>\`<code>--from-schema-datamodel prisma/schema.prisma --to-url "\$DATABASE\_URL" --script</code> | Génère un script SQL différentiel (utile en CI/CD). |



<h1 id="help">9. Aide en ligne</h1>

| Commande                       | Description                               |
| ------------------------------ | ----------------------------------------- |
| `npx prisma --help`            | Affiche la liste des commandes Prisma.    |
| `npx prisma <commande> --help` | Affiche l’aide spécifique à une commande. |



<h1 id="commande-recursive">10. Commandes courantes par ordre logique d’usage</h1>

```bash
# Étapes initiales
npx prisma init
npx prisma migrate dev --name init
npx prisma studio

# Développement itératif
npx prisma generate
npx prisma migrate dev --name ajout_articles
npx prisma db seed
npx prisma studio

# Production ou CI/CD
npx prisma migrate deploy
npx prisma migrate status
npx prisma migrate diff

# Gestion directe
npx prisma db push
npx prisma db pull
npx prisma db drop
npx prisma db execute --file script.sql

# Outils
npx prisma validate
npx prisma format
```

