# React
[Official React Website](https://reactjs.org/)  
[More Docs on Typescript](https://www.typescriptlang.org/docs/handbook/react.html)

### Create an application
In the folder where we want to create our application:  
>npx create-react-app some_name		|	yarn create react-app some_name  

Flag to create including typescript: 
>--template typescript  

Typescript is a typed superset of JavaScript. Typing is useful for maintaining bigger projects over a long time.  
  
To build a production application:  
>npm run build		|	yarn build

### Other libraries
To add [Typescript](https://create-react-app.dev/docs/adding-typescript/) to the project:  
>npm install --save typescript @types/node @types/react @types/react-dom @types/jest  

or  

>yarn add typescript @types/node @types/react @types/react-dom @types/jest  

And then rename the file extensions from *.js to *.tsx

To add[React Icons](https://www.npmjs.com/package/react-icons):  
>npm install react-icons --save  

or  

>yarn add react-icons

To add [values.js](https://github.com/noeldelgado/Values.js/):  
>npm install values.js --save

## State Hook
When we want page content to change using functions the page will need to rerendered that content. 
For this it will need to be aware of the 'state'. For this we use the 'useState' import.

	const [count, setCount] = useState(initialCount);

We can then use setCount() to change the value and re-render.

## Effect Hook
We can create 'side' effects everytime a page is rerendered. For this we use the 'useEffect' import. 
With an ampty array as second argument the useEffect will only run on the initial render. We can use this when fetching data. 
When we pass a value it will run again when this value changes. We can return a 'cleanup' function to prevent memory leaks.  
Example:
 
	const [size, setSize] = useState(window.innerWidth)
	useEffect(() => {
		window.addEventListener('resize', () => {setSize(window.innerWidth)})
		return () => {
			window.removeEventListener('resize', () => {setSize(window.innerWidth)})
		}
	}
	
This will become particularly useful when we use conditional rendering, because there will be a lot more renders.

## Conditional Rendering
We can have multiple returns, where the first return that meets conditions will render. The others will just be ignored. 

## Short Circuit Evaluation
If there is no need for an 'else' in an if/else statement (or in ternary operator), we can use short circuits instead.  
Example:

	const [showWelcome, setShowWelcome] = useState(false)
	{showWelcome && <Welcome />}
	
Instead of: 

	const [showWelcome, setShowWelcome] = useState(false)
	{showWelcome ? <Welcome /> : null}

## Forms
To add custom form handling we will need to disable the default like this:

	const handleSubmit = (e) => {
		e.preventDefault()
		// Custom Handling
	}
	...
	<form onSubmit={handleSubmit}>
	...

We will need to bind our inputs to state values:

	const [name, setName] = useState('')
	...
	<input type='text' id='name' name='name' value={name} 
	onChange={(e) => setName(e.target.value}/>

## Reference Hook
Unlike useEffect this hook does not trigger re-render. It preserves value and is mainly used to target DOM nodes/elements (for example inputs).

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

## Reducer Hook



---
#JavaScript 