---
title: "Refresh the Datasource"
component: "Grid"
description: "Learn how to refresh the Grid dataSource."
---

# Refresh the Datasource

You can add/delete the datasource records through an external button. To reflect the datasource changes in grid,
you need to invoke the [`refresh`](../../api/grid/#refresh) method.

Please follow the below steps to refresh the grid after datasource change.

**Step 1**:

Add/delete the datasource record by using the following code.

```typescript
    this.grid.dataSource.unshift(data); // Add a new record.

    this.grid.dataSource.splice(selectedRow, 1); // Delete a record.

```

**Step 2**:

Refresh the grid after the datasource change by using the [`refresh`](../../api/grid/#refresh) method.

```typescript
    this.grid.refresh(); // Refresh the Grid.

```

{% tab template="grid/change-headertext", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts"%}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { GridComponent } from '@syncfusion/ej2-angular-grids';
import { data } from './datasource';


@Component({
    selector: 'app-root',
    template: `<button ej-button class='e-flat' (click)='add()'> Add </button>
               <button ej-button class='e-flat' (click)='delete()'> Delete </button>
                <ejs-grid #grid [dataSource]='data' [height]='280' >
                    <e-columns>
                        <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=90></e-column>
                        <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                        <e-column field='Freight' headerText='Freight' textAlign='Right' format='C2' width=90></e-column>
                        <e-column field='ShipCity' headerText='Ship City' width=120 ></e-column>
                    </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    @ViewChild('grid') public grid: GridComponent;

    ngOnInit(): void {
        this.data = data;
    }
    add(): void {
        const rdata: object = { OrderID: 10247, CustomerID: 'ASDFG', Freight: 40.4, OrderDate: new Date(8367642e5) };
        (this.grid.dataSource as object[]).unshift(rdata);
        this.grid.refresh();
    }
    delete(): void {
        const selectedRow: number = this.grid.getSelectedRowIndexes()[0];
        if (this.grid.getSelectedRowIndexes().length) {
            (this.grid.dataSource as object[]).splice(selectedRow, 1);
        } else {
            alert('No records selected for delete operation');
        }
        this.grid.refresh();
    }
}

```

{% endtab %}
