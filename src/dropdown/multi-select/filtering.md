---
title: "Multiselect Filtering"
component: "MultiSelect"
description: "This section explains the built-in filtering support with a rich set of filtering configurations in Syncfusion angular multiselect component."
---

# Filtering

The MultiSelect has built-in support to filter data items when `allowFiltering` is enabled. The filter
operation starts as soon as you start typing characters in the MultiSelect input.

To display filtered items in the popup, filter the required data and return it to the MultiSelect
via [updateData](/api/multi-select/filteringEventArgs/#updatedata) method by using the [filtering](../api/multi-select/#filtering) event.

The following sample illustrates how to query the data source and pass the data to the MultiSelect
through the `updateData` method in `filtering` event.

{% tab template="multiselect/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component } from '@angular/core';
import { FilteringEventArgs } from '@syncfusion/ej2-angular-dropdowns';
import { DataManager,Query } from '@syncfusion/ej2-data';
import { EmitType } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    // specifies the template string for the MultiSelect component
    template: `<ejs-multiselect id='multiselectelement' [dataSource]='searchData' [fields]='fields' [allowFiltering]='true' [placeholder]='placeholder' (filtering)='onFiltering($event)'></ejs-multiselect>`
})
export class AppComponent {
    constructor() {
    }
    // defined the array of data
    public searchData: { [key: string]: Object }[] = [
    { index: "s1", country: "Alaska" }, { index: "s2", country: "California" },
    { index: "s3", country: "Florida" }, { index: "s4", country: "Georgia" }
    ];
    // map the appropriate column
    public fields: Object = { text: "country", value: "index" };
    // set the placeholder to the MultiSelect input
    public placeholder: string = 'Select countries';
    //Bind the filter event
    public onFiltering: EmitType =  (e: FilteringEventArgs) => {
        let query = new Query();
        //frame the query based on search string with filter type.
        query = (e.text != "") ? query.where("country", "startswith", e.text, true) : query;
        //pass the filter data source, filter query to updateData method.
        e.updateData(this.searchData, query);
    };
}

```

{% endtab %}

## Limit the minimum filter character

When filtering the list items, you can set the limit for character count to raise remote request and fetch
filtered data on the MultiSelect. This can be done by manual validation within the filter event handler.

In the following example, the remote request does not fetch the search data until the search key contains three characters.

{% tab template="multiselect/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component } from '@angular/core';
import { FilteringEventArgs } from '@syncfusion/ej2-angular-dropdowns';
import { Query, DataManager, ODataV4Adaptor } from '@syncfusion/ej2-data';
import { EmitType } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    // specifies the template string for the MultiSelect component
    template: `<ejs-multiselect id='multiselectelement' [dataSource]='searchData' [fields]='fields' [allowFiltering]='true' [placeholder]='placeholder' [sortOrder]='sorting' [query]='query' (filtering)='onFiltering($event)'></ejs-multiselect>`
})
export class AppComponent {
    constructor() {
    }
    //bind the DataManager instance to dataSource property
    public searchData: DataManager = new DataManager({
            url: 'https://services.odata.org/V4/Northwind/Northwind.svc/Customers',
            adaptor: new ODataV4Adaptor,
            crossDomain: true
    });
    // map the appropriate column
    public fields: Object = { text: 'ContactName', value: 'CustomerID' };
    //bind the Query instance to query property
    public query: Query = new Query().select(['ContactName', 'CustomerID']).take(7);
    // set the placeholder to the MultiSelect input
    public placeholder: string = 'Select customers';
    //sort the resulted items
    public sorting: string = 'Ascending';
    //Bind the filter event
    public onFiltering: EmitType =  (e: FilteringEventArgs) => {
        // load overall data when search key empty.
        if(e.text == '') e.updateData(this.searchData);
        else{
           // restrict the remote request until search key contains 3 characters.
          if (e.text.length < 3) { return; }
          let query: Query = new Query().select(['ContactName', 'CustomerID']);
          query = (e.text !== '') ? query.where('ContactName', 'startswith', e.text, true) : query;
          e.updateData(this.searchData, query);
        }
    };
}

```

{% endtab %}

## Change the filter type

While filtering, you can change the filter type to `contains`,
`startsWith`, or `endsWith` for string type within the filter event handler.

In the following examples, data filtering is done with `endsWith` type.

