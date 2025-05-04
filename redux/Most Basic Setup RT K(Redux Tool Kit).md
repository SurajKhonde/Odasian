Using <span style="color: #ffbd33;">Vite</span>– Fastest Way
```shell
npm create vite@latest my-app --template react 
cd my-app 
npm install 
npm run dev
```
#### Now Install Tailwindcss
```shell
npm install tailwindcss @tailwindcss/vite
```
####  vite.config.ts
```shell
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'
import tailwindcss from '@tailwindcss/vite'
// https://vite.dev/config/
export default defineConfig({
plugins: [react(),
tailwindcss(),
],
})
```
### src /index.css
```shell
@import "tailwindcss";
```
### Main.jsx
```shell
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';
import './index.css';
import { Provider } from 'react-redux';
import { store } from './redux/store';
ReactDOM.createRoot(document.getElementById('root')).render(
<Provider store={store}>
<App />

</Provider>

);

```
### index.html
```html
<!doctype html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<link rel="icon" type="image/svg+xml" href="/vite.svg" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Vite + React</title>
</head>
<body>
<div id="root"></div>
<script type="module" src="/src/main.jsx"></script>
</body>
</html>

```

Vite set Up done 

#### Redux Toolkit Setup
File Structure Example
```bash
/src
  /redux
    store.js
    counterSlice.js
  /components
    Navbar.jsx
  App.jsx
  main.jsx
  index.css

```
####  src/redux/counterSlice.js
```jsx
import { createSlice } from '@reduxjs/toolkit';
const counterSlice = createSlice({
  name: 'counter',
  initialState: { value: 0 },
  reducers: {
    increment: (state) => {
      state.value += 1;
    },
    decrement: (state) => {
      state.value -= 1;
    },
  },
});
export const { increment, decrement } = counterSlice.actions;
export default counterSlice.reducer;
```
### src/redux/store.js
```jsx
import { configureStore } from '@reduxjs/toolkit';
import counterReducer from './counterSlice';
export const store = configureStore({
  reducer: {
    counter: counterReducer,
  },
});

```
### src/App.jsx
```jsx
import { useDispatch } from 'react-redux';
import { increment, decrement } from './redux/counterSlice';
import Navbar from './components/Navbar';

export default function App() {
  const dispatch = useDispatch();

  return (
    <div>
      <Navbar />
      <div className="flex flex-col items-center mt-20 gap-4">
        <h2 className="text-3xl font-semibold">Counter</h2>
        <div className="flex gap-6">
          <button
            onClick={() => dispatch(increment())}
            className="bg-green-500 hover:bg-green-600 text-white px-6 py-2 rounded shadow"
          >
            Increment
          </button>
          <button
            onClick={() => dispatch(decrement())}
            className="bg-red-500 hover:bg-red-600 text-white px-6 py-2 rounded shadow"
          >
            Decrement
          </button>
        </div>
      </div>
    </div>
  );
}

```
#### src/main.jsx (Entry Point)
```jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';
import './index.css';
import { Provider } from 'react-redux';
import { store } from './redux/store';

ReactDOM.createRoot(document.getElementById('root')).render(
  <Provider store={store}>
    <App />
  </Provider>
);

```
**Run the App**
npm run dev
