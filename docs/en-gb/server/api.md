# API

## How to write API

-  add new router file `./api/example.router.ts`, example:

```js
/**
 * @file
 * @description
 * @author
 */

const express = require('express');
const router = express.Router();

// ORM
import { getConnection } from 'typeorm';
import { Users } from '@sqlmodels/Users.model';

// Responses generator
import { genResponseSuccessSimple } from '@utils/response.util';

// Scheme validator
const joi = require('joi');
import { validateViaJoiSchema } from '@utils/validator.util';

// Routes
router.get('/path/:id', permissions(['namespace.key']), actionName);

/**
 * Description
 * @param req
 * @param res
 */
async function actionName(req, res) {
      // Schema
      const schema = joi.object().keys({
         key: joi
            .number()
            .min(0)
            .required(),
      });

      // Validation
      if (!validateViaJoiSchema(req.body, schema))
         return res.status(422).json(genResponseErrorDataInvalid('Invalid data', []));

      // Connection repository example
      const connection = getConnection();
      const repoUsers = connection.getRepository(Users);
      const jwtPayload = req.jwt;

      // Find
      try {
         const user = await repoUsers.findOne(jwtPayload.user_id);
      } catch (e) {
         return res.status(404).json(genResponseErrorSimple('Response text.'));
      }

      // ...

      return res.status(200).json(genResponseSuccessData('Response text.', {}));
   },
);
```

Routes have their path and permissions. If URL matches and permissions are OK the middleware is called.

```js
router.get(
   // URL
   '/path/:id',
   // Required user permissions (see SQL DB - 'permissions' table)
   permissions(['namespace.key']),
   // Middleware
   middlewareFunction,
);
```

-  declare it as a new router at `./api/Router.ts

```js
router.use('/example', routePing);
```
