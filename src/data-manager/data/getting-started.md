---
title: "Angular DataManager | Getting started | Syncfusion"
component: "DataManager"
description: "Learn how to connect the Angular DataManager to a data source and perform queries against it. Also learn how to use DataManager with the Angular Data Grid Component"
---

# Getting started

## Dependencies

Below is the list of minimum dependencies required to use the DataManager.

```javascript
|-- @syncfusion/ej2-data
    |-- @syncfusion/ej2-base
    |-- es6-promise (Required when window.Promise is not available)
```

> **@syncfusion/ej2-data** requires the presence of a Promise feature in global environment. In the browser, window.Promise must be available.

## Setup Angular Environment

You can use [`Angular CLI`](https://github.com/angular/angular-cli) to setup your Angular applications.
To install Angular CLI use the following command.

```bash
npm install -g @angular/cli
```

## Create an Angular Application

Start a new Angular application using below Angular CLI command.

```bash
ng new data-app
cd data-app
```

* Install Syncfusion packages using below command.

```sh
npm install @syncfusion/ej2-data --save
```

The above package installs [`dependencies`](#dependencies) which are required to render the component in Angular environment.

## Connection to a data source

The DataManager can act as gateway for both local and remote data source which will uses the query to interact with the data source.

### Binding to JSON data

**DataManager** can be bound to local data source by assigning the array of JavaScript objects to the **json** property or simply passing them
to the constructor while instantiating.

{% tab template="data/getting-started/default", sourceFiles="app/**/*.ts,app/**/*.html" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { DataManager, Query } from '@syncfusion/ej2-data';
@Component({
    selector: 'app-root',
    templateUrl: 'app.template.html',
    styles: [`
            .e-table {
                border: solid 1px #e0e0e0;
                border-collapse: collapse;
                font-family: Roboto;
            }

            .e-table td, .e-table th {
                border-style: solid;
                border-width: 1px 0 0;
                border-color: #e0e0e0;
                display: table-cell;
                font-size: 14px;
                line-height: 20px;
                overflow: hidden;
                padding: 8px 21px;
                vertical-align: middle;
                white-space: nowrap;
                width: auto;
            }
    `]
})
export class AppComponent implements OnInit {

    public items: object[];

    public ngOnInit(): void {
        this.items = new DataManager(data as JSON[]).executeLocal(new Query().take(6));
    }
}

```

{% endtab %}

### Binding to OData

**DataManager** can be bound to remote data source by assigning service end point URL to the **url** property.
Now all **DataManager** operations will address the provided service end point.

{% tab template="data/getting-started/default", sourceFiles="app/**/*.ts,app/**/*.html" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { DataManager, Query, ReturnOption } from '@syncfusion/ej2-data';

const SERVICE_URI = 'https://js.syncfusion.com/demos/ejServices/Wcf/Northwind.svc/Orders';

@Component({
    selector: 'app-root',
    templateUrl: 'app.template.html',
    styles: [`
            .e-table {
                border: solid 1px #e0e0e0;
                border-collapse: collapse;
                font-family: Roboto;
            }

            .e-table td, .e-table th {
                border-style: solid;
                border-width: 1px 0 0;
                border-color: #e0e0e0;
                display: table-cell;
                font-size: 14px;
                line-height: 20px;
                overflow: hidden;
                padding: 8px 21px;
                vertical-align: middle;
                white-space: nowrap;
                width: auto;
            }
    `]
})
export class AppComponent implements OnInit {

    public items: object[];

    public ngOnInit(): void {
        new DataManager({ url: SERVICE_URI }).executeQuery(new Query().take(6)).then((e: ReturnOption) => {
            this.items = e.result as object[];
        }).catch((e) => true);
    }
}

```

{% endtab %}

## Filter

The data filtering is a trivial operation which will let us to get reduced view of data based on filter criteria.
The filter expression can be built easily using **where** method of **Query** class.

{% tab template="data/getting-started/default", sourceFiles="app/**/*.ts,app/**/*.html" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { DataManager, Query } from '@syncfusion/ej2-data';
@Component({
    selector: 'app-root',
    templateUrl: 'app.template.html',
    styles: [`
            .e-table {
                border: solid 1px #e0e0e0;
                border-collapse: collapse;
                font-family: Roboto;
            }

            .e-table td, .e-table th {
                border-style: solid;
                border-width: 1px 0 0;
                border-color: #e0e0e0;
                display: table-cell;
                font-size: 14px;
                line-height: 20px;
                overflow: hidden;
                padding: 8px 21px;
                vertical-align: middle;
                white-space: nowrap;
                width: auto;
            }
    `]
})
export class AppComponent implements OnInit {

    public items: object[];

    public ngOnInit(): void {
        this.items = new DataManager(data as JSON[]).executeLocal(new Query().where('EmployeeID', 'equal', 3));
    }
}

```

{% endtab %}

## Sort

The data can be ordered either in ascending or descending using **sortBy** method of **Query** class.

{% tab template="data/getting-started/default", sourceFiles="app/**/*.ts,app/**/*.html" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { DataManager, Query } from '@syncfusion/ej2-data';
@Component({
    selector: 'app-root',
    templateUrl: 'app.template.html',
    styles: [`
            .e-table {
                border: solid 1px #e0e0e0;
                border-collapse: collapse;
                font-family: Roboto;
            }

            .e-table td, .e-table th {
                border-style: solid;
                border-width: 1px 0 0;
                border-color: #e0e0e0;
                display: table-cell;
                font-size: 14px;
                line-height: 20px;
                overflow: hidden;
                padding: 8px 21px;
                vertical-align: middle;
                white-space: nowrap;
                width: auto;
            }
    `]
})
export class AppComponent implements OnInit {

    public items: object[];

    public ngOnInit(): void {
        this.items = new DataManager(data as JSON[]).executeLocal(new Query().sortBy('CustomerID').take(8));
    }

}

```

{% endtab %}

## Page

The **page** method of the Query class is used to get range of data based on the page number and the total page size.

{% tab template="data/getting-started/default", sourceFiles="app/**/*.ts,app/**/*.html" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { DataManager, Query } from '@syncfusion/ej2-data';
@Component({
    selector: 'app-root',
    templateUrl: 'app.template.html',
    styles: [`
            .e-table {
                border: solid 1px #e0e0e0;
                border-collapse: collapse;
                font-family: Roboto;
            }

            .e-table td, .e-table th {
                border-style: solid;
                border-width: 1px 0 0;
                border-color: #e0e0e0;
                display: table-cell;
                font-size: 14px;
                line-height: 20px;
                overflow: hidden;
                padding: 8px 21px;
                vertical-align: middle;
                white-space: nowrap;
                width: auto;
            }
    `]
})
export class AppComponent implements OnInit {

    public items: object[];

    public ngOnInit(): void {
        this.items = new DataManager(data as JSON[]).executeLocal(new Query().page(1, 8));
    }
}

```

{% endtab %}

## Component binding

DataManager component can be used with Syncfusion components which supports data binding.

### Local data binding

A DataSource can be created in-line with other Syncfusion component configuration settings.

{% tab template="data/getting-started/component-local", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { DataManager } from '@syncfusion/ej2-data';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' height="315px">
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=90></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                    <e-column field='Freight' headerText='Freight' textAlign='Right' format='C2' width=90></e-column>
                    <e-column field='OrderDate' headerText='Order Date' textAlign='Right' format='yMd' width=120></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: DataManager;

    public ngOnInit(): void {
        this.data = new DataManager(data as JSON[]);
    }
}

```

{% endtab %}

### Remote data binding

To bind remote data to Syncfusion component, you can assign a service data as an instance of **DataManager** to the [`dataSource`](../api/grid/#datasource) property.

{% tab template="data/getting-started/component-local", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { DataManager } from '@syncfusion/ej2-data';

const SERVICE_URI = 'https://js.syncfusion.com/demos/ejServices/Wcf/Northwind.svc/Orders/?$top=20';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' height="315px">
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=90></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                    <e-column field='EmployeeID' headerText='EmployeeID' textAlign='Right' width=90></e-column>
                    <e-column field='ShipName' headerText='Ship Name' textAlign='Left' width=120></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: DataManager;

    public ngOnInit(): void {
        this.data = new DataManager({ url: SERVICE_URI });
    }
}

```

{% endtab %}
