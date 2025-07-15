# React

[Official React Website](https://reactjs.org/)  
[More Docs on Typescript](https://www.typescriptlang.org/docs/handbook/react.html)

React (also known as React.js or ReactJS) is a free and open-source front-end [[JavaScript]] library for building user interfaces based on UI components. It is maintained by Meta (formerly Facebook) and a community of individual developers and companies. React can be used as a base in the development of single-page or mobile applications. However, React is only concerned with state management and rendering that state to the DOM, so creating React applications usually requires the use of additional libraries for routing, as well as certain client-side functionality.

## Create an application

In the folder where we want to create our application:
>npx create-react-app some_name		|	yarn create react-app some_name

Flag to create including typescript:
>--template typescript

Typescript is a typed superset of JavaScript. Typing is useful for maintaining bigger projects over a long time.  
  
To build a production application:
>npm run build		|	yarn build

### Adding Typescript

To add [Typescript](https://create-react-app.dev/docs/adding-typescript/) to the project:

>npm install --save-dev typescript @types/react @types/react-dom

or  

>yarn add --dev typescript @types/react @types/react-dom

And then rename the file extensions from *.js to *.tsx

## Adding Other Libraries

- To add [React Icons](https://www.npmjs.com/package/react-icons):

>npm install react-icons --save

or

>yarn add react-icons

- To add [values.js](https://github.com/noeldelgado/Values.js/):

>npm install values.js --save

or

> yarn add value.js





---
#JavaScript 