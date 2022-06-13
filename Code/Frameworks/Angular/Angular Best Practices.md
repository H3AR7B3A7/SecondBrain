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

### Functions vs Pipes
Angular makes it easy to call functions from the template. However sometimes these functions can be called way more times than is needed (every time a change occurs in the template). Often it is better to use a pipe for performance.

-   Avoid impure pipes (like a function it is called on any change)
-   By default Angular uses pure pipes (called only when inputs are changed)

``` typescript
@Pipe({
  name: 'someFilter',
  pure: true
})
```

## Memo Decorator

We can easily cache *primitive* values using the memo decorator to avoid repeated computations.

```typescript
import memo from 'memo-decorator'

@Pipe({ name: 'somepipe'})
export class SomePipe implements PipeTransform {

	@memo()
	transform(value: any, args?: any): any {
		return value.someField * 2
	}
}
```

```
yarn add memo-decorator
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

### Useful Operators for HttpClient

#### forkJoin
Make two calls simultaneously:

```typescript
getCharactersAndPlanets() {
	return forkJoin(
		this.getCharacters(),
		this.getPlanets()
	).pipe(
		map((res) => {
			return { characters: res[0], planets: res[1]}
		}),
		catchError(error => of(error))
	)
}
```

#### switchMap
Make a sequential call adding data to a first call:

```typescript
getCharacterAndHomeworld() {
	return this.http.get(url)
		.pipe(
			switchMap(character => {
				return this.http.get(character['homeworld'])
					.pipe(
						map(hw => {
							character['homeworld'] = hw
							return character
						})
					)
			})
		)
}
```

#### mergeMap
Make sequential calls adding data for each result of the first call:

```typescript
getCharactersAndHomeworlds() {
	return this.http.get(url)
		.pipe(
			swotchMap(res => {
				return from(res['results'])
			}),
			mergeMap((person: any) => {
				return this.http.get(person['homeworld'])
					.pipe(
						map(hw => {
							person['homeworld'] = hw
							return person
						})
					)
			}),
			toArray()
		)
}
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

## State Management

Goals:
-   Single source of truth
-   Predictability
-   Immutability
-   Ability to track state changes

Types of state:
-   Application state
-   Session state
-   Entity state

Multiple options:
-   Services
-   NgRx
-   NgRx-data (NgRx wrapper - less code)
-   Observable Store
-   Akita
-   Ngxs
-   MobX
-   Some custom implementation

### Services

-   Simplest solutions
-   Problems arise when multiple services manage the same state in different places
-   Can be managed if those services use the same store service
-   Need for good inter-team communication

### NgRx

-   Redux + RxJS
-   Single source of truth
-   Immutable Data
-   Provides consistency across teams
-   Diagnostic tool to watch store
-   Flow: Component -> Actions -> ( Effects -> Server -> Effects -> Actions -> )
		Reducers -> State in Store -> Selectors -> Component
-   A lot of code

```
yarn add @ngrx/effect
yarn add @ngrx/entity
yarn add @ngrx/store
yarn add @ngrx/store-devtools
```

### NgRx-data

-   NgRx - but simplified
-   Eliminate NgRx boilerplate
-   One line of code per entity
-   Customize as needed
-   Flow: Component -> ngrx-data-service (entity wrapper) -> Component

```
yarn add @ngrx/data
```

### Observable Store

Observable Store provides a simple way to manage state in a front-end application while achieving many of the key goals offered by more complex state management options.

-   Single source of truth
-   State is read-only / immutable
-   Provide state change notifications to any subscriber
-   Track state change history
-   Minimal amount of code required
-   Works with any library / framework
-   Flow: Component -> Service (Observable Store wrapper) -> Component

```
yarn add @codewithdan/observable-store
```

## Bundle Sizes

When adding large 3d party dependencies to our application it might be a good idea to check the impact it has on our file sizes.

We can monitor bundle sizes by installing SME:

> yarn global add source-map-explorer

And build the app with sourceMaps, by default Angular will build a production build:

> yarn run build --sourceMap=true

In the dist folder under our project run SME on the bundle you want to inspect (main bundle), eg:

> source-map-explorer main.946363c07a664402.js

## Security Considerations

-   CORS
	-   CORS allows a browser to call a different domain or port
	-   Enable on the server as needed
	-   Limit allowed domains, headers, and methods
-   CSRF / XSRF
	-   Enable CSRF on the server if using cookie authentication
	-   Angular will read a token from a cookie set by the server and add it to the request
	-   Change the cookie/header name as appropriate for your server
	-   Server will validate the header value
-   Route Guards
	-   Define route guards needed by applications based on user or group/role
	-   Keep in mind that route guards  don't "secure" an application
	-   Rely on the server to secure data, APIs, etc.
-   Sensitive Data
	-   Anyone can access the browser developer tools to view variables, local/session storage, cookies, etc.
	-   Do not store sensitive data (secrets, keys, passwords, etc.) in the browser
	-   If an API requires a "secret" to be passed, consider calling it through a "middle-man" service that you own
	-   Use JWT tokens where possible for server authentication (set appropriate TTL expiration for tokens)

### HttpInterceptors

-   HTTP Interceptors provide a centralized place to hook into requests/responses
-   Add withCredentials when using cookies and calling via CORS

```typescript
@Injectable()
export class CorsInterceptor implements HttpInterceptor {

	intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
		const authReq = req.clone({
			withCredentials: true,
			headers: req.headers.set('X-requested-With', 'XMLHttpRequest')
		})
		return next.handle(authReq)
	}
}
```

-   Interceptors can be used to pass tokens required by services

```typescript
@Injectable()
export class AuthInterceptor implements HttpInterceptor {

	intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
		const authHeader = this.authService.getAuthToken()
		const authReq = req.clone({
			headers: req.headers.set('Authorization', authHeader)
		})
		return next.handle(authReq)
	}
}
```

-   Interceptors can be provided in the Core module
-   Since more than one interceptor can be used, set multi to true

```typescript
@NgModule({
	providers: [{
		provide: HTTP_INTERCEPTORS,
		useClass: AuthInterceptor,
		multi: true
	}]
})
export class CoreModule {}
```

---
#Angular #BestPractice 