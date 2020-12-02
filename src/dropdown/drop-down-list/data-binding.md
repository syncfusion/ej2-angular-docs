---
title: "Drop-down list Data binding"
component: "DropDownList"
description: "This section for Syncfusion angular drop-down list component shows how to bind with local data source and how to fetch data from remote data service."
---

# Data Binding

The DropDownList loads the data either from local data sources or
remote data services using the
[dataSource](../api/combo-box/#datasource) property. It supports
the data type of `array` or `DataManager`.

The DropDownList also supports different kinds of data services such as OData, OData V4, and Web API,
and data formats such as XML, JSON, and JSONP with the help of `DataManager` adaptors.

| Fields | Type | Description |
|------|------|-------------|
| text |  `string` | Specifies the display text of each list item. |
| value |  `number or string` | Specifies the hidden data value mapped to each list item that should contain a unique value. |
| groupBy |  `string` | Specifies the category under which the list item has to be grouped. |
| iconCss |  `string` | Specifies the icon class of each list item. |

> When binding complex data to the DropDownList, fields should be mapped correctly. Otherwise, the selected item remains undefined.

## Binding local data

Local data can be represented in two ways as described below.

### 1. Array of simple data

The DropDownList has support to load array of primitive data such as strings and numbers. Here, both value and text field act the same.

{% tab template="dropdownlist/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the DropDownList component with change event
    template: `<ejs-dropdownlist id='ddlelement' #samples [dataSource]='data' [placeholder]='placeholder'></ejs-dropdownlist>`
})
export class AppComponent {
    constructor() {
    }
    // defined the array of data
    public data: string[] = ['Badminton', 'Basketball', 'Cricket', 'Golf', 'Hockey', 'Rugby'];
    // set placeholder text to DropDownList input element
    public placeholder: string = 'Select a game';
}
```

{% endtab %}

### 2. Array of JSON data

The DropDownList can generate its list items through an array of complex data. For this,
the appropriate columns should be mapped to the [fields](../api/drop-down-list/#fields)
property.

In the following example, `Id` column and `Game` column from complex data have been mapped to the `value` field and `text` field, respectively.

{% tab template="dropdownlist/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the DropDownList component with change event
    template: `<ejs-dropdownlist id='ddlelement' #samples [dataSource]='data' [fields]='fields' [placeholder]='text'></ejs-dropdownlist>`
})
export class AppComponent {
    constructor() {
    }
    // defined the array of data
    public data: { [key: string]: Object }[] = [ { Id: 'game1', Game: 'Badminton' },
                 { Id: 'game2', Game: 'Football' }, { Id: 'game3', Game: 'Tennis' }];
    // maps the appropriate column to fields property
    public fields: Object = { text: 'Game', value: 'Id' };
    //set the placeholder to DropDownList input
    public text: string = "Select a game";
}
```

{% endtab %}

### 3. Array of Complex data

The DropDownList can generate its list items through an array of complex data. For this,
the appropriate columns should be mapped to the [fields](../api/drop-down-list/#fields)
property.

In the following example, `Code.Id` column and `Country.Name` column from complex data have been mapped
to the `value` field and `text` field, respectively.

{% tab template="dropdownlist/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the DropDownList component with change event
    template: `<ejs-dropdownlist id='ddlelement' #samples [dataSource]='data' [fields]='fields' [placeholder]='text'></ejs-dropdownlist>`
})
export class AppComponent {
    constructor() {
    }
    // defined the array of data
    public data: { [key: string]: Object }[] = [
        { Country: { Name: 'Australia' }, Code: { Id: 'AU' }},
        { Country: { Name: 'Bermuda' },Code: { Id: 'BM' }},
        { Country:{ Name: 'Canada'}, Code:{ Id: 'CA'} },
        { Country:{Name: 'Cameroon'}, Code:{ Id: 'CM'} },
        { Country:{Name: 'Denmark'}, Code:{ Id: 'DK' }},
        { Country:{Name: 'France'}, Code: { Id:'FR'} }
    ];
    // maps the appropriate column to fields property
    public fields: Object = { text: 'Country.Name', value: 'Code.Id' };
    //set the placeholder to DropDownList input
    public text: string = "Select a country";
}
```

{% endtab %}

## Binding remote data

The DropDownList supports retrieval of data from remote data services with the help
of `DataManager` component. The `Query` property is
used to fetch data from the database and bind it to the DropDownList.

The following sample displays the first 6 contacts from “Customers” table of the `Northwind` Data Service.

{% tab template="dropdownlist/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';
import { Query, DataManager, ODataV4Adaptor } from '@syncfusion/ej2-data'

@Component({
    selector: 'app-root',
    // specifies the template string for the DropDownList component with change event
    template: `<ejs-dropdownlist id='ddlelement' #samples [dataSource]='data' [fields]='fields' [placeholder]='text' [query]='query' [sortOrder]='sorting'></ejs-dropdownlist>`
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
    public query: Query = new Query().from('Customers').select(['ContactName', 'CustomerID']).take(6),
    //set the placeholder to DropDownList input
    public text: string = "Select a customer";
    //sort the result items
    public sorting: string = 'Ascending';
}
```

{% endtab %}

## Data binding using Async pipe

An `Observable` is used extensively by Angular since it provide significant benefits over techniques for event handling, asynchronous programming, and handling multiple values.

DropDownList data can be consumed from an `Observable` object by piping it through an `async` pipe. The `async` pipe is used to subscribe the observable object and resolve with the latest value emitted by it.

{% tab template="dropdownlist/async-pipe", isDefaultActive = "true", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { Observable } from 'rxjs';
import { CategoriesService } from './categories.service';
import { map } from 'rxjs/operators';
import { HttpClient } from '@angular/common/http';

@Component({
    selector: 'app-root',
    // specifies the template string for the DropDownList component with dataSource
    template: `<ejs-dropdownlist  id='customers2' formControlName="skillname" name="skillname" #remote2 [dataSource]='data | async'  [fields]='remoteFields' [placeholder]='remoteWaterMark' ></ejs-dropdownlist >`,
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

  // set the placeholder to DropDownList input element
  public remoteWaterMark: string = 'Select a customer';
}

```

{% endtab %}

## See Also

* [How to load data using template](./templates#item-template)
* [How to group the data using header](./grouping/)
* [How to filter the bound data](./filtering/)
* [How to get the count of the data when using remote data](./how-to/remote-data-bind/)
* [How to achieve cascading](./how-to/cascading/)
* [How to add item in between the options](./how-to/add-item/)
* [How to remove an item](./how-to/remove-item/)