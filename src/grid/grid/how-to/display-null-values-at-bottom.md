---
title: "Display null date values at always"
component: "Grid"
description: "Learn how to display null date values at always."
---

# Display the null date values at bottom of the Grid while perform sorting

By default the null values are displayed at bottom of the Grid row while perform sorting in ascending order. As well as this values are displayed at top of the Grid row while perform sorting with descending order. But you can customize this default order to display the null values at always bottom row of the Grid by using [`column.sortComparer`](../../api/grid/column/#sortcomparer) method.

In the below demo we have displayed the null date values at bottom of the Grid row while sorting the **OrderDate** column in both ways.

{% tab template="grid/null-date-value", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { SortEventArgs  } from '@syncfusion/ej2-angular-grids';

let action: string;

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' allowSorting='true' (actionBegin)='actionBegin($event)' >
                    <e-columns>
                        <e-column field='OrderID' headerText='Order ID' width='100'></e-column>
                        <e-column field='CustomerID' headerText='Customer ID' width='120'></e-column>
                        <e-column field='OrderDate' headerText='Order Date' format='yMd'
                        [sortComparer]='sortComparer'  width='120'></e-column>
                        <e-column field='ShipCountry' headerText='Ship Country' width='150'></e-column>
                    </e-columns>
                </ejs-grid>`
})

export class AppComponent implements OnInit {

    public data: object[];
    ngOnInit(): void {
        this.data = data;
    }
    actionBegin(args: SortEventArgs) {
        if (args.requestType === 'sorting') {
            action = args.direction;
        }
    }
    sortComparer(reference, comparer) {
        const sortAsc = action === 'Ascending' ? true : false;
        if (sortAsc && reference === null) {
            return 1;
        } else if (sortAsc && comparer === null) {
            return -1;
        } else if (!sortAsc && reference === null) {
            return -1;
        } else if (!sortAsc && comparer === null) {
            return 1;
        } else {
            return reference - comparer;
        }
    }
}

```

{% endtab %}