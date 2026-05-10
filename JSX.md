# What is JSX?

- JSX = JavaScript XML(Extensible Markup Language).

- jsx allows html like syntax inside javascript,react uses it to create isolated components.

- when we write in jsx the browser does not understand that , so ==_**BABEL**_== transpiles those jsx to plain javascript so that the browser can understand.
- Example:

```jsx
 <h1>Sanbi<h1>
```

it transpiles to this -

```javascript
React.createElement("h1", null, "Sanbi");
```

- for boolean, undefined and null the jsx will not show anything.
- we can not use if/else but we can use ternary operation.
- no loops are available in jsx . We need to use `map`
-
