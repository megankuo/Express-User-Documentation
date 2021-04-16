## Overview

When a server receives an `HTTP` request from the client (browser) it usually processes it and eventually returns some information to client via a `HTTP` response.
This is known as the application’s request-response cycle. For a more in-depth understanding on request-response cycles, see [The Request/Response Cycle of the Web](https://medium.com/@jen_strong/the-request-response-cycle-of-the-web-1b7e206e9047). 
In Express, [middleware](https://expressjs.com/en/guide/using-middleware.html) are functions (or logic) that provide a convenient mechanism to handle `HTTP` requests entering your application. 
Middleware functions can be chained together to perform a series of logic, one after the other. The last middleware function will typically end the request-response cycle by returning a response to the client.

There are five(5) main categories of middleware that express supports, namely:

- [Built-in](https://expressjs.com/en/guide/using-middleware.html#middleware.built-in)
- [Third-party](https://expressjs.com/en/guide/using-middleware.html#middleware.third-party)  
- [Error-handling](https://expressjs.com/en/guide/using-middleware.html#middleware.error-handling)
- [Application-level](https://expressjs.com/en/guide/using-middleware.html#middleware.application)
- [Router-level](https://expressjs.com/en/guide/using-middleware.html#middleware.router)

In this section you'll walk through an example of adding several middleware to Express.

## Using Middleware in Express

1. Add into `src/app.js` a built-in middleware in that parses incoming requests that contain JSON data:

    ``` { .js .annotate hl_lines="7"}
    const express = require('express');
    const router = express.Router();
   
    const app = express();
   
    // Middleware
    app.use(express.json());

    ...

    module.exports = app;
    ```

    This allows Express to handle html form data that are sent to the server via a `POST`.

2. Install [Helmet](https://www.npmjs.com/package/helmet):
> npm install helmet

3. Import `helmet` in `src/app.js`:
    ``` { .js .annotate hl_lines="3"}
    const express = require('express');
    const router = express.Router();
    const helmet = require('helmet');
   
    ...

    module.exports = app;
    ```
4. Load `helmet` middleware:

    ``` { .js .annotate hl_lines="8"}
    const express = require('express');
    const router = express.Router();
   
    const app = express();
   
    // Middleware
    app.use(express.json());
    app.use(helmet());
   
    ...

    module.exports = app;
    ```

    Helmet is a third-party middleware that adds some default protection to your Express application by setting various [`HTTP` headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers). 

5. Define a custom error-handling middleware function:

    ``` { .js .annotate hl_lines="9 10 11 12"}
    const express = require('express');
    const router = express.Router();
   
    const app = express();
   
    // Middleware
    app.use(express.json());
    app.use(helmet());
    app.use(function (err, req, res, next) {
        //Extra logic for handling errors
        res.status(500).send('Something broke!');
    });
    ...

    module.exports = app;
    ```

    Error-handling middleware allows you to catch and process errors that occur within the application.

!!!success "Congratulations 👏"
    That is for middleware! If it interests you, there is a lot more to middleware provided in the [Express Middleware Documentation](https://expressjs.com/en/guide/using-middleware.html#middleware.built-in).


## Conclusion

By the end of this section, you will have successfully learned the following:

- [x] That they are different types of middleware that Express supports
- [x] How to add built-in, third-party, and error-handling middleware to Express applications.


Great job 🤗. Check out the next page if you've had any issues getting the project to work.

**[Troubleshooting](/pages/troubleshooting)**


