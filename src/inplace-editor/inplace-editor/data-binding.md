---
title: "Data Binding"
component: "In-place Editor"
description: "Learn how to bind local and remote data for dependent components of the Essential JS 2 In-place Editor component."
---

# Data Binding

The Essential JS 2 components load the data either from local data sources or remote data services using the `dataSource` property and it supports the data type of an array or `DataManager`. Also supports different kind of data services such as OData, OData V4, Web API, and data formats such as XML, JSON, JSONP with the help of `DataManager` adaptors.

## Local Data Binding

To bind local data to the Essential JS 2 components, you can assign a JavaScript array of object or string to the `dataSource` property. The local data source can also be provided as an instance of the `DataManager`.

{% tab template="in-place-editor/data", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
    <div id='container'>
        <span class="content-title"> Select customer name: </span>
        <ejs-inplaceeditor id="element" mode="Inline" type="DropDownList" value="Maria Anders" [model]="model"></ejs-inplaceeditor>
    </div>
    `
})

export class AppComponent {
  public gameList: Object[] = [
    { Id: '1', Name: 'Maria Anders' },
    { Id: '2', Name: 'Ana Trujillo' },
    { Id: '3', Name: 'Antonio Moreno' },
    { Id: '4', Name: 'Thomas Hardy' },
    { Id: '5', Name: 'Chiristina Berglund' },
    { Id: '6', Name: 'Hanna Moos' }
   ];
  public fields: object = { text: 'Name' };
  public model: object = { dataSource: this.gameList, fields: this.fields, placeholder: 'Select a customer'};
}
```

{% endtab %}

## Remote Data Binding

To bind remote data to the Essential JS 2 component, assign service data as an instance of `DataManager` to the `dataSource` property. To interact with remote data source, provide the endpoint URL.

### OData V4

The OData V4 is an improved version of OData protocols, and the [DataManager](../data/getting-started/) can also retrieve and consume OData V4 services. To fetch data from the server by using `DataManager` with the adaptor property configure as [ODataV4Adaptor](../data/adaptors/#odatav4-adaptor).

In the following sample, **In-place Editor** renders a `DropDownList` component and its `dataSource` property configured for fetching a data from the server by using `ODataV4Adaptor` with `DataManager`.

{% tab template="in-place-editor/data", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript
import { Component } from '@angular/core';
import { DataManager, ODataV4Adaptor, Query } from '@syncfusion/ej2-data';

@Component({
    selector: 'app-root',
    template: `
    <div id='container'>
            <span class="content-title"> Select customer name: </span>
            <ejs-inplaceeditor id="element" mode="Inline" type="DropDownList" value="Maria Anders" [model]="model"></ejs-inplaceeditor>
    </div>
    `
})

export class AppComponent {
    public fields: object = { text: 'ContactName', value: 'CustomerID' };
    public dataSource: DataManager = new DataManager({
            url: 'https://services.odata.org/V4/Northwind/Northwind.svc/',
            adaptor: new ODataV4Adaptor,
            crossDomain: true
        });
    public query: Query = new Query().from('Customers').select(['ContactName', 'CustomerID']).take(6);
    public model: object = { dataSource: this.dataSource, placeholder: 'Select a customer', query: this.query, fields: this.fields };
}
```

{% endtab %}

### Web API

Data can fetch from the server by using [DataManager](../data/getting-started/) with the adaptor property configure as [WebApiAdaptor](../data/adaptors/#web-api-adaptor).

In the following sample, **In-place Editor** render a `DropDownList` component and its `dataSource` property configured for fetching a data from the server by using `WebApiAdaptor` with `DataManager`.

{% tab template="in-place-editor/data", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { InPlaceEditorComponent } from '@syncfusion/ej2-angular-inplace-editor';
import { DataManager, WebApiAdaptor, Query } from '@syncfusion/ej2-data';

@Component({
    selector: 'app-root',
    template: `
    <div id='container'>
        <span class="content-title"> Select customer name: </span>
        <ejs-inplaceeditor id="element" mode="Inline" type="DropDownList" value="Maria Anders" [model]="model"></ejs-inplaceeditor>
    </div>
    `
})

export class AppComponent implements OnInit {
    public fields: object = { text: 'ContactName', value: 'CustomerID' };
    public model: object;
    ngOnInit(): void {
        new DataManager({
            url: 'https://js.syncfusion.com/demos/ejServices/Wcf/Northwind.svc/Customers/',
            adaptor: new WebApiAdaptor
        }).executeQuery(new Query().take(8)).then((e) => {
        this.model = { dataSource: e.result.d,  placeholder: 'Select a customer', fields: this.fields };
        });
    }
}
```

{% endtab %}