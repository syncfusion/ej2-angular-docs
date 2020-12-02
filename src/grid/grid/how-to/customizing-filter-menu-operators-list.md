---
title: "Customizing filter menu operators list"
component: "Grid"
description: "Learn how to Customizing filter menu operators list."
---

# Customizing filter menu operators list

You can customize the default filter operator list by defining the
[`filterSettings.operators`](../../api/grid/filterSettings/#operators) property. The available options are:

* **stringOperator**- defines customized string operator list.
* **numberOperator** - defines customized number operator list.
* **dateOperator** - defines customized date operator list.
* **booleanOperator** - defines customized boolean operator list.

In the following sample, we have customized string filter operators.
{% tab template="grid/filtering1", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

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
           type: 'Menu',
           operators: {
               stringOperator: [
                   { value: 'startsWith', text: 'starts with' },
                   { value: 'endsWith', text: 'ends with' },
                   { value: 'contains', text: 'contains' }
                ],
            }
        };
    }
}

```

{% endtab %}
