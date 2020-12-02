---
title: "ListBox data binding and initialization through HTML tags"
component: "ListBox"
description: "Angular ListBox supports databinding with local and remote data source."
---

# Data Binding

The ListBox loads the data either from local data sources or remote data services using the [`dataSource`](../api/list-box/#datasource) property. It supports
the data type of `array` or `DataManager`.

| Fields | Type | Description |
|------|------|-------------|
| [`text`](../api/list-box/fieldSettingsModel/#text) |  `string` | Specifies the display text of each list item. |
| [`value`](../api/list-box/fieldSettingsModel/#value) |  `string` | Specifies the hidden data value mapped to each list item that should contain a unique value. |
| [`groupBy`](../api/list-box/fieldSettingsModel/#groupby) |  `string` | Specifies the category under which the list item has to be grouped. |
| [`iconCss`](../api/list-box/fieldSettingsModel/#iconcss) |  `string` | Specifies the iconCss class that needs to be mapped. |
| [`htmlAttributes`](../api/list-box/fieldSettingsModel/#htmlattributes) |  `string` | Allows additional attributes to configure the elements in various ways to meet the criteria. |

> When binding complex data to the ListBox, fields should be mapped correctly. Otherwise, the selected item remains undefined.

## Local Data

Local data can be represented by the following ways as described below.

### Array of string

The ListBox has support to load array of primitive data such as strings or numbers. Here, both value and text field acts as same.

{% tab template="listbox/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-listbox [dataSource]="data"></ejs-listbox>`
})

export class AppComponent {
public data: string[] = ['Badminton', 'Cricket', 'Football', 'Golf', 'Tennis', 'Basket Ball', 'Base Ball', 'Hockey', 'Volley Ball'];
}

```

{% endtab %}

### Array of object

The ListBox can generate its list items through an array of object data. For this,
the appropriate columns should be mapped to the [`fields`](../api/list-box/#fields) property.

In the following example, `id` and `sports` column from complex data have been mapped to the `value` field and `text` field, respectively.

{% tab template="listbox/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-listbox [dataSource]="data" [fields]="setfield"></ejs-listbox>`
})

export class AppComponent {
public data: { [key: string]: Object }[] = [
    { id: 'game1', sports: 'Badminton' },
    { id: 'game2', sports: 'Cricket'},
    { id: 'game3', sports: 'Football'},
    { id: 'game4', sports: 'Golf'},
    { id: 'game5', sports: 'Tennis'},
    { id: 'game6', sports: 'Basket Ball'},
    { id: 'game7', sports: 'Base Ball'},
    { id: 'game8', sports: 'Hockey'},
    { id: 'game9', sports: 'Volley Ball'}
];

public setfield = {
    text: "sports",
    value: "id"
 }
}
```

{% endtab %}

### Array of complex object

The ListBox can generate its list items through an array of complex data. For this,
the appropriate columns should be mapped to the [`fields`](../api/list-box/#fields) property.

In the following example, `Sports.Name` column from complex data have been mapped to the `text` field.

{% tab template="listbox/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-listbox [dataSource]="data" [fields]="setfield"></ejs-listbox>`
})

export class AppComponent {
public data: { [key: string]: Object }[] = [
    { Id: 'game1', Sports: { Name: 'Badminton'} },
    { Id: 'game2', Sports: { Name: 'Cricket'} },
    { Id: 'game3', Sports: { Name: 'Football'} },
    { Id: 'game4', Sports: { Name: 'Golf'} },
    { Id: 'game5', Sports: { Name: 'Tennis'} },
    { Id: 'game6', Sports: { Name: 'Basket Ball'} },
    { Id: 'game7', Sports: { Name: 'Base Ball'} },
    { Id: 'game8', Sports: { Name: 'Hockey'} },
    { Id: 'game9', Sports: { Name: 'Volley Ball'} }
];

public setfield = { text: "Sports.Name" }
}
```

{% endtab %}

## Remote Data

The ListBox supports retrieval of data from remote data services with the help of [`DataManager`](https://ej2.syncfusion.com/documentation/data/getting-started/) component. The [`Query`](../api/list-box/#query) property is used to fetch
data from the database and bind it to the ListBox.

The following sample displays the first 10 products from `Products` table of the `Northwind` Data Service.

{% tab template="listbox/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { DataManager,ODataV4Adaptor,Query } from '@syncfusion/ej2-data';

@Component({
    selector: 'app-container',
    template: `<ejs-listbox [dataSource]="data" [fields]="setfield" [query]="query"></ejs-listbox>`
})

export class AppComponent {
    public data:DataManager = new DataManager({
          url: 'https://services.odata.org/V4/Northwind/Northwind.svc/',
           adaptor: new ODataV4Adaptor,
    })
    public query = new Query().from('Products').select('ProductID,ProductName').take(10);

    public setfield = { text: "ProductName" }
}
```

{% endtab %}