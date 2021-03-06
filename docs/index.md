# Introduction

Welcome! 👋 This documentation will guide you through setting up a [**Node.js**](https://nodejs.org/) project for building small to medium-scale RESTful APIs using [**Express.js**](https://expressjs.com/).
The aim is to provide a sustainable structure that simplifies complex projects into smaller, more reusable, and modular components.
We will also focus on best practices and various ways to optimize workflow when working collaboratively.

> :fontawesome-brands-node-js:{ .node-js } [**Node.js**](https://nodejs.org/) (or informally *Node*) is an open-source, cross-platform runtime environment that allows developers to run JavaScript on the server. Node provides an environment to run scripts server-side to produce dynamic web content for the client.
>
> [**Express.js**](https://expressjs.com/) is an unopinionated and fairly minimalist *Node* web framework that provides a robust set of features to develop production-ready web and mobile applications.

## Intended Users

This documentation is targeted towards the following users:

- Beginner to intermediate developers who need to setup a backend for a personal project.
- Software development teams working on small or medium-sized web applications.

## Prerequisite Knowledge

The documentation assumes the following:

- Working knowledge of JavaScript([ES6](https://262.ecma-international.org/6.0/)), HTML, CSS - you are expected to know how to write basic HTML and CSS to make a simple static website.
- Ability to use the terminal to run simple commands. 
- Working knowledge of Node.js - you should be familiar with using a package manager such as [`npm`](https://www.npmjs.com/) or [`yarn`](https://yarnpkg.com/) to install Node.js packages or modules.

## Software Requirements

Before proceeding, ensure you have the following installed:

- [**Node.js**](https://nodejs.org/en/) v14.x or later
- [**Npm Package Manager**](https://www.npmjs.com/get-npm) v7.x or later
- [**Visual Studio Code**](https://code.visualstudio.com/download)

> Although the screenshots provided will be from VS Code, *most* of the instructions in this documentation are independent of your IDE.
> IDEs such as [Visual Studio](https://visualstudio.microsoft.com/), [WebStorm](https://www.jetbrains.com/webstorm/), and [Atom](https://atom.io/) are also viable alternatives.

## Procedures Overview

The main sections of the documentation are summarized below:

- **[Elaboration on Project Structure](pages/project-structure)**
- **[Configuring Project for Collaboration](pages/configuration)**
- **[Installing Express.js](pages/installing-express)**
- **[Adding Routes](pages/routes)**
- **[Middleware](pages/middleware)**


## Typographical Conventions
1. Some code snippets may have clickable numbers that can be useful 
if you do not understand what a specific piece of code does. 
   See an example of this below:

    ``` { .js .annotate }
    const sum = (numbers) => {
        return numbers.reduce((a, b) => a + b, 0); // (1)
    };
    ```
    
    1. Return the sum of the numbers in the list.
    
2. Changes to a previously created files will be highlighted in yellow:

    ``` { .js .annotate hl_lines="2"}
    const sum = (numbers) => {
        const multiplier = 2;
        return numbers.reduce((a, b) => multiplier * (a + b), 0);
    };
    ```
   
3. File names and npm packages will be formatted like: `somefile.js`.

4. Instructions that require you to run a command in terminal will be formatted like:
> run some command in the terminal



## Notes and Warning Messages

Throughout the documentation, we will use message blocks to alert you to relevant information. 
Each possible message block, from most important to least important:

!!! danger
    Specifies actions that may cause an error or will cause the application to crash.

[comment]: <> (!!! failure)

[comment]: <> (    Specifies actions that may lead to unexpected behaviour.)

[comment]: <> (!!! bug)

[comment]: <> (    Specifies actions that may cause an error.)

!!! warning
    Specifies content that must be read before proceeding.

!!! Info
    Indicates additional information or tips.

!!! success
    Indicates what success looks like.
