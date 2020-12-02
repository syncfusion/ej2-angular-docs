---
title: "Restrict to type decimal points in a NumericTextBox while editing the numeric column"
component: "Grid"
description: "Learn how restrict to type decimal points in a NumericTextBox while editing the numeric column."
---

# Restrict to type decimal points in a NumericTextBox while editing the numeric column

By default, the number of decimal places will be restricted to two in the NumericTextBox while editing the numeric column. We can restrict to type the decimal points in a NumericTextBox by using the [`validateDecimalOnType`](https://ej2.syncfusion.com/angular/documentation/api/numerictextbox/#validatedecimalontype) and [`decimals`](https://ej2.syncfusion.com/angular/documentation/api/numerictextbox/#decimals) properties of NumericTextBox.

In the below demo, while editing the row we have restricted to type the decimal point value in the NumericTextBox of **Freight** column.

{% tab template="grid/prevent-decimalpoint", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { EditSettingsModel, ToolbarItems, IEditCell } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [editSettings]='editSettings' [toolbar]='toolbar' height='265px'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' isPrimaryKey='true' width=100></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                    <e-column field='Freight' headerText='Freight' textAlign= 'Right'
                    editType= 'numericedit' [edit]='numericParams' width=120></e-column>
                    <e-column field='ShipCity' headerText='Ship City' editType= 'dropdownedit' width=150>
                    </e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public editSettings: EditSettingsModel;
    public toolbar: ToolbarItems[];
    public numericParams: IEditCell;
    ngOnInit(): void {
        this.data = data;
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true };
        this.toolbar = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
        this.numericParams = { params: {
            validateDecimalOnType: true,
            decimals: 0,
            format: 'N' }
        };
    }
}


```

{% endtab %}