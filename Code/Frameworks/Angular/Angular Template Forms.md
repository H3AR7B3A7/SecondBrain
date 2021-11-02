# Template Forms
Using template forms in our [[Angular]] application , while easy to use, is not testable by our unit tests.

## Why Template Forms
- Easy to create / read when the form isn't too complex
  - We only need data model
  - A form model is generated for us from html

## Characteristics
- Generated form model
- HTML validation
- Two-way data binding

## Directives
- ngForm
- ngModel
- ngModelGroup

Example:

```
<form (ngSubmit)="save()" #signUpForm="ngForm">
  <input id="firstNameId" type=text" [(ngModel)]="customer.firstName" name="firstName" #firstNameVar="ngModel">
  <button type="submit" [disabled]="!signUpForm.valid">
    Save
  </button>
</form>
```

The form tag automatically creates a FormGroup.
The input tag automatically creates a FormControl.

_We can use template reference variables (#) to access form model and form control states._

## Validation
Validation in template forms happens in the template itself:

```
<input type="text" required minlength="3" formControlName="firstName">
```

## Used Libraries
- Bootstrap

  > ng add @ng-bootstrap/ng-bootstrap

- NGX Bootstrap

  - Buttons

    > ng add ngx-bootstrap --component buttons

  - Date Picker

    > ng add ngx-bootstrap --component datepicker

  - Time Picker

    > ng add ngx-bootstrap --component timepicker

  - Rating

    > ng add ngx-bootstrap --component rating

_The --component parameter is not working for Angular 11+._



---
#Typescript 