## Basic Setup 
There are many ways to start developing a React project. Some of the most common methods include:
**Create React App (CRA)**
- Easiest and most beginner-friendly.
- Comes with Webpack, Babel, and everything pre-configured.

<span style="color: red;">Downside</span>: harder to customize and considered a bit outdated now.

**Vite**
- Super fast dev server, ES module-based, modern.
- Great alternative to CRA with better performance.
- Easy to set up, and supports React out of the box.
**Parcel**
- Zero-config like Vite, but supports more features out of the box (like TypeScript, SCSS, images).
- Automatically handles bundling and hot module replacement.
- Slightly heavier than Vite but still easy to use.
- Manual Webpack + Babel Setup
- Gives you complete control.
- Good if you want to learn how things work under the hood.
- <span style="color: #f28b82;">Takes more time to configure everything yourself.</span>

Let's Build React app we are using here Create React app and <span style="color: #33ff57;">Pracel ,Vite</span>
 ```bash
 sudo apt install nodejs npm 
 node --version 
 npm --version
```
Using Create React App (CRA) – Standard Way
```bash
npx create-react-app my-app 
cd my-app 
npm start
```
Using <span style="color: #ffbd33;">Vite</span>– Fastest Way
```shell
npm create vite@latest my-app --template react 
cd my-app 
npm install 
npm run dev
```

<span style="color: #33ff57;">Pros</span>: Super fast, lightweight, supports TypeScript easily.
<span style="color: #ff5733;">Cons</span>: Requires some manual setup for advanced features.
Using Parcel – Alternative Bundler
```bash
mkdir my-app && cd my-app 
npm init -y
npm install react react-dom parcel
```
in index.html
```html
<body>
<div id="root"></div>
<script type="module" src="./index.js"></script>
</body>
```
<span style="color: #ff6433"  ># Basic Files Structure in React projects</span>
```bash
ls -a
//The -a flag ensures that the output also includes hidden files.
node_modules/
public/
src/
.gitignore
README.md
package-lock.json
package.json
```
![[image.png]]
 **React work on MVC  <span style =color:#ff3368 >Model View Controller</span>
 1. Model (Data & Logic)
    - Manages application data and business logic.
    - Fetches and updates data (e.g., from a database or API).
    - Example: Mongoose models in a MERN stack app.
2. View (User Interface)
    - The presentation layer that displays data.
    - In React, components serve as the View.
    - Example: A React component rendering user data.
3. Controller (Handles User Input)
    - Manages communication between the Model and View.
    - Processes user input, updates the Model, and refreshes the View.
    - Example: Express.js routes handling API requests.

![[image (1).png]]
#### *UI LAYER*
React itself doesn’t care whether the user is using a mobile phone, a tablet, a desktop web browser, a screen reader, a command-line interface, or any other kind of device or interface that may be invented in the future. **React just renders components.** How those components get presented to the user is up to a separate library.
The library that handles rendering of React components in web browsers is called*ReactDOM.*
If you want to render React elements to native mobile apps, you use <span style="color: #ff6033;">React Native</span>.
If you want to render React components to static HTML, you can use *ReactDOMServer.*
ReactDOM has a number of functions for interfacing between React and web browsers, but the one that every React application makes use of is called **ReactDOM.render.**
![[image (2).png]]
## VIRTUAL DOM
The Document Object Model, or DOM, is a web browser’s internal representation of a web page. It converts HTML, styles, and content into nodes that can be operated on using JavaScript.
Compared to other kinds of JavaScript code,<span style="color: #ff6033;">DOM manipulation is slow and inefficient.</span> This is because whenever the DOM changes, the browser has to check whether the change will require the page to be redrawn and then the redrawing has to happen.Adding to the difficulty of DOM manipulation is that the DOM’s functions aren’t always easy to use and some of them have excessively long names like *Document.getElementsByClassName*. For both of these reasons, many different JavaScript DOM manipulation libraries have been created.The single most popular and widely used DOM manipulation library of all time was 
 **jQuery.**
            
**The Old Days of Web Development: The Messy Kitchen**
Now, every time a customer changes their order (a user interaction), you have to <span style="color: #ff6033;">rearrange the entire kitchen</span>—move the stove, shift the fridge, and reorganize the shelves. This process is <span style="color: #ff6033;">slow and tiring</span>, just like direct DOM manipulation was in JavaScript.
Then came a smart assistant—**jQuery**!  It helped you rearrange things **faster**, but you still had to tell it exactly what to move and when to move it. The kitchen still got messy, and it took **time** to fix things.
#### **The Arrival of React: The Magic Blueprint**
One day, a brilliant team at Facebook invented a smart planning board
—> the  <span style="color: #ff6033;">Virtual DOM!</span> 
Instead of changing the whole kitchen every time an order changes, this board <span style="color: #ff6033;">first makes</span> a draft of the changes.
- If only a plate needs moving, it tells the chef to move just that plate.
- If a shelf needs cleaning, it focuses on just that shelf.
- Everything happens efficiently, with no unnecessary effort.
<span style="color: #ff6033;">What’s Happening Today? </span>
Now, we have even **smarter chefs**:
 React Fiber– A super-fast way to update pages with even better performance.
Concurrent Rendering – React can pause and prioritize tasks, making apps feel smoother.
Server Components – React can now pre-build parts of the kitchen before customers even order!
<span style="color: #ff6033;">Why Did React Need Fiber? </span>
Imagine you’re playing a video game , but every time something happens—like opening your inventory—the game freezes for a second  before updating. Annoying, right?
Before React Fiber, React worked in a similar way:
- When the UI needed updates, React would **pause everything** to process all changes at once.
- If the update was big (like rendering a long list), it could <span style="color: #ff6033;">block the main thread</span>, making the UI feel slow or unresponsive.

**What is React Fiber?  (Think of it Like Multi-Tasking)**
React Fiber is a complete rewrite of React’s rendering engine that introduced **Concurrent Rendering**.
Imagine you’re a chef  cooking multiple dishes . Instead of focusing on one dish until it's done(blocking the UI), Fiber lets you:
1. Pause a task (low-priority update)
2. Work on something urgent first (high-priority update)
3. Come back and finish the paused task
This way, your restaurant never freezes and stays smooth!
How Concurrent Rendering Works (A Real-World Example)
Let’s say you’re on a shopping website :
4. You type in the search bar (high-priority action).
5. The site is also loading product images (low-priority task).
6. With old React, the UI might freeze while waiting for the images to load.
7. With Concurrent Rendering, React pauses image loading and keeps the search responsive!

let’s break down Concurrent Rendering  with a story!
The Old Theater  (Before Concurrent Rendering)

Imagine you’re watching a stage play in an old theater. The actors (React) are performing a scene, but suddenly, an important guest (a user interaction) arrives at the door.

- The problem? The play must finish the entire scene before anyone can open the door!
- Even if the guest is VIP (a high-priority task like typing in a search box), the theater won’t pause the scene.
- This makes the guest wait longer, causing delays and a bad experience.

This is how React used to work before Concurrent Rendering—it handled UI updates one at a time and couldn't stop mid-way for urgent tasks.
The Smart Theater  (After Concurrent Rendering)
Now, imagine the theater upgraded to a smart system (React Fiber + Concurrent Rendering).

- The new system allows the actors to pause mid-scene if a VIP arrives.
- A stage manager (React Scheduler) decides:
    Urgent tasks (user input, animations) happen immediately.
    Less urgent tasks (background data fetching, image loading) can wait.
