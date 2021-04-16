# Project Structure

When working on a project, it is important to have a clear project structure. Although the importance of having a project structure may seem insignificant when working on a small project, programmers and engineers will often collaborate with each other to write thousands of lines of code. It would be pure chaos if there was no defined project structure to keep all of your code organized. On top of this, troubleshooting issues and implementing new features would be a nightmare.

!!! Info "Model-view-Controller (MVC)"
    An MVC is a sotware design pattern that is used to divide all related program logic into three core logical components called the **Model**, **View**, and **Controller**.
    The Controller is used to control what View is displayed while using the Model to provide data for the View to render.

## Current Folder Structure

In the introduction section, you will have created a new project folder with the following folders and files structure:

```bash
|-- project-name              # Root Directory
    |-- node_modules/         # Downloaded Libraries
    |-- .eslintrc.js          # Linting Rules 
    |-- .prettierrc.js        # Code Formatting Rules
    |-- package.json          # Metadata and Package List
    |-- package-lock.json     # Version Number for Dependencies
```

## Create a Subfolder

In this section you will create a subfolder. Folders that are created inside of the root folder (also known as *root directory* or *root*) of your project are called subfolders. Subfolders can also contain their own subfolders and so forth. It is recommended that you do not use more than three or four levels to keep your project organized.

1. Type the command below in the Terminal to create a docs folder.
   > mkdir src

   If successful, you should see a new folder inside of your project folder in the Explorer Tab in VSC like the example below.

    ```bash
    |-- project-name
        |-- src/ # Source (src) Will Contain Working Files
        |-- node_modules/
        |-- .eslintrc.js
        |-- .prettierrc.js
        |-- package.json
        |-- package-lock.json
    ```

## Create Nested Subfolders

After you have created your first subfolder in the project, we will be creating more folders inside of the src folder. The newly created folders are called nested subfolders.

1. Type the command below to move into your src directory.
   > cd src

2. Type each line of the commands below to create all of the nested subfolders that you will need.
   > mkdir api

   > mkdir config

   > mkdir db

   > mkdir models

   > mkdir services

   > mkdir utils

   > mkdir views

    Once you have created all of the folders then you will see the folder structure from the example below.

    ```bash
    |-- project-name              # Root Directory
        |-- src/
        |   |-- api/              # Application Programming Interfaces
        |   |-- config/           # Configuration/Settings Files
        |   |-- db/               # Mock Database or Connection to Database
        |   |-- models/           # Database Models
        |   |-- services/         # Services Layer for Business Logic (Talks to Database)
        |   |-- utils/            # Miscellaneous Helper Functions
        |   |-- views/            # Static Template Files (EJS, Pug, or Mustache)
        |-- node_modules/
        |-- .eslintrc.js
        |-- .prettierrc.js
        |-- package.json
        |-- package-lock.json
        |-- README.md
    ```

3. Type the command below to move into your api directory.
   > cd api

4. Type each line of the commands below to create all of the nested subfolders that you will need.
   > mkdir controllers
   > mkdir middleware
   > mkdir routes

   If successful your folder structure should resemble the folder structure below:

    ```bash
    |-- project-name
        |-- src/
        |   |-- api/
        |   |   |-- controllers/  # Request Managers
        |   |   |-- middleware/   # Intermediary b/w Client Request & Server Response
        |   |   |-- routes/       # API Endpoints (URIs)
        |   |-- config/
        |   |-- db/
        |   |-- models/
        |   |-- services/
        |   |-- utils/
        |   |-- views/
        |-- node_modules/
        |-- .eslintrc.js
        |-- .prettierrc.js
        |-- package.json
        |-- package-lock.json
        |-- README.md
    ```

## Conclusion

By the end of this section, you will have successfully learned the following:

- [x] Why project stucture is important.
- [x]How to organize the subfolders.
- [x]How to organize nested subfolders.
- [x]How to organize the folders inside of the public folder.

Congratulations! 🎉 You can go ahead and click on the link below to learn more about how to configure your project:

**[Configuration](/pages/config)**
