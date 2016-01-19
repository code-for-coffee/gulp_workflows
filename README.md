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

* What is a task?
* A task is something we must do to achieve a result.
* In Gulp, we create tasks to perform tasks that can transform our code.
* A task may perform one job; it may also perform many at once.

In our `gulpfile.js` we need to include the `gulp` module. To do this, we should define a variable: `var gulp = require('gulp');` This will allow us to call upon Gulp to **create a task**.

##### My First (Default) Task

After declaring our `gulp` variable, we should create our first task. This will require us to call upon Gulp to define a task. We must also have a name for our task. By *default*, Gulp requires a `default` task. It is the first task that Gulp will look for when reading your `gulpfile.js`. Let's define our first (default) task:

```javascript
var gulp = require('gulp');

//define a task with the name of 'default' 
// and a callback to perform when the task is ran
gulp.task('default', function() {
  console.log('I am the default task. Hear me roar');
});
```
[https://github.com/code-for-coffee/gulp_workflows/blob/master/gulpfile_lo3.js](Source)

In your terminal, run `gulp`. This will have the library look for a `default` task in your `gulpfile.js`. It will then execute the callback that you define for your task. The output will appear as follows:

```bash
Starting 'default'...
I am the default task. Hear me roar
Finished 'default' after 144 μs
```


#### Project: A Gulp Workflow that supports ES6 and Modules for the Web
