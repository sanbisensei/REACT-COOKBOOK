# Controlled & Uncontrolled Forms

## State Vs Refs

### State

- State is React's way of managing dynamic data that drives rendering.
- When State changes, the component re-renders.

### Refs

- Refs let you access and manipulate DOM elements.
- It also allows you to access persistent values without triggering re-renders.

---

## Why We need this Pattern?

- In forms, refs are often used to focus inputs or access DOM elements directly.
- However, refs do not update React state or trigger re-renders.
- This can make the UI and form data harder to keep in sync.
- To handle forms properly, React provides two approaches:
  - Controlled Components
  - Uncontrolled Components
