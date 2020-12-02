---
title: "Select grid rows based on certain condition"
component: "Grid"
description: "Learn how to select grid rows based on certain condition"
---

# Select grid rows based on certain condition

You can select the specific row in the grid based on a certain condition by using the [`selectRows`](../../api/grid/#selectrows) method in the [`dataBound`](../../api/grid/#databound) event of Grid.

In the below demo, we have selected the grid rows only when **EmployeeID** column value greater than **3**.

{% tab template="grid/custom-column", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent, SelectionSettingsModel } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<div id="GridParent">
                    <ejs-grid #Grid [dataSource]='data' allowPaging='true' [selectionSettings]='selectionOptions'
                    (rowDataBound)='rowDataBound($event)' (dataBound)='dataBound($event)' height='273px'>
                        <e-columns>
                            <e-column field='OrderID' headerText='Order ID' textAlign='Right' isPrimaryKey='true' width=100></e-column>
                            <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                            <e-column field='EmployeeID' headerText='Employee ID' textAlign= 'Right' width=120></e-column>
                            <e-column field='ShipCity' headerText='Ship City'  width=120></e-column>
                            <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                        </e-columns>
                    </ejs-grid>
               </div>`
})
export class AppComponent implements OnInit {
    public data: object[];
    @ViewChild('Grid') public grid: GridComponent;
    public selectionOptions: SelectionSettingsModel;
    public selIndex: number[] = [];
    ngOnInit(): void {
        this.data = data;
        this.selectionOptions = { type: 'Multiple' };
    }
    public rowDataBound(args): void {
        const EmployeeID = 'EmployeeID';
        if (args.data[EmployeeID] > 3) {
            this.selIndex.push(parseInt(args.row.getAttribute('aria-rowindex'), 10));
        }
    }
    public dataBound(args): void {
        if (this.selIndex.length) {
            this.grid.selectRows(this.selIndex);
            this.selIndex = [];
        }
    }
}

```

{% endtab %}