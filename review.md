# Midterm Reviews

## Values, Types, and operators

### Types of data in javascript:

```js
Undefined -> typeof returns underfined
Null -> typeof returns object
Boolean -> boolean
string -> string
Number -> number
Object (functions)-> object
Symbol -> symbol

Booleans, numbers, strings, null, undefined -> primitives (immutable, compared by value)

Object is compared by references
```

```js
// OBJECTS
console.log({} === {})  // false because triple equal compares everything

const foo = {};
const bar = foo;    // share the same reference
console.log(foo === bar)  // true since they are sharing the same reference
```

```js
// NUMBERS are 64 bits
// numbers represent POS/NEG, floats
// 52 bits for the value, 11 bits for the exponent, 1 bit for the sign

// float number comparison
0.1 + 0.2 === 0.3  // false
Math.abs((0.1+0.2)-0.3) < 0.00000000004 // true

// special NUMBERS:
NaN  // not a number -> reuslts from any numeric operation giving back meaningless result
Infinity, -Infinity 
0/0 // NaN
1/0 // Infinity
-1/0 // -Infinity

big number // Infinity

typeof(NaN) // number
typeof(Infinity) // number

NaN + 1 // NaN
NaN === NaN // false
NaN == NaN // false

// HOWEVER FOR THE BITWISE OPERATORS	
// NaN, Infinity, -Infinity == 0
NaN | 2 // 2
Infinity & 10 // 0
```

### operators:

```js
// + - * / % **
// + converts to positive, - converts to negative
+12
-12
-"12"	// -> numbers
+"12"
-true // -1
+"a" // NaN

// logical operators
// if operations not boolean, convert the value on the left to be boolean

a || b // returns a if a is true, otherwise return b
potentially_falsey || default_value 

a && b // returns a if a is false


// comparison operators
=== // check both types and values
== // checks value
```

### Strings:

```js
"\n" is new line, "\t" is a tab

> "hello \"world\"" // putting string in a string
'hello "world"'

"\\" // actual backslash
"\uxxxx" // unicode charactre

comparison operators compare the unicode 

`
to indicate string in multiple lines
${var} indicates variable
`

```

### Undefined and Null

```js
underfined // no value
1) function not return a value
2) const a; -> undefined
3) missing arg to a function

null // no object
null -> object set to null
undefined -> not intialized

5 * NaN = NaN
5 * undefined = Undefined
5 * null = 0 // null is 0

// edge cases
+"" // 0 + force operand to a number
+ "ss" // NaN
```

### Symbols

```js
const s1 = Symbol("hello");
const s2 = Symbol("hello");

s1 === s2 // false

// use for to find the register, replace to overwrite
const s3 = Symbol.for("hello")
const s4 = Symbol.for("hello")

s3 === s4 // true
```

## Variables and Functions

### const vs. let

```js
const a; // give you error
let a; // give us undefined

var ignores the scope, const and let care about scopes

```



## Objects:

```js
const a = "foo";
const b = "baz";
const obj = {a,b};
log(obj) // {a: foo, b: baz}

// obj methods:
let obj = {};
obj = {
  doStuff: function(){
    console.log("Hi, I am a method");
  },
}


const obj = {
  f(){console.log("metjod");},
}

// remove property using delete
delete obj.f;

// detecting properties continued
Object.hasOwn(obj, 'f'); // true

// looping properties:
for (const prop in obj){}

// looping over object props and vals
for (const [prop,val] in Object.entries(obj)){
  console.log(prop + " is " + val);
}

data = null;
const res = data?.pop(); 


//objs
const data = {a:1,b:2};
const p = 'a';
data.p // undefined
```

## Functions

```js
function hiEveryone(greeting, ...names){
  console.log(greeting);
  console.log(names);
}

// using arguments object
const f = function(){
  console.log("number of args" + arguments.length);
  for(let i = 0, j = arguments.length; i<j ; i++){
    console.log(arguments[i]);
  }
}

f(1,2,3)
```

## Splice vs. Slice

