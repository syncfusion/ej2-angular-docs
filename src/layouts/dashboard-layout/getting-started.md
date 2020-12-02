---
title: "Getting Started"
component: "DashboardLayout"
description: "This section explains how to create a DashboardLayout component in the Angular application with its basic features."
---

# Getting Started

This section explains how to create a simple **DashboardLayout** component and its basic usage.

## Prerequisites

To get started with **DashboardLayout** component, ensure the compatible versions of Angular and Typescript.

* Angular : `4+`
* Typescript : `2.6+`

## Setting up angular project

Angular provides the easiest way to set angular CLI projects using Angular CLI tool.

Install the CLI application globally to your machine by using following command.

```sh
npm install -g @angular/cli
```

Create a new angular application

```sh
ng new syncfusion-angular-app
```

Navigate to the created project folder by using following command.

```sh
cd syncfusion-angular-app
```

>Refer [Syncfusion Angular Getting Started](../../getting-started/angular-cli/#getting-started-with-angular-cli) section to know more about setting up `angular-cli` project.

## Adding Dependencies

The following list of dependencies are required to use the DashboardLayout component in your application.

```javascript
|-- @syncfusion/ej2-angular-layouts
    |-- @syncfusion/ej2-angular-base
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-layouts

```

* Install Syncfusion DashboardLayout package using below command.

```cmd
npm install @syncfusion/ej2-angular-layouts --save
```

The above package installs [Dashboard Layout component dependencies](#adding-dependencies) which are required to render the component in an Angular environment.

## Adding style sheet to the application

To render the DashboardLayout component, import the DashboardLayout and its dependent component's styles as given below in `[src/styles.css]`.

```css
@import "../../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../../node_modules/@syncfusion/ej2-angular-layouts/styles/material.css";
```

>Note: To refer the combined component styles, use Syncfusion [`CRG`](https://crg.syncfusion.com/) (Custom Resource Generator) in your application.

## Add DashboardLayout to the application

You can render the DashboardLayout component in the following two ways.

* Defined the panels property as the attribute in the HTML element directly.
* Using the `panels` property through tag helper.

## Setting the `panels` property using HTML attributes

You can render the DashboardLayout component by adding the panels property as the attribute to the HTML element directly. Add the HTML div element with panel definition for DashboardLayout into your `app.template.html` file.

`[src/app/app.template.html]`

```html
<div class="control-section">
    <ejs-dashboardlayout id='defaultLayout' [columns]="5" #defaultLayout [cellSpacing]='cellSpacing'>
        <div id="one" class="e-panel" data-row="0" data-col="0" data-sizeX="1" data-sizeY="1">
            <span id="close" class="e-template-icon e-clear-icon"></span>
            <div class="e-panel-container">
                <div class="text-align">0</div>
            </div>
        </div>
        <div id="two" class="e-panel" data-row="1" data-col="0" data-sizeX="1" data-sizeY="2">
            <span id="close" class="e-template-icon e-clear-icon"></span>
            <div class="e-panel-container">
                <div class="text-align">1</div>
            </div>
        </div>
        <div id="three" class="e-panel" data-row="0" data-col="1" data-sizeX="2" data-sizeY="2">
            <span id="close" class="e-template-icon e-clear-icon"></span>
            <div class="e-panel-container">
                <div class="text-align">2</div>
            </div>
        </div>
        <div id="four" class="e-panel" data-row="2" data-col="1" data-sizeX="1" data-sizeY="1">
            <span id="close" class="e-template-icon e-clear-icon"></span>
            <div class="e-panel-container">
                <div class="text-align">3</div>
            </div>
        </div>
        <div id="five" class="e-panel" data-row="2" data-col="2" data-sizeX="2" data-sizeY="1">
            <span id="close" class="e-template-icon e-clear-icon"></span>
            <div class="e-panel-container">
                <div class="text-align">4</div>
            </div>
        </div>
        <div id="six" class="e-panel" data-row="0" data-col="3" data-sizeX="1" data-sizeY="1">
            <span id="close" class="e-template-icon e-clear-icon"></span>
            <div class="e-panel-container">
                <div class="text-align">5</div>
            </div>
        </div>
        <div id="seven" class="e-panel" data-row="1" data-col="3" data-sizeX="1" data-sizeY="1">
            <span id="close" class="e-template-icon e-clear-icon"></span>
            <div class="e-panel-container">
                <div class="text-align">6</div>
            </div>
        </div>
        <div id="eight" class="e-panel" data-row="0" data-col="4" data-sizeX="1" data-sizeY="3">
            <span id="close" class="e-template-icon e-clear-icon"></span>
            <div class="e-panel-container">
                <div class="text-align">7</div>
            </div>
        </div>
    </ejs-dashboardlayout>
</div>
```

Now, modify the `templateUrl` in `app.component.ts` file to render DashboardLayout component.

`[src/app/app.component.ts]`

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  styleUrls: ['default-style.css'],
  templateUrl: 'app.template.html'
})

export class AppComponent {
}
```

* Import DashboardLayout module into Angular application(app.module.ts) from the package `@syncfusion/ej2-angular-layouts`.

```javascript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the DashboardLayoutModule for the Dashboard Layout component
import { DashboardLayoutModule } from '@syncfusion/ej2-angular-layouts';
import { AppComponent }  from './app.component';

@NgModule({
  //declaration of ej2-angular-layouts module into NgModule
  imports:      [ BrowserModule, DashboardLayoutModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Run the application

Now, use the `npm start` command to run the application in the browser.

```html
npm start
```

The following example shows a basic DashboardLayout by adding the panels property directly into the HTML element.

{% tab template="dashboard-layout/getting-started", sourceFiles="app/app.component.ts,app/app.template.html,app/app.module.ts,app/main.ts,app/default-style.css" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['app/default-style.css'],
    templateUrl: 'app/app.template.html',
    encapsulation: ViewEncapsulation.None
})

export class AppComponent {
    public cellSpacing: number[] = [10, 10];
}
```

{% endtab %}

## Setting the `panels` property through binding

You can render the DashboardLayout component by using the **panels** property through binding.

`[src/app/app.template.html]`

```html
<div class="control-section">
    <ejs-dashboardlayout id='defaultLayout' #defaultLayout [cellSpacing]='cellSpacing' [panels]='panels' [columns]="5">
    </ejs-dashboardlayout>
</div>

```

Now, modify the `templateUrl` in `app.component.ts` file to render DashboardLayout component.

`[src/app/app.component.ts]`

```typescript
import { Component,ViewEncapsulation } from '@angular/core';

@Component({
  selector: 'app-root',
  styleUrls: ['app/default-style.css'],
  templateUrl: 'app/app.template.html',
  encapsulation: ViewEncapsulation.None
})
export class AppComponent {
  public cellSpacing: number[] = [10, 10];
  public panels: any = [{ "sizeX": 1, "sizeY": 1, "row": 0, "col": 0, content: '<div class="content">0</div>' },
    { "sizeX": 3, "sizeY": 2, "row": 0, "col": 1, content: '<div class="content">1</div>' },
    { "sizeX": 1, "sizeY": 3, "row": 0, "col": 4, content: '<div class="content">2</div>' },
    { "sizeX": 1, "sizeY": 1, "row": 1, "col": 0, content: '<div class="content">3</div>' },
    { "sizeX": 2, "sizeY": 1, "row": 2, "col": 0, content: '<div class="content">4</div>' },
    { "sizeX": 1, "sizeY": 1, "row": 2, "col": 2, content: '<div class="content">5</div>' },
    { "sizeX": 1, "sizeY": 1, "row": 2, "col": 3, content: '<div class="content">6</div>' }
  ]
}
```

The following example shows a basic DashboardLayout by using the `panels` property.

{% tab template="dashboard-layout/getting-started-panel", sourceFiles="app/app.component.ts,app/app.template.html,app/app.module.ts,app/main.ts,app/default-style.css" %}

```typescript
import { Component,ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['app/default-style.css'],
    templateUrl: 'app/app.template.html',
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    public cellSpacing: number[] = [10, 10];
    public panels: any = [{ "sizeX": 1, "sizeY": 1, "row": 0, "col": 0, content: '<div class="content">0</div>' },
    { "sizeX": 3, "sizeY": 2, "row": 0, "col": 1, content: '<div class="content">1</div>' },
    { "sizeX": 1, "sizeY": 3, "row": 0, "col": 4, content: '<div class="content">2</div>' },
    { "sizeX": 1, "sizeY": 1, "row": 1, "col": 0, content: '<div class="content">3</div>' },
    { "sizeX": 2, "sizeY": 1, "row": 2, "col": 0, content: '<div class="content">4</div>' },
    { "sizeX": 1, "sizeY": 1, "row": 2, "col": 2, content: '<div class="content">5</div>' },
    { "sizeX": 1, "sizeY": 1, "row": 2, "col": 3, content: '<div class="content">6</div>' }
    ]
}
```

{% endtab %}