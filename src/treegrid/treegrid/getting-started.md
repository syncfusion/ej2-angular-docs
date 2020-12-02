---
title: "Getting Started"
component: "TreeGrid"
description: "Learn how to create a TreeGrid and to enable the features like paging, filtering and sorting in Angular2"
---

# Getting started

This section explains the steps required to create a simple Essential JS 2 TreeGrid and demonstrates the basic usage of the TreeGrid control in a Angular CLI application.

To get start quickly with Angular TreeGrid using CLI and Schematics, you can check on this video:

`youtube:2LJKv7rao6Y`

## Setup Angular Environment

You can use the [`Angular CLI`](https://github.com/angular/angular-cli) to setup your Angular applications.
To install Angular CLI use the following command.

```bash
npm install -g @angular/cli
```

## Create an Angular Application

Start a new Angular application using the Angular CLI command as follows.

```bash
ng new my-app
cd my-app
```

## Adding Syncfusion TreeGrid package

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) registry.

To install TreeGrid component, use the following command.

```bash
npm install @syncfusion/ej2-angular-treegrid --save
```

> The **--save** will instruct NPM to include the TreeGrid package inside of the `dependencies` section of the `package.json`.

## Registering TreeGrid Module

Import TreeGrid module into the Angular application(app.module.ts) from the package `@syncfusion/ej2-angular-treegrid` [src/app/app.module.ts].

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the TreeGridModule for the TreeGrid component
import { TreeGridModule } from '@syncfusion/ej2-angular-treegrid';
import { AppComponent }  from './app.component';

