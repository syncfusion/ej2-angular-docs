---
title: "Button Getting Started"
component: "Button"
description: "This section helps to learn how to create the button in Angular application with its basic features in step-by-step procedure."
---

# Getting Started

This section explains how to create a simple Button and demonstrate the basic usage of the Button module in an Angular environment.

## Dependencies

The list of dependencies required to use the Button module in your application is given below:

 ```typescript
|-- @syncfusion/ej2-angular-buttons
    |-- @syncfusion/ej2-angular-base
    |-- @syncfusion/ej2-base
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

## Installing Syncfusion Button package

To install Button package, use the following command.

```cmd
npm install @syncfusion/ej2-angular-buttons --save
```

The above package installs [Button dependencies](./getting-started#dependencies) which
are required to render the button component in the Angular environment.

## Adding Button module

Import Button module into Angular application(app.module.ts) from the package
`@syncfusion/ej2-angular-buttons`.

 ```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

// Imported Syncfusion button module from buttons package.
import { ButtonModule } from '@syncfusion/ej2-angular-buttons';

import { AppComponent }  from './app.component';

@NgModule({
  imports:      [ BrowserModule, ButtonModule ], // Registering EJ2 Button Module
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Adding Syncfusion Button component

Modify the template in `app.component.ts` file to render the Button module.

 ```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `<!-- To render Button. -->
             <button ejs-button>Button</button>`
})
export class AppComponent  { }
```

## Adding CSS reference

Add Button component's styles as given below in `style.css`.

```css
@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-buttons/styles/material.css";
```

## Running the application

Run the application in the browser using the following command:

```cmd
ng serve
```

The following example shows a basic Button component.

{% tab template="button/default", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<!-- To render Button. -->
               <button ejs-button>Button</button>`
})

export class AppComponent { }
```

{% endtab %}

## Change Button type

To change the default Button to flat Button, set the [`cssClass`](../api/button#cssclass) property with `e-flat` and text content of the Button is set using [`content`](../api/button#content) property.

{% tab template="button/default", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<!-- To change the Button type. -->
               <button ejs-button cssClass="e-flat" content="Button"></button>`
})

export class AppComponent { }
```

{% endtab %}
