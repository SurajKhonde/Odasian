<span style="color: #ff6033;">What is a Re-render in React?</span>
A re-render in React means that a component updates and re-executes its function, creating a new UI based on state, props, or context changes.
React follows a virtual DOM diffing algorithm, where:
- It creates a new virtual DOM tree.
- Compares it with the previous virtual DOM.
- Updates only the changed parts in the real DOM (efficient rendering).
Why Does React Re-render?
React re-renders a component when:<span style="color: #ff6033;"> State Changes (useState)</span>
```javascript
const [count, setCount] = useState(0);
const increment = () => setCount(count + 1); // Triggers re-render
```
```javascript
const Child = ({ value }) => <p>{value}</p>;
const Parent = () => <Child value={Math.random()} />; // Re-renders Child
```
 Context Value Changes (<span style="color: #ff6033;">useContext</span>)
 ```javascript
 const ThemeContext = createContext();
const App = () => (
  <ThemeContext.Provider value="dark">
    <Child />
  </ThemeContext.Provider>
); // Re-renders all children if value changes

```
**Parent Component Re-renders**
- If a parent component **re-renders**, all its child components **re-render**, even if their props didn’t change.
 New References for Objects or Functions
 ```javascript
const obj1 = { key: "value" };
const obj2 = { key: "value" };
console.log(obj1 === obj2); // false ❌ (Different references)
```
How to Optimize and Prevent Unnecessary Re-renders?
Use React.memo() for Pure Components
```javascript
const MemoizedComponent = React.memo(({ value }) => {
  console.log("Rendered");
  return <p>{value}</p>;
});
```
Use useCallback() to Memoize Functions
```javascript
const handleClick = useCallback(() => {
  console.log("Clicked");
}, []);
```
Prevents new function creation on every render.
**Use useMemo() to Memoize Expensive Calculations**
```javascript
const computedValue = useMemo(() => expensiveCalculation(data), [data]);
```
Prevents unnecessary recalculations.

Use Immutable State Updates
```javascript
const computedValue = useMemo(() => expensiveCalculation(data), [data]);

```

**How does rendering work in React ?**
React uses a Virtual DOM as a layer between the developer’s description of how the UI should appear and the actual rendering effort performed by the application. To render UI in the browser, the app must modify the Document Object Model (DOM) of the browser.
*`The virtual DOM (VDOM) is a programming concept where an ideal, or “virtual”, representation of a UI is kept in memory and synced with the “real” DOM by a library such as ReactDOM. This process is called reconciliation.`*
![[image (4).png]]
React reconciliation uses a diffing mechanism. It examines two trees — the existing virtual DOM and the new one — to discover the most effective way to change them. <span style="color: #ff6033;"> To avoid the slower worst-case situation of O(n³), the aim is to do the comparison in linear time, O(n).</span>

<span style="color:#ff336c;"> Pure Components in React</span>
A Pure Component in React is a component that only re-renders if its props or state change. It avoids unnecessary re-renders by implementing **shallow** comparison in shouldComponentUpdate() (for class components) or using React.memo() (for functional components).

<span style="color:#e77c12;">Nothing is really pure</span>
React doesn’t enforce purity — it’s **up to you** to make sure the component:
- Doesn’t depend on **external state**
- Doesn’t have **side effects in rendering**
- Doesn’t mutate its props
- And that you’re not triggering re-renders in some hidden way (like context updates)
So technically, any component can be **"impure"** if you’re not careful, even if you use `React.memo()` or extend `PureComponent`.

This is a really cool example that shows **why just using `React.memo` isn't enough** if you're not careful.
The Problem: Hidden Re-renders in `React.memo`
```javascript
import React, { useState } from "react";
const Child = React.memo(({ user }) => {
  console.log("👶 Child rendered");
  return <div>{user.name}</div>;
});

export default function Parent() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <button onClick={() => setCount(count + 1)}>Increment: {count}</button>
      <Child user={{ name: "John" }} />
    </div>
  );
}

```
#### ❓What you expect:
- `Child` is wrapped in `React.memo`, and the `user` prop looks the same every time (`{ name: "John" }`), so it **shouldn’t re-render**, right?
#####  What actually happens:
 `Child` still re-renders **every time** the button is clicked.
