## Overview

In this section you will explore the use of [**ESLint**](https://eslint.org/) and [**Prettier**](https://prettier.io/) to standards for writing and formatting code. 
As is common practice, you will use Prettier to handle formatting-related issues and ESLint for non-formatting (code quality) issues - see [Prettier vs. Linters](https://prettier.io/docs/en/comparison.html).
This is particularly important for teams where collaboration is necessary. Using ESLint and Prettier provide many benefits, for instance[^1]:

- Increased Code Consistency
- Better Codebase Coherence
- Detect Problematic Code Patterns
- Easier Code Formatting

Indeed, these benefits are not just limited to development teams, they are equally useful for individuals working on personal projects.
When potential employers look at your GitHub projects, one the first things they look at is the coding style.[^2]

You'll start by installing ESLint and Prettier, then walking through an example of how to start customizing the rules you want to adhere to.

## Installation & Initial Setup

Before you are able to adding code style and formatter rules, you need to install a few packages using the terminal, as outlined below:

!!!error "Prerequisite"
    You will use the `touch` command for creating files via the command line. `touch` is native on Linux and Unix systems. If you are on a Windows machine you can install `touch` globally by running the following command: 
    > npm install touch-cli -g

1. Install Prettier:
>  npm install --save-dev prettier

2. Install ESLint:
>  npm install --save-dev eslint

3. Install relevant ESLint dependencies:
> npm install --save-dev eslint-config-prettier eslint-plugin-prettier


4. Create a `.prettierrc.js` file in the root of the directory:
> touch .prettierrc.js

5. Open the `.prettierrc.js` file created above and add the following formatting rules:

    ``` { .js .annotate }
    
    module.exports = {
        semi: true, // (1)
        tabWidth: 4, // (2)
        singleQuote: true, // (3)
    };
    ```
    
    1. Ensures that semicolons are added at the end of all statements.
    2. Specifies the number of spaces per indentation level to be 4.
    3. Specifies that single quotes  are used instead of double quotes
       
    The rules above are some basic settings suggested by Prettier. Click on the numbers on each line to see what each rule means.
    For a detailed overview of all the possible rules for Prettier, see [Prettier Options](https://prettier.io/docs/en/options.html).


6. Create a `.eslint.js` file in the root of the directory:
> touch .eslint.js


7. Open the `.eslint.js` file created above and add the following:
    
    ``` { .js .annotate }
    
    module.exports = {
        extends: ['prettier'], // (1)
        plugins: ['prettier'], // (2)
        rules: {
            'prettier/prettier': ['error'] // (3)
        },
    };
    ```

    1. Enables the config from `eslint-config-prettier` (Step 3 👆). Turns off some ESLint rules that conflict with Prettier.
    2. Registers `eslint-plugin-prettier` as plugin (Step 3 👆). 
    3. Enable a rule that allows you to use Prettier from within ESLint.
    

!!!info "Development Dependencies"
    In general, *Node* packages that are only required during development, should be installed using the  npm `--save-dev` flag, as shown in step 1 above.


## Customization
Prettier is highly opinionated which means you have much less fine-tuning control over formatting. 
On the other hand, ESLint is much less opinionated and hence provides you with more control relating to code-quality standards.
Thankfully, well-known companies such as Airbnb and Google have written their own code style guides - see [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript) and [Google Java Style Guide](https://google.github.io/styleguide/javaguide.html). 
ESLint allows you to 'extend' or import the rules from either of the code-styles guides mentioned above. 
It is worth noting that there is no hard and fast rule for establishing code-style rules and guidelines. 
As an example, you will use the [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript) as a base config
and add a custom rule for illustrative purposes.

1. Install and save the necessary peer dependencies to use the Airbnb style guide:
> npm install --save-dev eslint-config-airbnb-base eslint-plugin-import

2. Add `'airbnb-base'` to the `extends` array in the `.eslintrc.js` file:
   
    ``` { .js .annotate hl_lines="2"} 
    
    module.exports = {
        extends: ['airbnb-base', 'prettier'], // (1)
        plugins: ['prettier'],
        rules: {
            'prettier/prettier': ['error'] 
        },
    };
    ```
   
    1. Imports preconfigured Airbnb style guide rules.
    
3. Open the `package.json` file in the root directory and add a script called `lint` for running ESLint:

    ``` { .js .annotate hl_lines="4"} 
    
    {
        ...
        "scripts": {
            "lint": "eslint . --fix --ext .js"
        },
        ...
    }
    ```
   
    This script allows you to use `npm run lint` to run the ESLint on all JavaScript files in the project. It also silently fixes any *fixable* issues for you!
    
4. Create a `server.js` file in the root of the directory:
> touch server.js

5. Open `server.js` and log "Hello World" to the console:

    ``` { .js } 
    console.log("Hello World")
    ```
   
6. Run the `lint` script that you added in step 3 above:
> npm run lint


7. Verify that the code is reformatted to be consistent with the rules you added to `.prettierrc.js`:

    ``` { .js } 
    console.log('Hello World');
    ```
   Notice, ESLint has automatically fixed some formatting issues for you. 
   ESLint changed the double quotes around *Hello World* to single quotes and added a semi-colon to the end of the statement.

    !!!warning 
        You may have also noticed that ESLint warns you about the use of the `console`. 
        This is because, by default, the airbnb code style guide that we extended from has chosen to warn developers on the use on the console.
        ESLint makes it very easy to overwrite **any** code-style rules you want. To allow the use of the `console`, see steps 8 & 9 below 👇.
   
8. (Optional) Append a rule to the `.eslintrc.js` file that allows the use of the console:

    ``` { .js .annotate hl_lines="6"} 
    
    module.exports = {
        extends: ['airbnb-base', 'prettier'], 
        plugins: ['prettier'],
        rules: {
            'prettier/prettier': ['error'],
            'no-console': 'off' // (1)
        },
    };
    ```

    1. Allow the use of `console` statements.

8. (Optional) Rerun the `lint` script **and** verify that ESLint no longer shows a warning message: 
> npm run lint

!!!success "Congratulations 👏"
    This is all you need to do to start using ESLint and Prettier in your projects. For a more detailed list of the rules that use for customizing your code style, see [ESLint Rules](https://eslint.org/docs/rules/).


!!!info "Extensions for ESLint and Prettier"
    Thankfully VS Code has extensions for both ESLint and Prettier:

    - [VS Code ESLint Extension](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint): allows you you see ESLint errors while you code (even before running `npm run lint`)
    - [VS Code Prettier Extension](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode):  allows you to format files automatically, everytime you save them.
    
    ESLint and Prettier also support other IDE's and editors:
    - [ESLint Editor Integrations](https://eslint.org/docs/user-guide/integrations)
    - [Prettier Editor Integrations](https://prettier.io/docs/en/editors.html)

## Conclusion

By the end of this section, you will have successfully learned the following:

- [x] The benefits of using tools such as ESLint and Prettier.
- [x] How to install and setup ESLint and Prettier.
- [x] How to customize ESLint.


Great job 🤗. You can go ahead and click on the link below to move on to the next step:

**[Installing Express](installing-express.md)**

[^1]: [Why You Should Use ESLint, Prettier & EditorConfig](https://blog.theodo.com/2019/08/why-you-should-use-eslint-prettier-and-editorconfig-together/).
[^2]: [Enforce your team’s coding style with Prettier and TsLint](https://itnext.io/enforce-your-team-coding-style-with-prettier-and-tslint-9faac5016ce7).
