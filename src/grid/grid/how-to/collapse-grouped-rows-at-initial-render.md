---
title: "Collapse all grouped rows at initial render"
component: "Grid"
description: "Learn how to collapse all grouped rows at initial render."
---

# Collapse all grouped rows at initial render

You can collapse all the grouped rows at initial rendering by using [`dataBound`](../../api/grid/#databound) event with  [`collapseAll`](../../api/grid/group/#collapseall) method of the grid.

In the below demo, all the grouped rows are collapsed at initial rendering.

{% tab template="grid/collapse-all-initial", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' [allowGrouping]='true' [groupSettings]='groupOptions'
     (dataBound)='dataBound()' height='267px'>
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
    public initial = true;
    public groupOptions: object;
    @ViewChild('grid') public grid: GridComponent;

    ngOnInit(): void {
        this.data = data;
        this.groupOptions = { columns: ['ShipCity'] };
    }
    dataBound() {
        if (this.initial === true) {
            this.grid.groupModule.collapseAll();
            this.initial = false;
        }
    }
}

```

{% endtab %}