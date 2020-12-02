---
title: "Customizing Filter Dialog by using additional Parameter"
component: "Grid"
description: "Learn how to customize the filter dialog in Grid by using an additional Parameter."
---

# Customizing Filter Dialog by using an additional Parameter

You can customize the default settings of the components which are used in Menu filter by using params of filter property in column definition.
In the below sample, OrderID and Freight Columns are numeric columns, while open the filter dialog then you can see that NumericTextBox with spin button is displayed to change/set the filter value. Now using the params option we hide the spin button in NumericTextBox for OrderID Column.

{% tab template="grid/filtering1", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { FilterSettingsModel } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [allowFiltering]='true' [allowPaging]='true' [filterSettings]='filterOption'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' [filter]='filterParams' textAlign='Right' width=90></e-column>
                    <e-column field='Name' headerText='Name' width=140></e-column>
                    <e-column field='ShipName' headerText='ShipName' width=140></e-column>
                    <e-column field='Freight' headerText='Freight' textAlign='Right' format='C2' width=90></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public filterParams: object;
    public filterOption: FilterSettingsModel = { type: 'Menu'};
    public height = '220px';
    ngOnInit(): void {
        this.data = data;
        this.filterParams = { params: { showSpinButton: false } };
    }
}

```

{% endtab %}