@NgModule({
  //declaration of ej2-angular-treegrid module into NgModule
  imports:      [ BrowserModule, TreeGridModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Adding CSS reference

The following CSS files are available in `../node_modules/@syncfusion` package folder.
This can be referenced in [src/styles.css] using the following code.

```css
@import '../node_modules/@syncfusion/ej2-base/styles/material.css';
@import '../node_modules/@syncfusion/ej2-buttons/styles/material.css';
@import '../node_modules/@syncfusion/ej2-calendars/styles/material.css';
@import '../node_modules/@syncfusion/ej2-dropdowns/styles/material.css';
@import '../node_modules/@syncfusion/ej2-inputs/styles/material.css';
@import '../node_modules/@syncfusion/ej2-navigations/styles/material.css';
@import '../node_modules/@syncfusion/ej2-popups/styles/material.css';
@import '../node_modules/@syncfusion/ej2-splitbuttons/styles/material.css';
@import '../node_modules/@syncfusion/ej2-grids/styles/material.css';
@import '../node_modules/@syncfusion/ej2-treegrid/styles/material.css';
```

## Add TreeGrid component

Modify the template in [src/app/app.component.ts] file to render the TreeGrid component.
Add the Angular TreeGrid by using `<ejs-treegrid>` selector in `template` section of the app.component.ts file.

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-container',
  // specifies the template string for the TreeGrid component
  template: `<ejs-treegrid> </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    ngOnInit(): void {
    }
}

```

## Defining Row Data

Bind data for the TreeGrid component by using `dataSource` property.
It accepts either an array of JavaScript object or `DataManager` instance.

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data'> </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];

    ngOnInit(): void {
        this.data = sampleData;
    }
}
```

## Defining Columns

The TreeGrid has an option to define the columns as an array. In these columns, the following properties are used to customize the columns.

* The `field` has been added to map with a property name in an array of JavaScript objects.
* The `headerText` has been added to change the title of columns.
* The `textAlign` has been used to change the alignment of columns. By default, columns will be left aligned. To change the columns to right align, define the `textAlign` to `Right`.
* Also, the another useful property, `format` has been used. Using this, you can format number and date values to standard or custom formats. Here it is defined for the conversion of date objects to formatted strings.

Tree Column is used to expand or collapse child rows is defined by using the [`treeColumnIndex`](../api/treegrid/#treecolumnindex) property.

{% tab template="treegrid/getting-started", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' [treeColumnIndex]='1' childMapping='subtasks'>
                <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=70></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=200></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=90></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
                </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];

    ngOnInit(): void {
        this.data = sampleData;
    }
}
```

{% endtab %}

In the above code example, the hierarchical data binding is represented in which the [`childMapping`](../api/treegrid/#childmapping) property denotes the hierarchy relationship; whereas in self-referencing data binding [`idMapping`](../api/treegrid/#idmapping)  and [`parentIdMapping`](../api/treegrid/#parentidmapping) denotes the hierarchy relationship.

## Module injection

To create TreeGrid with additional features, inject the required modules. The following modules are used to extend TreeGrid's basic functionality.

* `PageService`- Inject this module to use paging feature.
* `SortService` - Inject this module to use sorting feature.
* `FilterService` - Inject this module to use filtering feature.
* `ExcelExportService` - Inject this module to use Excel export feature.
* `PdfExportService` - Inject this module to use PDF export feature.

These modules should be injected into the `providers` section of root `NgModule` or component class.

> Additional feature modules are available [here](./modules)

## Enable Paging

The paging feature enables users to view the TreeGrid record in a paged view. It can be enabled by setting the  [`allowPaging`](../api/treegrid/#allowpaging) property to true. Also, need to inject the `PageService` module in the `providers` section as follows. If the `PageService` module is not injected, the pager will not be rendered in the TreeGrid. The pager can be customized using the [`pageSettings`](../api/treegrid/#pagesettings) property.

In root-level paging mode, paging is based on the root-level rows only i.e., it ignores the child rows count and it can be enabled by using the [`pageSettings.pageSizeMode`](../api/treegrid/pageSettingsModel/#pagesizemode) property.

{% tab template="treegrid/getting-started", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';
import {PageSettingsModel } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' [treeColumnIndex]='1' childMapping='subtasks'
                [allowPaging]="true" [pageSettings]='pageSettings'>
                <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=90></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
                </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public pageSettings: PageSettingsModel;

    ngOnInit(): void {
        this.data = sampleData;
        this.pageSettings = { pageSize: 6 };
    }
}
```

{% endtab %}

## Enable Sorting

The sorting feature enables the user to order the records.
It can be enabled by setting [`allowSorting`](../api/treegrid/#allowsorting) property to true.
Also, need to inject the `SortService` module in the provider section as follow.
If we didn't inject the `SortService` module, then user not able to sort when click on headers.
Sorting feature can be customized using [`sortSettings`](../api/treegrid/#sortsettings) property.

{% tab template="treegrid/getting-started", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';
import { PageSettingsModel, SortSettingsModel } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' [treeColumnIndex]='1' [sortSettings]="sortSettings"
                [allowSorting]="true" childMapping='subtasks' [allowPaging]="true" [pageSettings]='pageSettings'>
                <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=90></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
                </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public sortSettings: SortSettingsModel;
    public pageSettings: PageSettingsModel;

    ngOnInit(): void {
        this.data = sampleData;
        this.sortSettings = { columns: [{ field: 'taskName', direction: 'Ascending' }, { field: 'taskID', direction: 'Descending' }]  };
        this.pageSettings = { pageSize: 6 };
    }
}
```

{% endtab %}

## Enable Filtering

The filtering feature enables you to view the reduced amount of records based on the filter criteria. It can be enabled by setting the [`allowFiltering`](../api/treegrid/#allowfiltering) property to true.  Also, need to inject the `FilterService` module in the provider section as follow. If `FilterService` module is not injected, filter bar will not be rendered in TreeGrid. Filtering feature can be customized using the [`filterSettings`](../api/treegrid/#filtersettings) property.

By default, filtered records are shown along with its parent records. This behavior can be changed by using the [`filterSettings-hierarchyMode`](../api/treegrid/filterSettingsModel/#hierarchymode) property.

{% tab template="treegrid/getting-started", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';
import {PageSettingsModel, SortSettingsModel } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' [treeColumnIndex]='1' [allowFiltering]="true" [sortSettings]="sortSettings"
                [allowSorting]="true" childMapping='subtasks' [allowPaging]="true" [pageSettings]='pageSettings'>
                    <e-columns>
                        <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                        <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                        <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=90></e-column>
                        <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
                    </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public sortSettings: SortSettingsModel;
    public pageSettings: PageSettingsModel;

    ngOnInit(): void {
        this.data = sampleData;
        this.sortSettings = { columns: [{ field: 'taskName', direction: 'Ascending' }, { field: 'taskID', direction: 'Descending' }]  };
        this.pageSettings = { pageSize: 6 };
    }
}
```

{% endtab %}

## Run the application

Use the following command to run the application in browser.

```javascript
ng serve --open
```

The output will appear as follows.

{% tab template="treegrid/getting-started", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' [treeColumnIndex]='1' [sortSettings]="sortSettings"
                [allowFiltering]="true" [allowSorting]="true"
                childMapping='subtasks' [allowPaging]="true" [pageSettings]='pageSettings'>
                    <e-columns>
                        <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                        <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                        <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=90></e-column>
                        <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
                    </e-columns>
               </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public sortSettings: SortSettingsModel;
    public pageSettings: PageSettingsModel;

    ngOnInit(): void {
        this.data = sampleData;
        this.sortSettings = { columns: [{ field: 'taskName', direction: 'Ascending' }, { field: 'taskID', direction: 'Descending' }]  };
        this.pageSettings = { pageSize: 6 };
    }
}

```

{% endtab %}