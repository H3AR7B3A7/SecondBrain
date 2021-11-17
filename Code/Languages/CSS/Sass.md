# Sass / Scss
Sass (short for syntactically awesome style sheets) is a preprocessor scripting language that is interpreted or compiled into Cascading Style Sheets ([[CSS]]). SassScript is the scripting language itself.

Sass consists of two syntaxes. The original syntax, called "the indented syntax," uses a syntax similar to Haml. It uses indentation to separate code blocks and newline characters to separate rules. The newer syntax, "SCSS" (Sassy CSS), uses block formatting like that of CSS. It uses braces to denote code blocks and semicolons to separate rules within a block. The indented syntax and SCSS files are traditionally given the extensions .sass and .scss, respectively.

CSS3 consists of a series of selectors and pseudo-selectors that group rules that apply to them. Sass (in the larger context of both syntaxes) extends CSS by providing several mechanisms available in more traditional programming languages, particularly object-oriented languages, but that are not available to CSS3 itself. When SassScript is interpreted, it creates blocks of CSS rules for various selectors as defined by the Sass file. The Sass interpreter translates SassScript into CSS. Alternatively, Sass can monitor the .sass or .scss file and translate it to an output .css file whenever the .sass or .scss file is saved.

The indented syntax is a metalanguage. SCSS is a nested metalanguage, as valid CSS is valid SCSS with the same semantics.

SassScript provides the following mechanisms: variables, nesting, mixins, and selector inheritance.

## Installing SASS
-   Install Node.js:
    [https://nodejs.org/en/download/](https://nodejs.org/en/download/)
    
-   Install Sass (with npm):
    > npm install -g sass
    
-   Install Sass (with Chocolatey):
    > choco install sass

## Compiling SCSS to CSS
To compile sass to css using the command line:
> sass index.scss index.css

Tip: Look for auto-compile plugins for you favorite IDE. These can watch for changes in your scss and automatically compile when needed.



---
#Styling #CSS