```js
// splice is cutting from an index, with a len
let a = [2,4,6,8,10,12];
let ret = a.splice(2); // a = 2,4, ret = 6,8,10,12
let ret = a.splice(2,2); // a = 2,4,10,12 ret = 6,8

let ret = a.splice(2,2,1,1) // a = 2,4,1,1,10,12   ret = 6,8


// slice returns the sub arr
const a = [2,4,6,8];
a.slice() // return 2,4,6,8
a.slice(1) // return 4,6,8
a.slice(1,3) // return 4,6
a.slice(-1) // 8
```

## Higher Order Functions:

```js
// forEach
numbers.forEach(function(element,ind){
	console.log(element);
});

// filter
arr.filter(callback(data)=>{
  // filter out the element
	return ;
})

// map
arr.map(function(word){
  return word.toUpperCase + '!';
})

//reduce
arr = [1,2,3,4]

arr.reduce((acc,cur)=>acc+cur, initialValue)

// function methods
// call   // pass args individually
// apply  // pass arg arr
// bind 
```

## This

```js
this is undefined in standalone function calls

call apply bind

```

## Prototype

```js
Object.getPrototypeOf({}) ==(===) Object.prototype // true
Object.getPrototypeOf(Object.prototype) // null

Object.getPrototypeOf(Function) // Function.prototype {}
// arr is from Array.prototype

prototype of Array.prototype // Object.prototype

Object.create(somePrototype) // creates a specific prototype

// hasOwnProperty()

```

## Web Server

```js
// net modules
// createServer()

//set up
const server = net.createServer((sock)=>{
  sock.on('data',(bindata) => {
  	console.log(`got data 		${binData}`)
  })
  sock.on('close',(data)=>{
    log(`closed ${sock.remoteAddress}:${sock.remotePort}`)
  })
})
// listen below


// write
sock.write(data,encoding)  // send data tp the client
sock.end() // stop the connection

```

## HTTP 

```js
// request
GET /teaching HTTP/1.1   // method path type
Host: jvers.com, User-Agent: ...; Linux x86-64; ...   // headers

// responses
// a status line
HTTP/1.1 200 OK  // status code and reason
Content-Type: text/html // response header
optional msg body

// URLs
protocol/scheme://domain:port/path?query_string#fragment_id
http://pizzaforyou.com:80/search?type=vegan#top_result

// client side make http requests:
nc hostname port //netcat
curl hostname // curl
chrome
```

## Socket and Server

creating TCP/IP servers and clients

```js
// create server
const net = require('net');
const server = net.createServer(function(sock){
	console.log("got connection", sock.remoteAddress, sock.remotePort);                                
})

server.listen(8080,'localhost');


// use socket to write back html
import {createServer} from 'net';


const server = createServer((socket)=>{
    console.log("connected");

    let msg = '';
    socket.on('data',(binarydata)=>{
        msg += binarydata
        let [method, path] = msg.split(' ');
    console.log("request method is ", method);
    console.log("request path is ", path);

    if (path == "/foo"){
        let response = 'HTTP/1.1 200 OK\r\n';
        response += "Content-Type: text/html\r\n\r\n";
        response += "<h1>You have reached the correct entry</h1>"
        socket.write(response);
    } else {
        let response = 'HTTP/1.1 404 NOT FOUND\r\n';
        response += "Content-Type: text/html\r\n\r\n";
        response += "<h1>Not Found</h1>"
        socket.write(response);
    }
    socket.end()
    })

    
})

server.listen(3000,'localhost')
```

## Customize Request and Responses:

```js

class Request {
  constructor(s) {
    const [method, path, ...remainder] = s.split(' ')
    this.method = method
    this.path = path
  }
}

class Response {
  constructor(sock, statusCode, headers={'Content-Type': 'text/html'}) {
    this.sock = sock
    this.statusCode = statusCode
    this.headers = headers
    this.body = null
  }

  responseHeadAsString() {
    let s = `HTTP/1.1 ${this.statusCode} ${DESCRIPTIONS[this.statusCode]}`

    // entries: {a: 1, b: 2} ===> [[a, 1], [b, 2], ....]
    // reduce: {a: 1... ====> to string 'a: 1\r\n'
    const headersString = Object.entries(this.headers).reduce((s, pair) => {
      const [name, value] = pair
      return s + `${name}: ${value}\r\n`
    }, '')

    // trim headers (remove excess \r\n ... double \r\n to handle no headers)
    // if body isn't null, then include body, otherwise ''
    // return `${s}\r\n${headersString.trim()}\r\n\r\n${this.body ?? ''}`
    return `${s}\r\n${headersString.trim()}`

    // convert our object of headers into a string
  }

  send(body, binary = false) {
    this.sock.write(this.responseHeadAsString());
    this.sock.write('\r\n\r\n');
    if (binary) {
        this.sock.write(body, 'binary');
    } else {
        this.sock.write(body);
    }
    this.sock.end();
  }
}

class App {
  constructor() {
    // we use arrow function to ensure that when
    // handleConnect is called (cb to createServer) ... it
    // is still bound to instance of App
    // this.handleConnect.bind(this)
    this.server = createServer(sock => this.handleConnect(sock))
    this.routes = {}
  }

  // add new routes
  // y method? add things like validation, path sanitization, etc.
  get(path, cb) {
    this.routes[path] = cb
  }

  // pass through to tcp/ip server's listen
  listen(port, hostName) {
    this.server.listen(port, hostName)
  }

  // method that handles our http request
  // and decides how to respond
  handleData(sock, data) {
    const req = new Request(data + '');
    const res = new Response(sock, 200);

    if (Object.hasOwn(this.routes, req.path)) {
        const routeHandler = this.routes[req.path];
        routeHandler(req, res);
    } else {
        const filePath = join(__root, req.path);
        readFile(filePath, (err, fileContent) => {
            if (err) {
                res.statusCode = 404;
                res.headers = {'Content-Type': 'text/plain', 'Server': 'ait'};
                res.send(DESCRIPTIONS[404]);
            } else {
                const ext = extname(filePath);
                const mimeType = MIMETYPES.get(ext);
                res.headers['Content-Type'] = mimeType;
                if (['.jpg', '.png', '.gif'].includes(ext)) { // you can expand this array for other binary types
                    res.send(fileContent, true);
                } else {
                    res.send(fileContent.toString());
                }
            }
        });
    }
  }



  handleConnect(sock) {
    // console.log('client connected')
    // handle request
    sock.on('data', data => this.handleData(sock, data))
  }



}
```

## Express

express runs on the server side

```js
// http module
import http from 'http';

function handelRequest(req,res){
  // req methods/properties
  // req.url
  
  // res methods/properties
  // res.writeHead(status,headers), res.end('hello')
  res.writehead(200,{'content-type': "text/plain"});
  res.end('hello');
}

http.createServer(handelRequest).listen(3000)

// express hello world
import express from 'express'
const app = express();

app.get('/',function(req,res){
  res.send('hello');
})
app.listen(3000);
console.log('Started server on port 3000')

// static file serving
import path from 'path'
import url from 'url'

const basePath = path.dirname(url.fileURLToPath(import.meta.url)) // find local directory in abs path
const publicPath = path.resolve(basePath,'public');
app.use(express.static(publicPath)); // marking the folder as public

// templating handelbars
app.set('view engine','hbs');
res.render('index',{'greeting': 'Hello'}) // handelbar

// request methods
req.url // url
req.headers // headers
req.method // GET ...
req.path // request path
req.query // query string
req.body // requst body
// response methods
res.status(status) // send status code back
res.send(body), res.send(status,body) // send body back
res.render(view, [locals],callback)
res.redirect([status],url)
res.set(name,val) // set headers and media type


// express enable body parsing
app.use(express.urlencoded({extended:false}));
```

## Templating Handelbar

```handlebars
<h3> {{description}} {{item}}</h3>

<!--  looping -->
<ul>
  {{#each item}}
  	<li> {{this}} </li>
  {{/each}}
</ul>

<!--  conditional -->
{{#if isActive}}
  <img src="star.gif" alt="Active">
{{else}}
  <img src="cry.gif" alt="Inactive">
{{/if}}
```

