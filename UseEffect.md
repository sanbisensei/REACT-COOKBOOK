# What is useEffect?

- `useEffect` is a React Hook.
- it is used to handle **_side Effects_** inside functional components.
- side effects are operations that happen outside rendering UI.

---

- A side effect means:
  anything that happens outside the normal React rendering process.

---

## Ask yourself:

- "Do I need to do something AFTER React renders the UI?"

#### If YES → probably useEffect.

---

## common Use Cases

- Common Use Cases
- Fetching API data
- Updating the DOM
- Timers (setInterval, setTimeout)
- Event listeners
- Local storage operations
- console.log()

---

## 6 Usages of useEffect & Syntax

1. ```jsx
   // Runs after every Render
   useEffect(() => {
     // side-Effect
   });
   ```
2. ```jsx
   // Runs once After Mounting (Initial Render)
   useEffect(() => {
     // side-Effect
   }, []);
   ```
3. ```jsx
   // Runs only After the State Changes
   useEffect(() => {
     // side-Effects
   }, [state]);
   ```
4. ```jsx
   // Runs only After the Props Changes
   useEffect(() => {
     // side-Effects
   }, [props]);
   ```
5. ```jsx
   // Runs only After the Props and/or State Changes
   useEffect(() => {
     // side-Effects
   }, [props, state]);
   ```
6. ```jsx
   useEffect(() => {
     // side-Effects
     return () => {
       // side-Effects Cleanup
     };
   }, [props, state]);
   ```

---

- `useEffect` runs after rendering, and its behavior depends on the dependency array.

- Or more specifically:
  1. No dependency array → runs after every render.
  2. Empty dependency array **_[]_** → runs once after initial render.
  3. Dependencies **_[value]_** → runs when those dependencies change.

---

# DEEP DIVE

## 1. useEffect() without Dependency

```jsx
import { useEffect, useState } from "react";

const Practice = () => {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log("Runs after EVERY render");
  });

  return (
    <div>
      <h1>{count}</h1>

      <button onClick={() => setCount(count + 1)}>Increase</button>
    </div>
  );
};

export default Practice;
```

### When it runs

- Initial Render
- Every Re-render
- Every State Change

---

## 2. useEffect with Empty Dependency

```jsx
import { useEffect } from "react";

const Practice = () => {
  useEffect(() => {
    console.log("Runs only once");
  }, []);

  return (
    <div>
      <h1>We Shall learn useEffect() today</h1>
    </div>
  );
};

export default Practice;
```

### Common Real World Usage

- API Calls
- Initial Data Fetching
- Authentication Check

---

## 3. useEffect With State Dependency

```jsx
import { useEffect, useState } from "react";

const Practice = () => {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log("Count changed");
  }, [count]);

  return (
    <div>
      <h1>{count}</h1>

      <button onClick={() => setCount(count + 1)}>Increase</button>
    </div>
  );
};

export default Practice;
```

### Runs When

- Initial Render
- count changes
- Does NOT Run When
  - Other states change.

---

## useEffect With Props Dependency

- Parent Component

```jsx
import { useState } from "react";
import Child from "./Child";

const Parent = () => {
  const [name, setName] = useState("Sanbi");

  return (
    <div>
      <Child username={name} />

      <button onClick={() => setName("React Master")}>Change Name</button>
    </div>
  );
};

export default Parent;
```

- Child component

```jsx
import { useEffect } from "react";

const Child = ({ username }) => {
  useEffect(() => {
    console.log("Prop changed");
  }, [username]);

  return <h1>{username}</h1>;
};

export default Child;
```

## Runs When Props Change

---

## 5. useEffect With Multiple Dependencies

```jsx
import { useEffect, useState } from "react";

const Practice = () => {
  const [count, setCount] = useState(0);
  const [name, setName] = useState("Sanbi");

  useEffect(() => {
    console.log("Count or Name changed");
  }, [count, name]);

  return (
    <div>
      <h1>{count}</h1>
      <h2>{name}</h2>
      <br />
      <button onClick={() => setCount(count + 1)}>Increase Count</button>
      <br />
      <button onClick={() => setName("React Dev")}>Change Name</button>
    </div>
  );
};

export default Practice;
```

#### Observation

- If we click Increase Count we will see output in the console coz its state is changing so React re-renders the UI thus useEffect function runs.
- If we click Change name , the useEffect will execute only once thus we see only one output in console, after that output how much we click the 'Change Name' it will it show any output coz state is not changing

### Runs When

- count changes
- name changes

---

## useEffect Cleanup Function

```jsx
import { useEffect, useState } from "react";

const Practice = () => {
  const [show, setShow] = useState(true);

  return (
    <div>
      <button onClick={() => setShow(!show)}>Toggle Component</button>

      {show && <Timer />}
    </div>
  );
};

const Timer = () => {
  useEffect(() => {
    const interval = setInterval(() => {
      console.log("Timer Running");
    }, 1000);

    return () => {
      clearInterval(interval);
      console.log("Cleanup Done");
    };
  }, []);

  return <h1>Timer Component</h1>;
};

export default Practice;
```

### Why Cleanup is Important

- Without cleanup:
  - Memory leaks happen
  - Multiple intervals may run
  - Event listeners stay attached
- Cleanup happens:
  - Before component unmounts
  - Before effect re-runs
