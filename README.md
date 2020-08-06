# NODE APP INSTRUCTIONS AND NODE MODULES

1. Add a .gitignore and place your module folder and any local file in there so it doesn't push to github.
2. Created a directory where I initialized node:
```javascript
npm init -y
```
this uses default options which you can then change later in your package.json.
3. Created two JS files, one to reference in my index locally, and one that references said file.
4. When I get a third party module, you do so like this:
```javascript
npm install chalk
```
in this instance I used chalk, which just gives nice colors to text in your console/terminal!
5. To use chalk, it was quite easy, it created a variable for the console log, and for chalk, then you can log anything using:
```javascript
const chalk = require('chalk');

const log = console.log;

log(chalk.blue('Hello', 'World!', 'Foo', 'bar', 'biz', 'baz'));

log(chalk.green(
    'I am a green line ' +
    chalk.blue.underline.bold('with a blue substring') +
    ' that becomes green again!'
));

log(`
CPU: ${chalk.red('90%')}`);
```
6. To check and make sure my node is working, I can use either:
```javascript
nodemon
or
node index.js
```
nodemon will constantly update my console, where as I have to run node index.js every time to check and make sure it works.

7. You can check all this out at my git hub repo:
[This is my Repo](https://github.com/kinawy/node_modules_practice)

------

# EXPRESS/VIEWS/ROUTES

1. To get express you have to first install it , and it can't hurt to check your package.json to make sure you have the proper dependencies:
```javascript
npm i express
```
2. Then you set a variable inside of your index.js file to store express and the app function inside of:
```javascript

const express = require('express');
const app = express();

```
3. To then set a get route you use app.get, and pass it the URL segement:
```javascript
    app.get('/', (req, res) => { // The / in string there is the url segment, then in the callback you get a request and a response, the response send will tell you this is the home page on the actual page you go to.
    res.send('This is the home page!')
    })
```
4. You then have to listen to a port on your local host:

```javascript
    app.listen(8000, () => {
    console.log('This works')
})
```
------

# TEMPLATES/LAYOUTS/CONTROLLERS

1. Install ejslayouts and ejs for templates and layouts, then express for controllers and check your dependencies to make sure its there:
```javascript
npm i ejs
npm i express
npm i ejs-layouts

const express = require('express');
const app = express();
const ejsLayouts = require('express-ejs-layouts');
```
2. Then set your view engine to ejs and tell it to use ejsLayouts:
```javascript
app.set('view engine', 'ejs')
app.use(ejsLayouts)
```
3. At this point you're using render, to get your pages up and running:
```javascript
app.get('/', (req, res) => {
    res.render('home');
  });
```
4. You then tell your app to require specific folders:
```javascript
app.use('/faves', require('./controllers/faves'));

app.use('/hates', require('./controllers/hates'));
```
5. I then used icecream cones in my layout.ejs to tell it where to insert stuff into the body:
```javascript
<%- body %>
```
6. Then in your other ejs files, you can write in javascript with ice cream cones or squids as you will to execute functions and add stuff to your layout:
```javascript
<h1><%= title %></h1>
<ul>
  <% foods.forEach((food) => { %>
    <li><%= food %></li>
  <% }) %>
</ul>
```
7. Then in your controllers folder, you have js files that do exactly that, control the flow of your ejs files, and keep a cleaner looking code:
```javascript
// Here is where you will tell your router to listen to express and export it through a module, which will then apply this router.get to your specific folders, and use the assigned key value pairs
const express = require('express');
const router = express.Router();


router.get('/foods', (req, res) => {
    res.render('faves/foods', {title: 'Favorite Foods', foods: ['coconut', 'avocado']});
  });
  
router.get('/animals', (req, res) => {
    res.render('faves/animals', {title: 'Favorite Animals', animals: ['sand crab', 'corny joke dog']})
  });

module.exports = router;
```
8. And now I should be able to use these routes to set up a web page!