- The play continues without blocking important interactions, making everything smoother.
This is Concurrent Rendering—React can now <span style="color: #ff6033;">pause, prioritize, and resume rendering</span>, leading to a faster, more responsive UI.
How React Updates the UI – Step by Step 🚀
Writing the UI Code (Component Rendering)
- The developer writes React components, which return React elements (JSX). ```
```javascript
function App() {
  return <h1>Hello, World!</h1>;
}
```
<span style="color: #ff6033;">Virtual DOM is Created (Initial Render)</span>
- React doesn’t touch the real DOM yet! Instead, it creates a lightweight JavaScript object (Virtual DOM) that represents the UI in memory.
- This makes updates faster because React can process changes before touching the real DOM.
<span style="color: #ff6033;">React Listens for Changes (Event Handling)</span>
- When a user interacts (clicks a button, types in a form), React listens to these events and **triggers a state change**.

<span style="color: #ff6033;">New Virtual DOM is Created</span>
- React re-renders the component, creating a new Virtual DOM representation of the UI after the state change.

<span style="color: #ff6033;">Reconciliation (Finding the Difference)</span>
- React compares the new Virtual DOM with the previous one to find the exact parts that changed.
- This is called <span style="color: #ff6033;">"diffing"</span>, and it helps avoid unnecessary updates to the real DOM.

<span style="color: #ff6033;">Minimal DOM Updates (Efficient Rendering)</span>
- React *updates only the changed parts* of the browser’s real DOM, rather than re-rendering the entire page.
- It batches updates together for better performance![[image (3).png]]<span style="color: #ff6033;">React Is Idiomatic</span>
**React is Just JavaScript**
React components are written in JavaScript, and if they look unfamiliar, it’s likely due to:
A different programming style (functional programming).
Newer JavaScript features (like ES6+ syntax).
[[why React Re-rendering]]  **Must read why react re render**
[[some golden  React rules]]   *React Rule*
### React Underwood journey
React.createElement()
```javascript
function App() {
  return <h1>Hello, World!</h1>;
}
```
As you now know, you can use a number of HTML elements as React components via
the *React.createElement()* method. Let’s take a close look at this API.
Remember, the “Hello world!” app looks like this:
```jsx
ReactDOM.render(
React.createElement('h1', null, 'Hello world!'),
document.getElementById('app')
);
```
The first parameter to createElement is the type of element to be created. The sec‐
ond (which is null in this case) is an object that specifies any properties (think DOM
attributes) that you want to pass to your element.
### React Lifecycle in Functional Components
React no longer uses class-based lifecycle methods like `componentDidMount`, `componentDidUpdate`, or `componentWillUnmount` — instead, **hooks like `useEffect`** handle these phases in **functional components**.
1. Mounting: The component is rendered for the **first time**
 ```jsx
 useEffect(() => {
  console.log("Component mounted!");
}, []);
```
2. Updating :- Happens when **state or props** change.
```jsx
useEffect(() => {
  console.log("Component updated because `count` changed");
}, [count]);

```
3. Unmounting :- Happens when the component is **removed from the DOM**
```javascript
useEffect(() => {
  console.log("Mounted");
  return () => {
    console.log("Component unmounted");
    // cleanup logic here (remove listeners, cancel API, etc.)
  };
}, []);

