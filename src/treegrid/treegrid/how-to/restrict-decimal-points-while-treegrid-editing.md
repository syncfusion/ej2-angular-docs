---
title: "Restrict to type decimal points in a NumericTextBox while editing the numeric column"
component: "TreeGrid"
description: "Learn how restrict to type decimal points in a NumericTextBox while editing the numeric column."
---

# Restrict to type decimal points in a NumericTextBox while editing the numeric column

By default, the number of decimal places will be restricted to two in the NumericTextBox while editing the numeric column. We can restrict to type the decimal points in a NumericTextBox by using the **validateDecimalOnType** and **decimals** properties of NumericTextBox.

In the below demo, while editing the row we have restricted to type the decimal point value in the NumericTextBox of **Price** column.

{% tab template="treegrid/refresh", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { stackedData } from './datasource';
import { TreeGridComponent, EditSettingsModel, ToolbarItems, ToolbarService, EditService } from '@syncfusion/ej2-angular-treegrid';
import {  IEditCell } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-container',
    providers: [ToolbarService, EditService],
    template: `<ejs-treegrid #treegridObj [dataSource]='data' childMapping='subtasks' [treeColumnIndex]='1' [height]='265' [editSettings]='editSettings' [toolbar]='toolbar'>
        <e-columns>
            <e-column field='orderID' headerText='Order ID' width='70' textAlign='Right' isPrimaryKey='true'></e-column>
            <e-column field='orderName' headerText='Order Name' width='100' ></e-column>
            <e-column field='orderDate' headerText='Order Date' textAlign='Right' [format]='formatOptions' editType= 'datepickeredit' width='100'></e-column>
            <e-column field='shippedDate' headerText='Shipped Date' textAlign='Right' [format]='formatOptions' editType= 'datepickeredit' width='100'></e-column>
            <e-column field='shipMentCategory' headerText='Shipment Category' width='100' ></e-column>
            <e-column field='units' headerText='Units' width='90' textAlign='Right'  editType= 'numericedit'></e-column>
            <e-column field='price' headerText='Price' width='90' textAlign='Right' [format]='numericFormatOptions' editType= 'numericedit' [edit]='numericParams' ></e-column>
        </e-columns>
    </ejs-treegrid>`,
})
export class AppComponent implements OnInit {

    public data: Object[] = [];
    public formatOptions: Object;
    public numericFormatOptions: Object;
    public editSettings: EditSettingsModel;
    public toolbar: ToolbarItems[];
    public numericParams: IEditCell

    ngOnInit(): void {
        this.data = stackedData;
        this.formatOptions = { format: 'y/M/d', type: 'date' };
        this.numericFormatOptions = {format: 'c2'}
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