{% tab template="multiselect/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component } from '@angular/core';
import { FilteringEventArgs } from '@syncfusion/ej2-angular-dropdowns';
import { Query, DataManager, ODataV4Adaptor } from '@syncfusion/ej2-data';
import { EmitType } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    // specifies the template string for the MultiSelect component
    template: `<ejs-multiselect id='multiselectelement' [dataSource]='searchData' [fields]='fields' [allowFiltering]='true' [placeholder]='placeholder' [sortOrder]='sorting'[query]='query' (filtering)='onFiltering($event)'></ejs-multiselect>`
})
export class AppComponent {
    constructor() {
    }
    //bind the DataManager instance to dataSource property
    public searchData: DataManager = new DataManager({
            url: 'https://services.odata.org/V4/Northwind/Northwind.svc/Customers',
            adaptor: new ODataV4Adaptor,
            crossDomain: true
    });
    // map the appropriate column
    public fields: Object = { text: 'ContactName', value: 'CustomerID' };
    //bind the Query instance to query property
    public query: Query = new Query().select(['ContactName', 'CustomerID']).take(7);
    // set the placeholder to the MultiSelect input
    public placeholder: string = 'Select names';
    //sort the resulted items
    public sorting: string = 'Ascending';
    //Bind the filter event
    public onFiltering: EmitType =  (e: FilteringEventArgs) => {
        // load overall data when search key empty.
        if(e.text == '') e.updateData(this.searchData);
        else{
          let query: Query = new Query().select(['ContactName', 'CustomerID']);
          // change the type of filtering
          query = (e.text !== '') ? query.where('ContactName', 'endswith', e.text, true) : query;
          e.updateData(this.searchData, query);
        }
    };
}

```

{% endtab %}

## Case sensitive filtering

Data items can be filtered either with or without case sensitivity using the DataManager. This can be done
by passing the fourth optional parameter of the `where` clause.

The following example shows how to perform case-sensitive filter.

{% tab template="multiselect/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component } from '@angular/core';
import { FilteringEventArgs } from '@syncfusion/ej2-angular-dropdowns';
import { EmitType } from '@syncfusion/ej2-base';
import { Query } from '@syncfusion/ej2-data';

@Component({
    selector: 'app-root',
    // specifies the template string for the MultiSelect component
    template: `<ejs-multiselect id='multiselectelement' [dataSource]='sportsData' [fields]='fields' [allowFiltering]='true' [placeholder]='placeholder' [popupHeight]='popupHeight' [sortOrder]='sorting' (filtering)='onFiltering($event)'></ejs-multiselect>`
})
export class AppComponent {
    constructor() {
    }
    //bind the DataManager instance to dataSource property
    public sportsData: { [key: string]: Object }[] = [
        { id: 'game1', sports: 'Badminton' },
        { id: 'game2', sports: 'Football' },
        { id: 'game3', sports: 'Tennis' },
        { id: 'game4', sports: 'Golf' },
        { id: 'game5', sports: 'Hockey' }
    ];
    // map the appropriate column
    public fields: Object = { text: 'sports', value: 'id' };
    // set the placeholder to the MultiSelect input
    public placeholder: string = 'Select games';
    //sort the resulted items
    public sorting: string = 'Ascending';
    //set the height of the popup element
    public popupHeight: string = '250px';
    //Bind the filter event
    public onFiltering: EmitType =  (e: FilteringEventArgs) => {
         // load overall data when search key empty.
        if(e.text == '') e.updateData(this.sportsData);
        else{
          let query: Query = new Query().select(['sports', 'id']);
           //enable the case sensitive filtering by passing false to 4th parameter.
          query = (e.text !== '') ? query.where('sports', 'startswith', e.text, false) : query;
          e.updateData(this.sportsData, query);
        }
    };
}

```

{% endtab %}

## Diacritics Filtering

MultiSelect supports diacritics filtering which will ignore the [diacritics](https://en.wikipedia.org/wiki/Diacritic) and
makes it easier to filter the results in international characters lists
when the [ignoreAccent](../api/multi-select/#ignoreaccent) is enabled.

In the following sample,data with diacritics are bound as dataSource for MultiSelect.

{% tab template="multiselect/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';


@Component({
    selector: 'app-root',
    // specifies the template string for the DropDownList component with change event
    template: `<ejs-multiselect id='diacritics' [dataSource]='data' [allowFiltering]='true' [ignoreAccent]='true' placeholder='e.g. aero'>
        </ejs-multiselect>`
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

* [How to bind the data](./data-binding/)
* [How to group the data using header](./grouping/)
* [How to add custom value to the MultiSelect](./custom-value/)