##### Why?
Because of this line:
`<Child user={{ name: "John" }} />`
- You're passing a **new object** every render.
- Even though the value is the same, the **reference is different**.
- `React.memo` does **shallow comparison**, so:
`{ name: "John" } !== { name: "John" } // true`
#### How to fix it?
Move the object **outside the render** (so it stays stable):
```javascript
const staticUser = { name: "John" };
function Parent() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <button onClick={() => setCount(count + 1)}>Increment: {count}</button>
      <Child user={staticUser} />
    </div>
  );
}

```
Now the `Child` component really **won't re-render** when `count` changes.
- `React.memo()` only helps if your **props are stable**
- Be careful with:
    - **Objects**
    - **Arrays**
    - **Functions**  
        because they’re often created fresh every render and break shallow comparison
in React, **props are read-only** for the child component.
- When a parent component  passes props to a **child**, the child can use them, but  cannot modify them directly.
- If you try to change a prop inside a child, React will complain (and it’s considered a bad practice).
Props are **immutable** from the child’s perspective:
```javascript
function Parent() {
  return <Child name="John" />;
}
function Child(props) {
  props.name = "Mike"; // ❌ This is NOT allowed
  return <div>{props.name}</div>;
}

```
React will throw a warning (or silently ignore in some cases), but it breaks the idea of **one-way data flow**.
What if the child needs to change something?
- The parent must pass a **callback function** (like `onChange`, `setValue`, etc.)
- The child calls that function to **request an update**, and the parent updates the value via `useState`.
```javascript
function Parent() {
  const [name, setName] = useState("John");

  return <Child name={name} setName={setName} />;
}

function Child({ name, setName }) {
  return (
    <div>
      <p>{name}</p>
      <button onClick={() => setName("Mike")}>Change Name</button>
    </div>
  );
}
```
- `name` is still passed down as a **read-only prop**
- `setName` is a **function** the child can call to **trigger a change**
##### One-way Data Flow
```
Parent → Child (props)
Child → Parent (callbacks)

```
###### Counter without Re-render
```jsx
import React, { useState } from "react";
import Child from "../Child";
const staticUser = { name: "John Doe" };
const Parent = () => {
  const [count, setCount] = useState(0);
  return (
    <div className="min-h-screen bg-blue-50 flex flex-col items-center justify-center p-6">
      <div className="bg-white p-8 rounded-xl shadow-xl w-full max-w-lg">
        <h1 className="text-3xl font-bold text-center text-blue-800 mb-4">
          Count: {count}
        </h1>
        <button
          onClick={() => setCount(count + 1)}
          className="bg-blue-500 text-white px-6 py-2 rounded-lg hover:bg-blue-700 transition-colors"
        >
          Increment
        </button>
        {/* Static object pass कर रहे हैं */}
        <div className="mt-6">
          <Child user={staticUser} />
        </div>
      </div>
    </div>
  );
};

export default Parent;
```

`Child.jsx`
```jsx
import React from "react";
const Child = ({ user }) => {
  console.log("Child rendered 🚀");
  return (
    <div className="bg-gray-200 p-4 rounded-lg shadow-md">
      <h2 className="text-xl font-semibold text-gray-700">User: {user.name}</h2>
    </div>
  );
};
export default Child;
```
here What Happen 
When react in Parent component add or Increment then child also re render due to parent Re render because of `state` changes.
**The issue is why child re render Unnecessarily??**
`Child.jsx`
```jsx
import React from "react";
const Child = useMemo(({ user }) => {
  console.log("Child rendered 🚀");
  return (
    <div className="bg-gray-200 p-4 rounded-lg shadow-md">
      <h2 className="text-xl font-semibold text-gray-700">User: {user.name}</h2>
    </div>
  );
});
export default Child;
```

###### Done, Khush to bahoot honge aaj But ....(Devil lies in details )
Key Concepts to Understand
`React.memo()`: It performs shallow comparison of the props to determine whether the component needs to re-render or not.
*Shallow comparison*: React will check if the props' references have changed. If the `reference` is the same, React will skip re-rendering the component (since React assumes that the data inside the object hasn't changed).
 *What is an Object Reference?*
