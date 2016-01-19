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
([Source](https://github.com/code-for-coffee/gulp_workflows/blob/master/gulpfile_lo3.js))

In your terminal, run `gulp`. This will have the library look for a `default` task in your `gulpfile.js`. It will then execute the callback that you define for your task. The output will appear as follows:

```bash
Starting 'default'...
I am the default task. Hear me roar
Finished 'default' after 144 μs
```


#### Project: A Gulp Workflow that supports ES6 and Modules for the Web

We're going to include a few external modules to create a Gulp workflow. Our workflow will support:

* Node-style `require()` statements using **Browserify**.
* Support ES6 (ES2016) and JSX (for React.js) using **Babelify** (and a few Babel plugins).
* Compile individual modules together using **vinyl-source-stream**.

We need to install a variety of modules. The installation commands are:
* `npm install --save-dev browserify`
* `npm install --save-dev babelify`
* `npm install --save-dev babel-preset-es2015 babel-preset-react`
* `npm install --save-dev vinyl-source-stream`

We can then add our modules to our `gulpfile.js`:

```javascript
var gulp = require('gulp');
var browserify = require('browserify');
var babelify = require('babelify');
var source = require('vinyl-source-stream');
```

We're all set with our dependencies. Now, it is time to create a file structure for our project. We should create a folder called `source` for our actual Javascript application. We'll create an `app.js` in that source directory. We should also create a `build` folder to contain our final, production-ready Javascript file. 

`touch source/.gitkeep build/.gitkeep source/app.js`

You'll notice that there is currently no file inside of our `build` directory other than a `.gitkeep`. We should define a task that will use the installed modules to transform our code and make it usable on the front-end. We should update our `gulpfile.js`'s **default** task.

```javascript
gulp.task('default', function() {
  return browserify('./source/app.js')
        .transform("babelify", {presets: ["es2015", "react"]})
        .bundle()
        .pipe(source('build.js'))
        .pipe(gulp.dest('./build/'))
});
```

Let's identify what is going on inside of our **default** task: 
* The task uses **browserify** to include our modules that are required in our `source/app.js` file.
* It then transforms any ES6 (ES2015) and React JSX templates into usable code on the client side. This usually translates our modern Javascript code into ES5 that most current evergreen browsers support.
* The task then bundles our files together.
* Next, the task creates a file called `build.js`.
* Gulp finally places the `build.js` inside of a destination (`dest`) folder of `build/`.
* [The full version of this Gulpfile.js may be found here](https://github.com/code-for-coffee/gulp_workflows/blob/master/gulfpile_lo4.js).

Run `gulp` in your terminal. Inspect the `build/build.js` file. *What do you see?*

##### Verifying that everything works

Let's write some ES6. We'll then use **gulp** to run tasks that will create a file prepared for the client side. To verify everything works, we can run the script generated in the console.

In my `app.js`, I want todefine an ES6 class called HelloWorld. The class should have a toString() method that returns 'Hello, world!'. I will then instantiate a new instance of the class and console log the `toString()` method that it contains. 

```javascript
// define an ES6 class called HelloWorld
class HelloWorld {
  // define a toString() method on the class
  toString() {
    return 'Hello, world!';
  }
}
// instantiate a new instance of HelloWorld
var sample = new HelloWorld();
// console.log sample's toString() method
console.log(sample.toString());
```
([Source](https://github.com/code-for-coffee/gulp_workflows/blob/master/app.js))

Now, we should run `gulp` in the terminal. Upon completion, open the `build/build.js` file. It will contain a large amount of obfuscated code such as `(function e(t,n,r){function s(o,u)....`. Copy and paste this code into a browser's Javascript console. Inside the console, you should see `Hello, world!`. 

##### Tips and Tricks

* You will need to re-run the `gulp` command every time you make a change.
* There is `nodemon` support for gulp.
* You can have `gulp` **watch** files for changes using [gulp-watch](https://www.npmjs.com/package/gulp-watch).



