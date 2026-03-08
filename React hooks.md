## $${\color{red}Reacts \ Hooks}$$

#### React Hooks are functions that allow you to use state and other React features in functional components. 
---

### 1. `useState`

Manage **local component state**.

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <>
      <p>{count}</p>
      <button onClick={() => setCount(count + 1)}>+</button>
    </>
  );
}
```

**Key points**

* Returns `[state, setState]`
* Triggers **re-render** on update
* Can store any type

```js
const [user, setUser] = useState(null);
```

---

### 2. `useEffect`

Handle **side effects**.

Examples:

* API calls
* DOM manipulation
* timers
* subscriptions

```jsx
import { useEffect } from "react";

useEffect(() => {
  console.log("Component mounted");

  return () => {
    console.log("Cleanup on unmount");
  };
}, []);
```

#### Dependency patterns

Run once:

```js
useEffect(() => {}, []);
```

Run on change:

```js
useEffect(() => {}, [value]);
```

Run every render:

```js
useEffect(() => {});
```

---

### 3. `useContext`

Access **global state via Context API**.

```jsx
import { useContext } from "react";
import { ThemeContext } from "./ThemeContext";

function Component() {
  const theme = useContext(ThemeContext);
  return <div>{theme}</div>;
}
```

Used for:

* authentication
* theme
* global settings

---

### 4. `useRef`

Persist values **without re-rendering**.

```jsx
import { useRef } from "react";

function Input() {
  const inputRef = useRef(null);

  const focus = () => {
    inputRef.current.focus();
  };

  return (
    <>
      <input ref={inputRef} />
      <button onClick={focus}>Focus</button>
    </>
  );
}
```

Use cases:

* DOM access
* store mutable values
* timers
* previous state

---

### 5. `useMemo`

Memoize **expensive calculations**.

```jsx
import { useMemo } from "react";

const expensiveValue = useMemo(() => {
  return heavyCalculation(data);
}, [data]);
```

Prevents unnecessary recalculation.

---

### 6. `useCallback`

Memoize **functions**.

```jsx
import { useCallback } from "react";

const handleClick = useCallback(() => {
  console.log("Clicked");
}, []);
```

Used for:

* preventing child re-renders
* stable function references

Often used with `React.memo`.

---

### 7. `useReducer`

Alternative to `useState` for **complex state logic**.

```jsx
import { useReducer } from "react";

function reducer(state, action) {
  switch (action.type) {
    case "increment":
      return { count: state.count + 1 };
    default:
      return state;
  }
}

const [state, dispatch] = useReducer(reducer, { count: 0 });

dispatch({ type: "increment" });
```

Best for:

* complex state
* predictable updates
* Redux-like logic

---

### 8. `useLayoutEffect`

Like `useEffect` but runs **before browser paint**.

```jsx
useLayoutEffect(() => {
  console.log("Runs before paint");
}, []);
```

Use cases:

* DOM measurements
* layout calculations

---

### 9. `useId`

Generate **stable unique IDs**.

```jsx
import { useId } from "react";

const id = useId();

<label htmlFor={id}>Name</label>
<input id={id} />
```

Useful for accessibility.

---

### 10. `useTransition`

Handle **non-urgent UI updates**.

```jsx
import { useTransition } from "react";

const [isPending, startTransition] = useTransition();

startTransition(() => {
  setData(newData);
});
```

Helps keep UI responsive.

---

### 11. `useDeferredValue`

Delay updates to improve performance.

```jsx
const deferredQuery = useDeferredValue(query);
```

Useful for:

* search inputs
* large lists

---

### 12. `useImperativeHandle`

Customize ref behavior in **forwardRef** components.

```jsx
import { useImperativeHandle, forwardRef } from "react";

const Input = forwardRef((props, ref) => {
  useImperativeHandle(ref, () => ({
    focus() {
      console.log("focus called");
    }
  }));
});
```

---

### Custom Hook Pattern

Reusable logic.

```jsx
function useFetch(url) {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch(url)
      .then(r => r.json())
      .then(setData);
  }, [url]);

  return data;
}
```

Usage:

```js
const data = useFetch("/api/posts");
```

---

### Hook Rules

**1. Only call hooks at top level**

❌ Wrong

```js
if (condition) {
  useEffect();
}
```

✅ Correct

```js
useEffect(() => {
  if (condition) {
  }
});
```

---

**2. Only call hooks inside React components or custom hooks**

❌

```js
function helper() {
  useState();
}
```

---

### Common Hook Stack

Typical modern React component:

```jsx
function Component() {
  const [data, setData] = useState([]);
  const ref = useRef(null);

  const filtered = useMemo(() => filter(data), [data]);

  useEffect(() => {
    fetchData().then(setData);
  }, []);

  const handleClick = useCallback(() => {
    console.log(filtered);
  }, [filtered]);
}
```

---
