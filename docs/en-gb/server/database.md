# Database

Server uses three different databases:

-  relational (prefered PostgreSQL) with [TypeORM](https://typeorm.io/) ORM
-  nosql document (MongoDB) with [mongoose](https://mongoosejs.com/) ODM
-  in-memory data structure store (redis)

## SQL

### Migrations

Migrations are based on the TypeORM ORM. All files are stored at `/database/sql/migrations/*.ts` and prioritized by timestamp in the name. The detailed migrations API is described at [TypeORM](https://typeorm.io/#/migrations/using-migration-api-to-write-migrations). The most common commands are added to `package.json`.

```bash
# Create
yarn dev:migration:create name-of-the-migration
# Generate (database – models diff)
yarn dev:migration:generate name-of-the-migration
# Run
yarn dev:migration:run
# Revert last
yarn dev:migration:revert
```

### Seeds

TypeORM doesn't have its own seed system. Therefore there is a little hack – TypeORM sets additional connection configuration at `ormconfig.js` and creates a new (parallel) type of migrations that are called "seeds". Their folder is `/database/sql/seeds/*.ts`.

```bash
# Create
yarn dev:seed:create name-of-the-seed
# Run
yarn dev:seed:run
# Revert last
yarn dev:seed:revert
```

## NoSQL
