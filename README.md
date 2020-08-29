# Cross-service requests validation and errors handling library.

## Installation

```bash
npm i --save @alexhelloworld/common
```

## Using:

To get current user logged in:

```js
import { currentUser } from '@alexhelloworld/common'
const user = currentUser
```

Middleware For the request validation and throw Bad Request Error in case of any errors:

```js
import { validateRequest } from '@alexhelloworld/common'

router.post(
  '/api/users/signin',
  [
    body('email').isEmail().withMessage('Email must be valid'),
    body('password').trim().notEmpty().withMessage('Password is required'),
  ],
  validateRequest,
  async (req: Request, res: Response) => {
    //Sign in code should be here
  }
)
```

##### Error handler and Errors templates

Error handler middleware to serialize all errors to the for understanfing between all the Microservices

```js
import { errorHandler } from '@alexhelloworld/common'
const app = express()
app.use(errorHandler)
```

Errors reusable:

```js
import { BadRequestError } from '@alexhelloworld/common'
import { NotFoundError } from '@alexhelloworld/common'
// 400
if (!passwordsMatch) {
  throw new BadRequestError('Invalid credentials')
}
// 404
app.get('*', () => {
  throw new NotFoundError()
})
```
