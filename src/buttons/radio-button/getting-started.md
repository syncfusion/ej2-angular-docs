---
title: "RadioButton Getting Started"
component: "RadioButton"
description: "This section helps to learn how to create the radiobutton in Angular application with its basic features in step-by-step procedure."
---

# Getting Started

This section explains how to create a simple RadioButton, and demonstrate the basic usage of the RadioButton module in an Angular environment.

## Dependencies

The following list of dependencies are required to use the RadioButton module in your application.

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

## Installing Syncfusion RadioButton package

To install RadioButton package, use the following command.

```cmd
npm install @syncfusion/ej2-angular-buttons --save
```

## Adding RadioButton module

Import RadioButton module into Angular application(app.module.ts) from the package
`@syncfusion/ej2-angular-buttons`.

```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

// Imported Syncfusion radiobutton module from buttons package.
import { RadioButtonModule } from '@syncfusion/ej2-angular-buttons';

import { AppComponent }  from './app.component';

@NgModule({
  imports:      [ BrowserModule, RadioButtonModule ], // Registering EJ2 RadioButton Module.
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Adding Syncfusion RadioButton component

Modify the template in `app.component.ts` file to render the RadioButton component.

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `<!-- To Render RadioButton. -->
             <ejs-radiobutton label="Default"></ejs-radiobutton>`
})
export class AppComponent  { }
```

## Adding CSS reference

Add RadioButton component's styles as given below in `style.css`.

```css
@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-buttons/styles/material.css";
```

## Running the application

Run the application in the browser using the following command:

```cmd
ng serve
```

The below example shows a basic RadioButton component,

{% tab template="radio-button/getting-started", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<ul>
               <!-- To Render RadioButton. -->
               <li><ejs-radiobutton label="Option 1" name="default"></ejs-radiobutton></li>

               <li><ejs-radiobutton label="Option 2" name="default" checked="true"></ejs-radiobutton></li>
               </ul>`
})

export class AppComponent { }
```

{% endtab %}

## Change the RadioButton state

The Essential JS 2 RadioButton contains 2 different states visually, they are as follows:
* Checked
* Unchecked

The RadioButton [`checked`](../api/radio-button#checked) property is used to handle the checked and unchecked state.
In the checked state an inner circle will be added to the visualization of RadioButton.

{% tab template= "radio-button/label-and-size", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<ul>
               <!-- checked state. -->
               <li><ejs-radiobutton label="Option 1" name="state" checked="true"></ejs-radiobutton></li>

               <!-- unchecked state. -->
               <li><ejs-radiobutton label="Option 2" name="state"></ejs-radiobutton></li>
               </ul>`
})

export class AppComponent { }

```

{% endtab %}