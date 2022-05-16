# Narwal (Nx)
## Install the Nx CLI

> npm i -g @nrwl/cli

## Create a monorepo

> npx create-nx-workspace@latest name

### With Plugin

Angular:

> npx create-nx-workspace@latest --preset=angular name

React:

> npx create-nx-workspace --preset=react name

React-native:

> npx create-nx-workspace --preset=react-native name

Create an empty workspace set up for building applications

> npx create-nx-workspace --preset=empty name

Create an empty workspace set up for building packages

> npx create-nx-workspace --preset=core name

Create an empty workspace set up for building packages with the @nrwl/js plugin installed

> npx create-nx-workspace --preset=ts name

We can go [here](https://nx.dev/getting-started/nx-setup) for more detailed options.

## Add plugins

Angular:

> npx add -D @nrwl/angular

React:

> npx add -D @nrwl/react

Express:

> npx add -D @nrwl/express

...

## Generate (Angular) App / Components / ...

App:

> nx g @nrwl/angular:app name

Component:

> ng g c name --project=my-nx-playground

> nx g @nrwl/angular:component name --project=my-nx-playground

### Help Flag

> nx g @nrwl/express:app --help

### Link to frontend application

> nx g @nrwl/express:app api --frontendProject=frontend-name

## Serve an Application

> nx serve name

## Module Federation

- Host
  - Remote
  - Remote
  - ...

### Add module federation

- Add library:

  > npm i @angular-architects/module-federation

- Adjust generated configuration

### Alternative

- Use nx commands:

> nx g app name --mfe --mfeType=host

> nx g app name --mfe --mfeType=remote --port=3000 --host=shell

## Create Libraries

Angular:

> nx g @nrwl/angular:lib name

React:

> nx g @nrwl/react:lib name

Plain TypeScript library:

> nx g @nrwl/workspace:lib name

Library in Folder

> nx g @nrwl/react:lib --directory=review ui-tile

### Best Naming Practice

- ui-name : ui components
- data-access-name : data access components
- util-name : utility components
- feature-name: routing components
- service-name: service components
- store-name: store components


### Generate and Export Component in Library

> nx g @nrwl/react:component --project=name component-name

## Linting

> nx lint --project=name --fix

## Generate Report

Report:

> nx report

## Generate Dependency Graph

> nx dep-graph

For indication of dependencies affected by changes, run:

> nx affected:dep-graph

## Running Tests

> nx test --project=name

To test all projects affected by changes, run:

> nx affected:test

### E2E Testing: Cypress

> nx e2e review-e2e --watch

### Unit Testing: Jest