## Middleware

```js
// application level
app.use(middlewareFunc());

// router level
app.use('path',middlewareFunc());
```

## Sessions and Cookies

managing and store states 

```js
Set-Cookies: foo = bar; Expires = Thu, 29 Oct 2016 07:28:00
Set-Cookies: foo = bar; Max-Age = 300; //seconds
```

```js
app.get('./make-a-cookie', function(req,res){
  res.append('Set-Cookie', 'MY_SESSION_ID = 123'; 'HttpOnly');
  res.append('Set-Cookie', 'color = #00ff00')
  res.send('made you a cookie')
})

// express session
const sessionOptions = {
  secret: 'secret for signing session id';
  saveUninitialized: false;
  resave: false;

}

app.use(session(sessionOptions))

// req new states
req.session // obj that can read and session data to
req.session.id/req.sessionID // id for the session
```

## MongoDB

```js
show databases --> show available databases
use db --> work with a specific database
show collections --> show items in the database
db.dropDatabase() --> drop the datatbase
db.collectionName.drop()

// adding a new obj
db.Person.insert({})
db.find({obj})
db.Person.update()
db.Person.remove()

// in react using mongoose
npm install --save mongoose

import mongoose from 'mongoose'

// connect to the database
mongoose.conect('mongodb://localhost/catdb')

// define the data in the collection
const Cat = new mongoose.Schema({
  name: String,
  update_at: Data
})
// registers it so that mongoose knows about it
mongoose.model('Cat',Cat);

// in app.mjs
MyModel.find({})
	.then(foundData=>console.log(foundData)) // return promise
	.catch(err=>console.log(err))

const foundData = await MyModel.find({
 
})

console.log(foundData)

// example of db io
app.get('/cats', (req, res) => {
  Cat.find({})  // empty objects finds all cats in collection
    .then(foundCats => {
	  res.render( 'cats', { cats: foundCats });
    })
    .catch(err => res.status(500).send('server error'));
  
});
```

## Mongoose

```js
import mongoose from 'mongoose'

// plugin setup
import slug from 'mongoose-slug-updater'
mongoose.plugin(slug)

mongoose.connect('mongodb://localhost/pizzadb');

// more stuff goes here (definitions for PizzaSchema, ToppingSchema, etc.)

const Pizza = mongoose.model('Pizza', PizzaSchema);
const Topping = mongoose.model('Topping', ToppingSchema);

// customizing schemas:
const ToppingSchema = new mongoose.Schema({
	name: String,
	extra: {type: Boolean, default:false}
});
const PizzaSchema = new mongoose.Schema({
	size: {type: String, enum: ['small', 'medium', 'large']},
	crust: String,
	toppings: [ToppingSchema],
 	// this will be populated by the plugin
	slug: { 
	  type: String, 
	  slug: ["size", "crust"], 
	  unique: true, 
	  slugPaddingSize: 4 
	}
});

// register model
const Pizza = mongoose.model('Pizza', PizzaSchema);
// retrieve existing model
const Pizza = mongoose.model('Pizza');
const pizza1 = new Pizza({
	size: 'small',
	crust: 'thin'
});

pizza1.save().then(function(savedPizza) {
    console.log('made me some pizza', savedPizza);
})

```



## Trick Questions:

```js
class MyList { // type of myList = function
  constructor(name) {
    this.name = name
    this.items = [];
  }

  addItems(...listItems) {
    this.items = [...this.items, ...listItems];
  }

  render() {
    console.log(this.name, '\n-----');
    this.items.forEach((listItem, i) => {
      console.log(`${i + 1}. ${listItem}`);
    });
  }
}

console.log(typeof list1 === '____A____'); // object
console.log(typeof MyList === '____B____'); //function
console.log(Object.getPrototypeOf(list1) === ____C____); // MyList.prototype
console.log(Object.getPrototypeOf(list1.render) === ____D____);
console.log(____E____.hasOwnProperty('addItems')); // MyList.prototype
```

