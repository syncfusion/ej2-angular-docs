---
title: "Custom Tooltip for Columns"
component: "Grid"
description: "Learn how to Custom Tooltip for Columns."
---

# Custom Tooltip for Columns

You can achieve the custom tooltip([`EJ2 Tooltip`](../../../tooltip/getting-started)) for Grid by using the
[`queryCellInfo`](../../api/grid/#querycellinfo) event.

Render the ToolTip component for the grid cells by using the following code in the
[`queryCellInfo`](../../api/grid/#querycellinfo) event.

```typescript
tooltip (args: QueryCellInfoEventArgs) {
    let tooltip: Tooltip = new Tooltip({
        content: args.data[args.column.field].toString();
    }, args.cell);
}

```

{% tab template="grid/custom-tooltip", sourceFiles="app/**/*.ts"%}

```typescript
import { Component, OnInit } from '@angular/core';
import { QueryCellInfoEventArgs } from '@syncfusion/ej2-angular-grids';
import { Tooltip } from '@syncfusion/ej2-popups';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' [height]='315' (queryCellInfo)='tooltip($event)' >
                    <e-columns>
                        <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=90></e-column>
                        <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                        <e-column field='Freight' headerText='Freight' textAlign='Right' format='C2' width=90></e-column>
                        <e-column field='ShipName' headerText='Ship Name' width=120></e-column>
                    </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];

    ngOnInit(): void {
        this.data = data;
    }
    tooltip(args: QueryCellInfoEventArgs) {
        const tooltip: Tooltip = new Tooltip({
            content: args.data[args.column.field].toString()
        }, args.cell as HTMLTableCellElement);
    }
}


```

{% endtab %}
