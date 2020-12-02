---
title: "Autocomplete Data binding"
component: "AutoComplete"
description: "This section for Syncfusion angular autocomplete component shows how to bind with local data source and how to fetch data from remote data service."
---

# Data binding

The AutoComplete loads the data either from local data sources or remote data services using the [`dataSource`](../api/auto-complete/#datasource)
property. It supports the data type of array or `DataManager`.

The AutoComplete also supports different kind of data services such as OData, OData V4,
Web API and data formats such as XML, JSON, JSONP with the help of DataManager Adaptors.

| Fields | Type | Description |
|------|------|-------------|
| value |  `number or string` | Specifies the hidden data value mapped to each list item that should contain a unique value. |
| groupBy |  `string` | Specifies the category under which the list item has to be grouped. |
| iconCss |  `string` | Specifies the icon class of each list item. |

>While binding complex data to AutoComplete, fields should be mapped correctly. Otherwise, the selected
item remains undefined.

## Bind to local data

Local data can be represented in two ways as described below.

### Array of string

The AutoComplete has support to load array of primitive data such as strings and numbers.

{% tab template="autocomplete/getting-started", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the AutoComplete component
    template: `<ejs-autocomplete id='atcelement' [dataSource]='sportsData' [placeholder]='placeholder'></ejs-autocomplete>`
})
export class AppComponent {
    constructor() {
    }
    // defined the array of data
    public sportsData: string[] = ['Badminton', 'Basketball', 'Cricket', 'Football', 'Golf', 'Gymnastics', 'Hockey', 'Tennis'];
    // set placeholder text to AutoComplete input element
    public placeholder: string = 'Find a game';
}

```

{% endtab %}

### Array of object

The AutoComplete can generate its list items through an array of complex data. For this,
the appropriate columns should be mapped to the [`fields`](../api/auto-complete/#fields)property.

In the following example, `Game` column from complex data have been mapped to the `value` field.

{% tab template="autocomplete/getting-started", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the AutoComplete component
    template: `<ejs-autocomplete id='atcelement' [dataSource]='sportsData' [fields]='fields' [placeholder]='text'></ejs-autocomplete>`
})
export class AppComponent {
    constructor() {
    }
    // defined the array of data
    public sportsData: { [key: string]: Object }[] = [
    { Id: 'Game1', Game: 'Badminton' },
    { Id: 'Game2', Game: 'Basketball' },
    { Id: 'Game3', Game: 'Cricket' },
    { Id: 'Game4', Game: 'Football' },
    { Id: 'Game5', Game: 'Golf' },
    { Id: 'Game6', Game: 'Hockey' },
    { Id: 'Game7', Game: 'Rugby' },
    { Id: 'Game8', Game: 'Snooker' }
    ];
    // maps the appropriate column to fields property
    public fields: Object = { value: 'Game' };
    //set the placeholder to AutoComplete input
    public text: string = "Find a game";
}

```

{% endtab %}

### Array of complex object

The AutoComplete can generate its list items through an array of complex data. For this,
the appropriate columns should be mapped to the [`fields`](../api/auto-complete/#fields)property.

In the following example, `Country.Name` column from complex data have been mapped to the `value` field.

{% tab template="autocomplete/getting-started", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the AutoComplete component
    template: `<ejs-autocomplete id='atcelement' [dataSource]='countriesData' [fields]='fields' [placeholder]='text'></ejs-autocomplete>`
})
export class AppComponent {
    constructor() {
    }
    // defined the array of data
    public countriesData: { [key: string]: Object }[] = [
     { Country: { Name: 'Australia' }, Code: { Id: 'AU' }},
        { Country: { Name: 'Bermuda' },Code: { Id: 'BM' }},
        { Country:{ Name: 'Canada'}, Code:{ Id: 'CA'} },
        { Country:{Name: 'Cameroon'}, Code:{ Id: 'CM'} },
        { Country:{Name: 'Denmark'}, Code:{ Id: 'DK' }},
        { Country:{Name: 'France'}, Code: { Id:'FR'} },
        { Country:{Name: 'Finland'}, Code:  { Id:'FI'} },
        { Country:{Name: 'Germany'}, Code: { Id:'DE'} },
        { Country:{Name: 'Greenland'}, Code:{ Id: 'GL' }},
        { Country:{Name: 'Hong Kong'}, Code: { Id:'HK'} },
        { Country:{Name: 'India'}, Code:{ Id: 'IN'} },
        { Country:{ Name: 'Italy'}, Code: { Id:'IT'} },
        { Country:{ Name: 'Japan'}, Code: { Id: 'JP'} },
        { Country:{Name: 'Mexico'}, Code: { Id: 'MX' }},
        { Country:{Name: 'Norway'}, Code: { Id: 'NO'} },
        { Country:{Name: 'Poland'}, Code: { Id: 'PL' }},
        { Country:{Name: 'Switzerland'}, Code: { Id: 'CH'} },
        { Country:{Name: 'United Kingdom'},Code: { Id: 'GB'} },
        { Country:{Name: 'United States'}, Code: { Id: 'US'} }
    ];
    // maps the appropriate column to fields property
    public fields: Object = { value: 'Country.Name' };
    //set the placeholder to AutoComplete input
    public text: string = "Find a country";
}

