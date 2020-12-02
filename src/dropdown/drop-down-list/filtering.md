---
title: "Drop-down list Filtering"
component: "DropDownList"
description: "This section explains the built-in filtering support with a rich set of filtering configurations in Syncfusion angular drop-down list component."
---

# Filtering

The DropDownList has built-in support to filter data items when `allowFiltering` is enabled. The filter
operation starts as soon as you start typing characters in the search box.

To display filtered items in the popup, filter the required data and return it to the DropDownList
via [updateData](/api/drop-down-list/filteringEventArgs/#updatedata) method by using
the [filtering](../../api/drop-down-list#filtering) event.

The following sample illustrates how to query the data source and pass the data to the DropDownList
through the `updateData` method in `filtering` event.

{% tab template="dropdownlist/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';
import { FilteringEventArgs } from '@syncfusion/ej2-dropdowns';
import { EmitType } from '@syncfusion/ej2-base';
import { Query } from '@syncfusion/ej2-data';

@Component({
    selector: 'app-root',
    // specifies the template string for the DropDownList component with change event
    template: `<ejs-dropdownlist id='ddlelement' #samples [dataSource]='data' [fields]='fields' [placeholder]='text' [allowFiltering]='true' (filtering)='onFiltering($event)'></ejs-dropdownlist>`
})
export class AppComponent {
    constructor() {
    }
    // defined the array of data
    public data: { [key: string]: Object }[] = [
        { Id: "s3", Country: "Alaska" },
        { Id: "s1", Country: "California" },
        { Id: "s2", Country: "Florida" },
        { Id: "s4", Country: "Georgia" }];
    // maps the appropriate column to fields property
    public fields: Object = { text: "Country", value: "Id" };
    // set the placeholder to the DropDownList input
    public text: string = "Select a country";
    //Bind the filter event
    public onFiltering: EmitType =  (e: FilteringEventArgs) => {
        let query = new Query();
        //frame the query based on search string with filter type.
        query = (e.text != "") ? query.where("Country", "startswith", e.text, true) : query;
        //pass the filter data source, filter query to updateData method.
        e.updateData(this.data, query);
    };
}
```

{% endtab %}

## Limit the minimum filter character

When filtering the list items, you can set the limit for character count to raise remote request and fetch
filtered data on the DropDownList. This can be done by manual validation within the filter event handler.

In the following example, the remote request does not fetch the search data until the search key contains three characters.

{% tab template="dropdownlist/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';
import { Query, DataManager, ODataV4Adaptor } from '@syncfusion/ej2-data';
import { FilteringEventArgs } from '@syncfusion/ej2-dropdowns';
import { EmitType } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    // specifies the template string for the DropDownList component with change event
    template: `<ejs-dropdownlist id='ddlelement' #samples [dataSource]='data' [query]='query' [fields]='fields' [placeholder]='text' [allowFiltering]='true' [sortOrder]='sorting' (filtering)='onFiltering($event)'></ejs-dropdownlist>`
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
    public query: Query = new Query().from('Customers').select(['ContactName', 'CustomerID']).take(6);
    // maps the appropriate column to fields property
    public fields: Object = { text: 'ContactName', value: 'CustomerID' };
    // set the placeholder to the DropDownList input
    public text: string = "Select a customer";
    //sort the result items
    public sorting: string = 'Ascending';
    //Bind the filter event
    public onFiltering: EmitType =  (e: FilteringEventArgs) => {
        // load overall data when search key empty.
        if (e.text === '') {
            e.updateData(this.data);
        } else {
           // restrict the remote request until search key contains 3 characters.
          if (e.text.length < 3) { return; }
          let query: Query = new Query().from('Customers').select(['ContactName', 'CustomerID']);
          query = (e.text !== '') ? query.where('ContactName', 'startswith', e.text, true) : query;
          e.updateData(this.data, query);
        }
    };
}
```

{% endtab %}

## Change the filter type

While filtering, you can change the filter type to `contains`,
`startsWith`, or `endsWith` for string type within the filter event handler.

In the following examples, data filtering is done with `endsWith` type.

{% tab template="dropdownlist/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';
import { Query, DataManager, ODataV4Adaptor } from '@syncfusion/ej2-data';
import { FilteringEventArgs } from '@syncfusion/ej2-dropdowns';
import { EmitType } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    // specifies the template string for the DropDownList component with change event
    template: `<ejs-dropdownlist id='ddlelement' #samples [dataSource]='data' [query]='query' [fields]='fields' [placeholder]='text' [popupHeight]='height' [sortOrder]='sorting' [allowFiltering]='true' (filtering)='onFiltering($event)'></ejs-dropdownlist>`
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
    public query: Query = new Query().from('Customers').select(['ContactName', 'CustomerID']).take(7);
    // maps the appropriate column to fields property
    public fields: Object = { text: 'ContactName', value: 'CustomerID' };
    // set the placeholder to the DropDownList input
    public text: string = "Select a customer";
    // set the height of the popup
    public height: string = '250px';
    //sort the result items
    public sorting: string = 'Ascending';
    //Bind the filter event
    public onFiltering: EmitType =  (e: FilteringEventArgs) => {
        // load overall data when search key empty.
        if (e.text === '') {
            e.updateData(this.data);
        } else {
          let query: Query = new Query().from('Customers').select(['ContactName', 'CustomerID']);
          // change the type of filtering
          query = (e.text !== '') ? query.where('ContactName', 'endswith', e.text, true) : query;
          e.updateData(this.data, query);
        }
    };
}
```

{% endtab %}

## Case sensitive filtering

Data items can be filtered either with or without case sensitivity using the DataManager. This can be done
by passing the fourth optional parameter of the `where` clause.

The following example shows how to perform case-sensitive filter.

{% tab template="dropdownlist/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';
import { Query, DataManager, ODataV4Adaptor } from '@syncfusion/ej2-data';
import { FilteringEventArgs } from '@syncfusion/ej2-dropdowns';
import { EmitType } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    // specifies the template string for the DropDownList component with change event
    template: `<ejs-dropdownlist id='ddlelement' #samples [dataSource]='data' [query]='query' [fields]='fields' [placeholder]='text' [popupHeight]='height' [sortOrder]='sorting' [allowFiltering]='true' (filtering)='onFiltering($event)'></ejs-dropdownlist>`
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
    public query: Query = new Query().from('Customers').select(['ContactName', 'CustomerID']).take(7);
    // maps the appropriate column to fields property
    public fields: Object = { text: 'ContactName', value: 'CustomerID' };
    // set the placeholder to the DropDownList input
    public text: string = "Select a customer";
    // set the height of the popup
    public height: '250px';
    //sort the result items
    public sorting: string = 'Ascending';
    //Bind the filter event
    public onFiltering: EmitType =  (e: FilteringEventArgs) => {
        // load overall data when search key empty.
        if (e.text === '') {
            e.updateData(this.data);
        } else {
          let query: Query = new Query().from('Customers').select(['ContactName', 'CustomerID']);
          //enable the case sensitive filtering by passing false to 4th parameter.
          query = (e.text !== '') ? query.where('ContactName', 'startswith', e.text, false) : query;
          e.updateData(this.data, query);
        }
    };
}
```

{% endtab %}

## Diacritics Filtering

The DropDownList supports diacritics filtering which will ignore the [diacritics](https://en.wikipedia.org/wiki/Diacritic) and
makes it easier to filter the results in international characters lists
when the [ignoreAccent](../api/drop-down-list/#ignoreaccent) is enabled.

In the following sample,data with diacritics are bound as dataSource for DropDownList.

{% tab template="dropdownlist/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';


@Component({
    selector: 'app-root',
    // specifies the template string for the DropDownList component with change event
    template: `<ejs-dropdownlist id='diacritics' [dataSource]='data' [allowFiltering]='true' [ignoreAccent]='true' placeholder='Select a value'
            filterBarPlaceholder='e.g: aero'>
        </ejs-dropdownlist>`
})
export class AppComponent {
    constructor() {
    }
    // create local data
    public data: string[] = [
        'Aeróbics',
        'Aeróbics en Agua',
        'Aerografía',
        'Aeromodelaje',
        'Águilas',
        'Ajedrez',
        'Ala Delta',
        'Álbumes de Música',
        'Alusivos',
        'Análisis de Escritura a Mano'];
}
```

{% endtab %}

## See Also

* [How to limit the search result while filtering](./how-to/search-on-filtering/)
* [How to highlight the matched characters in filtering](./how-to/highlight-filtering/)
* [How to modify the result data using remote data source](./how-to/modify-data/)