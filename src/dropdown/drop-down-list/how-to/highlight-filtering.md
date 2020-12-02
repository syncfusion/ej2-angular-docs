---
title: "Drop-down list hightlight the character in filtering"
component: "DropDownList"
description: "This section explains on how to highlight the matched character in filtering Syncfusion Angular drop-down list component."
---

# Highlight the matched character in filtering

By using the `highlightSearch` method, you can highlight the matched character in DropDownList filtering.

The following example demonstrates about how to highlight the matched character in filtering.

{% tab template="dropdownlist/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';
import { Query, DataManager, ODataV4Adaptor } from '@syncfusion/ej2-data';
import { FilteringEventArgs, highlightSearch } from '@syncfusion/ej2-dropdowns';

@Component({
    selector: 'app-root',
    // specifies the template string for the DropDownList component with change event
    template: `<ejs-dropdownlist id='ddlelement' [dataSource]='data' [query]='query' [fields]='fields' [placeholder]='text' [allowFiltering]='true' [sortOrder]='sorting' (filtering)='onFiltering($event)'></ejs-dropdownlist>`
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
    public fields: Object = {
        text: 'ContactName', value: 'CustomerID', itemCreated: (e: any) => {
            highlightSearch(e.item, this.queryString, true, 'StartsWith');
        }
    };
    // set the placeholder to the DropDownList input
    public text: string = "Select a customer";
    //sort the result items
    public sorting: string = 'Ascending';
    public queryString: string;
    //Bind the filter event
    public onFiltering: any = (e: FilteringEventArgs) => {
        // take text for highlight the character in list items.
        this.queryString = e.text;
        let query: Query = new Query().from('Customers').select(['ContactName', 'CustomerID']);
        query = (e.text !== '') ? query.where('ContactName', 'startswith', e.text, true) : query;
        e.updateData(this.data, query);
    };
}

```

{% endtab %}