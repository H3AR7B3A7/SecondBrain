# Angular
# Getting Started With Angular
[Official Angular Pages](https://angular.io/)

Angular is a [[Code/Languages/JavaScript/Typescript/Typescript]]-based open-source web application framework led by the Angular Team at Google and by a community of individuals and corporations. Angular is a complete rewrite from the same team that built AngularJS.

### Installation
- **Install NPM & Node.js**: Download installer [here](https://nodejs.org/en/download/).
- **Install Typescript**: npm install -g typescript
- **Install Angular**: npm install -g @angular/cli

### Interesting Libraries
- ESLint

> ng add @angular-eslint/schematics

- Material

  > ng add @angular/material

- Flex Layout

  > npm i @angular/flex-layout

See: [Flexbox Layout Examples](https://tburleson-layouts-demos.firebaseapp.com/#/docs)

- Bootstrap

  > ng add @ng-bootstrap/ng-bootstrap

- Font-Awesome

  > npm i font-awesome

### VSC Extensions:
- Angular Essentials
- Angular Language service
- Angular Snippets
- Nx Console
- TSLint
- Material Icon Theme

## Creating a Project
Navigate to the desired folder and use following commands:

> ng n name --routing --prefix prefix --style scss --strict  
> ng serve -o

## The CLI
### Configuring Global CLI

> ng config -g schematics.@schematics/angular:component.style scss

On Windows the 'Global Config' file can be found here:

> C:\Users\<User>\.angular-config.json

### Default templates
On Windows we can find the templates that are generated with 'ng n name' here:

> C:\Users\<User>\AppData\Roaming\npm\node_modules\@angular\cli\node_modules\@schematics\angular\application\files\src

We can:

- Modify the html/style templates that are present to our liking
- Add our own default favicon
- Add other default resources to our assets folder by appending them with '.template'
- Create and customize different environments
- Create additional file structures we always want to be present in our projects
- ...

We can also make changes to the default package.json & README.md here:

> C:\Users\<User>\AppData\Roaming\npm\node_modules\@angular\cli\node_modules\@schematics\angular\workspace\files

_My global files are included in this project as an example, feel free to take a look and copy or modify them to your needs._

## Components
### Create a Component
> ng generate component name

--dry-run (Run without making changes to see what would happen)  
--skip-tests (Don't generate spec.ts)  
--inline-style (Don't generate stylesheet)  
--inline-template (Don't generate html template)
--flat (Generate without parent folder)

Example component decorator:

```typescript
@Component({
    selector: 'app-hero',
    templateUrl: './hero.component.html',
    styleUrls: ['./hero.component.css']
})
```

To render the template of the new component we add the selector to _app.component.html_:

```html
<app-hero></app-hero>
```

### Binding Components in Templates
See _[testProject](testProject)_ for examples of:

- Variable Binding
- Class Binding
- Style Binding
- Event Binding
- Input Binding
- Output Binding
- Local References

### Encapsulating CSS Styling
ViewEncapsulation enumeration values:

- Emulated: Default, an emulation of native scoping in shadow DOM
- Native: Only works in browsers that support shadow DOM
- None: No encapsulation

Example:

```typescript
import { Component, ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'app-hero',
    templateUrl: './hero.component.html',
    styleUrls: ['./hero.component.css'],
    encapsulation: ViewEncapsulation.Emulated
})
```

### Changing Detection Strategies
Every component has a _'change detector'_ that compares changed properties with their previous values. This can be a performance bottleneck for components that render hundreds of items in a list. In this case we might want to use the \*_OnPush_ strategy which only triggers the change detection when the reference of _@Input_ properties change.

Example:

```typescript
import { Component, ChangeDetectionStrategy } from '@angular/core';

@Component({
    selector: 'app-hero',
    templateUrl: './hero.component.html',
    changeDetection: ChangeDetectionStrategy.OnPush
})
```

## The Component Lifecycle
Available lifecycle hooks:

- OnInit
- OnDestroy
- OnChanges
- DoCheck
- AfterContentInit
- AfterContentChecked
- AfterViewInit
- AfterViewChecked

### The OnInit Interface
The _ngOnInit()_ method is called upon the initialization of a component. At this point all input bindings and data-bound properties have been set. The _OnInit_ hook can for example be used to initialize components with data from external sources.

### The OnDestroy Interface
The _ngOnDestroy()_ method is called upon destruction of a component. Components get destroyed through using the _ngIf directive_ or by _routing_ to other components using a URI. When this happens it can be useful to use the OnDestroy interface to clean up:

- Resetting timers & intervals
- Unsubscribing from observable streams

### The OnChanges Interface
The _ngOnChanges()_ method is called when the binding of a value changes. It accepts an object of type SimpleChanges as a parameter. The resulting objects holds a previousValue and currentValue, but also a boolean which tells us wether it is the 'first' change.

## Directives
Directives are HTML attributes that extend the behavior or the appearance of standard HTML elements. When we apply them to an HTML element or even an Angular component, we can add custom behavior to it or alter its appearance. There are three types:

- Components
- Structural directives
- Attribute directives

Built in _structural directives_:

- ngIf
- ngFor
- ngSwitch

See _[jestProject](jestProject)_ for more examples.

To create just an interface model:

> ng generate interface name --type=model

### ngIf
Used for the conditional rendering of HTML elements in the DOM.

```html
<p *ngIf="team === 'Avengers'; else noHero">{{ name }} is an avenger!</p>
<ng-template #noHero>
  <p>No avengers found</p>
</ng-template>
```

### ngFor
Used for iterating through a collection of elements and rendering a template for each one.

```html
<ul>
    <li *ngFor="let hero of listOfHeroes>
    {{ hero.name }}
    </li>
</ul>
```

### ngSwitch
Used as a switch statement evaluating some property and rendering the appropriate HTML element.

```html
<ng-container [ngSwitch]="hero.team">
  <div *ngSwitchCase="'Avengers'">{{ hero.name }} is an Avenger.</div>
  <div *ngSwitchCase="'Justice League'">
    {{ hero.name }} is in the Justice League.
  </div>
</ng-container>
```

## Pipes
Pipes allow us to filter and map the outcome of our expressions on a view level. They transform data in the desired format and display the output in the template.

Some default examples:

```html
<p>{{ 'Example' | uppercase }}</p>
<p>{{ 'Example' | lowercase }}</p>
<p>{{ 0.123 | percent }}</p>
<p>{{ 100 | currency }}</p>
<p>{{ 100 | currency:'EUR' }}</p>
<p>{{ listOfHeroes | slice:2:4 }}</p>
<p>{{ today | date }}</p>
<p>{{ today | date:'fullDate' }}</p>
<p>{{ hero | json }}</p>
<p>{{ delayedHero | async }}</p>
```

## Custom Pipes
To create a pipe _in the current directory_:

> ng generate pipe name

Pipes are pure by default, which means they will not update when a value gets changed, only when a new value is assigned. So when we add an object to an existing array or change a value of an object and want it to be affected by the pipe we create a new array/object (immutability principle):

```typescript
listOfHeroes: Hero[] = [...heroes, heroX];
```

To change this behavior we can also make the pipe impure:

```typescript
@Pipe({
    name: 'sort',
    pure: false
})
```

If the object changes a lot and they are many, this can affect performance.

## Custom Directives
To create a directive _in the current directory_:

> ng generate directive name

## Modules
See _[ModulesAndStructure](ModulesAndStructure)_ for examples on the following topics.

To create a module:

> ng generate module name

--dry-run (Run without making changes to see what would happen)  
--flat (Generate without parent folder)  
--routing (Generate routing module)

They contain:

- Declarations: Registered components, directives and pipes
- Imports: Other modules containing declarations to be used by this module
- Exports: Artifacts available for other modules (aka the public API)
- Providers: Provided services, accessible from any module
- Bootstrap: Main component, 'AppModule'

### Registering Components with a Module
You can do this by running the command inside the module folder or using the module option.

Using the module option:

> ng generate component cars/carList --module=cars

### Exposing Module Features
To be able to add the the features template to the apps template using the selector we need to:

- Add the component to the exports in the features module.ts.
- Import the module in app.module.ts.

### Module Separation
By functionality:

- **Root** module: The main module, 'AppModule'
- **Feature** modules: A set of functionalities (ex: Orders, Products, Customers, ...)
- **Core** modules: Application wide artifacts (ex: Navbar, Footer, Loading spinner, ...)
- **Shared** modules: Reusable artifacts imported by different feature modules

By loading:

- **Eager** loaded modules: Declared in imports
- **Lazy** loaded modules: Through navigation

## Configuration & Environments
We can run commands in different environments by using the following option in the CLI:

> ng command --configuration=name

We can add other environments to the defaults (development and production) by creating the matching configuration files in the _environments folder_. The naming convention to follow here is: _environment.{name}.ts_.

The environment file exports an environment object. By default a boolean 'production' property is already set. We need to define all required properties in this object. For example the URL of the backend API will be set here.

When we created the environment, we can define the appropriate configurations in the _angular.json_:

```json
"configurations": {
    "production": {
        "fileReplacements": [
            {
                "replace": "src/environments/environment.ts",
                "with": "src/environments/environment.prod.ts"
            }
        ]
    }
}
```

When running **ng build --configuration=production** the CLI will replace the default environment file with the one for production.

## Dependency Injection
In previous examples our data was tightly coupled to our component, meaning it was declared inside them.

- In real world application our data is rarely static.
- We only want our component to handle 'presenting' the data, and not be concerned on how to get the data.

We can generate a **service** that we can use to inject our data in any class that needs it.

> ng generate service cars/car

### Share a Dependency Through Components
Add selector to parent template:

```html
<app-favorite-cars></app-favorite-cars>
```

Add the service to providers in parent component:

```typescript
@Component({
    selector: 'app-car-list',
    templateUrl: './car-list.component.html',
    styleUrls: ['./car-list.component.css'],
    providers: [CarService]
})
```

#### Restricting DI Down the Tree
We can restrict DI down to only one level by using the 'viewProviders' attribute:

```typescript
@Component({
    selector: 'app-car-list',
    templateUrl: './car-list.component.html',
    styleUrls: ['./car-list.component.css'],
    viewProviders: [CarService]
})
```

#### Restricting Provider Lookup
The **@Host()** decorator will prevent bubbling up the hierarchy to look for the dependency, it will instead throw an exception.

```typescript
constructor(@Host() private carService: CarService) { }
```

The **@Optional()** decorator will prevent this error.
The **@SkipSelf()** and **@Self()** decorators will respectively make the injector skip or check the local injector of the current component. When skipping it will start looking higher in the hierarchy.

#### Overriding Providers
The provider argument we used before was a shorthand for:

```typescript
providers: [{ provide: CarService, useClass: CarService }]
```

The useClass property overwrites the initial implementation. It could also take a factory function that returns one of multiple services depending on a condition:

```typescript
export function carFactory(isFavorite: boolean){
    return () => {
        if (isFavorite) {
            return new FavoriteCarService();
        }
        return new CarService();
    };
}
...
providers: [{provide: CarService, useFactory: carFactory(true)}]
```

If the 2 services also inject other dependencies into their constructor, we have to add them to the **deps** property of the provide object literal:

```typescript
providers: [
  { provide: CarService, useFactory: carFactory(true), deps: [HttpClient] },
]
```

And inject it into the factory:

```typescript
export function carFactory(isFavorite: boolean) {
  return (http: HttpClient) => {
    if (isFavorite) {
      return new FavoriteCarService()
    }
    return new CarService()
  }
}
```

### Dependency Injection of Values
When the dependency we want to provide is not a class, but a value, we can use the **useValue** syntax:

```typescript
export interface AppConfig {
    title: string,
    version: number
}

export const appSettings: AppConfig = {
    title: 'My app'
    version: 1.0
;}
```

We can't pass an interface to providers, so we create an **InjectionToken**:

```typescript
export const APP_CONFIG = new InjectionToken<AppConfig>('app.config');
...
providers: [{provide: APP_CONFIG, useValue: appSettings}]
...
constructor (@Inject(APP_CONFIG) config: AppConfig){
    this.title = config.title;
    this.version = config.version;
}
```

## Asynchronous Data Services
Strategies:

- Callback
- Promise
- Observables

### Callback Hell
```typescript
getRootFolder(folder => {
    getAssetsFolder(folder, assets => {
        getPhotos(assets, photos => {
            ...
        })
    })
})
```

### Promises
```typescript
getRootFolder().then(getAssetsFolder).then(getPhotos)
```

Limitations:

- They cannot be canceled
- They are immediately executed
- They are one time operations, no easy retry
- They respond with only one value

### Observables
Observables will emit values over a period of time.
To create an observable:

- Operator "of"
- Keyword "new" Observable

_It is good practice to name observable variables ending with "$"._

Observables maintain a list of observers and inform them of data changes.

- **Subscribe** : We can subscribe to an observable to follow multiple changes.
- **toPromise** : We can use it to get a promise (single change).
- **pipe** : We can pipe observed changes before subscribing to them.
  The pipe method allows for multiple params (from 'rxjs/operators') manipulating data like a recipe.

### Reactive Functional Programming
A programming paradigm for reactive programming (asynchronous dataflow programming) using the building blocks of functional programming (e.g. map, reduce, filter). FRP has been used for programming graphical user interfaces (GUIs), robotics, games, and music, aiming to simplify these problems by explicitly modeling time.

### Angular In Memory Web API
An in-memory web api for Angular demos and tests (not for production) that emulates CRUD operations over a REST API. It intercepts Angular Http and HttpClient requests that would otherwise go to the remote server and redirects them to an in-memory data store that you control.

- Install the package

  > npm install angular-in-memory-web-api --save-dev

- Generate a service

  > ng g s services/data --skip-tests

- Make the DataService class implement InMemoryDbService
- Implement the 'createDb' function and make it return an array (with or w/o data)
- Add HttpClientInMemoryWebApiModule.forRoot(DataService) to the imports in the module.ts

_We use .forRoot to implement the service as a singleton for the whole application._

### HttpClientModule
The HttpClientModule provides a variety of Angular services that we can use to handle asynchronous HTTP communication.

The HttpClient service has methods representing all the possible HTTP verbs and return observable streams we can subscribe to.

### Auth Interceptor
We can create a service and implement HttpInterceptor, or we can use:

> ng g interceptor auth

That implements the method:

```typescript
intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
    return next.handle(req)
}
```

And add a provider to the module:

```typescript
providers: [
    {
        provide: HTTP_INTERCEPTORS,
        useClass: AuthInterceptorService;
        multi: true
    }
],
```

### Handling HTTP Errors
We can pipe our HTTP requests to catch errors using catchError:

```typescript
import { catchError, retry } from 'rxjs/operators'
...
getHeroes(): Observable<Hero[]> {
    return this.http.get<Hero[]>(heroesUrl).pipe(
        retry(2),
        catchError((error: HttpErrorResponse) => {
            console.error(error)
            return throwError(error)
        })
    )
}
```

_We can also easily add some retry logic._

### Cleaning Up Resources
- Unsubscribe from observables manually
- Use the _async_ pipe

## Libraries
To create a library:

> ng g library libraryName

To add components to our library:

> ng g c name --project libraryName

We should not forget to build our library:

> ng build libraryName

To add 3d party libraries or our own previously created ones:

> ng add libraryName

## Routing
HTML 5 Style:

- LEverages HTML 5 history pushState
- Default
- More natural url
- Requires url rewriting

Hash-based:

- Leverages url fragments
- Does not require url rewriting
- Set by using the option:

```
{ useHash: true }
```

## Production
The angular CLI command to build our application used to te a parameter --prod to create a production build, because the default value was --dev.

However, now the default creates a production build:

> ng build

By default lazy loaded modules get loaded on demand. We can change the strategy of our application in regards of when to load our lazy loaded modules.

For example, in our app.module we add:

```typescript
@NgModule({
    imports: [
        ...
        RouterModule.forRoot(appRoutes, {preloadingStrategy: PreloadAllModules})
        ...
    ]
})
```

We can also create our own (more complex) preloading strategies.

## Testing
### Testing With(out) Testbed
When Angular CLI generates components it also generates tests in \*.spec.ts. These contain some boilerplate implementing a testbed for template testing. When we aren't testing against the template however, we can speed up testing by not using the testbed.

### Common commands
> ng test  
> npm test  
> ng test --watch false  
> npm test --watch false  
> ng test --code-coverage  
> ng test --karma-config karma.conf.js --watch false

To always get code coverage, edit _angular.json_:

```json
"test": {
    "options": {
        "codeCoverage": true
    }
}
```

To run tests on _FireFox_ browser:

> npm install karma-firefox-launcher

To run tests on _Edge_ browser:

> npm install karma-edge-launcher

To run tests on _Chromium-Edge_ browser:

> npm install -D @chiragrupani/karma-chromium-edge-launcher

And edit _karma.conf.js_:

```json
plugins: [
    require('karma-firefox-launcher'),
    // require('karma-edge-launcher'),
    require('@chiragrupani/karma-chromium-edge-launcher'),
    ]
...
browsers: ['Chrome','Edge','Firefox']
```

Or don't edit browsers array and run individually:

> ng test --browsers Edge  
> ng test --browsers Firefox

### General Concepts
- Tests
  - Unit Tests
    - Isolated Unit Tests
    - Integrated Unit Tests (including template)
      - Shallow Test
      - Deep Tests (including children)
  - End-to-end Tests
- AAA
  - Arrange
  - Act
  - Assert
- Mocking
  - Mocking objects to mimic their behavior without their full functionality

### Jasmine
Jasmine is the default unit testing framework in Angular.

Main functions:

- describe()
- beforeEach()
- it()
- expect()
  - Matchers
    - toBe()
    - toContain()
    - toBeDefined()

### Karma
Karma is the command line test runner. It can launch multiple browsers to run our tests depending on how it is configured.

### Protractor
Protractor was the default end-to-end testing framework in Angular, up until Angular 12.
It is no longer recommended or even included, because there are better third party alternatives.

## Testing with Other Frameworks
### Jest
[Full Migration Manual](https://www.amadousall.com/how-to-set-up-angular-unit-testing-with-jest/)

Automated migration:

> ng add @briebug/jest-schematic

Common commands:

> ng test  
> npm test  
> ng test --coverage  
> npx jest --coverage  
> ng test --watch  
> npx jest --watch  
> ng test --watchAll  
> npx jest --watchAll

### Mocha
[Full Migration Manual](https://www.radzen.com/blog/testing-angular-webpack-mocha/)



---
#Angular #Typescript 