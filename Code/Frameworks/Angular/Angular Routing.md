# Angular Routing
*Routing in our [[Angular]] application*

## Routing Parameters
### Required Parameters

In routing:

```
{ path: '/products/:id, component: ProductDetailComponent }
```

In ProductDetailComponent:

```
constructor(
  private route: ActivatedRoute,
  ...
) { }

ngOnInit() : void {
  const id = +this.route.snapshot.paramMap.get('id')
  ...
}
```

### Optional Parameters

In template:

```
[routerLink]="['/products', { name: productName, code: productCode, startDate: availabilityStart, endDate: availabilityEnd }]"
```

In component.ts:

```
constructor(
  private route: ActivatedRoute,
  ...
) { }

ngOnInit() : void {
  const name = +this.route.snapshot.paramMap.get('name')
  ...
}
```

### Query Parameters
Unlike optional params, query params can be retained across routing paths.

In template:

```
<a
  [routerLink]="['/products', product.id]"
  [queryParams]="{ filterBy: listFilter, showImage: showImage }"
>
```

To return query params from another template:

```
<button
  class="btn btn-outline-secondary mr-3"
  style="width: 80px"
  [routerLink]="['/products']"
  queryParamsHandling="preserve"
>
```

To read the retained params:

```
constructor(
  private route: ActivatedRoute,
  ...
) { }

ngOnInit(): void {
    this.listFilter = this.route.snapshot.queryParamMap.get('filterBy') || ''
    this.showImage = this.route.snapshot.queryParamMap.get('showImage') === 'true'
    ...
  }
```

## Route Resolving
For pre-fetching data we can use a route resolver.

### Route's Data Property
We can provide static data to a route using the data property.

In the route:

```
{
  path: '/products',
  component: ProductListComponent,
  data: { pageTitle: 'Product List' }
}
```

To get the data:

```
constructor(
  private route: ActivatedRoute,
  ...
) { }

ngOnInit(): void {
    this.pageTitle = this.route.snapshot.data['pageTitle']
    ...
  }
```

### Route Resolver
For dynamic data we need to use a resolver.

- Create a service
- Implement the Resolve interface
- Add the resolver to your routing
- In the component, read the resolved data from the route

## Child Routes
Example:

```
{
  path: 'products/:id/edit',
  component: ProductEditComponent,
  resolve: { resolvedData: ProductResolver },
  children: [
    {
      path: '',
      redirectTo: 'info',
      pathMatch: 'full'
    },
    {
      path: 'info',
      component: ProductEditInfoComponent
    },
    {
      path: 'tags',
      component: ProductEditTagsComponent
    }
  ]
}
```

### Using Resolved Data of Parent Component
```
ngOnInit(): void {
  this.route.parent.data.subscribe(data => {
    this.product = data['resolvedData'].product
  })
}
```

## Component-less Routes
Component-less routes “consume” URL segments without instantiating components.

Since there is no component containing a router-outlet, all the children will be displayed in the higher level outlet.

Since there is no component associated with the route, the router will merge its params, data, and resolve into the children. As a result the sibling components can access the common parameters directly, without going through the parent route.

## Routing Animation
- Import BrowserAnimationsModule
- Define the desired animations
- Register the animations with the component
- Trigger the animation from the router outlet

## Routing Events
- NavigationStart
- RoutesRecognized
- NavigationEnd

We can log router event in console by adding options to our routing:

```
RouterModule.forRoot(ROUTES, { enableTracing: true })
```

## Secondary Routes
We can have multiple router-outlets provided the secondary outlets have a name.

When routing to a named router outlet, the url in the address bar reflects both primary and secondary route path. The secondary paths appear within parentheses after the primary path.

![App Structure](app-structure.png)

Some examples to route to secondary outlets in template or in code:

```
[routerLink]="[{ outlets: { popup: ['messages'] } }]"
[routerLink]="['/products', product.id, 'edit', { outlets: { popup: ['summary', product-id] } }]"
this.router.navigate([{ outlets: { popup: ['messages'] } }])
```

To clear the outlet:

```
[routerLink]="[{ outlets: { popup: null } }]"
this.router.navigate([{ outlets: { popup: null } }])
this.router.navigateByUrl('/login')
```

## Guards
In order of execution:

- canDeactivate
- canLoad
- canActivateChild
- canActivate
- resolve

A guard automatically guards each of the routes children.

## Lazy Loading
Loading modules on demand when needed instead of on application start.

Required:

- Feature module
- Routes grouped under a single parent
- Not imported in another module

We can also use preloading, aka eager lazy loading, to download lazy loaded modules behind the scene before the user routes to them.
Preloading makes sense when we are confident modules will be loaded at some point.
How modules are preloaded is based on the **preloading strategy**:

- No preloading (on demand)
- Pre-load all

  ```
  { preloadingStrategy: PreloadAllModules }
  ```

- Custom

  We can create our own service and implement PreloadingStrategy to create our own custom strategy.
  
  
  ---
  #Typescript 