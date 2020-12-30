---
title: "Hide sorting options on excel filter dialog"
component: "Grid"
description: "Learn how to hide sorting options in excel filter dialog."
---

# Hide sorting options in excel filter dialog

You can hide the sorting options on the excel filter dialog by setting display as none for the following classes.

```css
.e-excel-ascending,
.e-excel-descending,
.e-separator.e-excel-separator {
  display: none;
}

```

{% tab template="grid/hide-sort-excel", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { FilterSettingsModel } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [allowFiltering]='true' [filterSettings]='filterOptions' height='273px'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=100></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=100></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=100></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public filterOptions: FilterSettingsModel;

    ngOnInit(): void {
        this.data = data;
        this.filterOptions = {
           type: 'Excel',
        };
    }
}

```

{% endtab %}