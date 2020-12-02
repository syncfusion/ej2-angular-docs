---
title: "Drop-down list How to get total count"
component: "DropDownList"
description: "This section explains on how to get the total count of list items of the Syncfusion Angular drop-down list component."
---

# Get the total count of data when remote data bind with DropDownList

Before component rendering, you can get the total items count by using
[`actionComplete`](../../api/drop-down-list/#actioncomplete) &nbsp;
event with its result arguments.
After rendering this component, you can get the total items count by using [`getItems`](../../api/drop-down-list/#getitems) method.

The following example demonstrate how to get the total items count.

{% tab template="dropdownlist/get-item", sourceFiles="app/**/*.ts,template.html"  %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { DropDownListComponent } from '@syncfusion/ej2-angular-dropdowns';
import { Query, DataManager, ODataV4Adaptor } from '@syncfusion/ej2-data'

@Component({
    selector: 'control-content',
    // specifies the template path for DropDownList component
    templateUrl: `template.html`
})
export class AppComponent {
    @ViewChild('sample')
    public dropDownListObject = DropDownListComponent;
    constructor() {

    }
    ngAfterViewInit(){
        let proxy=this;
        document.getElementById('btn').onclick = () => {
            // get items count using getItems method
            console.log("Total items count: " + proxy.dropDownListObject.getItems().length);
            let element: HTMLElement = document.createElement('p');
            element.innerText = "Total items count: " + proxy.dropDownListObject.getItems().length;
            document.getElementById('event').append(element);
        }
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
    public actionComplete(e: any): void {
         // get total items count
        console.log("Total items count: " + e.result.length);
        let element: HTMLElement = document.createElement('p');
        element.innerText = "Total items count: " + e.result.length;
        document.getElementById('event').append(element);
    }
}

```

{% endtab %}