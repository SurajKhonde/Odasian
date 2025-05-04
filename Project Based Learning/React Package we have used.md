#### `React`
![[Pasted image 20250428094332.png]]
How Install React 
`npm i react`
what is in it ?
![[Pasted image 20250428095841.png]]
what is it have?
all word started with use are hooks like `useState, useEffects , useRefs `
>[!warning ]
>React is most useful package if you want to work In React Project

How to check what is in it ?
`import * as react from "react"`
`console.log(react)`

####  `react-dom`
![[Pasted image 20250428101352.png]]

how to install  react-dom
`npm i react-dom`
**The main working  is Inject Our React code inside the Html**
```jsx
import { createRoot } from 'react-dom/client';
function App() {
  return <div>Hello World</div>;
}
const root = createRoot(document.getElementById('root'));
root.render(<App />);
```

#### `react-router-dom`
##### Essential React Router Concepts
These are the most important and commonly used exports. If you're building React apps with routing, you’ll use these **almost every time**:

| Name              | What It Does                                 | Where/How It’s Used                                               |
| ----------------- | -------------------------------------------- | ----------------------------------------------------------------- |
| `BrowserRouter`   | Main wrapper for routing in web apps         | Wrap your whole app in this (usually in `main.jsx` or `index.js`) |
| `Routes`          | Container for your `<Route />`s              | Put inside `<BrowserRouter>`                                      |
| `Route`           | Defines a path and the component to show     | Inside `<Routes>`                                                 |
| `Navigate`        | Redirects to another route programmatically  | Use inside components to auto-redirect                            |
| `Link`            | Like an `<a>` tag, but without page reload   | Used for internal navigation                                      |
| `NavLink`         | Like `Link`, but supports “active” styling   | Great for navbars and sidebars                                    |
| `useNavigate`     | Hook to navigate programmatically            | Useful inside event handlers or `useEffect`                       |
| `useParams`       | Get `:id` or other route params              | Inside components rendered by a `<Route>`                         |
| `useLocation`     | Get current URL/location object              | Useful to know where you are in the app                           |
| `useSearchParams` | Read/update query string (e.g. `?sort=name`) | Easy query param handling                                         |
| `Outlet`          | Placeholder for nested route rendering       | Used in layouts or parent routes                                  |
#### ` React Redux`
![[Pasted image 20250428104445.png]]
![[Pasted image 20250428104606.png]]
`npm i react-redux`
