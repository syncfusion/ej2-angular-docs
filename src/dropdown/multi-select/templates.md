---
title: "Multiselect Template"
component: "MultiSelect"
description: "This section demonstrates the customization of the appearance of each item in the pop-up list of Syncfusion angular multiselect component using template option."
---

# Templates

The MultiSelect has been provided with several options to customize each list item, group title,
selected value, header, and footer elements. It uses the Essential JS 2
`Template engine` to compile and render the elements properly.

## Item template

The content of each list item within the MultiSelect can be customized with the
help of [itemTemplate](../api/multi-select/#itemtemplate)
property.

In the following sample, each list item is split into two columns to display relevant data's.

{% tab template="multiselect/item-template", sourceFiles="app/**/*.ts,itemTemplate.html"  %}

```typescript
import { Component } from '@angular/core';
import { Query, DataManager, ODataV4Adaptor } from '@syncfusion/ej2-data'

@Component({
    selector: 'app-root',
    // specifies the template url path
    templateUrl: './itemTemplate.html'
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
    public fields: Object = { text: 'FirstName', value: 'EmployeeID' };
    //bind the Query instance to query property
    public query: Query = new Query().from('Employees').select(['FirstName', 'City','EmployeeID']).take(6);
    //set the placeholder to MultiSelect input
    public text: string = "Select an employee";
    //sort the result items
    public sorting: string = 'Ascending';
}
```

{% endtab %}

## Value template

The currently selected value that is displayed by default on the MultiSelect input
element can be customized using the [valueTemplate](../api/multi-select/#valuetemplate) property.

In the following sample, the selected value is displayed as a combined text of both `FirstName` and `City`
in the MultiSelect input, which is separated by a hyphen.

{% tab template="multiselect/value-template", sourceFiles="app/**/*.ts,valueTemplate.html"  %}

```typescript
import { Component } from '@angular/core';
import { Query, DataManager, ODataV4Adaptor } from '@syncfusion/ej2-data'

@Component({
    selector: 'app-root',
    // specifies the template url path
    templateUrl: './valueTemplate.html'
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
    public fields: Object = { text: 'FirstName', value: 'EmployeeID' };
    //bind the Query instance to query property
    public query: Query = new Query().from('Employees').select(['FirstName', 'City','EmployeeID']).take(6);
    //set the placeholder to MultiSelect input
    public text: string = "Select an employee";
    //sort the result items
    public sorting: string = 'Ascending';
    public box : string = 'box';
}
```

{% endtab %}

## Group template

The group header title under which appropriate sub-items are categorized can also be
customize with the help of
[groupTemplate](../api/multi-select/#grouptemplate) property.
This template is common for both inline and floating group header template.

In the following sample, employees are grouped according to their city.

{% tab template="multiselect/group-template", sourceFiles="app/**/*.ts,groupTemplate.html"  %}

```typescript
import { Component } from '@angular/core';
import { Query, Predicate, DataManager, ODataV4Adaptor } from '@syncfusion/ej2-data'

@Component({
    selector: 'app-root',
    // specifies the template url path
    templateUrl: './groupTemplate.html'
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
    // form  predicate to fetch the grouped data
    public groupPredicate = new Predicate('City', 'equal','london').or('City','equal','seattle');
    // maps the appropriate column to fields property
    public fields: Object = { text: 'FirstName', value: 'EmployeeID', groupBy:'City' };
    //bind the Query instance to query property
    public query: Query = new Query().from('Employees').select(['FirstName', 'City','EmployeeID']).take(6).where(this.groupPredicate);
    //set the placeholder to MultiSelect input
    public text: string = "Select an employee";
    //sort the result items
    public sorting: string = 'Ascending';
}
```

{% endtab %}

## Header template

The header element is shown statically at the top of the popup list items within the
MultiSelect, and any custom element can be placed as a header element using the
[headerTemplate](../api/multi-select/#headertemplate) property.

In the following sample, the list items and its headers are designed and displayed as two columns
similar to multiple columns of the grid.

{% tab template="multiselect/header-template", sourceFiles="app/**/*.ts,headerTemplate.html"  %}

```typescript
import { Component } from '@angular/core';
import { Query, DataManager, ODataV4Adaptor } from '@syncfusion/ej2-data';

@Component({
    selector: 'app-root',
    // specifies the template url path
    templateUrl: './headerTemplate.html'
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
    public fields: Object = { text: 'FirstName', value: 'EmployeeID' };
    //bind the Query instance to query property
    public query: Query = new Query().from('Employees').select(['FirstName', 'City','EmployeeID']).take(6);
    //set the placeholder to MultiSelect input
    public text: string = "Select an employee";
    //sort the result items
    public sorting: string = 'Ascending';
}
```

{% endtab %}

## Footer template

The MultiSelect has options to show a footer element at the bottom of the list items
in the popup list.
Here, you can place any custom element as a footer element using the
[footerTemplate](../api/multi-select/#footertemplate) property.

In the following sample, footer element displays the total number of list items present in the MultiSelect.

{% tab template="multiselect/footer-template", sourceFiles="app/**/*.ts,footerTemplate.html"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template url path
    templateUrl: './footerTemplate.html'
})
export class AppComponent {
    // create a object for MultiSelect
    constructor() {
    }
    // defined the array of data
    public data: Object[] = ['Badminton', 'Basketball', 'Cricket', 'Golf'];
    // set placeholder text to MultiSelect input element
    public text: string = 'Select a game';
}
```

{% endtab %}

## No records template

The MultiSelect is provided with support to custom design the popup list content when no data is found
and no matches found on search with the help of
[noRecordsTemplate](../api/multi-select/#norecordstemplate) property.

In the following sample, popup list content displays the notification of no data available.

{% tab template="multiselect/norecords-template", sourceFiles="app/**/*.ts,index.css"  %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the MultiSelect component
    template:  `<ejs-multiselect id='multiselectelement' [dataSource]='data' placeholder='Find a item'>
                    <ng-template #noRecordsTemplate>
                        <span class='norecord'> NO DATA AVAILABLE</span>
                    </ng-template>
                 </ejs-multiselect>`
})
export class AppComponent {
    // defined the empty array data
    public data: string[] = [];
}
```

{% endtab %}

## Action failure template

There is also an option to custom design the popup list content when the data fetch request
fails at the remote server. This can be achieved using the
[actionFailureTemplate](../api/multi-select/#actionfailuretemplate) property.

In the following sample, when the data fetch request fails, the MultiSelect displays the notification.

{% tab template="multiselect/norecords-template", sourceFiles="app/**/*.ts,index.css"  %}

```typescript

import { Component } from '@angular/core';
//import data manager related classes
import { Query, DataManager, ODataV4Adaptor } from '@syncfusion/ej2-data';

@Component({
    selector: 'app-root',
    // specifies the template string for the MultiSelect component
    template:  `<ejs-multiselect id='multiselectelement' [dataSource]='data' [query]='query'
                [fields]='fields' placeholder='Find an employee'>
                    <ng-template #actionFailureTemplate>
                        <span class='action-failure'> Data fetch get fails</span>
                    </ng-template>
                 </ejs-multiselect>`
})
export class AppComponent {
    //bind the data manager instance to dataSource property
    public data: DataManager = new DataManager({
            // Here, use the wrong url to display the action failure template
            url: 'https://services.odata.org/V4/Northwind/Northwind.svcs/',
            adaptor: new ODataV4Adaptor,
            crossDomain: true
    });
    //bind the Query instance to query property
    public query: Query =  new Query().from('Employees').select(['FirstName']).take(6);
    // maps the appropriate column to fields property
    public fields: Object =  { text: 'FirstName', value: 'EmployeeID' };
}

```

{% endtab %}

## See Also

* [How to bind the data](./data-binding/)
* [How to group the data using header](./grouping/)
* [How to customize the options in MultiSelect](./chip-customization/)