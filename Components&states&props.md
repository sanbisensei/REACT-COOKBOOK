# What is a Component

- it is a Plain Old JS function.
- the function must Return "Something".
- The "Something" is the JSX.
- The component may have data private to itself. We call it **_"State"_**.
- The component may have data to share with other Components. We call them **_"Props"_**.

## State and Props

![state&props](./images/state&props.png)

- A component has its own private data which is called **_States_**. but this component has to interact with another component.
- to interact with other componets we need to pass something called **_props_**.
- **States**: states are datas managed inside a component.when state changes the component re-renders.
- **Props**: props are the argument we pass to another component to exchange data.props are read only.

## Difference between State and Normal variable

| State                             | Normal Variable                            |
| --------------------------------- | ------------------------------------------ |
| Managed by React                  | Managed by JavaScript                      |
| Changing state causes re-render   | Changing variable does NOT cause re-render |
| Preserves data between renders    | Gets recreated on every render             |
| Created using `useState()`        | Created using `let`, `const`, or `var`     |
| Used for UI-related reactive data | Used for temporary calculations            |

---

- example of Normal variable:

```jsx
export default function Counter() {
  let count = 0;

  function increase() {
    count++;
    console.log(count);
  }

  return <button onClick={increase}>Count: {count}</button>;
}
```

- the problems are :

1. `count` changes internally
2. React does not re-render
3. UI still shows 0

- example of state:

```jsx
import { useState } from "react";

export default function Counter() {
  const [count, setCount] = useState(0);

  function increase() {
    setCount(count + 1);
  }

  return <button onClick={increase}>Count: {count}</button>;
}
```

- What happens:

1. `setCount()` updates state.
2. React detects the change.
3. Component re-renders.
4. UI updates automatically.
