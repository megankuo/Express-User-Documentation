
Possible project structure. This is not written in stone, MVC and other architecture are often highly opinionated.
```bash
|-- project-name              # Root Directory
    |-- docs/                 # Documentation
    |-- public/               # Publicly Accessible Assets
    |   |-- images/
    |   |-- js/               # Client-side JavaScript
    |   |-- styles/           # CSS Stylesheets   
    |-- src/
    |   |-- app.js            # Application Entry Point
    |   |-- api/
    |   |   |-- controllers/  # Request Managers
    |   |   |-- middleware/   # Intermediary b/w Client Request & Server Response
    |   |   |-- routes/       # API Endpoints (URIs)
    |   |-- config/           # Configuration/Settings Files
    |   |-- db/               # Mock Database or Connection to Database
    |   |-- models/           # Database Models
    |   |-- services/         # Services Layer for Business Logic (Talks to Database)
    |   |-- utils/            # Miscellaneous Helper Functions
    |   |-- views/            # Static Template Files (EJS, Pug, or Mustache)
    |-- test/                 # Test Suite   
    |-- .env                  # Environment Variables
    |-- .eslintignore
    |-- .eslintrc.js          # Linting Rules
    |-- .gitignore            # Files/Directory Git Should Ignore 
    |-- .prettierignore   
    |-- .prettierrc.js        # Code Formatting Rules
    |-- package.json          # Metadata and Package List
    |-- README.md
    |-- server.js             # Application Server 
```

``` { .js .annotate }
/** .eslintrc.js */

module.exports = {
    extends: 'airbnb-base', // (1)
    env: { // (2)
        browser: true,
        commonjs: true,
        node: true,
        es6: true,
        jquery: true,
    },
    rules: {
        indent: ['error', 4], // (3)
        'linebreak-style': 0, // (4)
        'max-len': ['error', { code: 120 }], // (5)
        'max-lines-per-function': ['error', { max: 35, skipComments: true }], // (6)
        'max-nested-callbacks': ['error', 2], // (7)
        'no-console': 'off', // (8)
    },
};
```

1. Inherit all rules from [airbnb code styleguide](https://github.com/airbnb/javascript).
2. Environments that provide predefined global variables - see [ESLint Environments](https://eslint.org/docs/user-guide/configuring/language-options#specifying-environments) for a complete list of supported environments.
3. Enforces consistent indentation (4 spaces).
4. Enforces consistent linebreak style.
5. Enforces a maximum line length of 120 characters.
6. Enforces a maximum function length of 35 lines.
7. Enforces a maximum depth or 3 that callbacks can be nested. A common pitfall that is easy to fall into is nesting callbacks, which makes code more difficult to read the deeper the callbacks are nested.
8. Allows the use of console.


``` { .js .annotate }
/** .prettierrc.js */

module.exports = {
    trailingComma: "es5",
    tabWidth: 4,
    semi: true,
    singleQuote: true,
};
```

``` { .js .annotate }
/** /src/app.js */

const express = require('express'); // (1)

const app = express(); // (2)

app.get('/', (req, res) => { // (3)
    res.send('Hello World'); // (4)
});

module.exports = app;
```

1. Import Express module
2. Create Express application 
3. Handle `GET` request made for the root URL. `req` is the incoming request and `res` is used to send back the desired HTTP response.
4. Return a message of 'Hello World' in response to the HTTP request.

Note, express supports methods that correspond to each HTTP request method (`GET`, `POST`, `PUT`, `DELETE`, etc. ). For a refresher on the different HTTP request methods, see [here](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods).

``` { .js .annotate }
/** server.js */

const app = require('./src/app'); // (1)

const port = process.env.PORT || 3000; // (2)

app.listen(port, () => { // (3)
    console.log(`🚀 Server started successfully, listening on port ${port}`);
});

```

1. Import instance of Express Application created in `/src/app.js`.
2. Specify port number for server to listen on. 
3. Start server and listen on specified port.