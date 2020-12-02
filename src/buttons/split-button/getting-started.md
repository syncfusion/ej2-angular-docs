---
title: "SplitButton Getting Started"
component: "SplitButton"
description: "This section helps to learn how to create the splitbutton in Angular application with its basic features in step-by-step procedure."
---

# Getting Started

This section explains how to create a simple SplitButton and demonstrate the basic usage of the SplitButton component in an Angular environment.

## Dependencies

The list of dependencies required to use the SplitButton component in your application is given as follows:

```js
|-- @syncfusion/ej2-angular-splitbuttons
    |-- @syncfusion/ej2-angular-base
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-splitbuttons
        |-- @syncfusion/ej2-popups
            |-- @syncfusion/ej2-buttons
```

## Setup Angular environment

You can use [Angular CLI](https://github.com/angular/angular-cli) to setup your Angular applications. To install Angular CLI use the following command.

```cmd
npm install -g @angular/cli
```

## Create an Angular application

Start a new Angular application using below Angular CLI command.

```cmd
ng new my-app
cd my-app
```

## Installing Syncfusion SplitButton package

To install SplitButton package, use the following command.

```cmd
npm install @syncfusion/ej2-angular-splitbuttons --save
```

The above package installs `SplitButton dependencies` which are required to render the component in the Angular environment.

## Adding SplitButton module

Import SplitButton module into Angular application(app.module.ts) from the package
`@syncfusion/ej2-angular-splitbuttons`.

 ```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

// Imported Syncfusion splitbutton module from splitbuttons package.
import { SplitButtonModule } from '@syncfusion/ej2-angular-splitbuttons';
import { AppComponent }  from './app.component';

@NgModule({
  imports:      [ BrowserModule, SplitButtonModule ], // Registering EJ2 SplitButton Module.
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Adding Syncfusion SplitButton component

Modify the template in `app.component.ts` file to render the SplitButton component.

 ```typescript
import { Component } from '@angular/core';
import { ItemModel } from '@syncfusion/ej2-angular-splitbuttons';

@Component({
    selector: 'app-root',
    template: `<!-- To Render splitbutton. -->
               <ejs-splitbutton content="Paste" [items]='items'></ejs-splitbutton>`
})

export class AppComponent {
  public items: ItemModel[] = [
     { text: 'Cut'},
     { text: 'Copy'},
     { text: 'Paste'}
     ];
}
```

## Adding CSS reference

Add SplitButton component's styles as given below in `style.css`.

```css
@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-buttons/styles/material.css";
@import "../node_modules/@syncfusion/ej2-popups/styles/material.css";
@import "../node_modules/@syncfusion/ej2-splitbuttons/styles/material.css";
```

## Running the application

Run the application in the browser using the following command:

```cmd
ng serve
```

The below example shows a basic splitbutton component,

{% tab template="split-button/getting-started", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { ItemModel } from '@syncfusion/ej2-angular-splitbuttons';

@Component({
    selector: 'app-root',
    template: `<!-- To Render splitbutton. -->
               <ejs-splitbutton content="Paste" [items]='items'></ejs-splitbutton>`
})

export class AppComponent {
  public items: ItemModel[] = [
     { text: 'Cut'},
     { text: 'Copy'},
     { text: 'Paste'}
     ];
}
```

{% endtab %}
