---
title: "Combo box Filtering"
component: "ComboBox"
description: "This section for Syncfusion angular combo box component explains the built-in filtering support with a rich set of filtering configurations."
---

# Filtering

The ComboBox has built-in support to filter the data items when [`allowFiltering`](../api/combo-box/#allowfiltering) enabled.
The filter operation starts as soon as you start typing characters in the component.

By making use of [filtering](../api/combo-box/#filtering) event, you can filter required data and
return the data to ComboBox via
`updateData` method.
So that those filtered items get displayed in the popup.

The following sample illustrates how to query the data source and pass the data to the ComboBox
through the `updateData` method in `filtering` event.

{% tab template="combobox/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';
import { FilteringEventArgs } from '@syncfusion/ej2-dropdowns';
import { EmitType } from '@syncfusion/ej2-base';
import { Query } from '@syncfusion/ej2-data';

@Component({
    selector: 'app-root',
    // specifies the template string for the ComboBox component with change event
    template: `<ejs-combobox id='comboelement' #samples [dataSource]='data' [fields]='fields' [placeholder]='text' [allowFiltering]='true' (filtering)='onFiltering($event)'></ejs-combobox>`
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
    // set the placeholder to the ComboBox input
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
filtered data on the ComboBox. This can be done by manual validation within the filter event handler.

In the following example, the remote request does not fetch the search data until the search key contains three characters.

{% tab template="combobox/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';
import { Query, DataManager, ODataV4Adaptor } from '@syncfusion/ej2-data';
import { FilteringEventArgs } from '@syncfusion/ej2-dropdowns';
import { EmitType } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    // specifies the template string for the ComboBox component with change event
    template: `<ejs-combobox id='comboelement' #samples [dataSource]='data' [query]='query' [fields]='fields' [placeholder]='text' [allowFiltering]='true' [sortOrder]='sorting' (filtering)='onFiltering($event)'></ejs-combobox>`
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
    // set the placeholder to the ComboBox input
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

{% tab template="combobox/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';
import { Query, DataManager, ODataV4Adaptor } from '@syncfusion/ej2-data';
import { FilteringEventArgs } from '@syncfusion/ej2-dropdowns';
import { EmitType } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    // specifies the template string for the ComboBox component
    template: `<ejs-combobox id='comboelement' #samples [dataSource]='data' [query]='query' [fields]='fields' [placeholder]='text' popupHeight='250px' [sortOrder]='sorting' [allowFiltering]='true' (filtering)='onFiltering($event)'></ejs-combobox>`
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
    // set the placeholder to the ComboBox input
    public text: string = "Select a customer";
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

{% tab template="combobox/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';
import { Query, DataManager, ODataV4Adaptor } from '@syncfusion/ej2-data';
import { FilteringEventArgs } from '@syncfusion/ej2-dropdowns';
import { EmitType } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    // specifies the template string for the ComboBox component with change event
    template: `<ejs-combobox id='comboelement' #samples [dataSource]='data' [query]='query' [fields]='fields' [placeholder]='text' popupHeight='250px' [sortOrder]='sorting' [allowFiltering]='true' (filtering)='onFiltering($event)'></ejs-combobox>`
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
    // set the placeholder to the ComboBox input
    public text: string = "Select a customer";
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

The ComboBox supports diacritics filtering which will ignore the [diacritics](https://en.wikipedia.org/wiki/Diacritic) and
makes it easier to filter the results in international characters lists
when the [ignoreAccent](../api/combo-box/#ignoreaccent) is enabled.

In the following sample,data with diacritics are bound as dataSource for ComboBox.

{% tab template="combobox/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the DropDownList component with change event
    template: `<ejs-combobox id='diacritics' [dataSource]='data' [allowFiltering]='true' [ignoreAccent]='true' placeholder='e.g. aero'>
        </ejs-combobox>`
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

* [How to achieve autofill while filtering](./how-to#autofill-supported-with-combobox)
* [How to group the data using header](./grouping/)