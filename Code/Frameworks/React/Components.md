# Components

Since React 16.8 (with [[Hooks]]), **functional components** are preferred because they are:

- **Simpler and cleaner**: Easier to write and read than class components.
- **Hook-enabled**: Can use `useState`, `useEffect`, and other Hooks for state and side effects.
- **More reusable**: Promote better separation of concerns and logic reuse via custom hooks.
- **Performance-friendly**: Slightly lighter than classes, with potential optimizations.

They've become the standard way to build React components.

```jsx
import React, { useState } from 'react';

const App = () => {
  const [todos, setTodos] = useState([]);

  const addTodo = text => {
    setTodos([...todos, { id: Date.now(), text }]);
  };

  const deleteTodo = id => {
    setTodos(todos.filter(todo => todo.id !== id));
  };

  return (
    <div>
      <TodoForm onAdd={addTodo} />
      <TodoList todos={todos} onDelete={deleteTodo} />
    </div>
  );
};

export default App;
```

## JSX

**JSX** is a syntax extension that looks like HTML but compiles to `React.createElement()` calls. Under the hood, it builds a **JavaScript object (React element)** representing the UI, which React uses to construct the **virtual DOM** and efficiently update the real DOM.

``` jsx
const element = <h1>Hello, world!</h1>;
```

## Default Export

- It allows other files to **import** this component easily, like so:

```js
import App from './App';
```

- It's especially useful in small projects or single-entry components, where there's only one main thing the file exports.

If you removed that line, you'd need to export explicitly:

```js
export const App = () => { ... }
```

And then import it like:

```js
import { App } from './App';
```

So in short: `export default App;` makes it simpler to import `App` without curly braces. It's a common practice for main components.

| Use Default Export When:                                      | Avoid Default Export When:                   |
| ------------------------------------------------------------- | -------------------------------------------- |
| The file only exports one main thing (component or function). | The file exports multiple things.            |
| You want simpler import syntax.                               | You want explicit and consistent imports.    |
| You’re okay with less strict tooling support.                 | You want better tooling and refactor safety. |

## Props

Props are short for **properties** — they’re inputs passed from a parent component to a child component in React.

- Props are **read-only** inside the child.
- They allow components to be **dynamic and reusable** by receiving different data.
- Passed as attributes in JSX, e.g.:
  `<TodoList todos={list} onDelete={handleDelete} />`.
- Accessed in the child as function parameters or `props` object.

```jsx
const TodoList = ({ todos, onDelete }) => (
  <ul>
    {todos.map(todo => (
      <li key={todo.id}>
        {todo.text}
        <button onClick={() => onDelete(todo.id)}>Delete</button>
      </li>
    ))}
  </ul>
);

export default TodoList;
```

## Unidirectional data flow

- The parent component holds the **source of truth** — the `todos` array and the `onDelete` function.
- The parent **passes these as props** (`todos` and `onDelete`) down _to_ the `TodoList` component.
- `TodoList` **receives** these props and **renders** the list accordingly.
- When you click a delete button inside `TodoList`, it **calls `onDelete(todo.id)`**, which is actually a function defined _in the parent_.
- The parent then **updates its state** (removes the todo), causing a **re-render**.
- This updated state is then passed _down again_ as props to `TodoList`.

Data flows **down** from parent to child via props, and **actions flow up** via callbacks (like `onDelete`) passed down, which notify the parent to update state. The child never directly changes the props — it only signals intent.

This unidirectional flow keeps state predictable and easier to debug.

|Concept|React|Angular|
|---|---|---|
|Data flow|Props down from parent to child|Inputs down from parent to child|
|Communication upward|Callbacks passed as props|EventEmitters (@Output)|
|State management|Usually in parent or external store|Usually in parent or service|
|Unidirectional flow?|Yes|Yes|

## Parent - Child Communication

### Context API

- Allows passing data **deeply** through the component tree without threading props at every level.
- Child components can **consume context directly**, skipping intermediate parents.
- Useful for global or shared data like themes, user info, or localization.
- Still unidirectional—context value flows down, but updates can be triggered by a provider.

### Refs (for imperative communication)

- Parent can get a **ref to a child component or DOM node**.
- Allows the parent to **call methods or access properties directly on the child**.
- This breaks the pure declarative flow and is generally discouraged unless needed (e.g., focus control).
- Usually used for DOM manipulation or controlling child behaviors imperatively.

### State management libraries (Redux, Zustand, MobX, Jotai, etc.)

- State lives outside components in a **shared store**.
- Components read from and write to the store directly.
- This decouples parent-child relationship since siblings or distant components can communicate without props.
- But internally, store updates still trigger unidirectional flows.

### Event emitters or pub-sub libraries

- Components can communicate by **publishing and subscribing to events** on a shared event bus.
- Less common in React but possible with external libraries or custom implementations.
- Can make debugging and tracing harder due to indirect communication.

| Method                 | Direction    | Use case                            | Notes                                   |
| ---------------------- | ------------ | ----------------------------------- | --------------------------------------- |
| Props + callbacks      | Down + up    | Standard parent-child communication | Recommended default                     |
| Context API            | Down (value) | Global/shared data                  | Avoid overusing for frequent changes    |
| Refs                   | Imperative   | Imperative control                  | Use sparingly, breaks declarative model |
| State stores           | Global/Local | App-wide state sharing              | Scales well, decouples components       |
| Event emitters/pub-sub | Any          | Loose component communication       | Can become hard to maintain             |

## Conditional Rendering

We can have multiple returns, where the first return that meets conditions will render. The others will just be ignored. 

```jsx
const [showWelcome, setShowWelcome] = useState(false)
{showWelcome ? <Welcome /> : null}
```

## Short Circuit Evaluation

If there is no need for an 'else' in an if/else statement (or in ternary operator), we can use short circuits instead.  
Example:

```js
const [showWelcome, setShowWelcome] = useState(false)
{showWelcome && <Welcome />}
```

_However, there is the possibility of weird behaviors, using short circuit evaluation:_
[Use ternaries rather than && in JSX](https://kentcdodds.com/blog/use-ternaries-rather-than-and-and-in-jsx)

## Forms

To add custom form handling we will need to disable the default like this:

```jsx
const handleSubmit = (e) => {
	e.preventDefault()
	// Custom Handling
}
...
<form onSubmit={handleSubmit}>
...
```

We will need to bind our inputs to state values:

```jsx
const [name, setName] = useState('')
	...
<input type='text' id='name' name='name' value={name} 
	onChange={(e) => setName(e.target.value}/>
```

## One-way Data Binding

- In **React**, it means the **UI (View)** reflects the **state (Model)**.
- When state updates, the UI **automatically re-renders**.
- But the flow is **one-way**: changes go **from state → view**, not the other way directly.
- The view can't update the model _by itself_ — it triggers an event handler.

![[Pasted image 20250715083450.png]]

|Concept|Description|
|---|---|
|State → UI|UI elements reflect the current state|
|UI → State (via events)|You update state through handlers (e.g. `onChange`, `onClick`)|
|No two-way sync|React doesn’t auto-bind inputs like Angular does — you control everything|
|Controlled components|Inputs use `value` from state and `onChange` to update it manually|

_In **Angular**, you can choose between **one-way** and **two-way data binding**, depending on what you need._





---
