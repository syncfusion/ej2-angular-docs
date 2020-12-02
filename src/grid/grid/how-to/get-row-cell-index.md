---
title: "Get specific row and cell index in Grid"
component: "Grid"
description: "Learn how to get specific row and cell index in Grid."
---

# Get specific row and cell index in Grid

You can get the specific row and cell index of the grid by using [`rowSelected`](../../) event of the grid. Here, we have get the row and cell index by using **aria-rowindex**(get row Index from **tr** element) and **aria-colindex**(column index from **td** element) attribute.

{% tab template="grid/collapse-all-initial", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' (rowSelected)='rowSelected($event)' height='267px'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})

export class AppComponent implements OnInit {

    public data: object[];
    @ViewChild('grid') public grid: GridComponent;

    ngOnInit(): void {
        this.data = data;
    }

    rowSelected(args) {
        alert('row index: ' + args.row.getAttribute('aria-rowindex'));
        alert('column index: ' + args.target.getAttribute('aria-colindex'));
    }

}

```

{% endtab %}