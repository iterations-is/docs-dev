# Getting started

To start server you need to install dependencies, configure basic settings and run databases.

Required:

-  [NodeJS](https://nodejs.org/)
-  [Yarn](https://yarnpkg.com)

Optional:

-  [Docker](https://www.docker.com/)

## Dependencies

```
git clone https://github.com/iterations-is/server-api.git
yarn install

```

## Application Modes

Iterations IS has a few modes:

-  development
   -  model-database sync is ensabled, you dont need to run migrations
   -  you need to run seeds manually
-  test
   -  the whole database is dropped every time server starts
   -  model-database sync is disabled
   -  migrations and seeds are run automatically (needs initial database migration)
-  production
   -  database is untouchable, server starts only application
   -  you need to run migrations and seeds manually (before server starts)

### Configuration

All configration files are located `./src/config`. You need to copy and change them according to your system. E.g.:

```bash
cp ./src/config/server.config.example.ts ./src/config/server.config.ts
vi ./src/config/server.config.ts
```

There is one more configuration file at root directory – ORM configuration.

```bash
cp ./ormconfig.example.ts ./ormconfig.ts
vi ./ormconfig.ts
```

### Databases

You can run your own databases or run docker-compose file.

```bash
docker-compose up -d
```

Before you start the server you need to run migrations and seeds.

```bash
yarn dev:migration:run
yarn dev:seed:run
```

## Start server

Everything is initialized now. Start your server in production or development (watching is enabled) mode:

```bash
yarn dev:start
```

## Production mode

```bash
yarn prod:start
yarn prod:mig:run
yarn prod:seed:run
```

Done. Use it.

## Test mode

Test mode is positioned as full-automatized server just for testing. Starting the server takes care about everything around databases (drop tables, etc.) and prepares server for testing.

```bash
yarn test:start
```

The command run migrations (you need to have at least one initial migration), apply seeds and start the server.

After successful start you need to run tests (with or without coverage).

```bash
yarn test
yarn test:coverage
```

Remove test server.

```bash
yarn test:del
```

# Other

[PM2](https://pm2.io/) is used as a default process manager for Iterations IS. Useful commands for debugging (you need to install pm2 globally or run it from `node_modules` folder):

```bash
pm2 monit
pm2 logs
```
