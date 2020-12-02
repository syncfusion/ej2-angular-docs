---
title: "Multiselect Data binding"
component: "MultiSelect"
description: "This section for Syncfusion angular multiselect component shows how to bind with local data source and how to fetch data from remote data service."
---

# Data Binding

The MultiSelect loads the data either from local data sources or
remote data services using the
[dataSource](../api/multi-select/#datasource) property. It supports
the data type of `array` or `DataManager`.

The MultiSelect also supports different kinds of data services such as OData, OData V4,
and Web API, and data formats such as XML, JSON, and JSONP with the help of `DataManager` adaptors.

| Fields | Type | Description |
|------|------|-------------|
| text |  `string` | Specifies the display text of each list item. |
| value |  `number or string` | Specifies the hidden data value mapped to each list item that should contain a unique value. |
| groupBy |  `string` | Specifies the category under which the list item has to be grouped. |
| iconCss |  `string` | Specifies the icon class of each list item. |

> When binding complex data to the MultiSelect, fields should be mapped correctly. Otherwise, the selected item remains undefined.

## Binding local data

Local data can be represented in two ways as described below.

### 1. Array of string

The MultiSelect has support to load array of primitive data such as strings and numbers. Here, both value and text field act the same.

{% tab template="multiselect/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the MultiSelect component with dataSource
    template: `<ejs-multiselect id='multiselectelement' [dataSource]='sportsData' [placeholder]='placeholder'></ejs-multiselect>`
})
export class AppComponent {
    constructor() {
    }
    // defined the array of data
    public sportsData: string[] = ['Badminton', 'Cricket', 'Football', 'Golf', 'Tennis'];
    // set placeholder to MultiSelect input element
    public placeholder: string = 'Select games';
}
```

{% endtab %}

### 2. Array of object

The MultiSelect can generate its list items through an array of complex data. For this,
the appropriate columns should be mapped to the [fields](../api/multi-select/#fields) property.

In the following example, `id` column and `sports` column from complex data have been mapped to the `value` field and `text` field, respectively.

{% tab template="multiselect/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component } from '@angular/core';
@Component({
    selector: 'app-root',
    // specifies the template string for the MultiSelect component
    template: `<ejs-multiselect id='multiselectelement' [dataSource]='sportsData' [fields]='fields'[placeholder]='placeholder'></ejs-multiselect>`
})
export class AppComponent {
    constructor() {
    }
    //set the data to dataSource property
    public sportsData: Object[] =  [
        { id: 'Game1', sports: 'Badminton' },
        { id: 'Game2', sports: 'Basketball' },
        { id: 'Game3', sports: 'Cricket' },
        { id: 'Game4', sports: 'Football' },
        { id: 'Game5', sports: 'Golf' }
    ];
    // maps the appropriate column to fields property
    public fields: Object = { text: 'sports', value: 'id' };
    // set placeholder to MultiSelect input element
    public placeholder: string = 'Select games';
}

```

{% endtab %}

### 2. Array of complex object

The MultiSelect can generate its list items through an array of complex data. For this,
the appropriate columns should be mapped to the [fields](../api/multi-select/#fields) property.

In the following example, `Code.Id` column and `Country.Name` column from complex data have been mapped
to the `value` field and `text` field, respectively.

{% tab template="multiselect/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the MultiSelect component
    template: `<ejs-multiselect id='multiselectelement' [dataSource]='sportsData' [fields]='fields'[placeholder]='placeholder'></ejs-multiselect>`
})
export class AppComponent {
    constructor() {
    }
    //set the data to dataSource property
    public sportsData: Object[] =  [
        { Country: { Name: 'Australia' }, Code: { Id: 'AU' }},
        { Country: { Name: 'Bermuda' },Code: { Id: 'BM' }},
        { Country:{ Name: 'Canada'}, Code:{ Id: 'CA'} },
        { Country:{Name: 'Cameroon'}, Code:{ Id: 'CM'} },
        { Country:{Name: 'Denmark'}, Code:{ Id: 'DK' }},
        { Country:{Name: 'France'}, Code: { Id:'FR'} }
    ];
    // maps the appropriate column to fields property
    public fields: Object = { text: 'Country.Name', value: 'Code.Id' };
    // set placeholder to MultiSelect input element
    public placeholder: string = 'Select a country';
}

```

{% endtab %}

## Binding remote data

The MultiSelect supports retrieval of data from remote data services with the help of
`DataManager` component.
The [Query](../api/multi-select/#query) property is used to fetch
data from the database and bind it to the MultiSelect.

The following sample displays the first 6 contacts from “Customers” table of the `Northwind` Data Service.

{% tab template="multiselect/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component } from '@angular/core';
//import DataManager related classes
import { Query, DataManager, ODataV4Adaptor } from '@syncfusion/ej2-data'

@Component({
    selector: 'app-root',
    // specifies the template string for the MultiSelect component
    template: `<ejs-multiselect id='multiselectelement' [dataSource]='data' [fields]='fields' [placeholder]='placeholder' [query]='query' [sortOrder]='sorting'></ejs-multiselect>`
})
export class AppComponent {
    constructor() {
    }
    //bind the DataManager instance to dataSource property
    public data: DataManager = new DataManager({
            url: 'https://services.odata.org/V4/Northwind/Northwind.svc/',
            adaptor: new ODataV4Adaptor,
            crossDomain: true
    });
    // maps the appropriate column to fields property
    public fields: Object = { text: 'ContactName', value: 'CustomerID' };
    //bind the Query instance to query property
    public query: Query = new Query().from('Customers').select(['ContactName', 'CustomerID']).take(5);
    // set placeholder to MultiSelect input element
    public placeholder: string = 'Select customers';
    //sort the result items
    public sorting: string = 'Ascending';
}

```

{% endtab %}

## Data binding using Async pipe

An `Observable` is used extensively by Angular since it provide significant benefits over techniques for event handling, asynchronous programming, and handling multiple values.

MultiSelect data can be consumed from an `Observable` object by piping it through an `async` pipe. The `async` pipe is used to subscribe the observable object and resolve with the latest value emitted by it.

{% tab template="multiselect/async-pipe", isDefaultActive = "true", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component } from '@angular/core';
import { Observable } from 'rxjs';
import { CategoriesService } from './categories.service';
import { map } from 'rxjs/operators';
import { HttpClient } from '@angular/common/http';

@Component({
    selector: 'app-root',
    // specifies the template string for the Multiselect component with dataSource
    template: `<ejs-multiselect  id='customers2' formControlName="skillname" name="skillname" #remote2 [dataSource]='data | async'  [fields]='remoteFields' [placeholder]='remoteWaterMark' ></ejs-multiselect >`,
    providers: [CategoriesService]
})
export class AppComponent {
    constructor(private http: HttpClient){
      this.data=this.http.get<{[key: string]:object;}[]>('https://services.odata.org/V4/Northwind/Northwind.svc/Customers').pipe(
      map((results : {[key: string]:object;}) => {
        return results.value;
      })
    );
  }

 public data: Observable<any>;

  // maps the remote data column to fields property
  public remoteFields: Object = { value: 'CustomerID' };

  // set the placeholder to Multiselect input element
  public remoteWaterMark: string = 'Select a customer';
}

```

{% endtab %}

## See Also

* [How to load data using template](./templates#item-template)
* [How to group the data using header](./grouping/)
* [How to filter the bound data](./filtering/)