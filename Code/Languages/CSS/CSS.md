# CSS
## Normalize
[Normalize.css](https://necolas.github.io/normalize.css/) is a modern, HTML5-ready alternative to CSS resets
It makes browsers render all elements more consistently and in line with modern standards. It precisely targets only the styles that need normalizing.

> npm install normalize.css

_We can also include the normalize stylesheet in our global files to be included on project setup. Check out this projects parent README for more info, or 'myGlobalFiles' for an example._

## Style Management
We can include paths for angular to look for our stylesheets in angular.json.
Here is an example:

```
"options": {
  ...
  "styles": [
    "src/styles.scss"
  ],
  "stylePreprocessorOptions": {
    "includePaths": [
      "src/default-styles"
    ]
  },
  "scripts": []
},
```

This way we do not have to include the path when importing a stylesheet:

```
@import "normalize";
```

## Naming Conventions
**BEM** (Block Element Modifier) is a highly useful, powerful, and simple naming convention that makes your front-end code easier to read and understand, easier to work with, easier to scale, more robust and explicit, and a lot more strict. It is a methodology that helps you to create reusable components and code sharing in front-end development.

**SMACSS** is another way to examine your design process and a way to fit those rigid frameworks into a flexible thought process. It is an attempt to document a consistent approach to site development when using CSS.

- We should use **classes** to style our elements
- We should (try to) not override styles

## CSS
Cascading Style Sheets (CSS) is a style sheet language used for describing the presentation of a document written in a markup language such as HTML. CSS is a cornerstone technology of the World Wide Web, alongside HTML and JavaScript.

### Relative Units
We should prefer to use relative units (unit / relative to):

- **em** - Font size of the parent, in the case of typographical properties like font-size, and font size of the element itself, in the case of other properties like width.
- **ex** - x-height of the element's font.
- **ch** - The advance measure (width) of the glyph "0" of the element's font.
- **rem** - Font size of the root element.
- **lh** - Line height of the element.
- **vw** - 1% of the viewport's width.
- **vh** - 1% of the viewport's height.
- **vmin** - 1% of the viewport's smaller dimension.
- **vmax** - 1% of the viewport's larger dimension.

### Custom Properties

We can define custom properties like this:

```

element {
  --main-bg-color: brown;
}

```

Since they are scoped to the class they are in we can use the :root pseudo class:

```

:root {
  --main-bg-color: brown;
}

```

We can then use the value in its scope like this:

```

element {
  background-color: var(--main-bg-color);
}

```

_We should however consider that custom properties are not supported by older browsers._

## SCSS or Sass
Sass (short for syntactically awesome style sheets) is a preprocessor scripting language that is interpreted or compiled into Cascading Style Sheets (CSS). SassScript is the scripting language itself.

### Variables
we can create variables, like this:

```
$base-color: #c6538c;
$border-dark: rgba($base-color, 0.88);
```

And use them in our classes:

```
.alert {
  border: 1px solid $border-dark;
}
```

_When used in classes they are scoped to the class. When used outside the class, they are scoped to the whole stylesheet._

### Mixin
Mixins allow us to define styles that can be re-used throughout your stylesheet:

```
@mixin reset-list {
  margin: 0;
  padding: 0;
  list-style: none;
}
```

And to apply them we use include:

```
element {
  @include reset-list;
}
```

_We can even use mixins inside another mixin._

### &
The ampersand can be used to refer to parent blocks. For example:

```
a {
  color:#ff0000;
    &:hover {
      color:#0000ff;
    }
}
```

Will be processed to:

```
a {
  color:#ff0000;
}

a:hover {
  color:#0000ff;
}
```

We can find some advanced examples [here](https://github.com/pluralsight-styling-angular-apps/demos-v2/tree/module-04-15).

## Conditional Styling
### Using [class]
In template:

```
[class.green]="event.time === '9:00 PM'"
```

In stylesheet:

```
.green{
  color: green;
}
```

### Using [ngClass]
In template:

```
[ngClass]="{ blue: event.time === '7:00 PM' }"
[ngClass]="getClass(event)"
```

In component.ts:

```
getClass(event: Event) {
  const isAtEight = event.time === '8:00 PM'
  return { bold: isAtEight }
}
```

Or:

```
getClass(event: Event) {
  if(event.time === '8:00 PM')
    return 'green bold'
  return ''
}
```

Or:

```
getClass(event: Event) {
  if(event.time === '8:00 PM')
    return ['green', 'bold']
  return []
}
```

_We can pass it an object inline, or return it with a function._

### Using [style]
In template:

```
[style.color]="'red'"
```

### Using [ngStyle]
In template:

```
[ngStyle]="{ 'font-style': event.time === '7:00 PM' ? 'italic' : 'normal' }"
[ngStyle]="getStyle()"
```

In component.ts:

```
getStyle() : any {
  if(event.time === '7:00 PM')
    return { 'font-style': 'italic', 'font-weight': 'bold' }
  return {}
}
```

_We need to use any as return type because the objects returned have different members._



---
#Styling #CSS