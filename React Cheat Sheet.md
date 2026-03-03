## $${\color{red}⚛️ \ React \ Cheat \ Sheet}$$

### 
**React** – a JavaScript library for building user interfaces (component-based, declarative, virtual DOM).


---

### 🧱 Core Concepts

### Component (Function Component)

```jsx
function Button({ label }) {
  return <button>{label}</button>;
}

export default Button;
```

✔️ PascalCase
✔️ Must return JSX
✔️ Props are function arguments

---

### JSX Rules

* Must return a single root element
* Use `className` instead of `class`
* JS inside `{}`

```jsx
const name = "John";
return <h1>Hello {name}</h1>;
```

---

### Props

```jsx
function Card({ title, children }) {
  return (
    <div>
      <h2>{title}</h2>
      {children}
    </div>
  );
}
```

Usage:

```jsx
<Card title="Hello">
  <p>Content</p>
</Card>
```

---

### State – `useState`

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <button onClick={() => setCount(count + 1)}>
      {count}
    </button>
  );
}
```

✔️ State update triggers re-render
✔️ Never mutate state directly

---

### Effects – `useEffect`

```jsx
import { useEffect } from "react";

useEffect(() => {
  console.log("Mounted");

  return () => console.log("Cleanup");
}, []);
```

Dependency array:

* `[]` → on mount
* `[value]` → when value changes
* none → every render

---

### 🔁 Rendering Lists

```jsx
const items = ["A", "B", "C"];

return (
  <ul>
    {items.map((item, index) => (
      <li key={index}>{item}</li>
    ))}
  </ul>
);
```

✔️ `key` must be stable and unique

---

### 🧠 Hooks Overview

| Hook          | Purpose                       |
| ------------- | ----------------------------- |
| `useState`    | Local state                   |
| `useEffect`   | Side effects                  |
| `useRef`      | DOM reference / mutable value |
| `useMemo`     | Memoized value                |
| `useCallback` | Memoized function             |
| `useContext`  | Consume context               |
| `useReducer`  | Complex state logic           |

---

### `useRef`

```jsx
const inputRef = useRef(null);

<input ref={inputRef} />
```

✔️ Does NOT trigger re-render
✔️ Used for DOM access

---

### `useMemo`

```jsx
const expensiveValue = useMemo(() => {
  return heavyCalculation(data);
}, [data]);
```

✔️ Prevents recalculation

---

### `useCallback`

```jsx
const handleClick = useCallback(() => {
  console.log("Clicked");
}, []);
```

✔️ Prevents function recreation

---

### 🌍 Context API

```jsx
const ThemeContext = createContext();

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Layout />
    </ThemeContext.Provider>
  );
}

function Layout() {
  const theme = useContext(ThemeContext);
}
```

✔️ Avoid prop drilling

---

### 📦 Forms (Controlled Component)

```jsx
const [value, setValue] = useState("");

<input
  value={value}
  onChange={(e) => setValue(e.target.value)}
/>
```

✔️ React controls input state

---

### 🚦 Conditional Rendering

```jsx
{isLoggedIn && <Dashboard />}

{isLoggedIn ? <Dashboard /> : <Login />}
```

---

### 🎯 Event Handling

```jsx
<button onClick={handleClick}>Click</button>
```

✔️ camelCase events
✔️ Pass function reference, not invocation

---

### 🔥 React Router (Client Routing)

**React Router**

```jsx
import { BrowserRouter, Routes, Route } from "react-router-dom";

<BrowserRouter>
  <Routes>
    <Route path="/" element={<Home />} />
    <Route path="/about" element={<About />} />
  </Routes>
</BrowserRouter>
```

---

### ⚡ Performance Tips

✔️ Use keys properly
✔️ Memoize heavy components (`React.memo`)
✔️ Avoid unnecessary state
✔️ Split components
✔️ Lazy load routes:

```jsx
const About = React.lazy(() => import("./About"));
```

---

### 🧪 Custom Hook

```jsx
function useToggle(initial = false) {
  const [state, setState] = useState(initial);
  const toggle = () => setState(s => !s);
  return [state, toggle];
}
```

✔️ Must start with `use`
✔️ Reusable logic

---

### 🧩 React 18+ Features

* Concurrent rendering
* `useTransition`
* `useDeferredValue`
* Automatic batching
* Suspense improvements

---

### 📁 Common Project Structure

```
src/
 ├─ components/
 ├─ pages/
 ├─ hooks/
 ├─ context/
 ├─ services/
 └─ App.jsx
```

---

### 🛠 Dev Tools

* **React Developer Tools** – inspect components
* **Vite** – fast dev server
* **Create React App** (legacy)

---

### 🧠 Mental Model

React =

```
UI = f(state)
```

Change state → React re-renders → DOM updates efficiently (Virtual DOM diffing).

