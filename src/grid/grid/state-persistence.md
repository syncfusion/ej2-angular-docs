---
title: "State Persistence"
component: "Grid"
description: "Learn how to persist the DataGrid state and model in the browser’s local storage."
---

# State Persistence

State persistence refers to the Grid's state maintained in the browser's
[`localStorage`](https://www.w3schools.com/html/html5_webstorage.asp#)
even if the browser is refreshed or if you move to the next page within the browser.
State persistence stores grid’s model object in the local storage when the
[`enablePersistence`](../api/grid/#enablepersistence) is defined as true.

## Maintaining Custom Query in State Persistence

Grid does not maintain the query params after page load event when
[`enablePersistence`](../api/grid/#enablepersistence) is set to true.
This is because the Grid refreshes its query params for every page load. You can maintain the custom query params by resetting the
[`addParams`](https://ej2.syncfusion.com/documentation/api/data/query/#addparams)
method in the [`actionBegin`](../api/grid/#actionbegin) event.

{% tab template="grid/grouping1", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { FilterService, PageService, GridComponent } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' [enablePersistence]='true' [allowPaging]='true' [allowFiltering]='true'
           height='210px' (actionBegin)='actionHandler($event)'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`,
    providers: [FilterService, PageService]
})
export class AppComponent implements OnInit {

    public data: object[];
    @ViewChild('grid')
    public grid: GridComponent;

    ngOnInit(): void {
        this.data = data;
    }

    actionHandler() {
        this.grid.query.addParams('$filter', 'EmployeeID eq 1');
    }

}

```

{% endtab %}

## Get/Set localStorage value

If the [`enablePersistence`](../api/grid/#enablepersistence) property set as true,
The Grid property value is saved in the **window.localStorage** for reference. You can get/set the localStorage value by using the
**getItem**/**setItem** method in **window.localStorage**.

```typescript
//get the Grid model.
let value: string = window.localStorage.getItem('gridGrid'); //"gridGrid" is component name + component id.
let model: Object = JSON.parse(model);

```

```typescript
//set the Grid model.
window.localStorage.setItem('gridGrid', JSON.stringify(model)); //"gridGrid" is component name + component id.

```

## Restore initial Grid state

When the [`enablePersistence`](../api/grid/#enablepersistence) property is set to **true**, the Grid will keep its state even if the page is reloaded. In some cases, you may be required to retain the Grid in its initial state. The Grid will not retain its initial state now since the [`enablePersistence`](../api/grid/#enablepersistence) property has been enabled.

You can achieve this by destroying the grid after disabling the [`enablePersistence`](../api/grid/#enablepersistence) property and clearing the local storage data, as shown in the sample below.

{% tab template="grid/grouping1", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { FilterService, PageService, GridComponent } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<button ej-button id='restore' (click)='clickHandler()'>Restore to initial state</button>
               <ejs-grid #grid id="Grid" [dataSource]='data' [enablePersistence]='true' [allowPaging]='true' [allowFiltering]='true'
           height='210px' (actionBegin)='actionHandler($event)'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`,
    providers: [FilterService, PageService]
})
export class AppComponent implements OnInit {

    public data: object[];
    @ViewChild('grid')
    public grid: GridComponent;

    ngOnInit(): void {
        this.data = data;
    }

    clickHandler() {
        this.grid.enablePersistence = false;
        window.localStorage.setItem("gridGrid", "");
        this.grid.destroy();
        //reloads the page
        location.reload();
   }
}

```

{% endtab %}