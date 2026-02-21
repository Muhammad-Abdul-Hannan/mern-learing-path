# 🚀 Express.js Learning Notes

These notes summarize what I learned about Express.js while continuing my MERN stack journey.

---

# 1️⃣ What is Express.js?

Express.js is a web framework built on top of Node.js.

It helps you:
- Build web servers
- Create REST APIs
- Handle routing
- Manage middleware
- Serve static files easily

It simplifies backend development compared to using pure Node.js.

---

# 2️⃣ Installation & Basic Setup

Make sure:
- Node.js is installed
- Project is initialized using `npm init`

Install Express:

```bash
npm install express
```

---

# 3️⃣ Creating a Basic Server

### app.js

```js
const express = require('express');
const app = express();

app.get('/', (req, res) => {
    res.send("App is running");
});

module.exports = app;
```

---

### server.js

```js
const app = require('./app');

const PORT = 5000;

app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

---

### package.json script

```json
"scripts": {
  "dev": "nodemon server.js"
}
```

If nodemon is not installed:

```json
"dev": "node server.js"
```

Run server:

```bash
npm run dev
```

Open:

```
http://localhost:5000/
```

Output:

```
App is running
```

---

# 4️⃣ Routing

Routing determines how an application responds to a client request at a specific endpoint.

Syntax:

```js
app.METHOD(PATH, HANDLER)
```

Where:
- app → Express instance
- METHOD → HTTP method (get, post, put, delete, etc.)
- PATH → Route path
- HANDLER → Function executed when route matches

Example:

```js
app.get('/about', (req, res) => {
    res.send('About Page');
});
```

---

## app.all()

Handles all HTTP methods for a path.

```js
app.all('/secret', (req, res, next) => {
  console.log('Accessing secret section...');
  next();
});
```

---

# 5️⃣ Route Parameters

Route parameters capture values from the URL.

Example:

```js
app.get('/users/:userId/books/:bookId', (req, res) => {
  res.send(req.params);
});
```

URL:

```
/users/34/books/8989
```

Output:

```json
{ "userId": "34", "bookId": "8989" }
```

---

## Using Hyphen and Dot

Hyphen:

```
/flights/:from-:to
```

Example:

```
/flights/LAX-SFO
```

Output:

```json
{ "from": "LAX", "to": "SFO" }
```

Dot:

```
/plantae/:genus.:species
```

Example:

```
/plantae/Prunus.persica
```

Output:

```json
{ "genus": "Prunus", "species": "persica" }
```

---

# 6️⃣ Route Handlers & Multiple Callbacks

A route can have multiple middleware functions.

Example:

```js
app.get('/example',
  (req, res, next) => {
    console.log('First');
    next();
  },
  (req, res) => {
    res.send('Second');
  }
);
```

---

## Skipping to Next Route

```js
app.get('/user/:id', (req, res, next) => {
  if (req.params.id === '0') {
    return next('route');
  }
  res.send(`User ${req.params.id}`);
});

app.get('/user/:id', (req, res) => {
  res.send('Special handler for user ID 0');
});
```

---

## Array of Callbacks

```js
const cb0 = (req, res, next) => { console.log('CB0'); next(); };
const cb1 = (req, res, next) => { console.log('CB1'); next(); };
const cb2 = (req, res) => { res.send('Hello from C!'); };

app.get('/example/c', [cb0, cb1, cb2]);
```

---

# 7️⃣ Serving Static Files

To serve images, CSS, JS files:

```js
app.use(express.static('public'));
```

If `img1.png` exists inside `public`:

```
http://localhost:5000/img1.png
```

Add prefix:

```js
app.use('/static', express.static('public'));
```

---

# 8️⃣ Response Methods

Common response methods:

| Method | Description |
|--------|------------|
| res.send() | Send response |
| res.json() | Send JSON response |
| res.redirect() | Redirect request |
| res.render() | Render template |
| res.sendFile() | Send file |
| res.download() | Download file |
| res.sendStatus() | Send status code |

Example:

```js
res.status(200).json({ message: "Success" });
```

---

# 9️⃣ app.route()

Chain multiple HTTP methods for same route.

```js
app.route('/book')
  .get((req, res) => {
    res.send('Get a book');
  })
  .post((req, res) => {
    res.send('Add a book');
  })
  .put((req, res) => {
    res.send('Update a book');
  });
```

---

# 🔟 express.Router (Modular Routing)

`express.Router()` creates modular route files (mini-app).

---

## test.routes.js

```js
const express = require('express');
const router = express.Router();

const authorize = (req, res, next) => {
    console.log('Authorized');
    next();
};

router.get('/', authorize, (req, res) => {
    res.send('I am main of birds');
});

router.get('/user/:userid', (req, res) => {
    res.send(`Bird user ${req.params.userid}`);
});

module.exports = router;
```

---

## Using Router in app.js

```js
const express = require('express');
const app = express();

const birdRoute = require('./routes/test.routes');

app.use('/birds', birdRoute);

app.get('/', (req, res) => {
    res.send('I am home page');
});

module.exports = app;
```

Now accessible routes:

```
/birds
/birds/user/5
```

---

# 📌 Summary

Today I learned:
- Express basics
- Creating server
- Routing system
- Route parameters
- Multiple route handlers
- Static file serving
- Response methods
- app.route()
- express.Router for modular routing

This strengthens my backend foundation for MERN stack development.