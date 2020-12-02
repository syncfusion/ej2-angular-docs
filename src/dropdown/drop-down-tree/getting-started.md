---
title: "Drop-down tree Getting started"
component: "DropDownTree"
description: "This section explains how to create a simple Syncfusion angular drop-down tree component and configure it's functionalities in angular."
---

# Getting Started

This section explains you about how to create a simple **Dropdown Tree** component and configure its available
functionalities in Angular.

## Dependencies

The following list of dependencies are required to use the Dropdown Tree component in your application.

```javascript
|-- @syncfusion/ej2-angular-dropdowns
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-data
    |-- @syncfusion/ej2-ng-base
    |-- @syncfusion/ej2-dropdowns
        |-- @syncfusion/ej2-lists
        |-- @syncfusion/ej2-inputs
        |-- @syncfusion/ej2-navigations
        |-- @syncfusion/ej2-popups
            |-- @syncfusion/ej2-buttons

```

## Setup angular environment

Angular provides the easiest way to set angular CLI projects using [`Angular CLI`](https://github.com/angular/angular-cli) tool.

Install the CLI application globally to your machine.

```bash
npm install -g @angular/cli
```

## Create an Angular Application

Start a new Angular application using below Angular CLI command.

```bash
ng new my-app
cd my-app
```

## Adding Syncfusion DropDown package

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) registry.

To install Dropdown Tree component, use the following command.

```bash
npm install @syncfusion/ej2-angular-dropdowns --save
```

> The **--save** will instruct NPM to include the Dropdown Tree package inside of the `dependencies` section of the `package.json`.

## Registering Dropdown Tree Module

Import Dropdown Tree module into Angular application(app.module.ts) from the package `@syncfusion/ej2-angular-dropdowns`.

```javascript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the DropDownTreeModule for the DropDownTree component
import { DropDownTreeModule } from '@syncfusion/ej2-angular-dropdowns';
import { AppComponent }  from './app.component';

@NgModule({
  //declaration of ej2-angular-dropdowns module into NgModule
  imports:      [ BrowserModule, DropDownTreeModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Adding CSS Reference

Add Dropdown Tree component's styles as given below in `styles.css`.

```css
@import '../node_modules/@syncfusion/ej2-base/styles/material.css';
@import '../node_modules/@syncfusion/ej2-buttons/styles/material.css';
@import '../node_modules/@syncfusion/ej2-dropdowns/styles/material.css';
@import '../node_modules/@syncfusion/ej2-navigations/styles/material.css';
@import '../node_modules/@syncfusion/ej2-inputs/styles/material.css';
@import '../node_modules/@syncfusion/ej2-popups/styles/material.css';
@import '../node_modules/@syncfusion/ej2-lists/styles/material.css';
@import '../node_modules/@syncfusion/ej2-angular-dropdowns/styles/material.css';
```

>Note: If you want to refer the combined component styles, please make use of
our [`CRG`](https://ej2crg.azurewebsites.net/) (Custom Resource Generator) in your application.

## Add Dropdown Tree component

Modify the template in [src/app/app.component.ts] file to render the Dropdown Tree component.
Add the Angular Dropdown Tree by using `ejs-dropdowntree` selector in `template` section of the app.component.ts file.

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `<ejs-dropdowntree id='dropdowntree'></ejs-dropdowntree>`
})
export class AppComponent {}
```

## Binding data source

The Dropdown Tree component can load the data either from local data sources or remote data services. This can be done using the `dataSource` property that is a member of the `fields` property. The dataSource property supports array of JavaScript objects and DataManager. Here, an array of JSON values is passed to the Dropdown Tree component.

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the DropDownTree component
    template: `<ejs-dropdowntree id='dropdowntree' [fields]='fields' placeholder='Select a Item'></ejs-dropdowntree>`
})
export class AppComponent {
    constructor() {
    }
    // defined the array of data
    public data: { [key: string]: Object }[] = [
     {
        nodeId: '01', nodeText: 'Music',
        nodeChild: [
            { nodeId: '01-01', nodeText: 'Gouttes.mp3' }
        ]
     },
     {
        nodeId: '02', nodeText: 'Videos', expanded: true,
        nodeChild: [
            { nodeId: '02-01', nodeText: 'Naturals.mp4' },
            { nodeId: '02-02', nodeText: 'Wild.mpeg' },
        ]
     },
     {
        nodeId: '03', nodeText: 'Documents',
        nodeChild: [
            { nodeId: '03-01', nodeText: 'Environment Pollution.docx' },
            { nodeId: '03-02', nodeText: 'Global Water, Sanitation, & Hygiene.docx' },
            { nodeId: '03-03', nodeText: 'Global Warming.ppt' },
            { nodeId: '03-04', nodeText: 'Social Network.pdf' },
            { nodeId: '03-05', nodeText: 'Youth Empowerment.pdf' },
        ]
     },
    ];
     //binding data source through fields property
    public fields: Object = { dataSource: this.data, value: 'nodeId', text: 'nodeText', child: 'nodeChild' };
}

```

## Run the application

After completing the configuration required to render a basic Dropdown Tree, run the following command to display the output in your default browser.

```javascript
ng serve --open
```

The following example illustrates the output in your browser.

{% tab template="dropdowntree/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    // specifies the template string for the DropDownTree component
    template: `<ejs-dropdowntree id='dropdowntree' [fields]='fields' placeholder='Select a Item'></ejs-dropdowntree>`
})
export class AppComponent {
    constructor() {
    }
    // defined the array of data
    public data: { [key: string]: Object }[] = [
     {
        nodeId: '01', nodeText: 'Music',
        nodeChild: [
            { nodeId: '01-01', nodeText: 'Gouttes.mp3' }
        ]
     },
     {
        nodeId: '02', nodeText: 'Videos', expanded: true,
        nodeChild: [
            { nodeId: '02-01', nodeText: 'Naturals.mp4' },
            { nodeId: '02-02', nodeText: 'Wild.mpeg' },
        ]
     },
     {
        nodeId: '03', nodeText: 'Documents',
        nodeChild: [
            { nodeId: '03-01', nodeText: 'Environment Pollution.docx' },
            { nodeId: '03-02', nodeText: 'Global Water, Sanitation, & Hygiene.docx' },
            { nodeId: '03-03', nodeText: 'Global Warming.ppt' },
            { nodeId: '03-04', nodeText: 'Social Network.pdf' },
            { nodeId: '03-05', nodeText: 'Youth Empowerment.pdf' },
        ]
     },
    ];
     //binding data source through fields property
    public fields: Object = { dataSource: this.data, value: 'nodeId', text: 'nodeText', child: 'nodeChild' };
}

```

{% endtab %}