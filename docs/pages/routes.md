
## Routes

In this section, we will walk you through how to set up the first **routes** for your Express server.

> In Express, a route interprets the **[HTTP request method](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)** made to the server.


**Routing** is the action of determining what information is display or what action is taken when a user navigates or triggers a specified **endpoint** or **path**.

A simple route is comprised of the following components
 
-   `app`: the instance of Express that you have created in [Getting Started](link)
-   `method`:  the Express [route method](https://expressjs.com/en/4x/api.html#app.METHOD) corresponding to HTTP requests (eg. `get`, `post`, or `put`)
-   `path`: the defined endpoint of the request
-   `handler`: the function that is called when the route is hit
```javascript
app.method(path, handler)
```
> The handler will be often be an [anonymous function](https://www.javascripttutorial.net/javascript-anonymous-functions/) written as either a regular function or an [arrow function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)


Steps
1.  Writing basic routes
    

2.  basic route components
    
3.  how to send back content

4.  Introducing a routers
    

5.  new router files in routes folder
    
6.  using the router path