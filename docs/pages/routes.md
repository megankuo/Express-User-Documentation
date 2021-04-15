
## Overview

In this section, we will walk you through how to set up your first **routes** for your Express server.

!!! Info "Routes & HTTP Requests"
    In Express, a route interprets the **[HTTP request method](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)** made to the server.


**Routing** is the action of determining what information is display or what action is taken when a user navigates or triggers a specified **endpoint** or **path**.

A simple route is comprised of the following components
 
-   `app`: the instance of Express that you have created in [Getting Started](link)
-   `method`:  the Express [route method](https://expressjs.com/en/4x/api.html#app.METHOD) corresponding to HTTP requests (eg. `get`, `post`, or `put`)
-   `path`: the defined endpoint of the request
-   `handler`: the function that is called when the route is hit
```javascript
app.method(path, handler)
```
!!! Info "Handler functions"
    The handler will be often be an [anonymous function](https://www.javascripttutorial.net/javascript-anonymous-functions/) written as either a regular function or an [arrow function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions). There may be more than one handler function per route.

## Setting up routes
We will cover the 2 most generic route methods: `get` and `post`. 
!!! Info "GET & POST"
    The GET method is used to request data from a server.  
    The POST method is used to send data to create date or update data on a server. [^1]

We left off in Getting Started with one route already set up to the root directory (`'/'`). The handler for this route is an anonymous function that takes in two parameters. The first parameter represents the HTTP request object (often written as `request` or `req`) and the second parameter is the response object (written as `response` or `res`).

A response method is called in the handler to terminate the request-response cycle.
```js
const express = require('express')
const app = express()
const port = 3000

app.get('/', (req, res) => { // (1)
  res.send('Hello World!') // (2)
})

app.listen(port, () => {
  console.log(`Example app listening at http://localhost:${port}`)
})
```
(1) `'/'` (forward slash) is your root directory.
(2) `res.send()` can send back various types of content.

### Returning a static webpage using GET 
As an example, let's create a route to display a contact page in the form of a static HTML page.

1.  Start with the route method and insert the path  
    `app.get('/contact')`
    
2.  Insert an empty handler that has the parameters for the request and response objects  
    `app.get('/', (req, res) => { })`

3.  Insert into the handler function, the action you want to perform.  
    Use `res.sendFile()` to serve a static HTML page.
```js
app.get('/contact', function(req, res) {
  res.sendFile('contact.html');
});
```

### Sending data using POST 
Suppose you have a form on your contact page for users to submit a message. You would use a POST request so that you can retrieve the submitted data and store it somewhere.

For example, we will use the following form.
```html
<form method="POST" action="/submit-form">
  <input type="email" name="email">
  <input type="text" name="message">
  <input type="submit">
</form>
```

1.  Start with the route method and insert the path  
    `app.post('/contact')`
> Note that you can use the same path with different methods to perform different actions
    
2.  Insert an empty handler that has the parameters for the request and response objects  
    `app.post('/contact', (req, res) => { })`

3.  Insert into the handler function, the action you want to perform.  
    Use `res.redirect()` to redirect your user to a confirmation page.
```js
app.post('/contact', function(req, res) {
  const email = req.body.email;
  const message = req.body.message;
  // insert code to do whateever you want with the form data
  res.redirect('confirmation.html');
});
```

## Routers
As the scope of your project grows or scales, you may find the need to organize your routes for ease of maintenance. Express provides a tool to help achieve this called a **Router**.

If you had several related endpoints, it would be more manageable to organize these related routes into their own file. The Express router can help you achieve this by allowing you to export this grouping into your entry point file. The entry point file acts as a main hub to direct requests to the appropriate endpoints.

### Router Example
We will add onto our previous example with the contact page routes. At the moment, these routes are in your entry point file (app.js). We want to move the contact routes to their own file for better organization.

1.  Create a new JavaScript File called "contactRoute.js"
    
2.  Require Express into contactRoute.js and create a new instance of the Router class by storing it to a new variable (`router`).
```js
let express = require('express');
let router = express.Router();
```
    
3.  Cut and paste the two contact routes into contactRoute.js
```js
let express = require('express');
let router = express.Router();

app.get('/contact', function(req, res) {
  res.sendFile('contact.html');
});

app.post('/contact', function(req, res) {
  const email = req.body.email;
  const message = req.body.message;
  // insert code to do whateever you want with the form data
  res.redirect('confirmation.html');
});
```

4.  Change `app` to `router` so that the routes are now associated to this router instance.  
    We can also remove 'contact' from our path as we will no longer need it.
```js
let express = require('express');
let router = express.Router();

router.get('/', function(req, res) {
  res.sendFile('contact.html');
});

router.post('/', function(req, res) {
  const email = req.body.email;
  const message = req.body.message;
  // insert code to do whateever you want with the form data
  res.redirect('confirmation.html');
});
```

5.  Add an export to the end of the file so we can access this router and its associated routes from other files.
```js
let express = require('express');
let router = express.Router();

router.get('/contact', function(req, res) {
  res.sendFile('contact.html');
});

router.post('/contact', function(req, res) {
  const email = req.body.email;
  const message = req.body.message;
  // insert code to do whateever you want with the form data
  res.redirect('confirmation.html');
});

module.exports = router;
```

6.  Import the contact router into our entry point file (app.js).
```js
let express = require('express');
let router = express.Router();

let contactRoute = require('contactRoute');

app.listen(port, () => {
  console.log(`Example app listening at http://localhost:${port}`)
})
```

7.  Use `app.use()` to load the router into the Express app.  
    Paths that start with `/contact` will now be sent to "contactRoute.js" for further routing.
```js
let express = require('express');
let router = express.Router();

let contactRoute = require('contactRoute');

app.use('/contact', contactRoute);

app.listen(port, () => {
  console.log(`Example app listening at http://localhost:${port}`)
})
```
[^1]: [HTTP Request Methods](https://www.w3schools.com/tags/ref_httpmethods.asp).