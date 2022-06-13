# Angular Architecture

## Considerations

-   App Overview:
	-   What is it for 
	-   What are the goals
	-   How is the client going to use it
	-   What are the strategic/business benefits
-   App Features
-   Domain Security
	-   Roles / Groups / Claims
	-   Communication to Angular app
	-   Communication with API
		-   Token-based / LDAP-server (with active directory)
-   Domain Rules (client or server side)
-   Logging
	-   Console
	-   Local Storage
	-   API
	-   3d party (cloud) logging capabilities
-   Services / Communication (http / websockets)
-   Data Models (reusable calls / view models)
-   Feature components and structure
-   Shared functionality
	-   Which 3d parties
	-   Native or with wrapper
	-   Used in one app or in many

## Architecture Planning Template

https://codewithdan.me/angular-architecture-planning
https://codewithdan.me/angular-architecture-planning-example

## Other Considerations
-   Accessibility
-   i18n
-   Environments
-   CI/CD
-   CDN, container, server
-   Unit testing
-   End-to-end testing
-   APIs
-   More

## Organizing Code

-   Convention-based
	-   Follow strict naming conventions
	-   Related code may be separated
	-   Can result in a lot of files in a folder in larger applications
-   Feature-based
	-   Features are organized in their own folder
	-   Features are self contained
	-   Easy to find everything related to a feature

## Features & Modules

## Libraries

To create a lib in a separate repo
> ng new test --create-application false

To create and build the library
> ng g library my-lib
> ng build my-lib
 
 To publish
> npm publish


---
#Angular #Architecture
## Structuring Components
