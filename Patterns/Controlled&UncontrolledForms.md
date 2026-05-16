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

---

## Controlled

```jsx
import { useRef, useState } from "react";

const ControlledForm = () => {
  const [form, setForm] = useState({ name: "", email: "", message: "" });
  const nameRef = useRef();
  const emailRef = useRef();
  const messageRef = useRef();

  const handleChange = (e) => {
    const { name, value } = e.target;
    setForm({ ...form, [name]: value });
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    if (!form.name) {
      nameRef.current.focus();
      return;
    }
    if (!form.email.includes("@")) {
      emailRef.current.focus();
      return;
    }
    if (!form.message) {
      messageRef.current.focus();
      return;
    }
    console.log("Form submitted:", form);
  };
  return (
    <form
      className="flex flex-col justify-center items-center border-2 border-blue-500"
      onSubmit={handleSubmit}
    >
      <h1>CONTROLLED</h1>
      <input
        className="border rounded-2xl p-2 my-3"
        name="name"
        type="text"
        ref={nameRef}
        value={form.name}
        onChange={handleChange}
        placeholder="Name"
      />
      <input
        className="border rounded-2xl p-2 my-3"
        name="email"
        type="email"
        ref={emailRef}
        value={form.email}
        onChange={handleChange}
        placeholder="Email"
      />
      <textarea
        className="border rounded-2xl p-2 my-3"
        name="message"
        ref={messageRef}
        value={form.message}
        onChange={handleChange}
        placeholder="Your message"
      />
      <button className="bg-blue-500 text-white p-1 rounded" type="submit">
        Send Feedback
      </button>
    </form>
  );
};

export default ControlledForm;
```

#### When to use ?

- Validate While typing (show error as user types). Basically before clicking submit button I wanna show error
- Disable submit button until form is valid
- Transform input(force uppercase,limit characters etc)

---

## unControlled

### with Ref

```jsx
import { useRef } from "react";

const UncontrolledForm = () => {
  const nameRef = useRef();
  const emailRef = useRef();
  const messageRef = useRef();

  const handleSubmit = (e) => {
    e.preventDefault();
    const name = nameRef.current.value;
    const email = emailRef.current.value;
    const message = messageRef.current.value;
    if (!name) {
      nameRef.current.focus();
      return;
    }
    if (!email.includes("@")) {
      emailRef.current.focus();
      return;
    }
    if (!message) {
      messageRef.current.focus();
      return;
    }

    console.log("Form submitted:", { name, email, message });
  };
  return (
    <form
      className="flex flex-col justify-center items-center border-2 border-amber-500"
      onClick={handleSubmit}
    >
      <h1>UNCONTROLLED</h1>
      <input
        className="border rounded-2xl p-2 my-3"
        type="text"
        ref={nameRef}
        placeholder="Name"
      />
      <input
        className="border rounded-2xl p-2 my-3"
        type="email"
        ref={emailRef}
        placeholder="Email"
      />
      <textarea
        className="border rounded-2xl p-2 my-3"
        ref={messageRef}
        placeholder="Your message"
      />
      <button className="bg-amber-500 text-white p-1 rounded" type="submit">
        Send Feedback
      </button>
    </form>
  );
};

export default UncontrolledForm;
```

#### When to use ?

- Simple form, no real time validation
- Just grab values on submit
- File inputs `<input type="file">` is always uncontrolled

### with Ref

```jsx
const UncontrolledFormNoRef = () => {
  const handleSubmit = (e) => {
    e.preventDefault();

    const formData = new FormData(e.target);
    const data = Object.fromEntries(formData.entries());
    console.log("Form Data:", data);
    alert(`Hello ${data.username}, your email is ${data.email}`);
  };
  return (
    <form
      className="flex flex-col justify-center items-center border-2 border-red-500"
      onSubmit={handleSubmit}
    >
      <h1>UNCONROLLED NO REF</h1>
      <input
        className="border rounded-2xl p-2 my-3"
        name="username"
        placeholder="Username"
      />
      <input
        className="border rounded-2xl p-2 my-3"
        name="email"
        type="email"
        placeholder="Email"
      />
      <button className="bg-purple-500 text-white p-1 rounded" type="submit">
        Submit
      </button>
    </form>
  );
};

export default UncontrolledFormNoRef;
```

#### When to use ?

- Super simple form
- No validation needed
- Just use FormData on submit

---

## Comparison Table

| Feature         | Controlled                                 | Uncontrolled (ref)                |
| --------------- | ------------------------------------------ | --------------------------------- |
| Data source     | `useState`                                 | `useRef`                          |
| Reads value     | every keystroke                            | only on submit                    |
| Re-renders      | yes, on every keystroke                    | no                                |
| Validation      | while typing                               | only on submit                    |
| Reset form      | `setForm({name:"", email:"", message:""})` | `nameRef.current.value = ""`      |
| Use value in UI | anytime                                    | only when you grab it             |
| File input      | not supported                              | always uncontrolled               |
| Code complexity | more code                                  | less code                         |
| Best for        | complex forms, real time feedback          | simple forms, just grab on submit |