When we talk about object references in JavaScript, we're referring to how JavaScript handles objects in memory. Objects in JavaScript are reference types, which means when you store an object in a variable, the variable stores a reference (or pointer) to the actual object in memory, not the object itself.
This means that if you modify the object, the reference stays the same, but the contents of the object can change. Similarly, if you assign the object to another variable, both variables will point to the same reference (i.e., the same object).
```jsx
let obj1 = { name: "John" };
let obj2 = obj1; // obj2 is now pointing to the same object as obj1
obj1.name = "Doe"; // This will also change obj2.name because both variables point to the same object.
console.log(obj2.name); // Output: "Doe"
```
*Key Takeaways About Object References and useMemo:*
- If the reference to the object changes (i.e., the object is completely different in memory), `useMemo` will recalculate.
- If the reference remains the same (even if the values inside the object change), `useMemo` will not recalculate.

Why React.memo works best with Primitives:
- **Primitives** (string, number, boolean) ka **reference** hamesha unique hota hai jab unki value change hoti hai.
    - Agar aapke paas ek primitive data (e.g., number or string) hai, to React `React.memo` ko use karke efficiently re-render kar sakta hai jab uski value change hoti hai.  
- **Complex Objects** (like arrays or objects) ka **reference** tab tak same hota hai jab tak unka address memory mein change na ho. Agar aap **object ke andar value change karte ho**, to React ko ye **na dikhega** (kyunki reference same raha). Isliye, React ko us object ko **re-render** karne ke liye force karne ki zarurat padti hai (e.g., using `useState` or `useEffect`).
**With Primitive (like string or number):**
```jsx
const ChildComponent = React.memo(({ count }) => {
  console.log('Child rendered!');
  return <div>Count: {count}</div>;
});

const ParentComponent = () => {
  const [count, setCount] = useState(0);

  return (
    <div>
      <button onClick={() => setCount(count + 1)}>Increase</button>
      <ChildComponent count={count} />
    </div>
  );
};

```
In the above example, since count is a primitive value (number), React.memo can easily compare the previous and new value of count. If the count changes, the child component will re-render.
`Object:`
```jsx
const ChildComponent = React.memo(({ user }) => {
  console.log('Child rendered!');
  return <div>{user.name}</div>;
});

const ParentComponent = () => {
  const [user, setUser] = useState({ name: 'Suraj' });

  const updateName = () => {
    setUser({ ...user, name: 'Ravi' }); // This creates a new object, so React.memo will re-render
  };

  return (
    <div>
      <button onClick={updateName}>Change Name</button>
      <ChildComponent user={user} />
    </div>
  );
};

```
React.memo will **re-render** the `ChildComponent` only when the reference to the `user` object changes. If we had just modified the properties of the existing `user` object (e.g., `user.name = 'Ravi'`), the reference wouldn't change, and `React.memo` wouldn't detect it as a change.

*Not Ideal (using React.memo with API Data):*
```jsx
const UserProfile = React.memo(({ userData }) => {
  console.log('User Profile rendered!');
  return <div>{userData.name}</div>;
});

// API call:
const fetchData = async () => {
  const response = await fetch('/api/user');
  const data = await response.json();
  setUserData(data); // Using this data directly with React.memo is not ideal if the reference stays the same.
};

```
**if the object reference remains the same** (even if the values inside the object change), React.memo will **not re-render**. That's why **React.memo** with API data (especially complex objects) may not always work as expected without creating a **new object reference**.
######  Conclusion:
- **`React.memo` works well with primitives** (strings, numbers, booleans), where it can easily compare values and decide whether to re-render or not.
- **For complex objects** like arrays or objects, **you need to ensure that the reference changes** if you want React to re-render the component. You can achieve this by creating a **new object** using techniques like spreading (`{ ...oldObject, newProperty: value }`) or using `useState`.
- **Avoid blindly using `React.memo`** with API data unless you are sure that object references are being handled properly.

>[! warning]
>Aapki baat bilkul sahi hai ki React.memo ko primitives ke sath prefer karna chahiye. Complex objects ke sath React.memo ka use tabhi karna chahiye jab aapko pata ho ki object reference change ho raha hai.