## Overview

When working on a project, it is important to have a clear project structure. Although the importance of having a project structure may seem insignificant when working on a small project, programmers and engineers will often collaborate with each other to write thousands of lines of code. It would be pure chaos if there was no defined project structure to keep all of your code organized. On top of this, troubleshooting issues and implementing new features would be a nightmare.

!!! Info "Model-view-Controller (MVC)"
    An MVC is a sotware design pattern that is used to divide all related program logic into three core logical components called the **Model**, **View**, and **Controller**.
    The Controller is used to control what View is displayed while using the Model to provide data for the View to render.

In this guide we will be using this project structure to guide you towards creating a small to medium sized project. As your project grows larger, you will want to modify and personalize your project as you find is necessary.

Please refer to the example below to see the overview of the project structure:

```bash
    |-- project-name              # Root Directory
        |-- src/                  # Application Programming Interfaces
        |   |-- api/              # API Endpoints (URIs)
        |   |   |-- routes/       # API Endpoitns (URIs)
        |   |   |   |--app.js     # Entry Point File
        |-- node_modules/         # Downloaded Libraries
        |-- .eslintrc.js          # Linting Rules 
        |-- .prettierrc.js        # Code Formatting Rules
        |-- package.json          # Metadata and Package List
        |-- package-lock.json     # Version Number for Dependencies
        |-- server.js             # Server File
```

## Create a Subfolder

Before we get started, you will want to create a folder where you will store your new express project. This folder is called the root folder (also known as *root directory* or *root*). In this section, you will be creating the subfolder structure for your project. Folders created inside of the root folder are called subfolders.

Go ahead and up your project in [**Visual Studio Code**](https://code.visualstudio.com/).

1. Type the command below in the Terminal to create a docs folder.

    > mkdir src

    If successful, you will see a new folder inside of your project folder in the Explorer Tab in VSC. The file will resemble the example below.

    ```bash
    |-- project-name
        |-- node_modules/
        |-- src/
        |   |-- api/
        |   |   |-- routes/       # API Endpoints (URIs)
        |-- .eslintrc.js
        |-- .prettierrc.js
        |-- package.json
        |-- package-lock.json
    ```

## Create Nested Subfolders

After you have created your first subfolder in the project, we will be creating more folders inside of the src folder. The newly created folders are called nested subfolders. The source (src) folder will contain all of the files needed to build your project.

1. Type the command below to move into your src directory.

    > cd src

2. Type each line of the commands below to create all of the nested subfolders that you will need.

    > mkdir api

3. Type the command below to move into your api directory.

    > cd api

4. Type each line of the commands below to create all of the nested subfolders that you will need.

    > mkdir routes

    If successful your folder structure should resemble the folder structure below:

    ```bash
    |-- project-name
        |-- node_modules/
        |-- src/
        |   |-- api/
        |   |   |-- routes/       # API Endpoints (URIs)
        |-- .eslintrc.js
        |-- .prettierrc.js
        |-- package.json
        |-- package-lock.json
    ```

    !!! Info "Medium to Large Projects"
        Here is an example of a medium to larger scaled project. You can choose what kinds of folders will be required for your personalized project.

        ```bash
        |-- project-name
            |-- node_modules/
            |-- public/
            |   |-- images/
            |   |-- js/
            |   |-- styles/
            |-- src/
            |   |-- api/
            |   |   |-- controllers/
            |   |   |-- middleware/
            |   |   |-- routes/
            |   |-- config/
            |   |-- db/
            |   |-- models/
            |   |-- services/
            |   |-- utils/
            |   |-- views/
            |-- .eslintrc.js
            |-- .prettierrc.js
            |-- package.json
            |-- package-lock.json
        ```

    !!! Info "Test Subfolder Recommendation"
        Another folder that we highly recommend creating is a test subfolder. As your projects get bigger, you will find that testing your applications will make it easier to maintain your code. Although it is not always necessary for smaller projects, it is considered good practice to use test suites to test your application.

## Conclusion

By the end of this section, you will have successfully learned the following:

- [x] Why project stucture is important
- [x] How to organize the subfolders
- [x] How to organize nested subfolders

Congratulations! 🎉 You can go ahead and click on the link below to learn more about how to configure your project:

**[Configuration](/pages/configuration)**
