---
title: "Switch Getting Started"
component: "Switch"
description: "This section helps to learn how to create the switch in Angular application with its basic features in step-by-step procedure."
---

# Getting Started

This section explains how to create a simple Switch, and demonstrate the basic usage of the Switch module in an Angular environment.

## Dependencies

The following list of dependencies are required to use the Switch module in your application.

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

## Installing Syncfusion Switch package

To install Switch package, use the following command.

```cmd
npm install @syncfusion/ej2-angular-buttons --save
```

The above package installs [Switch dependencies](./getting-started#dependencies) which
are required to render the Switch component in the Angular environment.

## Adding Switch module

Import Switch module into Angular application(app.module.ts) from the package
`@syncfusion/ej2-angular-buttons`.

 ```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

// Imported Syncfusion Switch module from buttons package.
import { SwitchModule } from '@syncfusion/ej2-angular-buttons';

import { AppComponent }  from './app.component';

@NgModule({
  imports:      [ BrowserModule, SwitchModule ], // Registering EJ2 Switch Module.
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Adding Syncfusion Switch component

Modify the template in `app.component.ts` file to render the Switch component.

 ```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `<!-- To Render Switch with checked state. -->
             <ejs-switch [checked]="true"></ejs-switch>`
})
export class AppComponent  { }
```

## Adding CSS reference

Add Switch component's styles as given below in `style.css`.

```css
@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-buttons/styles/material.css";
```

## Running the application

Run the application in the browser using the following command:

```cmd
ng serve
```

The below example shows a basic Switch component,

{% tab template="switch/getting-started", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<!-- To Render Switch with checked state. -->
               <ejs-switch [checked]="true"></ejs-switch>`
})

export class AppComponent { }
```

{% endtab %}

## Set text on Switch

This section explains how to set [`onLabel`](../api/switch#onlabel)
and [`offLabel`](../api/switch#offlabel) texts on Switch. In the following example, `onLabel` is set as
`ON` and `offLabel` is set as `OFF`.

{% tab template="switch/text", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<!-- To Render Switch. -->
               <ejs-switch onLabel="ON" offLabel="OFF" [checked]="true"></ejs-switch>`
})

export class AppComponent { }
```

{% endtab %}

> Switch does not have text support for material themes, and does not support long custom text.
