---
title: "Angular DataManager | Data Binding | Syncfusion"
component: "DataManager"
description: "Learn how to consume local and remote data sources using the Angular DataManager."
---

# Data Binding

[`DataManager`](https://ej2.syncfusion.com/documentation/api/data/dataManager/) supports both RESTful JSON data services binding and local JavaScript object array binding.

## Local data binding

[`DataManager`](https://ej2.syncfusion.com/documentation/api/data/dataManager/) can be bound to local data source by assigning the
array of JavaScript objects to the **json** property or simply passing them
to the constructor while instantiating. Now the JavaScript object array can be queried and manipulated.

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
        this.items = new DataManager(data as JSON[]).executeLocal(new Query().take(8));
    }
}

```

{% endtab %}

## Remote data binding

[`DataManager`](https://ej2.syncfusion.com/documentation/api/data/dataManager/) can be bound to remote data source by assigning service end point URL to the **url** property. With the
provided **url**, the [`DataManager`](https://ej2.syncfusion.com/documentation/api/data/dataManager/) handles all communication with the
data server with help of queries.

When querying data, the [`DataManager`](https://ej2.syncfusion.com/documentation/api/data/dataManager/) will convert the query object(
[`Query`](https://ej2.syncfusion.com/documentation/api/data/query/)) into server request after calling
[`executeQuery`](https://ej2.syncfusion.com/documentation/api/data/dataManager/#executequery) and waits for the server response(**JSON** format).

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

> The queried data will not be cached locally unless offline mode is enabled.

## See Also

* [Binding with OData service](../data/adaptors/#odata-adaptor)
* [Binding with ODataV4 service](../data/adaptors/#odatav4-adaptor)
* [Binding with Web API](../data/adaptors/#web-api-adaptor)
* [How to write custom adaptor](../data/adaptors/#writing-custom-adaptor)
* [How to work in offline mode](../data/how-to/#work-in-offline-mode)
* [How to send additional parameters](../data/how-to/#sending-additional-parameters-to-server)
* [How to add custom request headers](../data/how-to/#adding-custom-headers)