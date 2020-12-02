---
title: "Getting Started"
component: "Grid"
description: "Learn how to create an Essential JS 2 DataGrid control and enable features like paging, filtering, sorting, and grouping."
---

# Getting started

This section explains you the steps required to create a simple Grid and demonstrate the basic usage of the Grid component in an Angular environment.

To get start quickly with Angular Grid using CLI and Schematics, you can check on this video:

`youtube:lk83TlHQ95c`

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

## Adding Syncfusion Grid package

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) registry.

To install Grid component, use the following command.

```bash
npm install @syncfusion/ej2-angular-grids --save
```

> The **--save** will instruct NPM to include the grid package inside of the **dependencies** section of the **package.json**.

## Registering Grid Module

Import Grid module into Angular application(app.module.ts) from the package **@syncfusion/ej2-angular-grids** [src/app/app.module.ts].

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the GridModule for the Grid component
import { GridModule } from '@syncfusion/ej2-angular-grids';
import { AppComponent }  from './app.component';

@NgModule({
  //declaration of ej2-angular-grids module into NgModule
  imports:      [ BrowserModule, GridModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Adding CSS reference

The following CSS files are available in **../node_modules/@syncfusion** package folder.
This can be referenced in [src/styles.css] using following code.

```css
@import '../node_modules/@syncfusion/ej2-base/styles/material.css';  
@import '../node_modules/@syncfusion/ej2-buttons/styles/material.css';  
@import '../node_modules/@syncfusion/ej2-calendars/styles/material.css';  
@import '../node_modules/@syncfusion/ej2-dropdowns/styles/material.css';  
@import '../node_modules/@syncfusion/ej2-inputs/styles/material.css';  
@import '../node_modules/@syncfusion/ej2-navigations/styles/material.css';
@import '../node_modules/@syncfusion/ej2-popups/styles/material.css';
@import '../node_modules/@syncfusion/ej2-splitbuttons/styles/material.css';  
@import '../node_modules/@syncfusion/ej2-angular-grids/styles/material.css';
```

## Add Grid component

Modify the template in [src/app/app.component.ts] file to render the grid component.
Add the Angular Grid by using `<ejs-grid>` selector in **template** section of the app.component.ts file.

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-root',
  // specifies the template string for the Grid component
  template: `<ejs-grid> </ejs-grid>`
})
export class AppComponent implements OnInit {

    ngOnInit(): void {
    }
}

```

## Defining Row Data

Bind data for the Grid component by using [`dataSource`](../api/grid/#datasource) property.
It accepts either array of JavaScript object or [`DataManager`](./data-binding) instance.

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data'> </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];

    ngOnInit(): void {
        this.data = data;
    }
}
```

## Defining Columns

The Grid has an option to define columns as directives. In these column directives, we have properties to customize columns.
Let’s check the properties used here:

* We have added [`field`](../api/grid/column/#field) to map with a property name an array of JavaScript objects.
* We have added [`headerText`](../api/grid/column/#headertext) to change the title of columns.
* We have used [`textAlign`](../api/grid/column/#textalign) to change the alignment of columns.
By default, columns will be left aligned. To change columns to right align, we need to define [`textAlign`](../api/grid/column/#textalign) as **Right**.
* Also, we have used another useful property, [`format`](./columns#format).
Using this, we can format number and date values to standard or custom formats.
Here, we have defined it for the conversion of numeric values to currency.

{% tab template="grid/paging", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=90></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                    <e-column field='Freight' headerText='Freight' textAlign='Right' format='C2' width=90></e-column>
                    <e-column field='OrderDate' headerText='Order Date' textAlign='Right' format='yMd' width=120></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];

    ngOnInit(): void {
        this.data = data;
    }
}
```

{% endtab %}

## Module Injection

To create grid with additional features, inject the required modules. The following modules are used to extend grid's basic functionality.

* **PageService** - Inject this provider to use paging feature.
* **SortService** - Inject this provider to use sorting feature.
* **FilterService** - Inject this provider to use filtering feature.
* **GroupService** - Inject this provider to use grouping feature.

These modules should be injected into the **providers** section of root **NgModule** or component class.

> Additional feature modules are available [`here`](./module).

## Enable Paging

The paging feature enables users to view the Grid record in a paged view.
It can be enabled by setting [`allowPaging`](../api/grid/#allowpaging) property to true.
Also, need to inject the **PageService** module in the provider section as follows.
If we didn't inject the **PageService** module, then the pager will not be rendered in Grid.
The pager can be customized using [`pageSettings`](../api/grid/#pagesettings) property.

{% tab template="grid/paging", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { PageSettingsModel } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [allowPaging]="true" [pageSettings]='pageSettings'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=90></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                    <e-column field='Freight' headerText='Freight' textAlign='Right' format='C2' width=90></e-column>
                    <e-column field='OrderDate' headerText='Order Date' textAlign='Right' format='yMd' width=120></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public pageSettings: PageSettingsModel;

    ngOnInit(): void {
        this.data = data;
        this.pageSettings = { pageSize: 6 };
    }
}

```

{% endtab %}

## Enable Sorting

The sorting feature enables the user to order the records.
It can be enabled by setting [`allowSorting`](../api/grid/#allowsorting) property as true.
Also, need to inject the **SortService** module in the provider section as follow.
If we didn't inject the **SortService** module, then user not able to sort when click on headers.
Sorting feature can be customized using [`sortSettings`](../api/grid/#sortsettings) property.

{% tab template="grid/sorting", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { PageSettingsModel } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [allowPaging]="true" [allowSorting]="true" [pageSettings]="pageSettings">
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=90></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                    <e-column field='Freight' headerText='Freight' textAlign='Right' format='C2' width=90></e-column>
                    <e-column field='OrderDate' headerText='Order Date' textAlign='Right' format='yMd' width=120></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public pageSettings: PageSettingsModel;

    ngOnInit(): void {
        this.data = data;
        this.pageSettings = { pageSize: 6 };
    }
}

```

{% endtab %}

## Enable Filtering

The filtering feature enables the user to view the reduced amount of records based on filter criteria.
It can be enabled by setting [`allowFiltering`](../api/grid/#allowfiltering) property as true.
Also, need to inject the **FilterService** module in the provider section as follow.
If we didn't inject the **FilterService** module, then filter bar will not be rendered in Grid.
Filtering feature can be customized using [`filterSettings`](../api/grid/#filtersettings) property.

{% tab template="grid/filtering", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import {PageSettingsModel } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [allowPaging]="true" [allowSorting]="true"
                [allowFiltering]="true" [pageSettings]="pageSettings">
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=90></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                    <e-column field='Freight' headerText='Freight' textAlign='Right' format='C2' width=90></e-column>
                    <e-column field='OrderDate' headerText='Order Date' textAlign='Right' format='yMd' width=120></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public pageSettings: PageSettingsModel;

    ngOnInit(): void {
        this.data = data;
        this.pageSettings = { pageSize: 6 };
    }
}

```

{% endtab %}

## Enable Grouping

The grouping feature enables users to view the Grid record in a grouped view.
It can be enabled by setting [`allowGrouping`](../api/grid/#allowgrouping) property to true.
Also, need to inject the **GroupService** module in the provider section as follow.
If we didn't inject the **GroupService** module, then the group drop area will not be rendered in Grid.
Grouping feature can be customized using [`groupSettings`](../api/grid/#groupsettings) property.

{% tab template="grid/grouping", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { PageSettingsModel } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [allowPaging]="true" [allowSorting]="true"
               [allowFiltering]="true" [allowGrouping]="true" [pageSettings]='pageSettings'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=90></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                    <e-column field='Freight' headerText='Freight' textAlign='Right' format='C2' width=90></e-column>
                    <e-column field='OrderDate' headerText='Order Date' textAlign='Right' format='yMd' width=120></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public pageSettings: PageSettingsModel;

    ngOnInit(): void {
        this.data = data;
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

{% tab template="grid/grouping", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { PageSettingsModel } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [allowPaging]="true" [allowSorting]="true"
               [allowFiltering]="true" [allowGrouping]="true" [pageSettings]='pageSettings'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=90></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                    <e-column field='Freight' headerText='Freight' textAlign='Right' format='C2' width=90></e-column>
                    <e-column field='OrderDate' headerText='Order Date' textAlign='Right' format='yMd' width=120></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public pageSettings: PageSettingsModel;

    ngOnInit(): void {
        this.data = data;
        this.pageSettings = { pageSize: 6 };
    }
}

```

{% endtab %}
