---
title: "ProgressButton Getting Started"
component: "ProgressButton"
description: "This section helps to learn how to create the progressbutton in Angular application with its basic features in step-by-step procedure."
---

# Getting Started

This section explains how to create a simple ProgressButton and demonstrate the basic usage of the ProgressButton component in an Angular environment.

## Dependencies

The list of dependencies required to use the ProgressButton component in your application is given as follows:

 ```typescript
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

## Installing Syncfusion ProgressButton package

To install ProgressButton package, use the following command.

```cmd
npm install @syncfusion/ej2-angular-splitbuttons --save
```

The above package installs `ProgressButton dependencies` which are required to render the component in the Angular environment.

## Adding ProgressButton module

Import ProgressButton module into Angular application(app.module.ts) from the package
`@syncfusion/ej2-angular-splitbuttons`.

```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

// Imported Syncfusion Progress button module from split buttons package
import { ProgressButtonModule } from '@syncfusion/ej2-angular-splitbuttons';

import { AppComponent }  from './app.component';

@NgModule({
  imports:      [ BrowserModule, ProgressButtonModule ], // Registering EJ2 ProgressButtonModule.
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Adding Syncfusion ProgressButton component

Modify the template in `app.component.ts` file to render the ProgressButton component.

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<!-- To render progress button. -->
               <button ejs-progressbutton content='Spin Left'></button>`
})

export class AppComponent {
}
```

## Adding CSS reference

Add ProgressButton component's styles as given below in `style.css`.

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

The below example shows a basic ProgressButton component.

{% tab template="progress-button/default", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<!-- To render progress button. -->
               <button ejs-progressbutton content='Spin Left'></button>`
})

export class AppComponent {
}
```

{% endtab %}

> ProgressButton supports different styles, types and sizes like [`Button`](https://ej2.syncfusion.com/angular/documentation/button/). In addition, it also supports `top` and `bottom` icon positions.

## Enable progress in button

You can enable the background filler UI by setting the [`enableProgress`](../api/progress-button#enableProgress) property to `true`.

{% tab template="progress-button/default", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<!-- To render progress button. -->
               <button ejs-progressbutton content='Spin Left' [enableProgress]='true'></button>`
})

export class AppComponent {
}
```

{% endtab %}
