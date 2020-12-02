---
title: "Render other components in a column"
component: "Grid"
description: "Learn how to Render other components in a column."
---

# Render other components in a column

You can render any component in a grid column using the [`template`](../../api/grid/column/#template) property.

Initialize the column template for your custom component. The [`template`](../../api/grid/column/#template) property
renders the custom component.

```html
    <div>
        <ejs-dropdownlist value='Order Placed' [dataSource]='dropData' [popupHeight]='150' [popupWidth]='150' ></ejs-dropdownlist>
    </div>

```

{% tab template="grid/column-sync-comp", sourceFiles="app/**/*.ts"%}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' [height]='300'>
                    <e-columns>
                        <e-column headerText='Order Status'width='200'>
                            <ng-template #template let-data>
                                <div>
                                    <ejs-dropdownlist value='Order Placed' [dataSource]='dropData' [popupHeight]='150' [popupWidth]='150' >
                                    </ejs-dropdownlist>
                                </div>
                            </ng-template>
                        </e-column>
                        <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=90></e-column>
                        <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                        <e-column field='Freight' headerText='Freight' textAlign='Right' format='C2' width=90></e-column>
                        <e-column field='OrderDate' headerText='Order Date' textAlign='Right' format='yMd' width=120></e-column>
                    </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public dropData: string[];

    ngOnInit(): void {
        this.data = data;
        this.dropData = ['Order Placed', 'Processing', 'Delivered'];
    }
}

```

{% endtab %}
