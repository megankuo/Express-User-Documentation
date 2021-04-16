# Overview

This section will focus on helping you set up an [**Express.js**](https://expressjs.com/) (or informally known as *Express*).
It is a web application framework for [**Node.js**](https://nodejs.org/) that is free and open-source. 
Express is used to provide server-side logic for web and mobile applications.

## Installation Steps for Express

In the introduction, you will have created a new project folder with all of the subfolders and subfolders required. First, we'll install express and any dependencies, and then walk you through how to create an Express server, so you can serve content to your front-end (browser).

1. Install [`nodemon`](https://github.com/remy/nodemon):
    > npm install --save-dev nodemon

2. Install Express:
    > npm install express

3. Create a `src` folder in the root directory:
    > mkdir src

4. Create an `app.js` file in the `src` directory:
    > touch src/app.js


5. Open the `app.js` file created above and add the following code:

    ``` { .js .annotate} 
    const express = require('express'); // (1)
    const app = express(); // (2)
    const port = 3000; // (3)
      
    app.get('/', (req, res) => { // (4)
        res.send('Hello World!');
    });
      
    module.exports = app; // (5)
    ```

    1. This line of code will import the express module into your app.js entry point file.
    2. This line of code will create a new Express application.
    3. This line of code will store the number of the port that we will be using to connect to your localhost.
    4. The GET method route will allow our application to send the string "Hello World!" as a response when we connect to our localhost. You will be learning more about HTTP methods like GET in a later section.
    5. Export the Express application so that `server.js` can use it.
   

6. Create an `server.js` file in the root directory:
    > touch server.js


7. Open the `server.js` file created above and add the following code:

      ``` { .js .annotate }
      const app = require('./src/app'); // (1)
      
      const port = 3000; // (2)
      
      app.listen(port, () => { // (3)
          console.log(`🚀 Server started successfully, listening on port ${port}: http://localhost:${port}`);
      });
      
      ```
      
      1. Import instance of Express Application created in `src/app.js`.
      2. Specify port number for server to listen on.
      3. Start server and listen on specified port.
   
## Start Express Server

In this last section, you will learn how to run your Express server on your **localhost**. You will be able to see the string "Hello World" from earlier in your internet browser by visiting your localhost:3000.

1. Open the `package.json` file in the root directory and add a script to start Express:

    ``` { .js .annotate hl_lines="4"} 
    
    {
        ...
        "scripts": {
            "start": "nodemon server.js", // (1)
            "lint": "eslint . --fix --ext .js"
        },
        ...
    }
    ```
   
    1. This script allows you to use `npm run start` or `npm start` to start the Express server.

2. Run the script create above to start the Express server:
> npm start

3. Open your internet browser of choice and type in the URL for the Express server:
    > [localhost:3000](http://localhost:3000)

!!!success
    
    Once the page loads, you should see "Hello World!" in your browser.
    This means that you have successfully installed and created your first working server!

[comment]: <> (    ![Express Success]&#40;images/installing-express-step3b.png&#41;{ align=left })


## Conclusion

By the end of this section, you will have successfully learned the following:

- [x] How to install Express
- [x] How to create a working Express server on your localhost

Great job 🤗. You can go ahead and click on the link below to move on to the next step:

**[Adding Routes](/pages/routes)**