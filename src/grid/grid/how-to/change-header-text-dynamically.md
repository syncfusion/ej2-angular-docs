---
title: "Change Column Header Text Dynamically"
component: "Grid"
description: "Learn how to change column header text dynamically."
---

# Change Column Header Text Dynamically

You can change the column [`headerText`](../../api/grid/column/#headertext) dynamically through an external button.

Follow the given steps to change the header text dynamically:

**Step 1**:

Get the column object corresponding to the field name by using the [`getColumnByField`](../../api/grid/#getcolumnbyfield) method.
Then change the header Text value.

```typescript
let column = this.grid.getColumnByField('ShipCity'); // Get column object.
column.headerText = 'Changed Text';

```

**Step 2**:

To reflect the changes in the grid header, invoke the [`refreshHeader`](../../api/grid/#refreshheader) method.

```typescript
this.grid.refreshHeader();

```

{% tab template="grid/change-headertext", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts"%}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { GridComponent } from '@syncfusion/ej2-angular-grids';
import { data } from './datasource';


@Component({
    selector: 'app-root',
    template: `<button ej-button class='e-flat' (click)='click()'>Change Header Text</button>
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
    click(): void {
        const column = this.grid.getColumnByField('ShipCity'); // get the JSON object of the column corresponding to the field name
        column.headerText = 'Changed Text'; // assign a new header text to the column
        this.grid.refreshHeader();
    }
}

```

{% endtab %}
