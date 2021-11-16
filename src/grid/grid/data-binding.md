---
title: "Data Binding"
component: "Grid"
description: "Learn how to bind local and remote data in the Essential JS 2 DataGrid control."
---

# Data Binding

The Grid uses **DataManager** which supports both RESTful JSON data services binding and local JavaScript object array binding.
The [`dataSource`](../api/grid/#datasource) property can be assigned either with the instance of **DataManager** or
JavaScript object array collection.
It supports two kinds of data binding methods:
* Local data
* Remote data

To learn about how to bind local, remote or observables data to Angular Grid, you can check on this video:

`youtube:Xkq1tXOXL7k`

## Local Data

To bind local data to the grid, you can assign a JavaScript object array to the
[`dataSource`](../api/grid/#datasource) property. The local data source can also be provided as an instance of the
**DataManager**.

{% tab template="grid/databinding", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];

    ngOnInit(): void {
        this.data = data.slice(0, 7);
    }
}

```

{% endtab %}

> By default, **DataManager** uses **JsonAdaptor** for local data-binding.

## Remote Data

To bind remote data to grid component, assign service data as an instance of **DataManager** to the
[`dataSource`](../api/grid/#datasource) property.
To interact with remote data source,  provide the endpoint **url**.

{% tab template="grid/databinding", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { DataManager, ODataAdaptor } from '@syncfusion/ej2-data';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: DataManager;

    ngOnInit(): void {
        this.data = new DataManager({
            url: 'https://js.syncfusion.com/demos/ejServices/Wcf/Northwind.svc/Orders?$top=7',
            adaptor: new ODataAdaptor()
        });
    }
}

```

{% endtab %}

> By default, **DataManager** uses **ODataAdaptor** for remote data-binding.

### Binding with OData Services

[`OData`](http://www.odata.org/documentation/odata-version-3-0/) is a standardized protocol for creating and consuming data.
You can retrieve data from OData service using DataManager. You can refer to the following code example of remote data binding using OData service.

{% tab template="grid/databinding", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { DataManager, ODataAdaptor } from '@syncfusion/ej2-data';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: DataManager;

    ngOnInit(): void {
        this.data = new DataManager({
            url: 'https://js.syncfusion.com/demos/ejServices/Wcf/Northwind.svc/Orders?$top=7',
            adaptor: new ODataAdaptor(),
            crossDomain: true
        });
    }
}

```

{% endtab %}

### Binding with OData v4 services

The ODataV4 is an improved version of OData protocols, and the **DataManager** can also retrieve and consume OData v4 services.
For more details on OData v4 services, refer to the
[`odata documentation`](http://docs.oasis-open.org/odata/odata/v4.0/errata03/os/complete/part1-protocol/odata-v4.0-errata03-os-part1-protocol-complete.html#_Toc453752197).
To bind OData v4 service, use the **ODataV4Adaptor**.

{% tab template="grid/databinding", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { DataManager, ODataV4Adaptor } from '@syncfusion/ej2-data';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: DataManager;

    ngOnInit(): void {
        this.data = new DataManager({
            url: 'https://services.odata.org/V4/Northwind/Northwind.svc/Orders/?$top=7',
            adaptor: new ODataV4Adaptor()
        });
    }
}

```

{% endtab %}

### Web API

You can use **WebApiAdaptor** to bind grid with Web API created using OData endpoint.

```typescript
import { Component, OnInit } from '@angular/core';
import { DataManager, WebApiAdaptor } from '@syncfusion/ej2-data';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: DataManager;

    ngOnInit(): void {
        this.data = new DataManager({
            url: 'api/OrderApi',
            adaptor: new WebApiAdaptor()
        });
    }
}

```

The response object should contain properties **Items** and **Count** whose values are a collection of entities and the total count of
the entities respectively.

The sample response object should look like below.

```json
{
    Items: [{..}, {..}, {..}, ...],
    Count: 830
}
```

### Remote Save Adaptor

You may need to perform all Grid Actions in client-side except the CRUD operations, that should be interacted with server-side to persist data. It can be achieved in Grid by using **RemoteSaveAdaptor**.

Datasource must be set to **json** property and set **RemoteSaveAdaptor** to the **adaptor** property. CRUD operations can be mapped to server-side using **updateUrl**, **insertUrl**, **removeUrl**, **batchUrl**, **crudUrl** properties.

You can use the following code example to use **RemoteSaveAdaptor** in Grid.

```typescript
import { Component, OnInit } from '@angular/core';
import { DataManager, RemoteSaveAdaptor } from '@syncfusion/ej2-data';
import { EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='dataSource' [editSettings]='editSettings' [toolbar]='toolbar'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: DataManager;
    public value: any;
    public editSettings: EditSettingsModel;
    public toolbar: ToolbarItems[];

    ngOnInit(): void {
        this.value = (window as any).griddata;
        this.data = new DataManager({
            json: JSON.parse(this.value),
            adaptor: new RemoteSaveAdaptor(),
            insertUrl: '/Home/Insert',
            updateUrl: '/Home/Update',
            removeUrl: '/Home/Delete'
        });
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true };
        this.toolbar = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
    }
}

```

The following code example describes how to fetch the data from **ViewBag** in angular.

```html
    <script type="text/javascript">
       window.griddata = '@Html.Raw(Json.Encode(ViewBag.dataSource))';
    </script>
```

The following code example describes the CRUD operations handled at server-side.

```json
    public ActionResult Index()
    {
        ViewBag.dataSource = OrdersDetails.GetAllRecords().ToArray();
        return View();
    }
    public ActionResult Update(OrdersDetails value)
    {
        ...
        return Json(value);
    }
    public ActionResult Insert(OrdersDetails value)
    {
        ...
        return Json(value);
    }
    public ActionResult Delete(int key)
    {
        ...
        return Json(data);
    }
```

### Custom Adaptor

You can create your own adaptor by extending the built-in adaptors. For the sake of demonstrating custom adaptor approach,
we are going to see how to add a serial number for the records
by overriding the built-in response processing using the **processResponse** method of the **ODataAdaptor**.

{% tab template="grid/databinding", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { DataManager, ODataAdaptor } from '@syncfusion/ej2-data';

class SerialNoAdaptor extends ODataAdaptor {
    processResponse() {
        let i = 0;
        const Sno = 'Sno';
        // calling base class processResponse function
        const original = super.processResponse.apply(this, arguments);
        // Adding serial number
        original.result.forEach((item) => item[Sno] = ++i);
        return { result: original.result, count: original.count };
    }
}

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data'>
                <e-columns>
                    <e-column field='Sno' headerText='SNO' textAlign='Right' width=150></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: DataManager;

    ngOnInit(): void {
        this.data = new DataManager({
            url: 'https://js.syncfusion.com/demos/ejServices/Wcf/Northwind.svc/Orders?$top=7',
            adaptor: new SerialNoAdaptor()
        });
    }
}

```

{% endtab %}

### Offline mode

On remote data binding, all grid actions such as paging, sorting, editing, grouping, filtering, etc, will be processed on server-side.
To avoid post back for every action, set the grid to load all data on initialization and make the actions process in client-side.
To enable this behavior, use the **offline** property of **DataManager**.

```typescript
import { Component, OnInit } from '@angular/core';
import { DataManager, ODataAdaptor } from '@syncfusion/ej2-data';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [allowPaging]='true' [allowGrouping]='true' [allowSorting]='true' [pageSettings]='pageOptions'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: DataManager;
    public pageOptions = { pageSize: 7 };

    ngOnInit(): void {
        this.data = new DataManager({
            url: 'https://js.syncfusion.com/demos/ejServices/Wcf/Northwind.svc/Orders?$top=7',
            adaptor: new ODataAdaptor(),
            offline: true
        });
    }
}

```

### Sending additional parameters

To add a custom parameter to the data request, use the **addParams** method of **Query** class.
Assign the **Query** object with additional parameters to the grid [`query`](../api/grid/#query) property.

```typescript
import { Component, OnInit } from '@angular/core';
import { DataManager, ODataAdaptor, Query } from '@syncfusion/ej2-data';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [query]='query'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: DataManager;
    public query: Query;

    ngOnInit(): void {
        this.data = new DataManager({
            url: 'https://js.syncfusion.com/demos/ejServices/Wcf/Northwind.svc/Orders?$top=7',
            adaptor: new ODataAdaptor()
        });
        this.query = new Query().addParams('ej2grid', 'true');
    }
}

