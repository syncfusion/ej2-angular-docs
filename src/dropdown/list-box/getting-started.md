---
title: "List box Getting started"
component: "ListBox"
description: "This section explains how to create a simple Syncfusion angular list box component and configure it's functionalities in angular."
---

# Getting Started

This section briefly explains how to create a simple **ListBox** component and configure its available
functionalities in Angular.

## Dependencies

The following list of dependencies are required to use the ListBox component in your application.

```javascript
|-- @syncfusion/ej2-angular-dropdowns
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-data
    |-- @syncfusion/ej2-angular-base
    |-- @syncfusion/ej2-dropdowns
        |-- @syncfusion/ej2-lists
        |-- @syncfusion/ej2-inputs
        |-- @syncfusion/ej2-navigations
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

## Installing Syncfusion ListBox package

To install ListBox package, use the following command.

```cmd
npm install @syncfusion/ej2-angular-dropdowns --save
```

The above package installs [ListBox dependencies](/list-box/getting-started#dependencies) which are required to
render the component in the Angular environment.

## Adding ListBox module

Import ListBox module into Angular application(app.module.ts) from the package
`@syncfusion/ej2-angular-dropdowns`.

 ```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the ListBoxModule for the ListBox component
import { ListBoxModule } from '@syncfusion/ej2-angular-dropdowns';
import { AppComponent }  from './app.component';

@NgModule({
  //declaration of ej2-angular-dropdowns module into NgModule
  imports:      [ BrowserModule, ListBoxModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Adding Syncfusion ListBox component

Modify the template in `app.component.ts` file to render the Button module.

 ```typescript
import { Component, ViewEncapsulation } from '@angular/core';

@Component({
  selector: 'app-root',
  // specifies the template string for the ListBox component
  template: `<ejs-listbox></ejs-listbox>`,
  encapsulation: ViewEncapsulation.None
})
export class AppComponent  { }

```

## Adding CSS reference

Add Button component's styles as given below in `style.css`.

```css
@import "../node_modules/@syncfusion/ej2-dropdowns/styles/material.css";
```

## Binding data source

After initialization, populate the ListBox with data using the `dataSource` property.
Here, an array of object is passed to the ListBox component.

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the ListBox component
    template: `<ejs-listbox [dataSource]='data'></ejs-listbox>`
})
export class AppComponent {
    constructor() {
    }
    // defined the array of object
    public data: { [key: string]: Object }[] = [
    { text: 'Hennessey Venom', id: 'list-01' },
    { text: 'Bugatti Chiron', id: 'list-02' },
    { text: 'Bugatti Veyron Super Sport', id: 'list-03' },
    { text: 'SSC Ultimate Aero', id: 'list-04' },
    { text: 'Koenigsegg CCR', id: 'list-05' },
    { text: 'McLaren F1', id: 'list-06' },
    { text: 'Aston Martin One- 77', id: 'list-07' },
    { text: 'Jaguar XJ220', id: 'list-08' },
    { text: 'McLaren P1', id: 'list-09' },
    { text: 'Ferrari LaFerrari', id: 'list-10' },
];
}
```

## Run the application

After completing the configuration required to render a basic ListBox, run the following command to
display the output in your default browser.

```cmd
ng serve
```

The following example illustrates the output in your browser.

{% tab template="listbox/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';
import { ListBoxComponent } from '@syncfusion/ej2-angular-dropdowns';

@Component({
    selector: 'app-container',
    // specifies the template string for the ListBox component with dataSource
    template: `<ejs-listbox [dataSource]='data'></ejs-listbox>`
})
export class AppComponent {
    // defined the array of object
    public data: { [key: string]: Object }[] = [
    { text: 'Hennessey Venom', id: 'list-01' },
    { text: 'Bugatti Chiron', id: 'list-02' },
    { text: 'Bugatti Veyron Super Sport', id: 'list-03' },
    { text: 'SSC Ultimate Aero', id: 'list-04' },
    { text: 'Koenigsegg CCR', id: 'list-05' },
    { text: 'McLaren F1', id: 'list-06' },
    { text: 'Aston Martin One- 77', id: 'list-07' },
    { text: 'Jaguar XJ220', id: 'list-08' },
    { text: 'McLaren P1', id: 'list-09' },
    { text: 'Ferrari LaFerrari', id: 'list-10' }
];
}

```

{% endtab %}