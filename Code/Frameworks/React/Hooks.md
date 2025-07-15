# Hooks

## State Hook

When we want page content to change using functions the page will need to rerendered that content. 
For this it will need to be aware of the 'state'. For this we use the 'useState' import.

```js
const [count, setCount] = useState(initialCount);
```

We can then use setCount() to change the value and re-render.

## Effect Hook

We can create __side-effects__ every time a page is rendered.  It is a simple and powerful tool in React, but it's easy to misuse, especially as apps grow.

With an empty array as second argument the `useEffect` will only run on the initial render. We can use this when fetching data.

When we pass a value it will run again when this value changes. We can return a __cleanup function__ to prevent memory leaks.

Example:

```js
const [size, setSize] = useState(window.innerWidth)
	useEffect(() => {
		window.addEventListener('resize', () => {setSize(window.innerWidth)})
		return () => {
			window.removeEventListener('resize', () =>{
				setSize(window.innerWidth)
			})
		}
	}
```

### ✅ When to Use `useState`

|Situation|Why it's Good|
|---|---|
|Component-local state (e.g. form input)|Keeps state simple and close to where it's used|
|UI state (e.g. toggle, modal open/close)|No need for global management|
|Short-lived state|No persistence needed, and won't be reused elsewhere|
|State that doesn’t affect other components|Reduces complexity and re-renders are isolated|
|Simple data (booleans, numbers, strings)|Ideal for handling basic UI flags and interactions|

### ❌ When **Not** to Use `useState`

|Situation|Why to Avoid|
|---|---|
|**Shared state** across many components|Better handled by Context, a store (Redux, Zustand, Jotai), etc.|
|**Deeply nested prop drilling** needed|Indicates poor structure; consider lifting state or using context|
|**Derived state from props**|Can cause inconsistencies; use memoization or compute directly|
|**Complex state logic** (many transitions)|Prefer `useReducer` for better structure and testability|
|**Persistent state** (e.g. synced with backend or localStorage)|Consider effects, stores, or external handling|
|**Frequent updates across many components**|Leads to performance issues; use a shared reactive store instead|

### 🔁 Gray Area (Be Cautious)

|Situation|Notes|
|---|---|
|State reused in sibling components|Might be okay short-term, but lift it or use context soon|
|State that feeds `useEffect`|Can be fine, but make sure it doesn't create complex dependencies|
|Async state updates|Watch out for race conditions or stale closures|

## React Query

- It's a **custom hook**, not a built-in React hook like `useState` or `useEffect`.
- It's specifically designed to **fetch, cache, and manage asynchronous data** (like from an API).
- It uses React’s lifecycle internally, but adds smart data management features.

> npm install @tanstack/react-query

or

> yarn add @tanstack/react-query

```jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import { QueryClient, QueryClientProvider } from '@tanstack/react-query';
import App from './App';

// Create a client
const queryClient = new QueryClient();

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <QueryClientProvider client={queryClient}>
      <App />
    </QueryClientProvider>
  </React.StrictMode>
);
```

Example:

```jsx
import { useQuery } from '@tanstack/react-query';

const fetchUsers = async () => {
  const res = await fetch('https://api.example.com/users');
  if (!res.ok) throw new Error('Failed to fetch');
  return res.json();
};

const Users = () => {
  const { data, isLoading, error } = useQuery({
    queryKey: ['users'],
    queryFn: fetchUsers,
  });

  if (isLoading) return <p>Loading...</p>;
  if (error) return <p>Error: {error.message}</p>;

  return (
    <ul>
      {data.map(user => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
};
```

### 🔑 `queryKey: ['users']` — What it does:

1. Uniquely identifies the query
    - React Query uses this key to **cache, track, and deduplicate** requests.
    - If another component also calls `useQuery({ queryKey: ['users'], ... })`, React Query **reuses the cached result** instead of fetching again.
2. Triggers re-fetching when the key changes
    - If you include variables in the key (e.g., `['user', userId]`), React Query knows to re-run the query when `userId` changes.

```js
const { data, isLoading, error, refetch, isFetching } = useQuery({ ... });
```

- `data` – the result of your API call
- `isLoading` – true while the data is initially loading
- `isFetching` – true if a background fetch is happening (e.g. refetching)
- `error` – if something went wrong
- `refetch` – a function to manually trigger a re-fetch

### Caching

By default, React Query **caches data** using the `queryKey`, and:

