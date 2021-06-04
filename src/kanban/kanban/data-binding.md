---
title: "Binding data to Kanban"
component: "Kanban"
description: "This section includes the data binding topics explaining how to bind various data sources to Kanban using DataManager adaptors."
---

# Data binding

The Kanban uses `DataManager`, which supports both RESTful data service binding and JavaScript object array binding. The [`dataSource`](../api/kanban#datasource) property of Kanban can be assigned either with the instance of `DataManager` or JavaScript object array collection, as it supports the following two data binding methods:

* Local data
* Remote data

## Local data

To bind local JSON data to the Kanban, you can simply assign a JavaScript object array to the [`dataSource`](../api/kanban#datasource) property. The JSON object dataSource can also be provided as an instance of `DataManager` and assigned to the Kanban `dataSource` property.

{% tab template="kanban/local-data" sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { CardSettingsModel } from '@syncfusion/ej2-angular-kanban';
import { kanbanData } from './datasource';

@Component({
  selector: 'app-root',
  template: `<ejs-kanban keyField='Status' [dataSource]='data' [cardSettings]='cardSettings'>
                <e-columns>
                  <e-column headerText='To do' keyField='Open'></e-column>
                  <e-column headerText='In Progress' keyField='InProgress'></e-column>
                  <e-column headerText='Testing' keyField='Testing'></e-column>
                  <e-column headerText='Done' keyField='Close'></e-column>
                </e-columns>
            </ejs-kanban>`
})
export class AppComponent {
    public data: Object[] = kanbanData;
    public cardSettings: CardSettingsModel = {
        contentField: 'Summary',
        headerField: 'Id'
    };
}

```

{% endtab %}

> By default, `DataManager` uses `JsonAdaptor` for binding local data.

## Remote data

To bind remote data to kanban component, assign service data as an instance of [`DataManager`](../data) to the [`dataSource`](../api/kanban#datasource) property. To interact with remote data source,  provide the endpoint **url**.

{% tab template="kanban/remote-data" sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { CardSettingsModel, DialogEventArgs } from '@syncfusion/ej2-angular-kanban';
import { DataManager, ODataAdaptor } from '@syncfusion/ej2-data';

@Component({
  selector: 'app-root',
  template: `<ejs-kanban keyField='Status' [dataSource]='dataManager' [cardSettings]='cardSettings' [allowDragAndDrop]='false' (dialogOpen)="dialogOpen($event)">
                <e-columns>
                  <e-column headerText='To do' keyField='Open'></e-column>
                  <e-column headerText='In Progress' keyField='InProgress'></e-column>
                  <e-column headerText='Testing' keyField='Testing'></e-column>
                  <e-column headerText='Done' keyField='Close'></e-column>
                </e-columns>
            </ejs-kanban>`
})
export class AppComponent {
    public cardSettings: CardSettingsModel = {
        contentField: 'Summary',
        headerField: 'Id'
    };
    private dataManager: DataManager = new DataManager({
       url: 'https://ej2services.syncfusion.com/production/web-services/api/Kanban',
       adaptor: new ODataAdaptor,
       crossDomain: true
    });
    public dialogOpen(args: DialogEventArgs): void {
      args.cancel = true;
    }
}

```

{% endtab %}

> By default, [`DataManager`](../data) uses **ODataAdaptor** for remote data-binding.

### OData services

[`OData`](http://www.odata.org/documentation/odata-version-3-0/) is a standardized protocol for creating and consuming data. You can retrieve data from OData service using the DataManager. Refer to the following code example for remote Data binding using OData service.

{% tab template="kanban/odata" sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { CardSettingsModel, DialogEventArgs } from '@syncfusion/ej2-angular-kanban';
import { DataManager, ODataAdaptor } from '@syncfusion/ej2-data';

@Component({
  selector: 'app-root',
  template: `<ejs-kanban keyField='Status' [dataSource]='dataManager' [cardSettings]='cardSettings' [allowDragAndDrop]='false' (dialogOpen)="dialogOpen($event)">
                <e-columns>
                  <e-column headerText='To do' keyField='Open'></e-column>
                  <e-column headerText='In Progress' keyField='InProgress'></e-column>
                  <e-column headerText='Testing' keyField='Testing'></e-column>
                  <e-column headerText='Done' keyField='Close'></e-column>
                </e-columns>
            </ejs-kanban>`
})
export class AppComponent {
    public cardSettings: CardSettingsModel = {
        contentField: 'Summary',
        headerField: 'Id'
    };
    private dataManager: DataManager = new DataManager({
       url: 'https://ej2services.syncfusion.com/production/web-services/api/Kanban',
       adaptor: new ODataAdaptor,
       crossDomain: true
    });
    public dialogOpen(args: DialogEventArgs): void {
      args.cancel = true;
    }
}

```

{% endtab %}

### OData v4 services

The ODataV4 is an improved version of OData protocols, and the [`DataManager`](../data) can also retrieve and consume OData v4 services. For more details on OData v4 services, refer to the [`odata documentation`](http://docs.oasis-open.org/odata/odata/v4.0/errata03/os/complete/part1-protocol/odata-v4.0-errata03-os-part1-protocol-complete.html#_Toc453752197). To bind OData v4 service, use the **ODataV4Adaptor**.

{% tab template="kanban/odataV4" sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { CardSettingsModel, DialogEventArgs } from '@syncfusion/ej2-angular-kanban';
import { DataManager, ODataV4Adaptor } from '@syncfusion/ej2-data';

@Component({
  selector: 'app-root',
  template: `<ejs-kanban keyField='ContactTitle' [dataSource]='dataManager' [cardSettings]='cardSettings' [allowDragAndDrop]='false' (dialogOpen)="dialogOpen($event)">
                <e-columns>
                  <e-column headerText='Order Administrator' keyField='Order Administrator'></e-column>
                  <e-column headerText='Sales Representative' keyField='Sales Representative'></e-column>
                  <e-column headerText='Export Administrator' keyField='Export Administrator'></e-column>
                </e-columns>
            </ejs-kanban>`
})
export class AppComponent {
    public cardSettings: CardSettingsModel = {
        contentField: 'ContactName',
        headerField: 'SupplierID'
    };
    private dataManager: DataManager = new DataManager({
       url: 'https://services.odata.org/v4/northwind/northwind.svc/Suppliers',
       adaptor: new ODataV4Adaptor,
    });
    public dialogOpen(args: DialogEventArgs): void {
      args.cancel = true;
    }
}

```

{% endtab %}

### Web API

You can use **WebApiAdaptor** to bind kanban with Web API created using OData endpoint.

```typescript
import { Component } from '@angular/core';
import { CardSettingsModel, DialogEventArgs } from '@syncfusion/ej2-angular-kanban';
import { DataManager, WebApiAdaptor } from '@syncfusion/ej2-data';

@Component({
  selector: 'app-root',
  template: `<ejs-kanban keyField='Status' [dataSource]='dataManager' [cardSettings]='cardSettings' [allowDragAndDrop]='false' (dialogOpen)="dialogOpen($event)">
                <e-columns>
                  <e-column headerText='To do' keyField='Open'></e-column>
                  <e-column headerText='In Progress' keyField='InProgress'></e-column>
                  <e-column headerText='Testing' keyField='Testing'></e-column>
                  <e-column headerText='Done' keyField='Close'></e-column>
                </e-columns>
            </ejs-kanban>`
})
export class AppComponent {
    public cardSettings: CardSettingsModel = {
        contentField: 'Summary',
        headerField: 'Id'
    };
    private dataManager: DataManager = new DataManager({
        url: '/api/Tasks',
        adaptor: new WebApiAdaptor
    });
    public dialogOpen(args: DialogEventArgs): void {
      args.cancel = true;
    }
}

```

Below server-side controller code to get the Kanban data.

```typescript

[HttpGet]
        public object Get()
        {
            var data = OrdersDetails.GetAllRecords().ToList();
            return data;
        }

```

### URL adaptor

The CRUD (Create, Read, Update and Delete) actions can be performed easily on Kanban cards using the various adaptors available within the `DataManager`. Most preferably, we will be using `UrlAdaptor` for performing CRUD actions on Kanban.

The CRUD operation in Kanban can be mapped to server-side controller actions using the properties `insertUrl`, `removeUrl`, `updateUrl`, and `crudUrl`.

* `insertUrl` – You can perform a single insertion operation on the server-side.
* `updateUrl` – You can update single data on the server-side.
* `removeUrl` – You can remove single data on the server-side.
* `crudUrl` – You can perform bulk data operation on the server-side.

```typescript
import { Component } from '@angular/core';
import { CardSettingsModel } from '@syncfusion/ej2-angular-kanban';
import { DataManager, UrlAdaptor } from '@syncfusion/ej2-data';

@Component({
  selector: 'app-root',
  template: `<ejs-kanban keyField='Status' [dataSource]='dataManager' [cardSettings]='cardSettings'>
                <e-columns>
                  <e-column headerText='To do' keyField='Open'></e-column>
                  <e-column headerText='In Progress' keyField='InProgress'></e-column>
                  <e-column headerText='Testing' keyField='Testing'></e-column>
                  <e-column headerText='Done' keyField='Close'></e-column>
                </e-columns>
            </ejs-kanban>`
})
export class AppComponent {
    public cardSettings: CardSettingsModel = {
        contentField: 'Summary',
        headerField: 'Id'
    };
    private dataManager: DataManager = new DataManager({
        url: 'Home/DataSource',
        updateUrl: 'Home/Update',
        insertUrl: 'Home/Insert',
        removeUrl: 'Home/Delete',
        adaptor: new UrlAdaptor(),
        crossDomain: true
    });
}

```

The server-side controller code to handle the CRUD operations are as follows.

```typescript

private NORTHWNDEntities db = new NORTHWNDEntities();
public ActionResult DataSource() {
    var DataSource = db.Tasks.ToList();
    return Json(DataSource, JsonRequestBehavior.AllowGet);
}
public ActionResult Insert(Params value) {
    //Insert card data into the database
    return Json(value, JsonRequestBehavior.AllowGet);
}
public ActionResult Update(Params value) {
    //Update card data into the database
    return Json(value, JsonRequestBehavior.AllowGet);
}
public void Delete(Params value) {
    //Delete card data from the database
}

public class Params {
    public int Id { get; set; }
    public string Status { get; set; }
    public string Summary { get; set; }
    public string Assignee { get; set; }
}

```

### Custom adaptor

It is possible to create your own custom adaptor by extending the built-in available adaptors. The following example demonstrates the custom adaptor usage and how to add a custom field `TaskId` for the cards by overriding the built-in response processing using the `processResponse` method of the `ODataAdaptor`.

{% tab template="kanban/custom" sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { CardSettingsModel, DialogEventArgs } from '@syncfusion/ej2-angular-kanban';
import { DataManager, ODataAdaptor } from '@syncfusion/ej2-data';

class TaskIdAdaptor extends ODataAdaptor {
    processResponse() {
        let i = 0;
        // calling base class processResponse function
        let original = super.processResponse.apply(this, arguments);
        // adding Task Id
        original.forEach((item) => item['Id'] = 'Task - ' + ++i);
        return original;
    }
}

@Component({
  selector: 'app-root',
  template: `<ejs-kanban keyField='Status' [dataSource]='dataManager' [cardSettings]='cardSettings' [allowDragAndDrop]='false' (dialogOpen)="dialogOpen($event)">
                <e-columns>
                  <e-column headerText='To do' keyField='Open'></e-column>
                  <e-column headerText='In Progress' keyField='InProgress'></e-column>
                  <e-column headerText='Testing' keyField='Testing'></e-column>
                  <e-column headerText='Done' keyField='Close'></e-column>
                </e-columns>
            </ejs-kanban>`
})
export class AppComponent {
    public cardSettings: CardSettingsModel = {
        contentField: 'Summary',
        headerField: 'Id'
    };
    private dataManager: DataManager = new DataManager({
       url: 'https://ej2services.syncfusion.com/production/web-services/api/Kanban',
       adaptor: new TaskIdAdaptor
    });
    public dialogOpen(args: DialogEventArgs): void {
      args.cancel = true;
    }
}

```

{% endtab %}

### Sending additional parameters to the server

To add a custom parameter to the data request, use the **addParams** method of **Query** class. Assign the **Query** object with additional parameters to the kanban [`query`](../api/kanban#query) property.

{% tab template="kanban/additional" sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { CardSettingsModel, DialogEventArgs } from '@syncfusion/ej2-angular-kanban';
import { DataManager, ODataAdaptor, Query } from '@syncfusion/ej2-data';

@Component({
  selector: 'app-root',
  template: `<ejs-kanban keyField='Status' [dataSource]='dataManager' [cardSettings]='cardSettings' [allowDragAndDrop]='false' (dialogOpen)="dialogOpen($event)" [query]='query'>
                <e-columns>
                  <e-column headerText='To do' keyField='Open'></e-column>
                  <e-column headerText='In Progress' keyField='InProgress'></e-column>
                  <e-column headerText='Testing' keyField='Testing'></e-column>
                  <e-column headerText='Done' keyField='Close'></e-column>
                </e-columns>
            </ejs-kanban>`
})
export class AppComponent {
    public cardSettings: CardSettingsModel = {
        contentField: 'Summary',
        headerField: 'Id'
    };
    private dataManager: DataManager = new DataManager({
       url: 'https://ej2services.syncfusion.com/production/web-services/api/Kanban',
       adaptor: new ODataAdaptor
    });
    public query: Query = new Query().addParams('ej2kanban', 'true');
    public dialogOpen(args: DialogEventArgs): void {
      args.cancel = true;
    }
}

```

{% endtab %}

> The parameters added using the [`query`](../api/kanban#query) property will be sent along with the data request for every kanban action.

### Handling HTTP error

During server interaction from the kanban, some server-side exceptions may occur, and you can acquire those error messages or exception details
in client-side using the [`actionFailure`](../api/kanban#actionfailure) event.

The argument passed to the [`actionFailure`](../api/kanban#actionfailure) event contains the error details returned from the server.

{% tab template="kanban/error" sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { CardSettingsModel } from '@syncfusion/ej2-angular-kanban';
import { DataManager } from '@syncfusion/ej2-data';

@Component({
  selector: 'app-root',
  template: `<ejs-kanban #Kanban keyField='Status' [dataSource]='dataManager' [cardSettings]='cardSettings'  (actionFailure)="onActionFailure($event)">
                <e-columns>
                  <e-column headerText='To do' keyField='Open'></e-column>
                  <e-column headerText='In Progress' keyField='InProgress'></e-column>
                  <e-column headerText='Testing' keyField='Testing'></e-column>
                  <e-column headerText='Done' keyField='Close'></e-column>
                </e-columns>
            </ejs-kanban>`
})
export class AppComponent {
    @ViewChild('Kanban') public kanban: KanbanComponent;
    public cardSettings: CardSettingsModel = {
        contentField: 'Summary',
        headerField: 'Id'
    };
    private dataManager: DataManager = new DataManager({
       url: 'http://some.com/invalidUrl'
    });
    onActionFailure(e: Error): void {
       let span: HTMLElement = document.createElement('span');
       this.kanban.element.parentNode.insertBefore(span, this.kanban.element);
       span.style.color = '#FF0000'
       span.innerHTML = 'Server exception: 404 Not found';
    }
}

```

{% endtab %}

> The [`actionFailure`](../api/kanban#actionfailure) event will be triggered not only for the server errors, but
also when there is an exception while processing the kanban actions.

## Loading data via ajax

You can use Kanban [`dataSource`](../api/kanban#datasource) property to bind the datasource to Kanban from external ajax request. In the following code, we have fetched the datasource from the server using ajax request and provided that to the [`dataSource`](../api/kanban#datasource) property by using the **onSuccess** event of ajax.

{% tab template="kanban/ajax" sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { KanbanComponent, CardSettingsModel, DialogEventArgs } from '@syncfusion/ej2-angular-kanban';
import { Ajax } from '@syncfusion/ej2-base';

@Component({
  selector: 'app-root',
  template: `<input type="button" id="btn" (click)="click()" value="Click"/>
  <ejs-kanban #Kanban keyField='ShipCountry' [dataSource]='dataManager' [cardSettings]='cardSettings'  (actionFailure)="onActionFailure($event)">
                <e-columns>
                  <e-column headerText='Denmark' keyField='Denmark'></e-column>
                  <e-column headerText='Brazil' keyField='Brazil'></e-column>
                  <e-column headerText='Switzerland' keyField='Switzerland'></e-column>
                  <e-column headerText='Germany' keyField='Germany'></e-column>
                </e-columns>
            </ejs-kanban>`
})
export class AppComponent {
    @ViewChild('Kanban') public kanban: KanbanComponent;
    public cardSettings: CardSettingsModel = {
        contentField: 'ShippedDate',
        headerField: 'OrderID'
    };
    click() {
        const kanban = this.kanban;  // Grid instance
        const ajax = new Ajax("https://ej2services.syncfusion.com/production/web-services/api/Orders", "GET");
        ajax.send();
        ajax.onSuccess = (data: string) => {
            kanban.dataSource = JSON.parse(data);
        };
    }
}

```

{% endtab %}

> * If you bind the dataSource from this way, then it acts like a local dataSource. So you cannot perform any server-side crud actions.
