# Gulp Workflows

* Wouldn't it be nice if there was a way to convert ES6 to code every browser can support? Of course! 
* Wouldn't it be cool if you could include module support from Node in client side code? Certainly.
* What could do this sort of magic for us? *Gulp Tasks*!

## Learning Objectives

By the end of this tutorial, you will understand:
* What Gulp is and what it can do
* How to install Gulp on your computer
* How to write a Gulp task and run it
* How to add use additional modules with Gulp

#### Introducing: Gulp

* Gulp is a software built on Node.
* It runs **tasks** that manipulate files on your system.
* It is an active, open-source project.
* There are many community-built plugins built to work directly with gulp.
* It is commonly used for bundling, minificiation, and ES6 support.
* **Grunt** is a popular alternative to Gulp.

#### Installing Gulp

To install **Gulp**, we should have a Node.js environment prepared. If you do not have one, you should visit [https://nodejs.org/en/](Nodejs.org) to learn more.

1. You'll want to install gulp globally. You can do this by running the `npm install gulp -g` command.
2. This states that we want to use `npm` to install the `gulp` package globally (for any project to use).
3. Gulp requires that we store our tasks in a `gulpfile.js`. This should be in the same directory as your `package.json`.
4. We also need to include gulp in our project. To do that, we will run `npm install gulp --save-dev`.
5. Now, we should run `gulp`! 
6. Oh no - we ran into a problem.

```bash
Using gulpfile ~/path/to/gulpfile.js
Task 'default' is not in your gulpfile
Please check the documentation for proper gulpfile formatting
```

Let's solve this problem by defining a Gulp task.

#### Defining a Gulp Task

#### Project: A Gulp Workflow that supports ES6 and Modules for the Web
