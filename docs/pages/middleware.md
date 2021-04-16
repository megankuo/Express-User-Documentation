## Overview

When a server receives an `HTTP` request from the client (browser) it usually processes it and eventually returns some information to client via a `HTTP` response.
This is known as the application’s request-response cycle. For a more in-depth understanding on request-response cycles, see [The Request/Response Cycle of the Web](https://medium.com/@jen_strong/the-request-response-cycle-of-the-web-1b7e206e9047). 
In Express, [middleware](https://expressjs.com/en/guide/using-middleware.html) are functions (or logic) that provide a convenient mechanism to handle `HTTP` requests entering your application. 
Middleware functions can be chained together to perform a series of logic, one after the other. The last middleware function will typically end the request-response cycle by returning a response to the client.

In this section you will get a brief introduction into the types of middleware that Express supports.
Afterwards you'll walk through an example of adding two types of middleware to Express.

## Types of Express Middleware
There are five(5) main categories of middleware that express supports, namely:

- [Built-in](https://expressjs.com/en/guide/using-middleware.html#middleware.built-in)
- [Third-party](https://expressjs.com/en/guide/using-middleware.html#middleware.third-party)  
- [Error-handling](https://expressjs.com/en/guide/using-middleware.html#middleware.error-handling)
- [Application-level](https://expressjs.com/en/guide/using-middleware.html#middleware.application)
- [Router-level](https://expressjs.com/en/guide/using-middleware.html#middleware.router)

