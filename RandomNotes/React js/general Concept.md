##### What is Encapsulation?
Encapsulation means hiding internal details and exposing only what is necessary. It’s about protecting internal state and logic from being directly accessed or modified from the outside.
In React, we use *components* to encapsulate:
- State (`useState`, `useReducer`)
- UI (`return JSX`)
- Behavior (functions inside the component)
No Encapsulation
```javascript
let count = 0;
function Counter() {
  count++; //  External global variable
  return <p>{count}</p>;
}

```
- State lives outside the component
- Anyone can change it
- React doesn’t track it = buggy UI
good way
```javascript
function Counter() {
  const [count, setCount] = useState(0); // State is private to the component
  return <button onClick={() => setCount(count + 1)}>{count}</button>;
}
```
- State is **inside** the component
- Other components can’t touch it
- Fully reactive and self-contained

Encapsulation in Components Also Means:
- Don’t leak state or internal logic unless needed
- Only expose props and callbacks if you _want_ others to interact
- Wrap business logic in **custom hooks** for separation and safety

Example with Custom Hook (**Encapsulating logic**):
```javascript
function useCounter() {
  const [count, setCount] = useState(0);
  const increment = () => setCount(c => c + 1);
  return { count, increment };
}

```
Now any component using `useCounter()` gets a clean, **encapsulated** counter