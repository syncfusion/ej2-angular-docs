---
title: "CheckBox Getting Started"
component: "CheckBox"
description: "This section helps to learn how to create the checkbox in Angular application with its basic features in step-by-step procedure."
---

# Getting Started

This section explains how to create a simple CheckBox, and demonstrate the basic usage of the CheckBox module in an Angular environment.

## Dependencies

The following list of dependencies are required to use the CheckBox module in your application.

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

## Installing Syncfusion CheckBox package

To install CheckBox package, use the following command.

```cmd
npm install @syncfusion/ej2-angular-buttons --save
```

The above package installs [CheckBox dependencies](./getting-started#dependencies) which
are required to render the component in the Angular environment.

## Adding CheckBox module

Import CheckBox module into Angular application(app.module.ts) from the package
`@syncfusion/ej2-angular-buttons`.

 ```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

// Imported Syncfusion checkbox module from buttons package.
import { CheckBoxModule } from '@syncfusion/ej2-angular-buttons';

import { AppComponent }  from './app.component';

@NgModule({
  imports:      [ BrowserModule, CheckBoxModule ], // Registering EJ2 Checkbox Module.
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Adding Syncfusion CheckBox component

Modify the template in `app.component.ts` file to render the CheckBox component.

 ```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `<!-- To Render CheckBox. -->
             <ejs-checkbox label="Default"></ejs-checkbox>`
})
export class AppComponent  { }
```

## Adding CSS reference

Add CheckBox component's styles as given below in `style.css`.

```css
@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-buttons/styles/material.css";
```

## Running the application

Run the application in the browser using the following command:

```cmd
ng serve
```

The below example shows a basic CheckBox component,

{% tab template="check-box/getting-started", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<!-- To Render CheckBox. -->
               <ejs-checkbox label="Default"></ejs-checkbox>`
})

export class AppComponent { }
```

{% endtab %}

## Change the CheckBox state

The Essential JS 2 CheckBox contains 3 different states visually, they are:
* Checked
* Unchecked
* Indeterminate

The CheckBox [`checked`](../api/check-box#checked) property is used to handle the checked and unchecked state.
In checked state a tick mark will be added to the visualization of CheckBox.

### Indeterminate

CheckBox indeterminate state can be set through [`indeterminate`](../api/check-box#indeterminate) property.
CheckBox indeterminate state masks the real value of CheckBox visually. Checkbox cannot be changed to indeterminate state through the user interface,
this state can be achieved only through the property.

{% tab template= "check-box/label-and-size", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<ul>
               <!-- checked state. -->
               <li><ejs-checkbox label="Checked State" [checked]="true"></ejs-checkbox></li>

               <!-- unchecked state. -->
               <li><ejs-checkbox label="Unchecked State"></ejs-checkbox></li>

               <!-- indeterminate state. -->
               <li><ejs-checkbox label="Indeterminate State" [indeterminate]="true"></ejs-checkbox></li>
               </ul>`
})

export class AppComponent { }

```

{% endtab %}