```
The return function inside `useEffect` is your **cleanup** — like `componentWillUnmount`.

**Transpiling**: The process of converting programming code from one version of a programming language into another version. This is necessary in web development because not all web browsers support the same set of new JavaScript features, but they do all support some core subset of JavaScript features. By using a JavaScript transpiler, programmers can write code using the latest version of JavaScript and then the transpiled code can be run in any web browser.

### JSX
Newcomers to React often remark on how it appears that React breaks one of the cardinal rules of web development, which is to not mix your programming logic with your HTML.
<span style="color: #ff6033;">Transpiler . . . Huh?</span> Before you can run a React application that uses JSX and modules, it must first be compiled. During the compile (also known as “build”) process, all of the modules are joined together and the JSX code is converted into pure JavaScript.
### Compilation vs. Transpilation (React Context)

|Concept|Compilation 🔧|Transpilation 🔄|
|---|---|---|
|**Definition**|Converts code into lower-level machine code (bytecode)|Converts code from one version/type of code to another|
|**Examples**|C++ → Machine Code, Java → Bytecode|JSX/ES6+ → Plain JavaScript (React apps)|
|**Used in**|C, C++, Java, Go, Rust|JavaScript (React, Vue), TypeScript, Babel|
|**Output**|Executable code (can be run by CPU or VM)|Still JavaScript (but in compatible version)|
|**Tools**|GCC, JVM|Babel, TypeScript Compiler (tsc), SWC, ESBuild|
  **JSX Transform**
One of the steps in the transpilation of React code is the JSX Transform. The JSX Transform is a process in which the transpiler takes JSX code (which isn’t natively understood by web browsers) and converts it into plain JavaScript (which is natively understood by web browsers).
##### Introducing Babel 
The tool we use for transpilation in JavaScript is called Babel. Babel is integrated into Create React App and is an automatic part of compiling a React app built with Create React App.
>[!important] NOTE Prior to version 17 of React, the JSX Transform converted JSX into React.createElement() statements. With React 17, the JSX Transform was rewritten so that it transforms JSX into browser-readable code without using React.createElement(). The result is that developers no longer need to import React into every component in order to use JSX.

##### Eliminating Browser Incompatibilities
Using transpilation does away with the age-old problem of browser incompatibilities and having to wait until every browser supports a new JavaScript language feature before using it. Rather than developers having to write special code and multiple if/then branches to accommodate older browsers, Babel makes it possible for developers to just write JavaScript using the latest syntax and then transpile that new JavaScript into a common denominator that will run in any web browser that’s likely to access the app.
#### JSX Is JavaScript XML
The first thing to know about JSX is that it’s XML. So, if you know a little bit about XML (or if you’ve used XHTML), the rules of writing JSX should sound familiar. Namely: 
➤ All elements must be closed. 
➤ Elements that cannot have child nodes (so-called “empty” elements) must be closed with       a slash. The most commonly used empty elements in HTML are br, img, input, and link.
➤ Attributes that are strings must have quotes around them. 
➤ HTML elements in JSX must be written in all lowercase letters.
#### Beware of Reserved Words 
Because JSX compiles to JavaScript, there is the potential that an element name or attribute name that you use in your JSX code can cause errors in your compiled program. To guard against this, certain HTML attribute names that are also reserved words used in JavaScript have to be renamed, as follows: 
➤ The class attribute becomes className. 
➤ The for attribute becomes htmlFor.
#### JSX Uses camelCase
Attribute names in HTML that contain more than one word are camel-cased in JSX. For example: 
➤ The onclick attribute becomes onClick.
➤ The tabindex attribute becomes tabIndex
In JSX, the value of an attribute can be omitted when it is explicitly true. So, to set the disabled attribute of a JSX input element to true, you can do either of the following:
```jsx
<input type="text" name="username" disabled = {true}/>
<input type="text" name="username" disabled/>
```
#### Use Curly Braces to Include Literal JavaScript
When you need to include a variable or a piece of JavaScript in your JSX that shouldn’t be interpreted by the transpiler, use curly braces around it.
```jsx
function SearchInput(props) { return (
{props.onChange(e.target.value)}}/>
) } export default SearchInput;
```
#### Remember to Use Double Curly Braces with Objects
```jsx
function Header(props){
return (
// Welcome to My Website
) } export default Header;
```
#### When to Use JavaScript in JSX
The concept of separation of concerns in programming says that layout code should be separated from logic. What this means in practice is that code that does calculations, retrieves data, combines data, and controls the flow of an application should be written as functions outside of the return statement in a component, rather than inside of curly braces in JSX.
Limited amounts of logic are necessary and perfectly normal inside of the return statement, however. There’s no hard-and-fast rule for how much is too much, but, generally, any JavaScript that you write in your JSX should only have to do with presentation, and it should be single JavaScript expressions, rather than functions or complex logic.
#### Conditionals in JSX
Oftentimes, a component needs to output different subcomponents, or hide certain components, based on the results of expressions or the values of variables. We call this conditional rendering.
There are three ways to write conditional statements in JavaScript, and you may use any of these to do conditional rendering.
#### Conditional Rendering with if/else and Element Variables
```jsx
import Header from './Header'; 
function Welcome(){
let header = <Header/>
return(
{header}
)} 
export default Welcome;
```
By using a conditional statement, you can assign a different element to a variable and thus change what gets rendered,
```jsx
import Header from './Header'; 
import Login from './Login'; 
function Welcome({loggedIn}) { 
let header; 
if (loggedIn) { header = <Header/>
 }else {
  header =<Login/> ; 
  }return (
{header}
); } export default Welcome;
```
Conditional Rendering with the && Operator
```jsx
import Header from './Header'; 
function Welcome({loggedIn}){ 
return ({loggedIn&&<Header/>} 
Note: if you don't see the header messsage, you're not logged in.
) } export default Welcome;
```
Conditional Rendering with the Conditional Operator
```jsx
import Header from './Header'; 
import Login from './Login'; function Welcome({loggedIn})
{ return(
<div>
{loggedIn ? <Header/> :<Login/> }
</div>
) } export default Welcome;
```
## All About Components
> A **React component** is a **reusable piece of code** (a function or class) that returns a part of the UI using **JSX**. React apps are made by composing many small components into one large tree.
![[Pasted image 20250411011320.png]]

Components Define Elements
The job of a component is to return an *element*. Each component within an application has a unique name, which is how you use it. The component name becomes the name of the React element when you include a component in another component,
```jsx
function WelcomeMessage() 
{ return "Welcome!"; } 
export default WelcomeMessage;
```

now
```javascript
import WelcomeMessage from './WelcomeMessage'; 
function WelcomeTitle(){ 
return(
<h1><WelcomeMessage/> <h1/>
);
} 
export default WelcomeTitle
```
Once you import a component into another component, this is where <span style="color: #ff6033;"> React elements come in.</span>
#### Elements Invoke Components
Once you’ve imported a component into another component, the imported component’s function‑ ality can be included in your new component’s JSX using an element. You can include as many components inside another component as you need to, and there’s no limit to how many levels of components a tree of components can have. Once you import a component, you can use the element it defines as many times as you need to and each usage will create a <span style="color: #ff6033;">new instance </span>of the component with its own data and memory.
```javascript
import React from 'react'; 
import CartItems from './CartItems'; 
import DisplayTotal from './DisplayTotal'; 
import CheckoutButton from './CheckoutButton';
import styles from './Cart.css.js';
function Cart(props){ 
return(
<div style={styles.cart}>
 <h2>Cart</h2>
<CartItems items = {props.inCart} />
<DisplayTotal items = {props.inCart} />
 <CheckoutButton />
 </div>
)}
export default Cart;
```



>[!success] 
>JAVASCRIPT LESSON: USING ARRAY.MAP() JavaScript’s Array.map function creates a new array using the result of applying a function to every element in an existing array. The map function is commonly used in React to build lists of React elements or strings from arrays. 

#### The syntax of Array.map is as follows:
```jsx
array.map(function(currentValue, index, arr),thisValue)
```
Take a closer look at the details:
➤ The array is any JavaScript array. The function passed into the map function
will run once for every element in the array.
➤ The currentValue is the value passed into the function and will change with every iteration through the array. 
➤ The index parameter is a number representing the current value’s position in the array.
➤ The arr parameter is the array object that the currentValue belongs to. 
➤ The thisValue parameter is a value to be used as the “this” value inside the function.
The only required parameter is currentValue. It is also what you will most com‑ monly see in real-­world React applications. Here’s how you can use Array.map() to make a series of list items from an array:
```jsx
const bulletedList = listItems.map(function(currentItem){
 return <li>{currentItem}</li>
}
```

For performance reasons, React requires each item in a list of JSX elements (such as
one built from an array) to have a unique key attribute. One way to give each element a unique key is to use the index parameter, like this:
```jsx
const bulletedList = listItems.map(function(currentItem,index){
 return <li key={index}>{currentItem}</li>
}
```
#### Standard HTML Attributes
##### Attributes Use camelCase
Whereas HTML5 attributes use all lowercase letters, and a few of them use dashes between multiple words (such as the accept-charset attribute), all attributes in React’s HTML components use capi‑ tal letters for words in the attribute after the first one. 
This type of capitalization is commonly called camelCase. For example, the HTML tabindex attribute is represented by tabIndex in React and onclick is represented by onClick.
##### Two Attributes Are Renamed
In a couple of cases, React attributes for built-­in elements have different names than HTML attrib‑ utes. The reason for this is to avoid potential clashes with reserved words in JavaScript. The attributes that are different in React are: 
➤ class in HTML is className in React.
➤ for in HTML is htmlFor in React.
>[!warning]
>NOTE Having a knowledge of JavaScript classes and class components is necessary in order for you to get a complete picture of how React works, but it is possible to write complete React applications without using classes. An explanation of classes can get pretty dense and theoretical, but don’t let it bog you down. If this chapter’s “Class Components” section confuses you, feel free to skip ahead or skim it for now and go straight to the “Function Components” section, which is what we’ll be working with for most of the rest of the book. You can come back and learn all about class components and JavaScript classes when you need to.

<span style="color: #e77c12">Before Going Deep Down on Class Component or Function Component </span>
Let's explore what Function Component
**Functional Component**
**functional component** is simply a **JavaScript function** that:
- Returns **JSX** (the UI you want to display)
- Can use **hooks** (`useState`, `useEffect`, etc.)
- Is the modern, preferred way to build React components
```jsx
import React from 'react';
function MyComponent() {
  return <h1>Hello from Functional Component!</h1>;
}
export default MyComponent;

```
Passing Props to a Functional Component
In Parent:
```jsx
<Welcome name="John" age={25} />

```
In Child:
```jsx
function Welcome({ name, age }) {
  return <p>Hello {name}, age {age}</p>;
}

```
Avoid Re-renders When Parent Updates
React re-renders child components **every time parent renders**, unless:
- You use `React.memo()` to memoize the component
- Props passed to child didn’t change
-  With `React.memo()`
```jsx
const Child = React.memo(function Child({ name }) {
  console.log('Child rendered');
  return <div>Hello {name}</div>;
});

```
Calling Other Components Inside Parent
```jsx
function Parent() {
  return (
    <div>
      <Header />
      <MainContent />
    </div>
  );
}
```
**Import them like:**
```jsx
import Header from './Header';
import MainContent from './MainContent';

```
<span style="color: #e77c12">Function Declarations</span> vs <span style="color: #e71253">Function Expressions</span>
Function declaration
```jsx
function Header() {
  return <h1>Header</h1>;
}
```
Function expression (arrow function):
```jsx
const Footer = () => {
  return <p>Footer</p>;
};
```
Export / Import Functional Components
```jsx
//Export default
export default MyComponent;
import MyComponent from './MyComponent';

```
Named exports (for multiple in one file):
```jsx
export const Button = () => <button>Click</button>;
export const Input = () => <input />;
import { Button, Input } from './FormElements';
```
<span style="color: #e77c12">React.memo</span> vs <span style="color: #e71253">useMemo</span> — What's the Difference?
For this understand we need to understand this What is Higher-Order Components (HOCs)
> **A Higher-Order Component (HOC)** is a function that takes a component and returns a new component with **enhanced functionality**.

You have many components that need to **show a loading spinner** until data is fetched.
```JSX
function User() {
  if (loading) return <Spinner />;
  return <div>{user.name}</div>;
}
function Posts() {
  if (loading) return <Spinner />;
  return <div>{posts.length} posts</div>;
}

```
You could do this in _every_ component like this
Create a **HOC** that wraps any component and adds **loading behavior**.
Create the HOC
```JSX
function withLoader(Component) {
  return function EnhancedComponent({ isLoading, ...props }) {
    if (isLoading) {
      return <p>⏳ Loading...</p>;
    }
    return <Component {...props} />;
  };
}

```
Use It With Any Component
```JSX
function User({ name }) {
  return <h2>User: {name}</h2>;
}
const UserWithLoader = withLoader(User);
// Render it
<UserWithLoader isLoading={true} name="John" />

```
Reuse It With Any Component
```JSX
function Product({ title }) {
  return <h2>Product: {title}</h2>;
}

const ProductWithLoader = withLoader(Product);

// Usage
<ProductWithLoader isLoading={false} title="iPhone 15" />
```
A **function** that takes a component and **returns a new component** with extra behavior or props.
```jsx
const withAuth = (Component) => (props) => {
  return isLoggedIn ? <Component {...props} /> : <LoginPage />;
};
//This wraps a specific component**, adds logic, and returns a new one.
```
A **Provider** (like `ReduxProvider` or `Context.Provider`) is
A **React component** that **injects values** into the component tree via the Context API.
```jsx
<AuthContext.Provider value={{ isLoggedIn: true }}>
  <App />
</AuthContext.Provider>
```
This does **not take a component and return a new one**. It just **wraps children** and provides context values via the React internals.

## Class Components
>[!warning]
>NOTE Having a knowledge of JavaScript classes and class components is necessary in order for you to get a complete picture of how React works, but it is possible to write complete React applications without using classes. An explanation of classes can get pretty dense and theoretical, but don’t let it bog you down.

###### React.createClass (Old Way to Make Components)
In the early days of React, components were created using a method called `React.createClass()`. You would pass an object with all the component's properties (like state, methods, etc.), and it would return a React component.
But as JavaScript evolved and introduced **ES6 classes**, React moved away from `createClass`. This old method was officially **deprecated in React 15.5**, meaning it's no longer recommended for use.
```bash
npm install create-react-class
```
```jsx
import React from 'react'; import createClass from 'create-react-class'; const UserProfile = createClass({ render() { return (

# User Profile

); } }); export default UserProfile;
```

###### Creating a component using a class
```jsx
import React from 'react'; 
class UserProfile extends React.Component {
constructor(props) { 
super(props); 
} render() { 
return (
<h1>User Profile</h1>

# User Profile

); } }; export default UserProfile;
```
###### JavaScript Classes — Just Syntactic Sugar
JavaScript introduced the `class` syntax in ES2015 (ES6) to make code look and feel more like traditional object-oriented languages like Java or C++.
>**JavaScript classes are not real classes** like in Java — they are just **prototypes under the hood**.

This is what we call **syntactic sugar** — a nicer, cleaner way to write something that was already possible before.
Before classes, JavaScript used **function constructors** and **prototypal inheritance** to build reusable objects. The new `class` syntax just makes that process easier to understand and write, especially for developers coming from other languages.

#### JavaScript Object Prototypes
JavaScript objects are collections of properties. JavaScript has several ways to cre‑ ate objects: 
 - By using Object Literal notation. 
 - By using the Object.create method. 
 - By using the new operator.
In JavaScript, you can **create objects** using a special way called the `new` operator.
#####  How it works:
1. You write a constructor function (a regular function that sets properties using `this`).
2. You call it with the `new` keyword to create a new object.
```JSX
// Constructor function
let a = function () { 
this.x = 10; 
this.y = 8; 
}; 
let b = new a();
```

The result of creating the b object will be an object with two properties, x and y. 
Type the following two statements to confirm this:
`console.log(b.x) 10`
`console.log(b.y) 8`
###### Modifying and Using the Prototype
You can add new properties to an object’s prototype, like this:
`a.prototype.z = 100;`

###### Methods Are Properties Too
A property of an object can have a function as its value. A property with a function value is what we refer to as a “method” in JavaScript. 
You can use the this keyword in methods, and it refers to the inheriting object, not the prototype. For example, add a method called sum() to the prototype object:
` a.prototype.sum = function() { return this.x + this.y };`
Now, change the values of x and y on the b object:
`b.x = 1000
`b.y = 2000
And then invoke the sum function on the b object:
`b.sum() // 3000`
Even though b doesn’t have its own function called `sum`, JavaScript runs the sum function on the prototype but uses the this values from b.
> [!hindi mode]
> - जब हम `new a()` लिखते हैं, तो JavaScript एक नया object बनाता है (`b`).
>- `b` में `x` और `y` उसकी खुद की properties होती हैं (own properties).
>- लेकिन अगर हम `b` से कोई property access करते हैं जो उसमें नहीं है, तो JavaScript `a.prototype` में देखती है। 
  Hindi में "Prototype" का मतलब:
> एक ऐसा object जिसमें default properties और methods होते हैं, जो new object खुद inherit करता है।
 आसान शब्दों में:
>  Prototype = Parent object या backup object, जिससे नया object चीज़ें उधार लेता है।

#### Understanding JavaScript Classes
To define a class, you can use either a <span style="color: #e77c12">class declaration</span> or a <span style="color:  #e71253">class expression.</span>
######  <span style="color: #e77c12">class declaration</span>
A class declaration starts with the class keyword followed by the name of the class.
```jsx
class Pizza ( constructor(toppings,size) 
{ this.toppings = toppings;
this.size = size; 
} 
}
```
Class declarations are similar in structure to *function declarations*.
Here’s an example of a function declaration: 
```jsx
function Pizza(toppings,size) 
{ this.toppings = toppings; 
this.size = size; 
}
```
An important difference between class declarations and function declarations, how‑ ever, is that function declarations are ***hoisted***
<span style="color: #1bd322">`Function hoisting means that you can reference a function created using a function declaration anywhere in a script, even before the function declaration actually appears in the file`</span>
```javascript
let MyPizza = new Pizza(['sausage','cheese'],'large');
function Pizza(toppings,size) { 
this.toppings = toppings;
this.size = size;
}
```
However, the class version of this code will produce an error, because the class named Pizza doesn’t exist when this code tries to use it
``` javascript
let MyPizza = new Pizza(['sausage','cheese'],'large'); 
class Pizza { constructor(toppings,size) { 
this.toppings = toppings; 
this.size = size; 
} 
}
```

###### Class Expression
To create a class using a class expression, you use either a named or unnamed class and assign it to a variable.
```javascript
let Pizza = class { 
constructor(toppings, size) 
{ this.toppings = toppings;
this.size = size;
} 
};
```
Note that when you use a class expression with a named class, the name you specify after the class keyword becomes the value of the name property of the class:
`console.log(Pizza.name);`
###### Class Body and the Constructor Method
The body of a class, like the body of a function, is the part between the curly braces. Inside the class body, you can define class members, such as its methods, fields, and constructor.
`constructor` is **optional** — if you don't write one, JavaScript adds an empty one for you.
```javascript
class Pizza {
  constructor(sauce, cheese, toppings) {
    this.sauce = sauce;
    this.cheese = cheese;
    this.toppings = toppings;
  }
}

let myPizza = new Pizza('tomato', 'mozzarella', ['basil', 'garlic']);
console.log(myPizza.sauce);     // tomato
console.log(myPizza.cheese);    // mozzarella
console.log(myPizza.toppings);  // ['basil', 'garlic']

```
- `new Pizza(...)` creates a new object.
- That object is passed into the `constructor()` as `this`.
- You attach values to `this`, and that becomes part of the final object.
##### Class _without_ `constructor()`
``` javascript 
class Car {
  brand = "Toyota";
  wheels = 4;
  drive() {
    console.log(`Driving a ${this.brand} car with ${this.wheels} wheels.`);
  }
}
let myCar = new Car();
myCar.drive(); // Driving a Toyota car with 4 wheels.

```
- Even though there's **no `constructor` method**, the class still works.
- JavaScript uses the **default constructor** behind the scenes.
- You can still define class properties directly, like `brand = "Toyota"`.
###### JavaScript Classes and Constructor (Simple Explanation)
- In JavaScript, when you create a class, you can use a special method called `constructor()` to initialize (set up) values for the object you're creating.
- This method **runs automatically** when you create a new object using the class.
>[!important]
>If you don't use a constructor, JavaScript adds an empty one:  
`constructor() {}`  
This is fine as long as you don’t need to accept arguments or run custom setup when creating the object.

###### Creating Subclasses with extends `extends` Keyword
In JavaScript (and especially in React when using classes), the `extends` keyword is used to **create a child class (subclass)** that inherits from a **parent class (superclass)**.
That means:  
🔹 The **child class automatically gets the properties and methods** from the parent.  
🔹 You can **add more** to the child without rewriting what's already in the parent.
### reference to class

#### React.Component
React.Component is the base class for every class component that you’ll make. It defines a number of methods, lifecycle methods, class properties, and instance properties that you can make use of and extend in your components.
importing `React.Component`
When you're writing a **class component** in React, your component must **extend** from `React.Component`.That means you need to **import React** into your file.
Two Common Ways to Import
**Default Import** (most common):
```jsx
import React from 'react';

```
- This brings in the entire **React** object.
- You can now use `React.Component`, `React.useState`, etc.

**Named Imports** (used when importing specific parts only):
```jsx
import { Component } from 'react';

```
>[! Note]
>In **React 17+**, importing React is **no longer required for JSX** in many setups,

how to write a class Based compoents
```jsx
//1. import React
import React from 'react';
// Or
import { Component } from 'react';
 //The Class Header
import React from 'react';
 class MyComponent extends React.Component{
// for name Import 
import { Component } from 'react';
class MyComponent extends Component{
//The Constructor Function
constructor(props) { super(props); this.state = { score: 0; userInput: '' } this.saveUserInput = this.saveUserInput.bind(this); this.updateScore = this.updateScore.bind(this); 
}
```
After the constructor header and the call to the super function, this constructor has two purposes—it initializes the component instance’s state, and it binds event handler methods to the component instance.
*Initializing Local State*
Each instance of a React component maintains its own state, and the constructor is where you initial‑ ize this state. The state of a component determines whether and when a component should re-­render
State and state management is at the heart of how React works
>[!information]
>For now, just know that the state of a component is stored in an object called state, and every time state changes, React attempts to re-­render the UI

The other object in a component instance that stores data is called *props* (which is short for proper‑ ties). This is data that is passed to a component by its parent component in a React component hierarchy.
If you’re going to use the props object in the constructor, you need to pass it to the superclass’s constructor when you call **super.**
```jsx
import {Component} from 'react'; 
class MyComponent extends Component { 
constructor(props){ 
super(props); 
this.state = {}; 
} 
... } 
export default MyComponent;
```
Binding Event Handlers in React (Class Components)
###### What are Event Handlers?
Event handlers are **functions** that run in response to user actions like clicks, input changes, etc.
###### Problem Without Binding
In class components, if you pass an event handler like `this.handleClick` directly to JSX **without binding**, `this` becomes `undefined` (not pointing to the class instance).
```javascript
class Foo extends React.Component {
  constructor(props) {
    super(props);
    this.message = "hello";
  }
  handleClick() {
    console.log(this.message); // ❌ this is undefined
  }
  render() {
    return (
      <button onClick={this.handleClick}>
        Click Me
      </button>
    );
  }
}
```
❗`this.handleClick` loses context when passed as a callback — it's no longer tied to the class instance.
###### Solution: Bind in Constructor
You **bind** the function to the current instance in the constructor.
```jsx
class Foo extends React.Component {
  constructor(props) {
    super(props);
    this.message = "hello";
    this.handleClick = this.handleClick.bind(this); 
  }

  handleClick() {
    console.log(this.message); 
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        Click Me
      </button>
    );
  }
}
```
Now `this` inside `handleClick` refers to the component instance, so you can access `this.message`.
###### Managing State in Class Components
The constructor function is the only place where you should ever directly update the state object of a component. For updating the state after the constructor function has run (during the life of the component, in other words), React provides a function called **setState.** The setState function tells React to update the state of the component using an object or function that you pass into it.
```jsx
import {Component} from 'react';
class Counter extends Component {
 constructor(props){
 super(props);
 this.state = {count: 0};
 this.incrementCount = this.incrementCount.bind(this);
 }
 incrementCount(){
 this.setState({count: this.state.count + 1});
 }
 render(){
 return (
 <div>
 <p>The current count is: {this.state.count}.</p>
 <button onClick = {()=>{this.incrementCount(this.state.count+1)}}>
 Add 1
 </button>
 </div>
 );
 }
}
export default Counter;
```
>[!warning]
>this is a **critical point** to understand when working with React's `setState`, especially in **class components** (though `useState` in functional components behaves similarly).

###### What does “`setState` is asynchronous” mean?
When you call `setState`, **React doesn’t update the state immediately**.  
Instead, it schedules an update and may **batch multiple `setState` calls together** to optimize performance.
```jsx
this.setState({ count: this.state.count + 1 });
console.log(this.state.count); // ❌ Might log the old value!

```
- You **think** the state changed.
- But `console.log` runs **before** the state actually updates.
- Result: You see stale data.
 $$Correct Way: Use Callback Form $$
 ```javascript
 this.setState((prevState) => ({
  count: prevState.count + 1
}))
```
Why is setState asynchronous?
To optimize performance, React **batches multiple updates together**, reducing re-renders and improving efficiency. This is why updates don’t happen immediately.
######  In Functional Components
The same concept applies with `useState`, but you handle it with `useEffect` or callback functions — there's **no built-in callback in `useState`**, unlike `setState`.
###### How to know when state updates in functional components?
```jsx
useEffect(() => {
  console.log("Count changed:", count);
}, [count]); // <- only runs when `count` changes

```

>[!IMPORTANT]
>🧩 Concepts like `this`, `bind`, `constructor`, and `lifecycle methods` (e.g., `componentDidMount`) give you **better insight** into the internal working of React.

###### Function Component Shortcuts
`export const Foo = props => <h1>Hello, World!</h1>;`
That’s the whole thing! The preceding code snippet takes advantage of the following rules of arrow  functions:
1. The parentheses around the parameter list are optional when a function only takes one
parameter.
2. The return keyword is optional when an arrow function doesn’t do anything except
return data.
3. The curly braces around the function body are optional if you skip the return keyword.
#### Differences between Function and Class Components
**## 📘 React: Function Components vs Class Components

| Feature                   | Function Components                          | Class Components                                                  |
| ------------------------- | -------------------------------------------- | ----------------------------------------------------------------- |
| **How it’s defined**      | Regular JavaScript function                  | Extends `React.Component`                                         |
| **Props**                 | Passed as function arguments                 | Accessed via `this.props`                                         |
| **Render method**         | Directly returns JSX                         | Must define a `render()` method                                   |
| **State**                 | Uses `useState` hook                         | Uses `this.state` and `this.setState`                             |
| **Hooks**                 | ✅ Can use hooks like `useEffect`, `useState` | ❌ Cannot use hooks                                                |
| **Lifecycle methods**     | Simulated with hooks                         | Uses methods like `componentDidMount`, `componentDidUpdate`, etc. |
| **Code simplicity**       | Shorter and easier to write                  | More verbose and complex                                          |
| **`this` keyword**        | Not required                                 | Must understand and bind `this`                                   |
| **Usage in modern React** | ✅ Preferred (modern React style)             | Less common in new codebases                                      |
######  REACT COMPONENT CHILDREN
Components that are rendered inside other components are called children, and the component they’re rendered inside of is called their parent. As in the physical world, being a child doesn’t prevent a component from being a parent to some other child, and all parents except for the root component are also children.
```javascript
export default function LoginForm() {
 return (
 <form>
 <UsernameInput />
 <PasswordInput />
 <LoginSubmit />
 </form>
 )
}
```

## THE COMPONENT LIFE-CYCLE
During the time when a React application is running, components become active, do their thing, and are destroyed. At each stage in the life of a component, certain events are fired and methods are invoked. These events and methods make up the component lifecycle.

The stages of a component’s life are: 
- Mounting: Mounting is where a component is constructed using the props passed into it and the default state, and the JSX returned by the component is rendered.
- Updating: Updating happens when the state of the component changes and the component is re-­rendered.
- Unmounting: Unmounting is the end of the component lifecycle, when the component is removed from the active application. 
- Error handling: The error handling methods run when an error happens during a compo‑ nent’s lifecycle.
In class components, you can override the lifecycle methods to run your own code in response to lifecycle events. Function components can simulate lifecycle methods using a hook called useEffect
![[Pasted image 20250413094832.png]]
### Mounting 
The mounting stage includes everything from when a component is first constructed until it is inserted into the DOM. During the mounting lifecycle stage, the following methods run, in this order:
- constructor 
-  static getDerivedStateFromProps 
- render 
- componentDidMount
###### constructor()
You’ve already learned about the constructor. This is the method that automatically runs in an instance of a class when it’s created. In a React component, it may include a call to the super method, initialization of the component’s state object, and binding of event handlers.
###### static getDerivedStateFromProps
This method is a static method, meaning that it doesn’t have access to the *this* keyword. The purpose of getDerivedStateFromProps is to check whether the props that the component uses have changed and to use the new props to update the state. This method runs both during the *mounting* stage as well as during the *updating* stage.
###### render 
Like getDerivedStateFromProps, the render method also runs once during the mounting stage. After mounting, render runs every time the component updates. This is the method that generates the JSX output of your component, and it’s the only required method in a class component.
###### componentDidMount()
The componentDidMount method runs when the component has finished mounting and has been inserted in the browser DOM. This is the point at which it’s safe to do things that depend on DOM nodes, or to fetch remote data.

### Updating
After your component has mounted, the updating lifecycle methods start running. React components update their data and re-­render in response to changes to the state object made using the setState function.
- static getDerivedStateFromProps
- shouldComponentUpdate
- render 
- getSnapshotBeforeUpdate 
- componentDidUpdate
The `getDerivedStateFromProps` and` render` methods serve the same purposes in the updating stage as they do during the mounting stage. So, let’s take a look at the three lifecycle methods that are unique to the updating stage.

 ###### shouldComponentUpdate
The default behavior of a React component is to update every time the state changes. There are times, however, when you might want to tell React that a change to the state doesn’t affect a component and so it’s not necessary to go through the updating process. This method, when it’s present, must return either `true` or `false`. If you have a component that you know will never need to be updated once it’s mounted, you can prevent it from updating by using this code:
```javascript
shouldComponentUpdate(){
 return false;
}
```
the way shouldComponentUpdate is used is to compare the previous props and state
with the new props and state and to decide whether to update the component. This is possible because React passes the props and state that will be used for the upcoming rendering into shouldComponentUpdate. 
```javascript
class ToDoItem extends Component {
 shouldComponentUpdate(nextProps, nextState) {
 return nextProps.isChecked != this.props.isChecked;
 }
 ...
}
```
###### getSnapshotBeforeUpdate
This lifecycle method happens right before the rendered output from the component is made active inthe DOM. The purpose of this method is to allow you to capture information about the state of the browser (or other output device) prior to it changing.
Although it’s *rare* that you’ll have a need to use this lifecycle method, one example use for it
is to maintain the scroll position of an element (such as a text box) between renders. If an
update to the browser DOM would affect what the user is currently viewing in the browser,
getSnapshotBeforeUpdate can be used to find out the relevant information about the browser DOM so that it can be restored after the update happens.
###### componentDidUpdate
This method runs immediately after a component updates. It’s useful for performing network requests based on new props passed to the component, or for performing operations that depend on the snap‑ shot of the DOM created during the getSnapShotBeforeUpdate method.If your component has a shouldComponentUpdate method that returns false, the component won’t 
update and this method won’t run.

### Unmounting
The process of removing a component from the DOM is called unmounting. Only one lifecycle method, `componentWillUnmount`, happens during this process.
###### componentWillUnmount
As its name implies, componentWillUnmount is invoked right before a component is removed from the DOM. If you need to do any cleanup in your application related to the component that will be unmounted, this is the place to do it.

- Stopping any network requests that are in progress.
- Stopping timers.
- Removing event listeners created in componentDidMount
### Error Handling
The fourth type of lifecycle methods are the ones that only run when something goes wrong with your component. These lifecycle methods are `getDerivedStateFromError` and `componentDidCatch.`
###### getDerivedStateFromError
If an error occurs in a component’s descendant components, the component will run the getDerivedStateFromError method. This lifecycle method receives the error that occurred and should return an object that will be used to update the state.
###### componentDidCatch
The componentDidCatch lifecycle method runs after a descendant component throws an error. Because componentDidCatch doesn’t run during the render phase of the lifecycle, it’s useful for per‑ forming tasks such as error logging.
## Improving Performance and Avoiding Errors
Lifecycle methods can be used to improve the performance of your React application and to prevent errors
###### Avoiding Memory Leaks
a memory leak
`is a fault in a computer program where memory is allocated unnecessarily.`
This can happen when a component is unmounted without removing timers or network requests involving the component continue to happen after the unmounting.Because a memory leak is a wasted use of resources, having a memory leak in your program can lead to reduced performance and unexpected behaviors.
Memory leaks have a tendency to build up the longer a program is running, and so you may not notice them at first but things can start to get weird as they accumulate.
To avoid memory leaks, you should always make sure to properly clean up after your components using the `componentWillUnmount()` method.
example of Memory Leak 
```JSX
import {Component} from 'react';
class Counter extends Component{
 constructor(){
 super();
 this.state = {count: 0};
 this.incrementCount = this.incrementCount.bind(this);
 }

 incrementCount(){
 this.setState({count: this.state.count + 1});
 console.log(this.state.count);
 }

 componentDidMount(){
 this.interval = setInterval(()=>{
 this.incrementCount();
 },1000)
 }

 render(){
 return (<p>The current count is: {this.state.count}.</p>);
 }
}
export default Counter;
```
Above is Classed Based components
parenet Components
```jsx
import {useState} from 'react';
import {Counter} from './Counter';
function CounterController() {
 const [displayCounter,setDisplayCounter] = useState(true);
 function toggleCounter(){
 setDisplayCounter(!displayCounter);
 };
 return (
 <div className="App">
 {displayCounter ? <Counter /> : null}
 <button onClick={toggleCounter}>Toggle Count</button>
 </div>
 );
}
export default CounterController;
```
When the App component mounts, the Counter component will also mount and the timer will start running and incrementing the counter in the browser and in the console![[Pasted image 20250413115525.png]]
>[!WARNING]
>When you click the Toggle Count button, the Counter component will disappear. However, the timer created by the setInterval function in the Counter component is never cleared, and so it continues to run after the component is removed.

After the component is unmounted, React will log a message to the browser console to tell you that you’re attempting to call setState on an unmounted component![[Pasted image 20250413115656.png]]
Trying to call setState on an unmounted component won’t do anything, since an unmounted com‑ ponent doesn’t have state. But, as React’s error message points out, it’s indicative of a *memory leak.*
To fix this problem, you can use the componentWillUnmount method in the Counter component to call clearInterval, which will stop the timer before the Counter component is unmounted

**Fixing a memory leak**
```JSX
import {Component} from 'react';
class Counter extends Component{
 constructor(){
 super();
 this.state = {count: 0};
 this.incrementCount = this.incrementCount.bind(this);
 }

 incrementCount(){
 this.setState({count: this.state.count + 1});
 console.log(this.state.count);
 }

 componentDidMount(){
 this.interval = setInterval(()=>{
 this.incrementCount();
 },1000)
 }
 componentWillUnmount(){
 clearInterval(this.interval);
 }

 render(){
 return (<p>The current count is: {this.state.count}.</p>);
 }
}
export default Counter;
```
Now Counter will be properly unmounted and the timer will be cleared when it’s removed from the browser. If you click the Toggle Counter button again, the counter will start over as you would expect it to, because a new timer will be created.
## React.PureComponent
If you have a component that only accepts props and returns JSX, without modifying state or affecting anything outside of itself, that component is known as a “pure component.” It gets this name from the concept of a pure function.
>[!information]
>A key characteristic of a pure function is that it always returns the same result when given the same input.

Pure components are opportunities to improve the performance of your React user interface. Because their output only depends on props passed to them, a simple comparison of the previous props and the new props will tell you whether the component will change when re-­rendered.
One way to do this comparison is by using the shouldComponentUpdate lifecycle method along with React’s shallowCompare function.
## React.memo
Function components can also be pure components, but because they can’t use lifecycle methods or extend React.PureComponent, a different method is required to optimize them.
**React.memo()** is a higher-­order function, meaning that it wraps around another function and adds its functionality to that function.
When you wrap your function component in React.memo(), it performs a comparison of the previous and next props and skip rendering if they’re the same.
The name of React.memo() refers to memoization, which is the caching of the results of a function and using the cached result if the function has the same input as when the cache was created.
```jsx
import React from 'react';
function ExampleComponent(props){
 return (<p>Hi, {props.firstName}. This component returns the same thing when
given the same props.</p>);
}
export default React.memo(ExampleComponent);
```
## React.StrictMode
`React.StrictMode` is a component that you can wrap around your components to activate additional checks of your code and produce warning messages that can be helpful during development. The default Create React App application wraps the root component with a element to turn on strict mode for the entire component tree. But, you can also just use on parts of your application by applying it more selectively.

## RENDERING COMPONENTS
The end result of the mounting and updating stages of the lifecycle in React is a single rendered component, called the root component.
Remember that by `rendered` we mean that all of the JSX for the root component and its subcomponents has been parsed and the resulting tree of components has been created.
Once React’s work has been done and the tree of components has been created, it’s the job of a sepa‑ rate node package to render the component in a way that it can be seen and used by people.
## Rendering with ReactDOM
The most common place for a tree of React elements to end up being used is in a web browser. The library responsible for converting a React component into HTML and inserting it into the DOM and then managing updates to the DOM is *ReactDOM*.
ReactDOM includes several methods that you can use to interact with the DOM, but the one that’s absolutely necessary for every React application designed for the browser to use is `ReactDOM.render`.
```jsx
ReactDOM.render(
 <React.StrictMode>
 <App/>
 </React.StrictMode>,
 document.getElementById('root')
);
```
The beauty of ReactDOM.render is that it performs an incredible number of calculations and DOM manipulations, controls the timing of DOM updates, manages the virtual DOM, and more—but as far as you, the programmer, are concerned, ``*it’s a black box*``
## Virtual DOM
After the root component has been mounted, the job of ReactDOM.render is to monitor changes to the rendered element coming in from React and figure out the most efficient way to update the browser DOM to match the newly rendered application through a process called ``*reconciliation*``.
you can think of rendering a React UI as a continual process of replacing a previous tree of elements with a new one: and this is in fact what React is doing. But, once a new tree of elements gets to ReactDOM.render’s reconciliation process, it looks for the minimal set of changes and just makes those.
```jsx
<nav>
 <ul>
 <li><a href="/" className="active navlink">Home</a></li>
 <li><a href="/aboutus" className="navlink">About Us</a></li>
 </ul>
</nav>
```
## ReactDOMServer
ReactDOMServer renders React components and returns an HTML string. It can be used on a web server to generate the initial HTML for a React application, which can then be served to web browsers to speed up the initial loading of the user interface.
Once the initial HTML for the application is rendered on the server and served to a web browser, the regular ReactDOM renderer takes over and handles updates. This technique is referred to as “Isomorphic React” or “Universal React.”

## react-pdf 
With react-­pdf, you can use React components to render PDF files. The built-­in components for assembling PDFs include Document, Page, View, and Text. Once you’ve composed your PDF docu‑ ment using these components, you can render them in the browser using ReactDOM.render, or you can save them as PDF documents using ReactPDF.render.

## COMPONENT TERMINOLOGY
Components and elements are the building blocks of React. If you understand components and JavaScript, you’re more than halfway to being a React developer. React components come with a lot of terminology, however. To help you keep everything straight, here’s a handy overview of some of the most commonly used lingo in React component development
###### Class component: 
A class component is a React component created by extending React .Component or React.PureComponent.
###### Function component: 
A function component is a JavaScript function that returns JSX code.
###### State: 
State is the data in a React user interface that determines when updates will happen.
###### Props:
Props are the data that’s passed from a parent component to a child component. In JSX, props are created using attributes (in the name=value format).
###### Stateful component: 
A stateful component is a component that has internal state, stored in either the state object (in the case of class components) or created using hooks (in the case of function components).
###### Stateless component: 
A stateless component is one that doesn’t have its own internal state. Stateless components are also known as “dumb” components or “presentational” components.
###### Pure component:
A pure component is one that always returns the same output when given the same input.
###### Root component: 
The root component is the single component that contains all the other components in your React application. Rendering the root component (using ReactDOM) causes the entire component tree to be rendered.
###### Parent component/child component: 
As in the HTML DOM, the relationship between com‑ ponents in a React component tree is described using the terms parent and child.
###### Component lifecycle: 
The component lifecycle is the progression of events and methods that happen during the life of a React component. It starts with mounting and ends with unmounting. In between mounting and unmounting, the update lifecycle methods happen.

# React Data Flow
Data, and moving data between the different parts of an application, is a critical piece of any interactive user interface.
## ONE-WAY DATA FLOW
One of the defining characteristics of React that distinguishes it from most other front-end UI libraries is its use of one-way data flow, also known as **unidirectional data flow.**
> One-way data flow means that all of the data in a React application flows from parent components to child components.

. Another common way to describe the flow of data in React is
>[!information]
>“Data flows down (or downstream), and events flow up (or upstream).”


While one-way data flow eliminates a common cause of complexity and errors in user interfaces, it can also create confusion and frustration unless you fully understand the ins and outs of using it to your advantage
![[Pasted image 20250413135452.png]]
Unidirectional data flow doesn’t mean that child components can’t send data to parent components.Sending data from child components (for example, an input form) to parent components (for example, the form containing the input) is a critical part of interactivity.
in React, passing data downstream is done using props, like this:
`<SearchForm term={searchTerm} />`

 ##### Why One-Way Data Flow?
 Two-way data flow, also known as *bidirectional* data flow, where a component’s data can be modified by its parent and changes within the component can directly affect data in the parent, is convenient.
 However, it also increases the complexity of a user interface, and this, in turn, increases the potential for errors.
 **![[Pasted image 20250413135920.png]]**
 >[!warning]
 >In bidirectional data flow, it’s not possible to tell whether the view was updated by the user interacting with the view or by the data in the model changing.

![[Pasted image 20250413140104.png]]
A view in unidirectional data flow can be expressed as a simple
`function: V = function(data)
one thing to test: whether changing the state of the application modifies the view as expected.
#### PROPS
Props in React are the primary way that data is shared between parent components and child components. To create a prop, simply give a React custom element an attribute, using the `name=value` format. Inside the component instance created by that element, the attribute will become a property of the props object.
Here are some key points about props :  
- A component can receive any number of props. 
- A prop’s value can be of any type of JavaScript data or an expression that evaluates to a value or function. 
- Props are read-only.
###### Components Receive Props
```jsx
<Taco meat="chicken" produce={[cabbage,radish,cilantro]} sauce="hot" />
```
If Taco is a function component, this element is the same as the following JavaScript function call:
```jsx
Taco({meat:"chicken",produce:[cabbage,radish,cilantro],sauce:"hot"});
```
Inside the Taco function’s header, the object passed to the function is given the name props, which is how you can access it inside of the function
```jsx
function Taco(props){
 return (<p>Your {props.sauce} {props.meat} taco will be ready shortly.</p>
}
export default Taco;
```
###### Props Can Be Any Data Type
The props you pass to a component can be any type of JavaScript data, including any of the six primitive data types (`undefined`, `Boolean`, `Number`, `String`, `BigInt`, and `Symbol`) as well as `objects`, `functions`, `arrays`, and even ``null.``
###### Props Are Read-Only
Once data has been passed to a component using props, that data is treated as immutable. This means that although a component receives props, once those props are values inside the component, your component can’t change them.
>[! rule]
>This is the strictest rule in React: a component must act like a pure function with regard to its props.

The reason for this rule is that React only re-renders components in response to state changes. Props are the mechanism for updating components according to state changes. If you were to change the value of a prop inside a component, it would cause the internal data of your component to be out of sync with what’s displayed in your browser and the value of the prop would be reset by the parent component with the next render.
`changing props inside a component won’t have the effect that you want`
```jsx
import {useState} from 'react';
function App(){
 const [theNumber,setTheNumber] = useState(0);
 return (
 <PropsMutator theNumber = {theNumber} setTheNumber = {setTheNumber} />
 )
}
function PropsMutator(props){
 let myNumber = props.theNumber;
 const changeProp = ()=>{
 myNumber = myNumber + 1;
 console.log("my number is: " + myNumber);
 }
 return (
 <>
 <h1>My number is: {myNumber}</h1>
 <h1>props.theNumber is: {props.theNumber}</h1>
 <button onClick = {changeProp}>change myNumber</button><br />
 <button onClick={()=>{props.setTheNumber(props.theNumber + 1)}}>
 use setTheNumber
 </button>
 </>
 )
}
export default App;
```
![[Pasted image 20250413152242.png]]

## REACT STATE
The key to React’s ability to be reactive is the concept and object called state.
What Is state?
 In a React component, state is an object containing a set of properties that may change over the lifetime of the component. Changes to the properties in the state object control the behavior and updating of the component.
###### Initializing state
is the process of defining the properties of the state object and setting their initial values. The initial values are the values that will be used for the first rendering of a component.
>[!note]
>In JavaScript functions, data doesn’t persist between invocations of the function. Prior to React Hooks, React function components also had no way to preserve data between calls. For this reason, function components were previously known as stateless components.

With React Hooks, function components can hook into functionality of React, including the state object. The hook that makes this possible is useState.
```jsx
import {useState} from 'react'
function NewsFeed(props) {
const [date,setDate] = useState(new Date());
const [headlines,setHeadlines] = useState([]);

 return(
 <>
 <h1>Headlines for {date.toLocaleString()}</h1>
 ...
 </>
 )
}
export default NewsFeed;
```
###### The Difference between state and props
Props and state look similar at first glance: 
- They’re both JavaScript objects. 
- Changes to each of them cause components to update. 
- Both are data that are used by a component to generate the HTML output of the component.
The basic difference is that the props object is passed to a component by its parent, while state is managed within a component.
To put it another way, props is similar to a function parameter, while state is similar to a local (private) variable defined inside the function. You can pass values from the state of a parent component to a child component (where they become part of the props object), but a component cannot modify the state of its children.
###### Updating state
Once the initial state of a component has been set and the component has been rendered, updates to the component (and to its children, if it has any) happen when the state changes.
###### Why Use const with useState?
It may seem wrong to use const for a stateful variable, since the whole purpose of a stateful variable is to be changed and the whole purpose of const is to prevent a variable from being changed. Nevertheless, it is recommended that you use const with useState, and it actually does make sense when you think about how functions (and therefore function components) work.
`const [count, setCount] = useState(0);`
- You're **not changing `count` directly**.
- You’re using `setCount` to **tell React to update the internal state** and **re-render the component**.
- On the next render, `useState` gives you **a fresh new `count` value** — but it's still a `const`, because it won't change **within the same function call**.
To set a stateful variable that’s a primitive data type, simply pass the new value to the `function: setCounter(4);`
If the new value depends on the previous value, you should use a function to access the previous state and return the new value: 
`setCounter((prevState)=>{return prevState+1})`
The copy you make of an object or array can’t be just any copy. It needs to be a shallow copy. One of the easiest ways to make a **shallow copy,** which is widely used in React, is by using the spread operator (...).
###### SHALLOW COPIES AND THE SPREAD OPERATOR
 One of the most useful new tools in JavaScript is the spread operator. The spread operator is made up of three periods (...) and its job is to expand (or spread) the value of a string, array, or object into separate parts.
 The spread operator is useful in cases where you want to include all of the elements of an array or object in a new object or array, such as when you’re creating a new array or object that’s partially made up of an existing one.
 >[!warning]
 >JavaScript arrays are reference values 

 When you use the = operator to make a copy of an array, the new array still has a reference to the old one.
 ```javascript
 let arr = ['red','green','blue'];
 let newArr = arr;
 newArr.push('orange');
 console.log(arr)
 
```
 ![[Pasted image 20250413155447.png]]
To make a copy of an array that doesn’t reference the original one, you need to copy each element in the original array into a new array.The new array created in this way is called a ***shallow copy***.
```javascript
let numbers = [1, 2, 3];
let numbersCopy = [];
for (i = 0; i < numbers.length; i++) {
 numbersCopy[i] = numbers[i];
}

```
Another method is to use the slice function. ***slice*** returns a shallow copy of an array based on the start and end element indexes you provide. If you call slice on an array without passing in any arguments, it returns a shallow copy of the whole array:
```javascript
numbersCopy = numbers.slice();
```
Changing an Array with Spread
```javascript
numbersCopy = [...numbers,14];
```
###### Copying an Object with Spread
The spread operator can also be used to create a shallow copy of an object. A shallow copy of an object is a copy that only includes the properties, and not the prototype:
```javascript
let obj1 = { foo: 'bar', x: 0 };
let clonedObj = { ...obj1 };
```
Combining two objects with spread is as simple as combining two arrays:
```javascript
 let obj1 = { foo: 'bar', x: 0 }; 
 let obj2 = { food: 'taco', y: 1 }; 
 let mergedObj = { ...obj1, ...obj2 }
```
###### Structured Clone ( Recommended if supported)
```js
const deepCopy = JSON.parse(JSON.stringify(original));
const deepCopy = structuredClone(originalObj); // new advanced 
```

######  `structuredClone()` – A Better Deep Copy

| Feature             | `JSON.stringify()` | `structuredClone()` |
| ------------------- | ------------------ | ------------------- |
| Deep copy           | Yes                | Yes                 |
| Functions           | Removed            | Still not supported |
| `undefined` values  | Removed            | Preserved           |
| `Date` objects      | Turned to strings  | Properly cloned     |
| Circular references | Error              | Handled correctly   |
| RegExp, Map, Set    | Lost               | Preserved           |
| Typed Arrays, Blob  | Lost               | Supported           |
```js
const obj = {
  name: "Alice",
  age: undefined,
  createdAt: new Date(),
  nested: {
    a: 1,
  },
};
obj.self = obj; // Circular reference
const cloned = structuredClone(obj);
console.log(cloned.age); // undefined
console.log(cloned.createdAt instanceof Date); // true
console.log(cloned === obj); // false
console.log(cloned.self === cloned); // true
```
| Feature                        | `props`                                                        | `state`                                            |
| ------------------------------ | -------------------------------------------------------------- | -------------------------------------------------- |
| **Definition**                 | Immutable data passed from parent to child                     | Mutable data managed within the component          |
| **Who sets it?**               | Parent component                                               | The component itself (`useState`, `this.setState`) |
| **Can be changed internally?** | No – read-only                                                 | Yes – with `setState` or `useState`                |
| **Purpose**                    | Communication between components                               | Internal component data and interactivity          |
| **Triggers re-render?**        | Yes – when parent sends new props                              | Yes – when state changes                           |
| **Accessible in child?**       | Yes                                                            | Yes (via props if lifted or shared)                |
| **Can be passed down?**        | Yes – via JSX like `<Child propName={...} />`                  | ❌ No – unless lifted to parent and passed down     |
| **Mutability**                 | Immutable                                                      | Mutable                                            |
| **Scope**                      | External (controlled by parent)                                | Internal (controlled by component itself)          |
| **Storage type**               | Fixed at render unless changed by parent                       | Dynamic; can be updated using state updater        |
| **Best for**                   | Configuration, customization, and composition                  | Interactivity, local memory (input, toggle, etc.)  |
| **Lifespan**                   | Lasts for the lifetime of component (unless changed by parent) | Same, but can change at any time using setters     |
| **Example**                    | `<Card title="My Title" />`                                    | `const [count, setCount] = useState(0)`            |
- **Props**: External, read-only, for _receiving data_ from parents.
- **State**: Internal, changeable, for _managing component behavior/data_.

## EVENTS
HOW EVENTS WORK IN REACT
### Why SyntheticEvent is Still Useful Today

Although most modern browsers now handle events in a similar way, **React still uses SyntheticEvent** because it offers **consistent behavior** and some **extra helpful features** that native events don’t provide. The main benefit today is that it gives every developer the same experience, no matter what browser is being used.
Another advantage is that SyntheticEvent **hides the complex implementation details** of how React manages events behind the scenes. As developers, we don’t need to worry about how React links a `click` or `change` event to the real DOM—it just works. Even though it's possible to dig into how SyntheticEvent maps to native events, React's documentation purposely keeps this vague, because it’s **not something we usually need to worry about**. These internal details can change with new React versions, so it’s safer to just use the API React provides and trust it to handle things correctly.