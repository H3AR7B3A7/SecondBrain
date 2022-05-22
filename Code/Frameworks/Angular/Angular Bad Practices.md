# Bad Practices in Angular to avoid
- Poor file naming
	- Should say something about the content
	- Should have the right suffix: e.g.: ...component.ts, ...service.ts
	- Name files consistently
	- The file name and the name of the class within should be directly related
	- Follow naming conventions
		- Classes should be upper camel-case
		- Members should be lower camel-case
		- File names should be kebab-case
- Not working in feature areas
	- Keep component typescript, styles and templates together
- Too much files in a directory
	- Hold no more than 7 files in a directory
- Multiple components / services / directives in one file
	- Use one file per component / service / directive
- Classes or modules with multiple functions / responsibility
	- Adhere to the Single Responsibility Principle
- Large functions
	- Refactor large functions into separate well named smaller ones
- Mutating objects
	- Use immutability creating new objects instead of mutating them
- Turn off strict mode
	- Keep strict mode on
	- Use the Angular default settings
- Not implementing lifecyclehook interfaces
	- Implement the interfaces for the used lifecyclehooks to get editor compiler errors when they are implemented incorrectly

---
#Angular 