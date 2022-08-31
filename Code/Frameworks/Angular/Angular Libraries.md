# Interesting Angular Libraries

- Angular Material
- Prime NG
- Ag-grid
- Ng Bootstrap 🤮

## Creating Libraries Best Practices

> ng new my-library-project --create-application=false
> cd my-library-project
> ng generate library @h3ar7b3a7/some-library-name


> (cd dist/h3ar7b3a7/some-library-name && npm link) && ng build --watch
> npm link @internal/nucleus-styling

*We can create a script to run these in package.json*

1.  Add "npm" to "devDependencies"


---
#Angular