```

{% endtab %}

## Bind to remote data

The AutoComplete supports retrieval of data from remote data services with the help of
`DataManager`component. The [`Query`](../api/auto-complete/#query)
property is used to fetch data from the database and bind it to the AutoComplete.

The following sample displays the first 6 contacts from the `Customers` table of the `Northwind` data service.

{% tab template="autocomplete/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component } from '@angular/core';
//import DataManager related classes
import { Query, DataManager, ODataV4Adaptor } from '@syncfusion/ej2-data';

@Component({
    selector: 'app-root',
    // specifies the template string for the AutoComplete component
    template: `<ejs-autocomplete id='atcelement' [dataSource]='data'
    [fields]='fields' [placeholder]='text' [sortOrder]='sorting' [query]='query'></ejs-autocomplete>`
    })
export class AppComponent {
    constructor() {
    }
    //bind the DataManager instance to dataSource property
    public data: DataManager = new DataManager({
            url: 'https://services.odata.org/V4/Northwind/Northwind.svc/Customers',
            adaptor: new ODataV4Adaptor,
            crossDomain: true
        });
    // maps the appropriate column to fields property
    public fields: Object = { value: 'ContactName' };
    //bind the Query instance to query property
    public query: Query = new Query().select(['ContactName']).take(6);
    //set the placeholder to AutoComplete input
    public text: string = "Find a customer";
    //sort the result items
    public sorting: string = 'Ascending';
}

```

{% endtab %}

## Data binding using Async pipe

An `Observable` is used extensively by Angular since it provide significant benefits over techniques for event handling, asynchronous programming, and handling multiple values.

AutoComplete data can be consumed from an `Observable` object by piping it through an `async` pipe. The `async` pipe is used to subscribe the observable object and resolve with the latest value emitted by it.

{% tab template="autocomplete/async-pipe", isDefaultActive = "true", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component } from '@angular/core';
import { Observable } from 'rxjs';
import { map } from 'rxjs/operators';
import { HttpClient } from '@angular/common/http';

@Component({
    selector: 'app-root',
    // specifies the template string for the AutoComplete component with dataSource
    template: ` <ejs-autocomplete  id='customers2' #remote2 [dataSource]='data | async'  [fields]='remoteFields' [placeholder]='remoteWaterMark' ></ejs-autocomplete >`
})
export class AppComponent {
    constructor(private http: HttpClient){
      this.data=this.http.get<{[key: string]:object;}[]>('https://services.odata.org/V4/Northwind/Northwind.svc/Customers').pipe(
      map((results : {[key: string]:any;}) => {
        return results.value;
      })
    );
  }

 public data: Observable<any>;

  // maps the remote data column to fields property
  public remoteFields: Object = { value: 'CustomerID' };

  // set the placeholder to AutoComplete input element
  public remoteWaterMark: string = 'Select a customer';
}

```

{% endtab %}

## See Also

* [How to load data using template](./templates#item-template)
* [How to group the data using header](./grouping/)
* [How to filter the bound data](./filtering/)
