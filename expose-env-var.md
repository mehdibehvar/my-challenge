# how prevent exposing env variables in the source code by vite.js

**this is a config for acces .env variable by proccess.env**
```js
import path from 'path';
import dotenv from 'dotenv';
import fs from 'fs';
// specify the adress of .env file
const envPath = path.resolve(__dirname, './.env');
// Load environment variables from .env file and put them in proccess.env
dotenv.config({ path: envPath });
```
*Italic Text*

- To prevent accidentally leaking env variables to the client,
 only variables prefixed with VITE_ are exposed to your Vite-processed code.
 e.g. for the following env variables:

 ```js 
VITE_SOME_KEY=123
DB_PASSWORD=foobar
```
Only VITE_SOME_KEY will be exposed as import.meta.env.VITE_SOME_KEY

- If you would like to expose an unprefixed variable, you can use define to expose it:

```js
    define: {
        "import.meta.env.APP_URL": process.env.APP_URL ? JSON.stringify(
            process.env.APP_URL
        ) : null,
        "import.meta.env.API_BASE_URL": process.env.API_BASE_URL ? JSON.stringify(
            process.env.API_BASE_URL
        ) : null,
        "import.meta.env.CLIENT_URL": process.env.CLIENT_URL ? JSON.stringify(
            process.env.CLIENT_URL
        ) : null,
    },
```
https://vitejs.dev/config/shared-options.html#envprefix

**note that if you use the following code it expose all variable in youre source code:
```js
const envConfig = dotenv.parse(fs.readFileSync(envPath));
    define: {
        'process.env': {
            ...envConfig
        }
    }
```