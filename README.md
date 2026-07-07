# MEN STACK NOTES

| CRUD Action | RESTful Action | HTTP Method | Definition |
| ----------- | -------------- | ----------- | ------------------------ |
|  | `new` | `GET` | Show a form to create a new item |
| Create | `create` | `POST` | Add a new item to the database |
| Read | `index` | `GET` | Show all items |
| Read | `show` | `GET` | Show one specific item |
|  | `edit` | `GET` | Show a form to edit an existing item |
| Update | `update` | `PUT` | Save changes to an existing item |
| Delete | `delete` | `DELETE` | Remove an item from the database |


## SETUP

- create a directory
- create server file `touch server.js`
- create a `.gitignore` file
- initialize a node project with `npm init -y`
- install express & morgan `npm i express morgan`

### ADD `node_modules` to `gitignore`

.gitignore
```bash
node_modules
```

  ### Write Server Boilerplate

server.js

```js
const express = require('express')
const morgan = require('morgan')
const app = express()

app.use(morgan('dev'));

app.listen(3000, () => {
  console.log('Listening on port 3000')
})
  ```

Run the server with `nodemon server.js`

Navigate to `http://localhost:3000` to view our server.

Use `Ctrl + c` to stop the server in the terminal.

## Creating a Test route

```js
app.get('/test', (req, res) => {
    res.send('<h1>This is a test</h1>')
})
```

### Using request paramenters

```js
app.get('/greet/:name', (req, res) => {
  res.send(`Hello, ${req.params.name}`);
  console.log(req.params)
});
```

Navigate to `http//localhost:300/greet/name`

## Rendering EJS

-install EJS with `npm i ejs`
-Create a views directory with `mkdir views`
-create an EJS file with `touch home.ejs`
-add HTML boilerplate with `!`

home.ejs
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Home</title>
</head>
<body>
  <h1>We are rendering an EJS page!</h1>
</body>
</html>

```

-Render EJS page using a controller like this one:

```js
app.get('/', (req, res) => {
    res.render('home.ejs')
})
```


<img width="845" height="576" alt="image" src="https://github.com/user-attachments/assets/aebb6937-bf9a-43dd-90e5-f05f01608679" />

### EJS Syntax

To use JavaScript in an EJS file, you need a scriplet tag:

```ejs
<% let user = Aziz %>
```

To display JavaScript values from an EJS file, you need an output tag: 

```ejs
<%= user %>
```

home.ejs
```ejs
    <title>
        <%= title %>
    </title>
```

## Using `forEach` in `ejs`

```ejs
<ul>
  <% inventory.forEach((item) => { %>
      <li><%= item.name %>: <%= item.qty %></li>
    <% }); %>
</ul>
```

### Creating dynamic links to a `show` page

`item.name` is dynamically showing up. The link is also dynamically changing with the item.

```ejs
<a href="<%=item.id %>"> <%= item.name %> </a>
```
We should see the URl change in the browser.

### Reusable Nav bar with partials

-Create a folder called `partials` inside of `views`
-Create a file called `nav.ejs` inside of `partials`

should include the opening `html`, `head`, and `body` tags:

```ejs
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title><%= title %></title>
    <link rel="stylesheet" href="/stylesheets/style.css">
</head>
<body>
    <nav>
        <a href="/">Home</a>
    </nav>

```

Indlude the `nav` in other files with this statement: 

```ejs
<%- include('./partials/nav') %>
```
### Adding CSS & images with `public`

-Create a folder called `public`
-Create a folder called `stylesheets` inside of `public`
-Create a file called `style.css` inside of `stylesheets`

Configure our server to look inside of the `public` folder for static files:

```js
//require the path from node at the top
const path = require('path')

//use static middleware with other middleware like morgan
app.use(express.static(path.join(__dirname, "public")))
```

- Link the stylesheet in the head of our `html` files (inside `nav` partial if we're using partials)

```ejs
<link rel="stylesheet" href="/stylesheets/style.css">
```

### Images

- Create an `images` folder inside of our `public` folder
- Link to images like normal: `    <img src="images\pexels-maryia-babuchenka-1765269573-36967061.jpg" alt="">
`
