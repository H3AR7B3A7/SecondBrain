# Angular Best Practices
Some best practices for [[Angular]] projects.

## LIFT

- Locate code quickly
- Identify code at a glace
- Flattest structure possible
- Try to be DRY

## Single Responsibility Principle

A single class (component, service, ...) or modules should have one responsibility.

## Project Structure

Use the angular CLI where possible:
-   ng n my-project --routing --style scss
-   ng g m core
-   ng g m shared
-   Creating features:
    -   ng g m feature-name
    -   ng g c feature-name/feature-name
    -   ng g s feature-name/data
    -   ng g c feature-name/feature-name/some-component

*Tip: When in doubt, use -d

Core:

-   Application wide services like AuthService
-   Interfaces / classes used by those services like User for this example

Shared:

-   For components / services / custom pipes / directives / models shared between features
-   Should be added to the imports array in the module that uses it

## Modules

-   Work in modules for different functionality, and try to make them work as a whole / unit.  
    A rule of thumb is that when you navigate to a whole different route (in your topmost router outlet), you probably need a module.  
    (The same goes for the top level in secondary outlets.)
-   Declare components in the module they belong to, not the top module. (See hierarchy for more info.)
-   Avoid exports and provides in the same module

## Models

-   Always prefer interfaces over classes when no objects need be created.
-   Only actual data models, presenting business logic end with .model.ts

## Routes

-   Lazy load feature modules on routing

{
    path: 'somewhere',
    loadChildren: () => import('./items/items.module').then(m => m.SomeModule)
}

-   Be sure to not include SomeModule (and its components) in AppModule
-   In the routing of SomeModule provide the path '' for the component to be loaded on '/somewhere'

{ path: '', component: SomeComponent }

-   Use a wildcard at the end of the routes to catch faulty paths and direct the user to a 404:

{ path: '**', component: PageNotFoundComponent }

-   or a default path:

{ path: '**', redirectTo: 'somewhere' }

-   Be mindful that angular routes should be in the right order. And the default value for pathMatch is 'prefix'. For example everything is prefixed by an empty string. We can use 'full' to match the whole path.

## Hierarchy

-   Start creating components / services / custom pipes / directives / models in the component they belong to.
-   Bubble them up to the first module they belong to when it is shared within the module.
-   Then bubble it up to a common shared module when it is shared outside the module.
-   Lastly, bubble them up to a library when they are shared among applications.

## Components

- Imports
	- Third party imports first
	- An empty line as spacer
	- Then imports from within our project
-   Order of members
    -   private fields
    -   public fields
    -   observables
    -   constructor
    -   getters/setters
    -   functions
-   Start private fields with _ and create a getter for them when they need to be accessed from outside the API or in tests.

private _someClassMember

get someClassMember() {
         return this._someClassMember
}

-   Use async pipes in the template whenever possible. You hardly ever need manual subscriptions.
-   To transform data use RxJS pipes. Push data coming from the component itself to a subject when you need to combine it with other observables.

## RxJS

-   Use $ behind an observable.
-   Prevent subscribing to observables, use async pipes in the template instead.
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

-   When creating a Subject, use asObservable() to prevent leaking the observer side of the Subject.

``` typescript
private someSubject = new Subject()

get someSubject$() {
      return this.someSubject.asObservable()
}
```

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

[https://www.codelab.esaturnus.com/bitbucket/projects/SAL/repos/planning-ui/pull-requests/44/overview](https://www.codelab.esaturnus.com/bitbucket/projects/SAL/repos/planning-ui/pull-requests/44/overview)

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

  

Proposal in progress...

## ![](https://www.codelab.esaturnus.com/confluence/download/attachments/118653271/image2022-5-17_11-50-36.png?version=1&modificationDate=1652781036991&api=v2 "Steven D'Hondt > Angular code structure > image2022-5-17_11-50-36.png")