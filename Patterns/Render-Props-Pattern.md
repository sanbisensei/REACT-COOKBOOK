# Render Props Pattern

---

## what is it?

- A Render prop pattern uses a prop but the value of the prop expects a function which return a JSX.
- So we need to take control on the rendering , so we need some dynamic behavior into it and we know nothing better a function ca do this type of thing.
- so imagine a function that can return a jsx dynamically and that function i can pass as a props to a component.Thats Render props pattern.

---

## Basic Syntax

- Component Part:

  ```jsx
  function LogicComponent({ render }) {
    const name = "Sanbi";

    return render(name);
  }
  ```

- Use this anywhere like this:

  ```jsx
  <LogicComponent render={(name) => <h1>Hello {name}</h1>} />
  ```

---

## Use Cases

- when writing an reusable component library with flexibility in mind

---

## Pitfall

- debugging can be a challenge
- performance problem ,because in every render it creates new inline function. so the aliternative pattern is **_HOOK PATTERN_**.
- mixing render props pattern and **_Higher Order Component Pattern_**.

---

- Learn this pattern not to write it but to understand if other code base uses it coz we have better alternatives now
