# Getting started

To start client you need to install dependencies and configure basic settings.

Required:

-  [NodeJS](https://nodejs.org/)
-  [Yarn](https://yarnpkg.com)

## Dependencies

```bash
git clone https://github.com/iterations-is/client-web.git
yarn install
```

## Configuration files

All configration files are located `./src/config`. You need to copy and change them according to your system. E.g.:

```bash
cp ./src/config/server.config.example.ts ./src/config/server.config.ts
vi ./src/config/server.config.ts
```

## Development

```bash
yarn dev
```

## Production

```
yarn build
yarn start
```
