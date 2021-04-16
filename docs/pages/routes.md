## Overview

In this section, we will walk you through how to set up your first **routes** for your Express server. Afterwards, we will see how we can clean up the code using [**routers**](/pages/routes/#setting-up-routers).

!!! Info "Routes & HTTP Requests"
    In Express, a route interprets the **[HTTP request method](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)** made to the server.


**Routing** is the action of determining what information is display or what action is taken when a user navigates or triggers a specified **endpoint** or **path**.

A simple route comprises the following components
 
-   `app` : the instance of Express that you have created in [Getting Started](link)
-   `method`:  the Express [**route method**](https://expressjs.com/en/4x/api.html#app.METHOD) corresponding to HTTP requests (eg. `get`, `post`, or `put`)
-   `path`: the defined endpoint of the request
-   `handler`: the function that is called when the route is hit

    

!!! Info "Handler functions"
    The handler will often be an [anonymous function](https://www.javascripttutorial.net/javascript-anonymous-functions/) written as either a regular function or an [arrow function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions). You may see more than one handler function per route in more complex routes.

## Setting up routes
We will cover the 2 most generic route methods: `GET` and `POST`. 
!!! Info "GET & POST"
    The `GET` method is used to request data from a server.  
    The `POST` method is used to send data to create date or update data on a server. [^1]

We left off in [Installing Express](../pages/installing-express/) with one route already set up to the root directory (`'/'`) from `src/app.js`. 
The handler for this route is an anonymous function that takes in two parameters. 
The first parameter represents the HTTP request object (often written as `request` or `req`) and the second parameter is the response object (written as `response` or `res`).

A [response method](https://expressjs.com/en/guide/routing.html#response-methods) is called in the handler to terminate the request-response cycle.

``` { .js .annotate hl_lines="4 5 6"}
const express = require('express');
const app = express();

app.get('/', (req, res) => { // (1)
  res.send('Hello World!'); // (2)
});

module.exports = app;
```

1. `'/'` (forward slash) is your root directory.
2. `res.send()` can send back various types of content.

!!! Info
    Remember you can click on the numbers at the end of a line of code for extra information about the specific examples used.


## Returning a Static Webpage Using GET 
As an example, let's create a route to display a contact page in the form of a static HTML page.

1.  Start with the route method and insert the path for your Express server to listen for.
    ``` { .js .annotate }
    app.get('/contact');
    ```
    
2.  Insert an empty handler that has the parameters for the request and response objects  
    ``` { .js .annotate }
    app.get('/contact', (req, res) => { });
    ```

3.  Insert the action you want to perform into the handler function:

    ``` { .js .annotate hl_lines="2"}
    app.get('/contact', (req, res) => {
      res.sendFile('contact.html'); // (1)
    });
    ```
    
    1. Use `res.sendFile()` to serve a static HTML page.

## Sending Data Using POST 
Suppose you have a form on your contact page for users to submit a message. You would use a [POST request](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/POST) so that you can retrieve the submitted data and store it somewhere.

For this example, we will pretend that the server is receiving data from the following form.
```html
<form method="POST" action="/contact">
  <input type="email" name="email">
  <input type="text" name="message">
  <input type="submit">
</form>
```
!!! warning "Action & Name Attributes"
    The [action attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/form) must match the path that will match the route path where we insert the handler logic.  
    The name attribute for each input will become the key/property of the object that the form will send to your server.


1.  Start with the route method and insert the path for your Express server to listen for.
    ``` { .js .annotate }
    app.post('/contact');
    ```
    Note that you can use the same path with different methods to perform different actions.
    
2.  Insert an empty handler that has the parameters for the request and response objects  
    ``` { .js .annotate }
    app.post('/contact', (req, res) => { });
    ```

3.  Insert the action you want to perform into the handler function.

    ``` { .js .annotate hl_lines="2 3 4 5"}
    app.post('/contact', (req, res) => {
      const email = req.body.email; // (1)
      const message = req.body.message;
      // code to process the form data
      res.redirect('/confirmation'); // (2)
    });
    ```
    
    1. req.body` it the object containing the input names and values from the form that was posted.
    2. Use `res.redirect()` to redirect your user to another page/route to end your handler function.


!!! success
    At this point, you have the tools to set up many routes in your `app.js. Next we will cover how to refactor your routes so `app.js` is more manageable.

    ``` { .js .annotate}
    const express = require('express');
    const app = express();

    app.get('/', (req, res) => {
      res.send('Hello World!');
    })

    app.get('/contact', (req, res) => {
      res.sendFile('contact.html');
    });

    app.post('/contact', (req, res) => {
      const email = req.body.email;
      const message = req.body.message;
      // code to process the form data
      res.redirect('/confirmation');
    });

    app.get('/reviews', (req, res) => {
      res.sendFile('reviews.html');
    });

    app.get('/reviews/add', (req, res) => { // (1)
      // code to add a review
      res.redirect('/reviews');
    });

    app.get('/reviews/delete', (req, res) => {
      // code to delete a review
      res.redirect('/reviews');
    });

    module.exports = app;
    ```
    
    1. Note that you can use multi-level paths as well.


## Setting up Routers
As the scope of your project grows or scales, you may find the need to organize your routes for ease of maintenance. Express provides a class to help achieve this called a [**Router**](https://expressjs.com/en/guide/routing.html#express-router).

If you had several related endpoints, it would be more manageable to organize these related routes into their own file. The Express router can help you achieve this by allowing you to export this grouping into another file (in our case `app.js`). This file acts as a main hub directing requests to the appropriate endpoints.

## Router Example
We will add onto our previous example with the contact page routes. At the moment, these routes are in `src/app.js`. We want to move the contact routes to their own file for better organization.

1.  Create a new JavaScript File called `contactRoute.js` in `src/api/routes`.  
    You can technically make this file anywhere you wish in your project but for this example, we will use this [project structure](/pages/project-structure).
    
2.  Require Express into `contactRoute.js` and create a new instance of the Router class by storing it to a new variable (`router`).

    ``` { .js .annotate hl_lines="6"}
    const express = require('express'); // (1)
    const router = express.Router(); // (2)
    ```
    
    1. Import the Express module so we can access its properties
    2. Make a new instance of the built-in Router class that will hold the routes we assign to it.
    

3.  Cut and paste the two contact routes from `app.js` into the `contactRoute.js` file.
    ``` { .js .annotate hl_lines="4 5 6 7 8 9 10 11 12 13"}
    const express = require('express');
    const router = express.Router();

    app.get('/contact', (req, res) => {
      res.sendFile('contact.html');
    });

    app.post('/contact', function(req, res) {
      const email = req.body.email;
      const message = req.body.message;
      // code to process the form data
      res.redirect('/confirmation');
    });
    ```

4.  Change `app` to `router` so that the routes are now associated to this router instance.  
    We can remove 'contact' from our path now as we will be setting the 'contact' path in `app.js`.
    ``` { .js .annotate hl_lines="4 8"}
    const express = require('express');
    const router = express.Router();

    router.get('/', function(req, res) {
      res.sendFile('contact.html');
    });

    router.post('/', function(req, res) {
      const email = req.body.email;
      const message = req.body.message;
      // code to process the form data
      res.redirect('/confirmation');
    });
    ```

5.  Add an export to the end of the file so we can access this router and its associated routes from other files.

    ``` { .js .annotate hl_lines="15"}
    const express = require('express');
    const router = express.Router();

    router.get('/contact', function(req, res) {
      res.sendFile('contact.html');
    });

    router.post('/contact', function(req, res) {
      const email = req.body.email;
      const message = req.body.message;
      // code to process the form data
      res.redirect('/confirmation');
    });

    module.exports = router; // (1)
    ```

    1. Your routes have been set to this variable so we only have to export the `router` and not the individual routes.


6.  Import the contact router into `app.js`.

    ``` { .js .annotate hl_lines="4"}
    const express = require('express');
    const app = express();

    const contactRoute = require('api/routes/contactRoute'); // (1)

    module.exports = app;
    ```

    1. Make sure you are requiring your router from wherever you have placed your `contactRoute.js` in your project.


7.  Use `app.use()` to load the router into the Express app.  
    Paths that start with `/contact` will now be sent to `contactRoute.js` for further routing.

    ``` { .js .annotate hl_lines="6"}
    const express = require('express');
    const app = express();

    const contactRoute = require('api/routes/contactRoute');

    app.use('/contact', contactRoute); // (1)

    module.exports = app;
    ```

    1. `app.use()` tells Express what functions you want to associate with the path in the first parameter.


!!! success
    You can have many router files in your project that you can import into another file for use. This will keep your files a mangeable size for readability.  

    ``` { .js .annotate }
    const express = require('express');
    const app = express();

    // Routes
    const indexRoute = require('api/routes/indexRoute');
    const contactRoute = require('api/routes/contactRoute');
    const authRoute = require('api/routes/authRoute');
    const reviewsRoute = require('api/routes/reviewsRoute');

    // Route Matchers
    app.use('/', indexRoute);
    app.use('/contact', contactRoute);
    app.use('/auth', authRoute);
    app.use('/reviews', reviewsRoute); // (1)

    module.exports = app;
    ```

    1. The `reviews/add` and `reviews/delete` paths now exist in a `reviewRoute.js` file as `/add` and `/delete`.

## Conclusion
By the end of this section, you will have successfully learned the following:

- [x] How to write a route to set the desired response to different HTTP requests
- [x] How to use the Express Router class to group routes
- [x] How to export and import the router for use in separate file

Great job 🤗. You can go ahead and click on the link below to move on to the next step:

**[Using Middleware](../pages/middleware)**
[^1]: [HTTP Request Methods](https://www.w3schools.com/tags/ref_httpmethods.asp).