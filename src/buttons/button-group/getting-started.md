---
title: "ButtonGroup Getting Started"
component: "ButtonGroup"
description: "This section helps to learn how to create the buttongroup in Angular application with its basic features in step-by-step procedure."
---

# Getting Started

This section explains how to create a simple CSS ButtonGroup, and demonstrate the basic usage of the CSS ButtonGroup component in an Angular environment.

## Dependencies

The following list of dependencies are required to use the ButtonGroup component in your application.

```js
|-- @syncfusion/ej2-splitbuttons
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

## Installing Syncfusion ButtonGroup package

To install ButtonGroup package, use the following command.

```cmd
npm install @syncfusion/ej2-angular-buttons --save
```

The above package installs [Button dependencies](./getting-started#dependencies) which
are required to render the ButtonGroup component in the Angular environment.

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

## Adding Syncfusion ButtonGroup component

Modify the template in `app.component.ts` file to render the ButtonGroup component.

 ```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `<div class='e-btn-group'>
              <button ejs-button>HTML</button>
              <button ejs-button>CSS</button>
              <button ejs-button>Javascript</button>
            </div>`
})
export class AppComponent  { }
```

> To render Button in CSS ButtonGroup component, import Button module into the angular application(app.module.ts) from the package `@syncfusion/ej2-angular-buttons` and its styles in `style.css`.

## Adding CSS reference

Add ButtonGroup component's styles as given below in `style.css`.

```css
@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-buttons/styles/material.css";
@import "../node_modules/@syncfusion/ej2-splitbuttons/styles/material.css";
```

## Running the application

Run the application in the browser using the following command:

```cmd
ng serve
```

The following example shows a basic ButtonGroup component.

{% tab template="button-group/default", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<!-- To render ButtonGroup. -->
               <div class='e-btn-group'>
                  <button ejs-button>HTML</button>
                  <button ejs-button>CSS</button>
                  <button ejs-button>Javascript</button>
                </div>`
})

export class AppComponent { }
```

{% endtab %}

## Orientation

ButtonGroup can be arranged both in a vertical and horizontal orientation. By default, it is horizontally oriented.

### Vertical Orientation

ButtonGroup can be aligned vertically by using the built-in CSS `e-vertical` to the target element.

The following example illustrates how to achieve vertical orientation in ButtonGroup.

{% tab template="button-group/default", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<!-- To render ButtonGroup. -->
               <div class='e-btn-group e-vertical'>
                  <button ejs-button>HTML</button>
                  <button ejs-button>CSS</button>
                  <button ejs-button>Javascript</button>
                </div>`
})

export class AppComponent { }
```

{% endtab %}

> ButtonGroup does not support SplitButton component nesting in a vertical orientation.
