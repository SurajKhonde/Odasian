```js
const express =require('express');
const cors = require('cors');
const bodyParser = require("body-parser");
const app = express(); 
const port = 8080;
app.use(cors());
app.use(bodyParser.urlencoded({ extended: true }));
app.use(bodyParser.json());
app.use(function (req, res, next) {
res.setHeader("Access-Control-Allow-Origin", "*");
res.setHeader(
"Access-Control-Allow-Methods",
"GET, POST, OPTIONS, PUT, PATCH, DELETE"
);
res.setHeader("Access-Control-Allow-Headers", "*");
res.setHeader("Access-Control-Allow-Credentials", true);
next();
});
app.get('/',(res,req)=>{
res.json('server is on stage sab changa si  ')
})
const server = app.listen(port, () =>
console.log(`Server up and running on port ${port} !`)
);
```
### `express`
```js
const express = require('express');
const app = express(); // <-- app uses application prototype
```
###### Important methods:

| Method                 | Purpose                                     |
| ---------------------- | ------------------------------------------- |
| `use()`                | Mount middleware                            |
| `get()`, `post()` etc. | Define route handlers                       |
| `listen()`             | Start the server                            |
| `set()`, `get()`       | Set app-level settings                      |
| `route()`              | Create route handlers using method chaining |
| `engine()`             | Register view engines                       |
| `render()`             | Render views (if using templates)           |
##### 2. request (Prototype of req object)
```js
app.get('/', (req, res) => {
  console.log(req.method);     // GET
  console.log(req.url);        // '/'
});
```
###### Important methods/properties:

| Method/Property | Purpose                             |
| --------------- | ----------------------------------- |
| `req.get()`     | Get headers                         |
| `req.query`     | Get query parameters                |
| `req.body`      | Get POST data (after `body-parser`) |
| `req.params`    | URL params like `/user/:id`         |
| `req.ip`        | Request IP                          |
| `req.protocol`  | `http` or `https`                   |
| `req.path`      | Request path without query          |

##### 3. response (Prototype of res object)
```js
app.get('/', (req, res) => {
  res.status(200).json({ message: 'Hello' });
});
```
###### Key methods:

| Method           | Purpose                   |
| ---------------- | ------------------------- |
| `res.status()`   | Set HTTP status           |
| `res.send()`     | Send text or HTML         |
| `res.json()`     | Send JSON                 |
| `res.sendFile()` | Send a file               |
| `res.download()` | Prompt file download      |
| `res.redirect()` | Redirect to another route |
| `res.cookie()`   | Set cookies               |
| `res.set()`      | Set headers               |
##### 4. HTTP Methods
| Method         | Usage                               |
| -------------- | ----------------------------------- |
| `app.get()`    | Handle GET requests                 |
| `app.post()`   | Handle POST requests                |
| `app.put()`    | Handle PUT (update)                 |
| `app.delete()` | Handle DELETE                       |
| `app.all()`    | Handle all HTTP methods for a route |
#####  5. Router and Route
```js
const router = express.Router();
router.get('/user', (req, res) => {
  res.send('User route');
});
```

##### 6. static
This is used to serve static files like images, CSS, and JS:
```js
app.use(express.static('public'));
```


### `const cors =reqiure('cors')`
`cors()` is a middleware from the `CORS` package that helps your server control who can access its resources (like APIs) from other origins (domains, ports, protocols).
By default, browsers **block** frontend JavaScript from calling a different domain's API unless that API **explicitly allows it** using **CORS headers**.
#### Basic Allow-All:
```js
const cors = require('cors');
app.use(cors());
```
This allows **any origin** to access your server — useful for development but **not safe for production**.
#### Allow Only One `Origin` for All Routes
```js
const cors = require('cors');
const corsOptions = {
  origin: 'http://192.168.1.5:3000', // only allow this origin
  methods: ['GET', 'POST', 'PUT', 'DELETE'], // allowed HTTP methods
  credentials: true // allow cookies if needed
};
app.use(cors(corsOptions));
```
#### Make Some Routes Private to Certain `IPs`
You can **write your own IP-check middleware** for special routes:
``` js 
function restrictToIP(allowedIP) {
  return function (req, res, next) {
    const ip = req.ip || req.connection.remoteAddress;

    if (ip.includes(allowedIP)) {
      next();
    } else {
      res.status(403).json({ message: 'Access denied from your IP.' });
    }
  };
}
```
###### Use It on Specific Routes:
```js
app.get('/private-data', restrictToIP('192.168.1.5'), (req, res) => {
  res.json({ secret: '42' });
});
```
![[Pasted image 20250508145128.png]]
### `const bodyParser = require("body-parser");`
Body parser is a middleware for Node.js that parses incoming request bodies and makes them available as objects in the `req.body` property. This is crucial for handling data submitted through HTML forms, JSON data, and other formats.
##### Key Features:
- **Parses various data formats:** Body parser can handle various data formats, including JSON, URL-encoded forms, and multipart/form-data.
- **Provides convenient access:** The parsed data is readily available in the `req.body` object, making it easy to access and use in your application.
- **Customizable:** You can configure body parser to handle specific data formats and set size limits.
```js
const bodyParser = require('body-parser');
console.log(bodyParser,'----------------------__>0001')
[Function: bodyParser] {
  json: [Getter],
  raw: [Getter],
  text: [Getter],
  urlencoded: [Getter]
}
```
##### Purpose of Each
These are **middleware functions** to parse incoming request bodies:

| Method                                      | Purpose                                                                          |
| ------------------------------------------- | -------------------------------------------------------------------------------- |
| `bodyParser.json()`                         | Parses JSON payload (e.g. React frontend sends `Content-Type: application/json`) |
| `bodyParser.urlencoded({ extended: true })` | Parses form data like `name=value&age=25` (from `<form>`)                        |
| `bodyParser.text()`                         | Parses plain text (like `Content-Type: text/plain`)                              |
| `bodyParser.raw()`                          | Parses binary/raw data (e.g., images, buffers)                                   |
###### Or if you're using Express v4.16+:
```js
app.use(express.json());
app.use(express.urlencoded({ extended: true }));
```
Express has these built in now, so you don’t strictly need to install `body-parser` separately.