```

> The parameters added using the [`query`](../api/grid/#query) property will be sent along with the data request for every grid action.

### Handle Http Error

During server interaction from the grid, some server-side exceptions may occur, and you can acquire those error messages or exception details
in client-side using the [`actionFailure`](../api/grid/#actionfailure) event.

The argument passed to the [`actionFailure`](../api/grid/#actionfailure) Grid event contains the error details
returned from the server.

```typescript
import { Component, OnInit } from '@angular/core';
import { DataManager } from '@syncfusion/ej2-data';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' (actionFailure)="onActionFailure($event)">
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: DataManager;

    ngOnInit(): void {
        this.data = new DataManager({
            url: 'http://some.com/invalidUrl'
        });
    }

    onActionFailure(e: Error): void {
        alert('Server exception: 404 Not found');
    }
}

```

> The [`actionFailure`](../api/grid/#actionfailure) event will be triggered not only for the server errors, but
also when there is an exception while processing the grid actions.

## Binding with ajax

You can use Grid [`dataSource`](../api/grid/#datasource) property to bind the datasource to Grid from external ajax request. In the below code we have fetched the datasource from the server with the help of ajax request and provided that to [`dataSource`](../api/grid/#datasource) property by using **onSuccess** event of the ajax.

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { GridComponent } from '@syncfusion/ej2-angular-grids';
import { Ajax } from '@syncfusion/ej2-base';

@Component({
  selector: 'app-root',
  template: `<input type="button" id="btn" (click)="click()" value="Click"/>
                <ejs-grid #Grid>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' textAlign='Right' width=120></e-column>
                    <e-column field='EmployeeID' headerText='Employee ID' textAlign='Right' width=120></e-column>
                    <e-column field='ShipCountry' headerText='Ship Country' textAlign='Right' width=120></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {
  public data: object[];
  @ViewChild('Grid') public grid: GridComponent;
  ngOnInit(): void {
  }
  click() {
    const grid = this.grid;  // Grid instance
    const ajax = new Ajax('https://ej2services.syncfusion.com/production/web-services/api/Orders', 'GET');
    ajax.send();
    ajax.onSuccess = (data: string) => {
       grid.dataSource = JSON.parse(data);
    };
  }
}

```

> * If you bind the dataSource from this way, then it acts like a local dataSource. So you cannot perform any server side crud actions.

## See also

* [Binding a firebase data source to Grid using AngularFire2](https://www.syncfusion.com/blogs/post/binding-a-firebase-data-source-to-grid-using-angularfire2.aspx)