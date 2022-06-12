# Angular Best Practices
Some best practices for [[Angular]] projects.
Be sure to also check out the [Official Angular Style Guide](https://angular.io/guide/styleguide).

## LIFT

- Locate code quickly
- Identify code at a glace
- Flattest structure possible
- Try to be DRY

## Single Responsibility Principle

A single class (component, service, ...) or modules should have one responsibility.

## Immutability

Create new objects instead of mutating existing ones.
For example:
```typescript
this.currentUser.classes.push(classId);
```
Can be written immutable by using the spread operator and functions that return new objects:
```typescript
this.currentUser = {
    ...this.currentUser,
    classes: this.currentUser.classes.concat(classId)
}
```

Another example:
```typescript
saveUser(user): Observable<any> {
    user.classes = user.classes || []
    this.currentUser = user
    return EMPTY.pipe(delay(1000))
}
```
Can be written like this:
```typescript
saveUser(user): Observable<any> {
    const classes = user.classes || []
    this.currentUser = { ...user, classes: [...classes]}
    return EMPTY.pipe(delay(1000))
}
```

## Small Functions

Refactor large functions into  well named smaller ones.

## Angular CLI
Use the angular CLI where possible.

### Example project structure
-   ng n my-project --routing --style scss
-   ng g m core
-   ng g m shared
-   Creating features:
    -   ng g m feature-name
    -   ng g c feature-name/feature-name
    -   ng g s feature-name/data
    -   ng g c feature-name/feature-name/some-component

*Tip: When in doubt, use -d

## Settings

-   Generally it is best to use Angular default settings
-   Do NOT set strict mode to false in tsconfig.json !!!
-   Do NOT set strictInjectionParameters to false in tsconfig.json
-   Do NOT set strictInputAccessModifiers to false in tsconfig.json
-   Do NOT set strictTemplates to false in tsconfig.json
-   Do NOT set aot to false in angular.json
-   Do NOT set enableIvy to false in tsconfig.app.json
-   In angular.json, defaultConfiguration should be set to 'production'

## Modules

-   Work with self contained modules
-   As a rule of thumb every feature should have 2 modules, one main module and a routing module.
-   Declare components in the module they belong to, not the top module. (See hierarchy for more info.)
-   Avoid exports and provides in the same module

### Core Module:

-   It contains application level services like AuthService
-   The core module will never be lazy loaded, so its services will always be available throughout the whole application
-   It also holds interfaces and classes used by those services like User for this example
-   (If it holds components it should be components that are used only once application wide, depending on the teams preference)
-   Application level components like a navigation bar
-   It should import CommonModule
-   We add the CoreModule to the imports of the AppModule

```typescript
@NgModule({
     imports: [ CommonModule ];
     exports: [ NavBarComponent ]
     declarations: [ NavBarComponent ]
     // providers: [ AuthService ]    <--- This could be considered instead of a Tree-Shakeable Provider in this case ???
})
export class CoreModule {}
```

-  Preventing core module to be imported in feature modules
```typescript
export class CoreModule extends EnsureModuleLoadedOnceGuard {
    constructor(@Optional() @SkipSelf() parentModule: CoreModule) {
        super(parentModule);
    }
}
```
-   Import guard
```typescript
export class EnsureModuleLoadedOnceGuard {
    constructor(targetModule: any) {
        if (targetModule) {
            throw new Error(`${targetModule.constructor.name} has already been loaded. Import this module in the AppModule only.`);
        }
    }
}
```

### Shared Module:

-   For components / services / custom pipes / directives / models shared between features
-   Should be added to the imports of the modules that use it
-   It should import CommonModule
-   It can export CommonModule, so feature modules don't need to import it separately

``` typescript
@NgModule({  
     imports: [ CommonModule ],  
     exports: [ LoadingSpinnerComponent ],  
     declarations: [ LoadingSpinnerComponent, ComonModule ],  
})  
export class CoreModule {}
```

### Feature Module:

-   Lazy load the feature module (Read the topic about lazy loading in Routing)

``` typescript
@NgModule({  
     imports: [ RouterModule, SharedModule ]; // Notice that there is no CommonModule  
     exports: [ ]  
     declarations: [ SomeComponent ]  
     // providers: [ SomeService ]    <--- Read the topic about Tree-Shakeable Providers in Services  
})  
export class SomeModule {}
```

## Routing

-   Use a wildcard at the end of the routes to catch faulty paths and direct the user to a 404:

``` json
{ path: '**', component: PageNotFoundComponent }
```

-   or a default path:

``` json
{ path: '**', redirectTo: 'somewhere' }
```

-   Be mindful that angular routes should be in the right order. And the default value for pathMatch is 'prefix'. For example everything is prefixed by an empty string. We can use 'full' to match the whole path.
-   When declaring routes in AppModule use RouterModule.forRoot(...) and RouterModule.forChild(...) in every other feature module
-   Use child routes appropriately: They allow users to bookmark the specific components

``` json
{
    path: 'somewhere/:id',
    component: SomeComponent,
    children: [
        { path: 'edit', component: SomeEditComponent },
        { path: 'details', component: SomeDetailsComponent },
    ]
}
```
-   Lazy load feature modules in routes

``` json
{
    path: 'somewhere',
    loadChildren: () => import('./items/items.module').then(m => m.SomeModule)
}
```

-   Be sure to not include SomeModule (and its components) in AppModule
-   In the routing of SomeModule provide the path '' for the component to be loaded on '/somewhere'

``` json
{ path: '', component: SomeComponent }
```

-   When using lazy loading we can opt to pre-load other modules in the background once the previous module is loaded, using PreloadAllModules or a custom preloading strategy.

``` typescript
@NgModule({  
  imports: [RouterModule.forRoot(routes, {  
    preloadingStrategy: PreloadAllModules  
  })],  
  exports: [RouterModule]  
})  
export class AppRoutingModule { }
```

## File Structure / Hierarchy

-   Keep the file structure rather flat
	-   A feature module holds components
	-   Those components can have very small components in them
	-   No deeper nesting is required or advised
	-   The flatter the structure, the better the oversight
	-   Max 7 files per folder is a good rule of thumb
-   Feature-based organization
	-   Features are organized in their own folder
	-   Features are self contained
	-   Easy to find everything related to a feature
-   Start creating components / services / custom pipes / directives / models in the component they belong to.
-   Bubble them up to the first module they belong to when it is shared within the module.
-   Then bubble it up to the shared module when it is shared outside the module.
-   Lastly, bubble them up to a library when they are shared among applications.

## Models

-   Always prefer interfaces over classes when the model doesn't require any supporting functions in it
-   Start interfaces with a capital 'I'
-   Only actual data models, presenting business logic end with .model.ts

### Immutability

For complex types and for triggering OnPush changes, we want to clone objects, instead of mutating them:
	-   Shallow
		-   Spread operator:  `clone = { ...original };`
			-   Does not copy methods
		-   Object assign: `let clone = Object.assign({}, original);`
			-   Does not copy methods`
	-   Deep : No one size fits all solution, the implementation depends on the object
		-   Stringify & Parse: `let clone = JSON.parse(JSON.stringify(original));
			-   Not all objects stringify well (dates, etc...)
			-   Does not copy methods
		-   Object create: `let clone = Object.create(original);`
			-   Does copy methods
			-   Not really cloning, creates new object from a prototype
		-   Immutable JS
			- Requires package `yarn add immutable`

```typescript
immutableSomethings = List<SomeObject>(originals)
const somethings = this.immutableSomethings.toArray()
fromJS(something).toJS() as Something
```

### Inheritance

Try to prefer composition over inheritance and use it only in those rare cases where it absolutely makes sense.

When two components are almost exactly the same (in terms of inputs and outputs), we can extend a base component which itself has no template.

## Components

### Container - Presentation Components

#### Container component

-   Manages the state by interacting with service/store
-   Contains only minor presentation, like for example a header/title
-   Passes state to presentation components using input properties

#### Presentation component

-   Presents/renders the data, but does not directly interact with state
-   Communicates with container component using output properties
-   Use OnPush as change detection strategy
-   Using child components makes it easy to implement child routes when appropriate

### Ordering
-   Order of imports
	-   Third party imports first
	-   An empty line as spacer
	-   Then imports from within our project
-   Order of members
    -   private fields
    -   public fields
    -   observables
    -   constructor
    -   getters/setters
    -   functions

### Conventions

-   Start private fields with _ and create a getter for them when they need to be accessed from outside the API or in tests.

``` typescript
private _someClassMember

get someClassMember() {
         return this._someClassMember
}
```

-   Use $ behind an observable.
-   Add prefixes to selectors that match the feature area they belong to

```typescript
@Component({
    // ...
    selector: 'feature-some-stuff',
})
```

-   Or using the CLI

 > ng g c some-stuff --prefix=feature

-   Remove the selector of components that are not meant to be embedded in any template
-   If styling or template is longer than 3 lines, keep them in separate files, instead of using `--inline-style` or `--inline-template`
-   Use scss if you plan to work with Angular Material
-   Use the @Input and @Output decorators over declaring inputs and outputs in the component decorator
- Keep the components as simple and focused as possible, delegate more complex logic to services

```typescript
applyFilter(filter: string) {
     this.visibleTabs = this.filterTabsService.complexFilteringMethod(filter, this.tabs)
}
```

-   Generally creating a component for a piece of functionality is a good thing, however when elements in the component have a lot of attributes (autofocus, autocomplete, disabled, ...) like buttons or text inputs, we would need to create input properties for all of them on that new component. In this case it might be better to not make for example a pair-of-buttons component.

### Communication

There are always multiple options, but we should use the right tool for the right job:
-   Data binding through Inputs and Outputs
	- Ideal for non-deeply nested *container-presentation* component communication
-   Event bus
	-   Mediator pattern
	-   Service acts as the middleman
	-   Relies on subject / observable
	-   Pro
		-   Simple to use
		-   Loosely coupled
		-   Lightweight
	- Con
		-   Can sometimes be hard to maintain
		-   Components don't know where data is coming from
		-   We must remember to unsubscribe
-   Observable service
	-   Observer pattern (usually)
	-   Service exposes observable directly to components
	-   Also relies on subject / observable
	-   Pro
		-   Simple to use (subscribe / unsubscribe)
		-   Components know where the data is coming from
		-   Easier to maintain
		-   Easy to share data between different layers
	-   Con
		-   Not as loosely coupled as an event bus
		-   Variations in Subjects should be understood
		-   Must remember to unsubscribe


#### Event bus

``` typescript
private subject = new Subject<any>()

on(event: Events, action; any): Subscription {
	return this.subject.pipe(
		filter((e: EmitEvent) => {
			return e.name === event
		}),
		map((e: EmitEvent) => {
			return e.value
		})
	).subscribe(action)
}

emit(event: EmitEvent) {
	this.subject.next(event)
}
```

```typescript
export class EmitEvent {
	constructor(public name: any, public value?: any) { }
}
export enum Events {
	SomeEvent
}
```

#### Observable service

```typescript
somethings: Something[] = []

// with immutable.js:
// immutableSomethings = List<Something>()

private somethingsSubject$ = new BehaviorSubject<Something[]>(this.somethings);
somethingsChanged$ = this.somethingsSubject.asObservable();

constructor(private cloner: CloneService) { }

getSomethings() : Observable<Something[]> {
	// with immutable.js:
	// return of(this.immutableSomethings.toJS())
	return of(this.somethings)
}

addSomething() : Observable<Something[]> {
	let id = this.somethings[this.somethings.length - 1].id + 1
	this.somethings.push({
		id: id,
		name: 'New Thing ' + id,
		/* ... */
	})
	this.somethingsSubject$.next(this.somethings)
	return of(this.somethings)
}

addSomethingClone() : Observable<Something[]> {
	return this.addSomething().pipe(
		map(things => {
			return this.cloner.deepClone(things)
		})
	)
}
```

## Services

### Singleton

-   Use Tree-Shakeable Providers for DI:

``` typescript
@Injectable({
  providedIn: 'root',
})
```

-   -   Why?
        -   The service does not need to be added to the modules providers array.
        -   If the service is only used within a lazy loaded module it will be lazy loaded with that module.
        -   If it is never used it will not be contained in the build (tree shaking).
        -   Removes the need to import library modules.
-   Alternatively use: providedIn: SomeModule if you don't want it to be available to applications unless they import the module

### Non-Singleton

-   Use the decorator of the component:

``` typescript
@Component({
  // ...
  providers: [SomeService]
})
```

## Custom Pipes

-   Avoid impure pipes
-   Don't forget to let angular know it is a pure pipe

``` typescript
@Pipe({
  name: 'someFilter',
  pure: true
})
```

## Directives

### Structural

#### ngFor:

*trackBy:*
The use of trackBy it's a performance optimization and is usually not needed by default, it's in principle only needed if running into performance issues.

Let's say that you are shipping to ancient mobile browsers or ancient versions of IE: you might want to consider applying trackBy as a precaution in your larger tables, but it really depends on your system and the use case.

## OnPush Change Detection Strategy

```typescript
@Component({
    // ...
    changeDetection: ChangeDetectionStrategy.OnPush,
})
```

Benefits of using the OnPush Changedetection strategy
-   Performance (component isn't checking until OnPush conditions are met)
-   Prevent the presentation component from updating state it should get from the container/parent

OnPush causes change detection to run when:
-   An input property reference changes
-   An output property / event emitter or DOM event fires
-   Async pipe receives an event
-   Change detection is manually invoked via ChangeDetectionRef

So in practice we need to:
-   Use immutable objects, because angular will detect changes by object reference
-   Subscribe to our observables using the async pipe in the template, instead of subscribing in ngOnInit

## RxJS

### Subjects

-   Subject
	-   Observers only get data that is emited after subscribing
-   BehaviorSubject
	-   Observers get the last value emited by the subject upon subscribing
	-   Requires an initial value in constructor
-   ReplaySubject
	-   Observers can get any number or all previously emited values upon subscribing
	-   Requires a size of the buffer in constructor
-   AsyncSubject
	-   Observers only get the last value when the sequence is completed

Subjects are both an *observer* and an *observable*. We should keep our Subjects private, and use asObservable() to expose it, to prevent leaking the observer side of the Subject:

``` typescript
private someSubject = new Subject()

get someSubject$() {
      return this.someSubject.asObservable()
}
```

### Unsubscribing

-   Unsubscribe in ngOnDestroy

```typescript
ngOnInit() {
	this.sub = this.someEventBus.on(
		Events.SomeEvent, (something => this.something = something))
}

ngOnDestroy() {
	if (this.sub) {
		this.sub.unsubscribe()
	}
}
```

-   AutoUnsubscribe decorator

```typescript
@AutoUnsubscribe()
export class SomeComponent implements OnDestroy {
	sub: Subscription

	constructor(private someEventBus: SomeEventBusService) { }

	ngOnInit() {
		this.sub = this.someEventBus.on(
			Events.SomeEvent, (something => this.something = something))
	}
}
```

-   SubSink ( `yarn add subsink`)

```
subs = new SubSink()

constructor(private someEventBus: SomeEventBusService) { }

ngOnInit() {
	this.subs.sink = this.someEventBus.on(
		Events.SomeEvent, (something => this.something = something))
}

ngOnDestroy() {
	this.subs.unsubscribe()
}
```

-   Let async pipes handle subscribing / unsubscribing
-   Use the takeUntil operator to complete observables instead of unsubscribing.

``` typescript
private stopFiring = new Subject()

someObservable$.pipe(
     // Do all the things...
     takeUntil(this.stopFiring)
);

// To complete the observable
this.stopFiring.next()
```

### Best Practices

-   Use async pipes in the template whenever possible. You hardly ever need manual subscriptions.
-   To transform data use RxJS pipes. Push data coming from the component itself to a subject when you need to combine it with other observables.
-   Use timer for polling.

``` typescript
someObservable$ = timer(1, 5000).pipe(
     switchMap(() => this.getDataService.getData(/*...*/)),
     retry(), // Retry when the call fails (don't wait 5s)
     share(), // When multiple sources subscribe only make one call for all subscriptions
     // ...
     takeUntil(this.stopPolling) // Stop when stopPolling fires
)
```

## State

...

## Bundle Sizes

When adding large 3d party dependencies to our application it might be a good idea to check the impact it has on our file sizes.

We can monitor bundle sizes by installing SME:

> yarn global add source-map-explorer

And build the app with sourceMaps, by default Angular will build a production build:

> yarn run build --sourceMap=true

In the dist folder under our project run SME on the bundle you want to inspect (main bundle), eg:

> source-map-explorer main.946363c07a664402.js

---
#Angular #BestPractice 