|Trigger|Will it refetch?|Notes|
|---|---|---|
|Component mounts (first time)|✅ Yes|It fetches and caches|
|Same `queryKey` mounts again|❌ No (uses cache)|It serves from cache unless the data is stale|
|Window refocus|✅ Yes (by default)|It assumes you may want fresh data|
|Network reconnect|✅ Yes (by default)|Handles flaky connections well|
|Manual call to `refetch()`|✅ Yes|You control when to update|
|Cache becomes "stale" (by time)|✅ Maybe|Controlled by `staleTime` setting (default: 0 ms)|
|Background polling|✅ Optional|You can enable it with `refetchInterval`|

### React Query Devtools

For debugging, you can add:

> npm install @tanstack/react-query-devtools

or

> yarn add @tanstack/react-query-devtools

```jsx
import { ReactQueryDevtools } from '@tanstack/react-query-devtools';

<QueryClientProvider client={queryClient}>
  <App />
  <ReactQueryDevtools initialIsOpen={false} />
</QueryClientProvider>
```

_Open the Devtools panel in your app (usually a small floating button) to inspect queries, cache, status, and more._

## Reference Hook

Unlike `useEffect` this hook does not trigger re-render. It preserves value and is mainly used to target DOM nodes/elements (for example inputs).

- Holds values across renders **without triggering re-renders**
- Most common use: **referencing DOM elements** (`<input ref={ref} />`)
- Can also store **mutable variables** like timers, previous values, or stable callback references
- `.current` is where the value lives (`ref.current`)
- Updates to `.current` are **not reactive** — use `useState` if the UI needs to respond

```jsx
function TextInputWithFocusButton() {
	const inputEl = useRef(null)
	const onButtonClick = () => {
		inputEl.current.focus()
	}
	return (
		<>
			<input ref={inputEl} type="text" />
			<button onClick={onButtonClick}>Focus the input</button>
		</>
	)
}
```

### ✅ When to Use `useRef`

|Situation|Why it's a Good Fit|
|---|---|
|**Accessing a DOM element**|To focus an input, scroll to a div, etc.|
|**Storing a mutable value**|Holds data that persists across renders **without causing re-renders**|
|**Avoiding stale closures**|Store latest value to use inside callbacks/effects|
|**Tracking previous values**|Like previous props or state without triggering re-renders|
|**Timeouts/intervals/abort controllers**|Store timer IDs or side-effect handles across renders|
|**Imperative control of child components**|Use with `forwardRef` to expose methods (rare)|

_`useRef` isn’t a hack — it’s a **low-level escape hatch**.  
Used properly (or wrapped in custom hooks), it supports **clean, efficient patterns** for timers, previous values, and stable references._

### ❌ When **Not** to Use `useRef`

|Situation|Why to Avoid|
|---|---|
|**You need reactivity (UI updates)**|`useRef` changes **don’t cause re-renders** — use `useState` instead|
|**Storing derived data**|Compute from props/state instead, or memoize it|
|**Global/shared state**|Use `Context` or a state store, not refs|
|**Avoiding prop drilling**|Use context or composition — refs won’t help|
|**Synchronizing remote data**|Refs aren't observable — use `useEffect` and state instead|

## Reducer Hook

...




## Custom Hooks

Telltale signals you should create a custom hook:

- **Repeated logic** across components
- Managing **complex state or effects**
- Encapsulating **side effects** (e.g., timers, subscriptions)
- Sharing **behavior or stateful logic** cleanly
- Abstracting **imperative code or refs**
- Improving **readability and reusability**

### Examples

#### useDebounce

```js
import { useState, useEffect } from 'react';

function useDebounce(value, delay = 300) {
  const [debouncedValue, setDebouncedValue] = useState(value);

  useEffect(() => {
    const handler = setTimeout(() => setDebouncedValue(value), delay);

    return () => clearTimeout(handler); // Cleanup on value or delay change
  }, [value, delay]);

  return debouncedValue;
}

export default useDebounce;
```

```jsx
function SearchInput() {
  const [text, setText] = useState('');
  const debouncedText = useDebounce(text, 500);

  useEffect(() => {
    // Trigger API call or expensive calculation here
    console.log('Searching for:', debouncedText);
  }, [debouncedText]);

  return (
    <input
      value={text}
      onChange={e => setText(e.target.value)}
      placeholder="Search..."
    />
  );
}
```

#### usePrevious

```js
import { useRef, useEffect } from 'react';

function usePrevious(value) {
  const ref = useRef();

  useEffect(() => {
    ref.current = value; // Update ref after render
  }, [value]);

  return ref.current; // Return previous value (before update)
}

export default usePrevious;
```

```jsx
import React, { useState } from 'react';
import usePrevious from './usePrevious';

function Counter() {
  const [count, setCount] = useState(0);
  const prevCount = usePrevious(count);

  return (
    <div>
      <p>Now: {count}</p>
      <p>Before: {prevCount}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```




---


