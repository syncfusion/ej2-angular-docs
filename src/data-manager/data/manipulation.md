---
title: "Angular DataManager | CRUD Data operations | Syncfusion"
component: "DataManager"
description: "Learn how to create, update, and delete (CRUD) records from the data source by using various methods in the DataManager"
---

# CRUD Data operations

In this section, you will see in detail about how to manipulate data using
[`DataManager`](https://ej2.syncfusion.com/documentation/api/data/dataManager/). The [`DataManager`](https://ej2.syncfusion.com/documentation/api/data/dataManager/) can create, update and
delete records either in local data source or remote data source.

Each data sources uses different way in handling the CRUD operations and hence
[`DataManager`](https://ej2.syncfusion.com/documentation/api/data/dataManager/) uses data adaptors to manipulate data that can be understood by a particular data source.

## Insert

The [`insert`](https://ej2.syncfusion.com/documentation/api/data/dataManager/#insert) method of [`DataManager`](https://ej2.syncfusion.com/documentation/api/data/dataManager/)
is used to add new record to the data source. For remote data source, the new record will be send along with the request to the server.

{% tab template="data/editing", sourceFiles="app/**/*.ts,app/**/*.html" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { DataManager, Query, ReturnOption } from '@syncfusion/ej2-data';
import { data } from './datasource';

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
            .e-form {
                display: block;
                padding-bottom: 10px;
            }
            .e-form input {
                width: 15%;
            }
    `]
})
export class AppComponent implements OnInit {

    public items: object[];
    public edit: { OrderID: string, CustomerID: string, EmployeeID: string };
    public dm: DataManager;
    public text: string;
    public show = true;
    public ngOnInit(): void {
      this.text = 'Insert';
      this.edit = { OrderID: null, CustomerID: null, EmployeeID: null };
      this.dm = new DataManager(data.slice(0, 5));
      this.dm.executeQuery(new Query())
        .then((e: ReturnOption) => this.items = e.result as object[]).catch((e) => true);
    }

    public insert(): void {
        this.dm.insert({
          OrderID: this.edit.OrderID,
          CustomerID: this.edit.CustomerID,
          EmployeeID: this.edit.EmployeeID
        });
        this.dm.executeQuery(new Query())
        .then((e: ReturnOption) => this.items = e.result as object[]).catch((e) => true);
    }
}

```

{% endtab %}

> In remote data sources, when the primary key field is an identity field, then it is advised to
return the created data in the response.

## Update

The [`update`](https://ej2.syncfusion.com/documentation/api/data/dataManager/#update) method of [`DataManager`](https://ej2.syncfusion.com/documentation/api/data/dataManager/)
is used to modify/update a record in the data source. For remote data source, the modified
record will be send along with the request to the server.

{% tab template="data/editing", sourceFiles="app/**/*.ts,app/**/*.html" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { DataManager, Query, ReturnOption } from '@syncfusion/ej2-data';
import { data } from './datasource';

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
            .e-form {
                display: block;
                padding-bottom: 10px;
            }
            .e-form input {
                width: 15%;
            }
    `]
})
export class AppComponent implements OnInit {

    public items: object[];
    public edit: { OrderID: string, CustomerID: string, EmployeeID: string };
    public dm: DataManager;
    public text: string;
    public show = true;
    public ngOnInit(): void {
      this.text = 'Update';
      this.edit = { OrderID: null, CustomerID: null, EmployeeID: null };
      this.dm = new DataManager(data.slice(0, 5));
      this.dm.executeQuery(new Query())
        .then((e: ReturnOption) => this.items = e.result as object[]).catch((e) => true);
    }

    public insert(): void {
        this.dm.update('OrderID', {
          OrderID: this.edit.OrderID,
          CustomerID: this.edit.CustomerID,
          EmployeeID: this.edit.EmployeeID
        });
        this.dm.executeQuery(new Query())
        .then((e: ReturnOption) => this.items = e.result as object[]).catch((e) => true);
    }
}

```

{% endtab %}

> Primary key name is required by the [`update`](https://ej2.syncfusion.com/documentation/api/data/dataManager/#update) method to find the record to be updated.

## Remove

The [`remove`](https://ej2.syncfusion.com/documentation/api/data/dataManager/#remove) method of [`DataManager`](https://ej2.syncfusion.com/documentation/api/data/dataManager/)
is used to remove a record from the data source. For remote data source, the record details
such as primary key and data will be send along with the request to the server.

{% tab template="data/editing", sourceFiles="app/**/*.ts,app/**/*.html" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { DataManager, Query, ReturnOption } from '@syncfusion/ej2-data';
import { data } from './datasource';

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
            .e-form {
                display: block;
                padding-bottom: 10px;
            }
            .e-form input {
                width: 15%;
            }
    `]
})
export class AppComponent implements OnInit {

    public items: object[];
    public edit: { OrderID: string, CustomerID: string, EmployeeID: string };
    public dm: DataManager;
    public text: string;
    public show = false;
    public ngOnInit(): void {
      this.text = 'Remove';
      this.edit = { OrderID: null, CustomerID: null, EmployeeID: null };
      this.dm = new DataManager(data.slice(0, 5));
      this.dm.executeQuery(new Query())
        .then((e: ReturnOption) => this.items = e.result as object[]).catch((e) => true);
    }

    public insert(): void {
        this.dm.remove( 'OrderID', {
          OrderID: this.edit.OrderID
        });
        this.dm.executeQuery(new Query())
        .then((e: ReturnOption) => this.items = e.result as object[]).catch((e) => true);
    }
}

```

{% endtab %}

> Primary key name and its value are required to find the record to be removed.

## Batch Edit Operation

[`DataManager`](https://ej2.syncfusion.com/documentation/api/data/dataManager/) supports batch processing for the CRUD operations. You
can use the [`saveChanges`](https://ej2.syncfusion.com/documentation/api/data/dataManager/#savechanges) method to batch the edit
operation. For remote data source, requests to add, remove and change are handled altogether at
a time rather than passing the request separately for each operation.

{% tab template="data/batchediting", sourceFiles="app/**/*.ts,app/**/*.html" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { DataManager, Query, ReturnOption } from '@syncfusion/ej2-data';
import { data } from './datasource';

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
            .e-form {
                display: block;
                padding-bottom: 10px;
            }
            .e-form input {
                width: 15%;
            }
    `]
})
export class AppComponent implements OnInit {

    public items: object[];
    public edit: { OrderID: string, CustomerID: string, EmployeeID: string };
    public dm: DataManager;
    public changes: { changedRecords: object[], addedRecords: object[], deletedRecords: object[] } =
    { changedRecords: [], addedRecords: [], deletedRecords: [] };
    public text: string;
    public ngOnInit(): void {
      this.text = 'Update';
      this.edit = { OrderID: null, CustomerID: null, EmployeeID: null };
      this.dm = new DataManager(data.slice(0, 5));
      this.dm.executeQuery(new Query())
        .then((e: ReturnOption) => this.items = e.result as object[]).catch((e) => true);
    }

    public save(): void {
        this.dm.saveChanges(this.changes);
        this.dm.executeQuery(new Query())
        .then((e: ReturnOption) => this.items = e.result as object[]).catch((e) => true);
        this.changes = { changedRecords: [], addedRecords: [], deletedRecords: [] };
    }

    public insert(action?: string): void {
        this.changes[action].push({
          OrderID: this.edit.OrderID,
          CustomerID: this.edit.CustomerID,
          EmployeeID: this.edit.EmployeeID
        });
        this.edit = { OrderID: null, CustomerID: null, EmployeeID: null };
    }
}

```

{% endtab %}