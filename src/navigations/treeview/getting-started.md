---
title: "Getting Started"
component: "TreeView"
description: "Rendering treeview using Angular"
---

# Getting Started

This section explains the steps required to create a simple **TreeView** component, and configure its available functionalities

## Setup Angular Environment

You can use [`Angular CLI`](https://github.com/angular/angular-cli) to setup your Angular applications.
To install Angular CLI use the following command.

```bash
npm install -g @angular/cli
```

## Create an Angular Application

Start a new Angular application using below Angular CLI command.

```bash
ng new my-app
cd my-app
```

## Adding Syncfusion Treeview package

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) registry.

To install Treeview component, use the following command.

```bash
npm install @syncfusion/ej2-angular-navigations --save
```

> The **--save** will instruct NPM to include the Treeview package inside of the `dependencies` section of the `package.json`.

## Registering Treeview Module

Import Treeview module into Angular application(app.module.ts) from the package `@syncfusion/ej2-angular-navigations` [src/app/app.module.ts].

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import Treeview component Module
import { TreeViewModule } from '@syncfusion/ej2-angular-navigations';
import { AppComponent }  from './app.component';

@NgModule({
  //declaration of Treeview module into NgModule
  imports:      [ BrowserModule, TreeViewModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Adding CSS Reference

* Add Treeview component's styles as given below in `styles.css`.

```css
@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-angular-navigations/styles/material.css";
@import "../node_modules/@syncfusion/ej2-inputs/styles/material.css";
@import "../node_modules/@syncfusion/ej2-buttons/styles/material.css";
```

>Note: If you want to refer the combined component styles, please make use of
our [`CRG`](https://ej2crg.azurewebsites.net/) (Custom Resource Generator) in your application.

## Add Treeview component

Modify the template in [src/app/app.component.ts] file to render the Treeview component.
Add the Angular Treeview by using `<ejs-treeview>` selector in `template` section of the app.component.ts file.

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `<ejs-treeview id='treeelement' ></ejs-treeview>`
})
export class AppComponent {}
```

## Binding data source

TreeView can load data either from local data sources or remote data services. This can be done using the [dataSource](../api/treeview/fieldsSettingsModel#datasource)
property that is a member of the `fields` property. The dataSource property supports array of JavaScript objects and `DataManager`.
Here, an array of JSON values is passed to the TreeView component.

```typescript
import { Component, ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<ejs-treeview id='treeelement' [fields]='field'></ejs-treeview>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    constructor() {
    }
    // defined the array of data
     public hierarchicalData: Object[] = [
        { id: '01', name: 'Music', expanded: true,
            subChild: [
                {id: '01-01', name: 'Gouttes.mp3'},
                      ]
        },
        {
            id: '02', name: 'Videos',
            subChild: [
                {id: '02-01', name: 'Naturals.mp4'},
                {id: '02-02', name: 'Wild.mpeg'}
        ]
        },
        {
            id: '03', name: 'Documents',
            subChild: [
                {id: '03-01', name: 'Environment Pollution.docx'},
                {id: '03-02', name: 'Global Water, Sanitation, & Hygiene.docx'},
                {id: '03-03', name: 'Global Warming.ppt'},
                {id: '03-02', name: 'Social Network.pdf'},
                {id: '03-03', name: 'Youth Empowerment.pdf'},
            ]
        }
    ];
    public field:Object ={ dataSource: this.hierarchicalData, id: 'id', text: 'name', child: 'subChild' };
}
```

## Run the application

Use the following command to run the application in browser.

```javascript
ng serve --open
```

The output will appear as follows.

{% tab template="tree-view/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<div id='treeparent'><ejs-treeview id='treeelement' [fields]='field'></ejs-treeview></div>`
})
export class AppComponent {
    constructor() {
    }
    // defined the array of data
    public hierarchicalData: Object[] = [
       { id: '01', name: 'Music', expanded: true,
            subChild: [
                {id: '01-01', name: 'Gouttes.mp3'},
                      ]
        },
        {
            id: '02', name: 'Videos',
            subChild: [
                {id: '02-01', name: 'Naturals.mp4'},
                {id: '02-02', name: 'Wild.mpeg'}
        ]
        },
        {
            id: '03', name: 'Documents',
            subChild: [
                {id: '03-01', name: 'Environment Pollution.docx'},
                {id: '03-02', name: 'Global Water, Sanitation, & Hygiene.docx'},
                {id: '03-03', name: 'Global Warming.ppt'},
                {id: '03-02', name: 'Social Network.pdf'},
                {id: '03-03', name: 'Youth Empowerment.pdf'},
            ]
        }
    ];
    public field:Object ={ dataSource: this.hierarchicalData, id: 'id', text: 'name', child: 'subChild' };
}
```

{% endtab %}

## See Also

* [How to customize treeview as accordion](./how-to/accordion-tree/)

* [How to set tooltip for treeview nodes](./how-to/set-tool-tip-for-tree-nodes/)

* [How to filter nodes in treeview](./how-to/filtering-tree-nodes/)

* [How to get all the child nodes through parentID](./how-to/get-all-child-nodes/)