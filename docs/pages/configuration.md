## Overview

In this section you will explore the use of [**ESLint**](https://eslint.org/) and [**Prettier**](https://prettier.io/) to help establish rules and standards for writing and formatting code. 
This is particularly important for teams where several developers must collaborate to build a product. Using ESLint and Prettier provides many benefits, for instance[^1]:

- Increased Code Consistency
- Better Codebase Coherence
- Detect Problematic Code Patterns
- Easier Code Formatting

Indeed, these benefits are not just limited to development teams, they are equally useful for individuals working on personal projects.
When potential employers look at you GitHub projects, one the first things they look at is the coding style.[^2]

You'll start by installing ESLint and Prettier, then walking through an example of how to start adding rules.

## Installation & Initial Setup

Before you are able to adding code style and formatter rules, you need to install a few packages using the terminal, as outlined below:

!!!error "Prerequisite"
    You will use the `touch` command for creating file from the command line, which is native on Linux and Unix systems. If you are on a Windows machine you can install `touch` globally by running the following command: 
    > npm install touch-cli -g

1. Install Prettier.
>  npm install --save-dev prettier

2. Install ESLint.
>  npm install --save-dev eslint

3. Install relevant ESLint dependencies.
> npm install --save-dev eslint-config-prettier eslint-plugin-prettier

4. Create a `.prettierrc.js` file in the root of the directory.
> touch .prettierrc.js

5. Open the `.prettierrc.js` file created above and add the following formatting rules:
    ```js
    module.exports = {
        semi: true,
        tabWidth: 4,
        printWidth: 80,
        singleQuote: true,
        trailingComma: "es5",
    };
    ```

5. Create a `.eslint.js` file in the root of the directory.
> touch .eslint.js

6. Open the `.eslint.js` file created above and add the following:
    ```js
    module.exports = {
        extends: 'airbnb-base',
        env: {
            commonjs: true,
            node: true,
        },
        rules: {
            indent: ['error', 4],
        },
    };
    ```

!!!info "Development Dependencies"
    In general, Node packages that are only required during development, should be installed using the  npm `--save-dev` flag, as shown in step 1 above.


## Customization
At this stage the rules you have defined for both

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


This

[^1]: [Why You Should Use ESLint, Prettier & EditorConfig](https://blog.theodo.com/2019/08/why-you-should-use-eslint-prettier-and-editorconfig-together/).
[^2]: [Enforce your team’s coding style with Prettier and TsLint](https://itnext.io/enforce-your-team-coding-style-with-prettier-and-tslint-9faac5016ce7).
