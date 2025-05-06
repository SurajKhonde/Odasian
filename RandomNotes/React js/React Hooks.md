## `useRef` 
`useRef` React का एक Hook है।
ये आपको कोई भी value बिना re-render कराए स्टोर करने देता है।
ये एक container object देता है जिसमें .current नाम की property होती है।
आप इसमें कुछ भी (DOM element, number, object) रख सकते हो।
English version 
The `useRef` hook returns a mutable object with a .current property that you can use to store a value. Unlike `useState`, updating a `useRef` value does not trigger a component re-render. 
###### फिर `useRef` क्यों चाहिए?
Problem —
React में जब आप `useState` से value बदलते हो तो पूरा component re-render होता है।
लेकिन कई बार हमें ऐसी value चाहिए जो:
- बदलती रहे
- पर component दोबारा re-render ना हो
Example: Timer, Previous Value, Form Element Access
Solution —
ऐसी situation में हम `useRef` यूज करते हैं।

###### जब-जब हम `useRef` का यूज़ करते हैं:
Situation	Why `useRef`?
- किसी `DOM` element को access करना	जैसे input field को focus करना
- कोई mutable (बदलने वाला) data रखना	जैसे previous value याद रखना
- Timer ID, Interval ID को store करना	ताकि stop कर सको
Basic Syntax:
```jsx
import { useRef } from 'react';
const myRef = useRef(initialValue);
```
`initialValue` वो value है जो आप start में रखना चाहते हो।
बाद में आप `myRef.current` से access करोगे या change करोगे।

अगर `useRef` से value store हो जाती है और re-render भी नहीं होता, तो हम हर जगह `useRef` क्यों नहीं इस्तेमाल करते?
चलो इसको धीरे-धीरे और compare करके समझते हैं कि:

`useState` क्यों use करें?
`useRef` क्यों नहीं हर जगह इस्तेमाल कर सकते?
###### `useState` (Recommended for UI)
```jsx
const [count, setCount] = useState(0);
return <h1>{count}</h1>;

const [name, setName] = useState("");
<input value={name} onChange={(e) => setName(e.target.value)} />
```
जब `count` change होता है → re-render होता है → UI पर नया count दिखता है
हर बदलाव पे React को पता चलता है
आप validation, character limit, auto formatting आदि आराम से कर सकते हो
###### `useRef` (Not recommended for UI)
```jsx
const countRef = useRef(0);
const increase = () => {
  countRef.current += 1;
};
return <h1>{countRef.current}</h1>;
//Form Field Example
// Using only `useRef`
const nameRef = useRef("");
<input ref={nameRef} />

```
`countRef.current` बदलेगा, लेकिन **React दुबारा render नहीं करेगा**,  
इसलिए `<h1>{countRef.current}</h1>` में पुराना ही दिखेगा

###### Final Rule of Thumb
- **UI में दिखाना है? → `useState`**
- **बस value रखना है silently? → `useRef`**

What is `useRef()`?
![[Pasted image 20250429142145.png]]
The `useRef()` Hook is a built-in React feature that persists values between component re-renders. Unlike state variables managed by `useState`, values stored in a ref object remain unchanged across renders, making it ideal for scenarios where data doesn't directly affect the UI but is essential for the component's behavior.

##### How does React `useRef()` work?
When React encounters a `useRef()` Hook, it returns a plain JavaScript object with a single property: `current`. This `current` property stores mutable values, which can be of any type, from simple values like numbers and strings to complex objects, functions, or even references to DOM elements.
![[Pasted image 20250429142819.png]]
React assigns the initial value you define to the `current` property of the returned reference. React will set the value of the useRef to `undefined` if you don't provide an initial value. Importantly, you can update this `current` value directly without triggering a re-render of the component.
```jsx
import { useRef } from "react";
    function MyComponent() {
      const reference = useRef(true);
      console.log(reference.current); // true
    }
```
Also, the returned reference object is mutable. You can update the `current` value directly, as shown in the snippet below.
```jsx
import { useRef } from "react";
    function MyComponent() {
      const reference = useRef(true);
      const handleUpdate = () => {
        reference.current = !reference.current;
      };
      console.log(reference.current); // true
      return <button onClick={handleUpdate}>Update</button>;
    }
```
Clicking the “Update” button changes the `reference.current` value from `true` to `false` and the other way around.
###### Use cases of useRef() React Hook
Beyond its ability to persist values, the `useRef()` Hook has several vital roles in React applications:
**Accessing DOM elements**
Imagine a login page where users need to enter their username and password. To enhance the user experience, you can automatically direct their focus to the username field as soon as the page loads.
To achieve this, use the `useRef` 's capacity to access rendered DOM elements. This feature returns the referenced DOM element and its properties, providing room for direct manipulations.
```jsx
import { useRef, useEffect } from “react”
    function Login() {
      const usernameRef = useRef(null)
      
      useEffect(() => {
        usernameRef.current.focus()
      }, [])
     return (
       <>
        <form>
          <input type="text" ref={usernameRef} />      
        </form>
       </>
     )
    }
```
###### Why Developers Often Showcase `focus() `with `useRef`?
But `useRef` ≠` focus()` — It's Just One Use Case
The truth is:
> `useRef` can give you access to **any DOM element**, not just inputs, and thus all **native methods** & **properties** that element supports.
For example:
- For a `<div>`:
    - `ref.current.innerText`
    - `ref.current.style.backgroundColor`
- For a `<video>`:
    - `ref.current.play()`
    - `ref.current.pause()
- For a `<canvas>`:
    - `ref.current.getContext("2d")`

So the **focus on `focus()`** is simply because it’s **easy to demo**, **not because it’s the main purpose** of `useRef`.